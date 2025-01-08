# owasp_juice_shop 

# Introduction

The OWASP Juice Shop is an intentionally vulnerable web application designed to help developers, security professionals, and enthusiasts practice ethical hacking. It provides a safe playground to explore and understand various web application vulnerabilities in a controlled environment. For this practical work, the goal was to dive into the world of penetration testing and uncover security flaws by completing a series of challenges spread across different levels of difficulty.

This exercise was not just about solving technical puzzles; it was also an opportunity to learn, experiment, and build a deeper understanding of web application security. Through hands-on experience, I was able to solve 41 with different levels. It was both challenging and rewarding.

![image](https://github.com/user-attachments/assets/649760f1-c242-40ca-b210-0fd739ed0e8e)

# Tools and Environment Setup

To effectively tackle the challenges presented in the OWASP Juice Shop, we had a practical environment with a combination of essential tools and resources. Here's an overview of the tools used :

- Kali Linux

- OWASP ZAP (Zed Attack Proxy)

- Burp Suite: Used for intercepting, analyzing, and manipulating HTTP requests and responses.

- Gobuster: used for brute-forcing to discover hidden files and directories within the application.

- Firefox Browser

# Challenges and Solutions

# 1 Star 

Before starting we had to find the scoreboard directory which we did by looking into the main.js file that contains the paths mentionned in it

![image](https://github.com/user-attachments/assets/1413d1ef-3869-40bf-815e-712109416979)

Now lets move to the next challenges, the first three challenges came with instructions.

## DOM XSS 

in this challenge we performed an XSS payload firstly by looking for an injection point
in our case it was the search bar, we used the XSS payload <iframe src="javascript:alert(xss)">

![image](https://github.com/user-attachments/assets/8cf4cbd4-0d20-4443-9c59-8938b3591452)

we can see that the script code was executed.

## Bonus Payload 

its the same thing as the first challenge with a diferent payload that hot a SoundClloud music player embeded in it

```
<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
```
![image](https://github.com/user-attachments/assets/b68464c8-460f-44c0-b2e2-26d32243c1a4)

by putting the payload on the search input and click enter the song start playing.


## Expose Metrics endpoint 

in  this challenge we had to find a metrics end point 

![image](https://github.com/user-attachments/assets/f22f382a-edc7-4c3f-a386-ebe1624f1400)

now that we know that the project is using Prometheus, we did a search to find the default path used for the metrics 

![image](https://github.com/user-attachments/assets/8f0aa70c-cff5-48a6-8d52-9924205dbf39)

we accessed the endpoint http://localhost:3000/metrics 

![image](https://github.com/user-attachments/assets/27a1da80-0797-4c14-abe1-1771f20e527e)

we can see valuable data such as CPU and memory usage statistics, informations about file uploads, including types ect

## Give zero-star feedback to the store 

To complete this challenge we intercepted the outgoing request using burp suite so we can modify it 

first we try to submit a feedback

![image](https://github.com/user-attachments/assets/48b3bfcc-4577-4a34-8090-9e4645e8d60b)

now that we intercepted the request 

![image](https://github.com/user-attachments/assets/76be6710-ce88-45b2-9192-d4834b90f8ec)

we just had to change the rating value to 0 

## Repetitive Registration

in this challenge we got a hint DRY that means don't repeat yourself
the following image shows the registration request 

![image](https://github.com/user-attachments/assets/9f4c5d44-374b-4bb4-89de-9886c1eb51ea)

we change the value of "passwordrepeat" and forwarded the request
now the challenged is solved, which shows that there is a problem of server-side validation for this condition.

## Error Handling 

In this challenge we had to provoke an error using we tried to try and look for a file that does not exist 

```
http://127.0.0.1:3000/ftp/test.pdf
```

![image](https://github.com/user-attachments/assets/96f1f817-a0f9-4e1e-a910-44cfeb69f5e2)

it shows also some sensitive data like technology used

## Outdated Allowlist 

to solve this challenge we knew that we are looking for a redirect crypto currency link 

![image](https://github.com/user-attachments/assets/078d1d71-4e2b-46d6-ab4b-b5239536c380)

So we went to the main.js code and searched for redirect as a keyword  

![image](https://github.com/user-attachments/assets/7882ce70-9d67-4224-9da9-efbba2d3aa91)

we added it to the url and clicked enter 

![image](https://github.com/user-attachments/assets/f2eca986-43cd-4092-b23e-b43e67e24e8c)

## Confidential Document 

after performing a gobuster command at the start of the challenge one of the directories found was **/ftp** which probably certainly contains important files.

![image](https://github.com/user-attachments/assets/158ae006-05ad-42e0-b6e7-8b98df85bc01)

we took a look at some of the files and found the confiential one  acquisation.md

![image](https://github.com/user-attachments/assets/8fd787fd-5e16-4360-85d0-0700c4ef87cf)

## Bully Chatbot 

for this challenge we interacted with the support chat bot in order to get a sort of coupon 

to solve the challenge we just had to keep asking dor the coupon 

![image](https://github.com/user-attachments/assets/55134af1-2cf0-4e23-b546-2b50e88a8c32)

## Missing Encoding 

In this challenge we had that was not loaded correctly on the photo wall

![image](https://github.com/user-attachments/assets/c942b40e-8c03-458e-ab9e-131c928af741)

and it's because of the image tag that contained specialcharacters that were not encoded

![image](https://github.com/user-attachments/assets/fb36c466-27b7-449e-a8eb-7295a52676da)

we used chatgbt to give us the encoded version of the url and that's what we got


```
 assets%2Fpublic%2Fimages%2Fuploads%2F%F0%9F%98%BC-%23zatschi-%23whoneedsfourlegs-1572600969477.jpg
```

we changed the value of the source and we got as a result the image of the cat

![image](https://github.com/user-attachments/assets/e02b3a3b-3831-452a-b142-8cb93fcbe355)

# 2 stars

## Login Admin 

In this challenge we are exploiting an sql injection vulnerabilityin order to login as an admin
first we tried a simple sql injection and based on the output we can see that its possible to perform the attack

![image](https://github.com/user-attachments/assets/a6320bf1-30fc-4693-a769-417b97f6544e)

we can find an admin email in the reviews section "admin@juice-sh.op"
we tried another sql injection which is **admin@juice-sh.op' OR '1'='1' --** this turns the SQL command to always returning true without the need of a password

![image](https://github.com/user-attachments/assets/7ad06d94-40d0-40d4-b036-76ff46cfb32b)

this is due to improper input sanitization

## Five-Star Feedback

after getting login admin we only had to go to the administration directory we found before in another challenge 

![image](https://github.com/user-attachments/assets/4a688f76-c39f-429e-8464-212899ebbd05)

using admin previliges we only had to click delete

![image](https://github.com/user-attachments/assets/c5b587e4-4b6f-4c87-9918-dee7df643a37)

## Deprecated Interface 

In this one we had to look for a b2b functions or intrface that are no longer properly maintained

![image](https://github.com/user-attachments/assets/518c80f8-75f4-403c-9adb-637300d9b875)

In the Complaint tab on the left side menu, there’s a place to upload files. But after inspecting the code, it shows that its limited to PDF and ZIP files.

![image](https://github.com/user-attachments/assets/bd0b3128-f1ab-44e0-98a6-7cf172bc887e)

we choose an xml file that was mentioned in the main.js as content type. It went through and the challenge was solved

![image](https://github.com/user-attachments/assets/3e9563d8-eaae-4e1e-bc1a-b9b7ac6c3dad)

## Password Strength 

This challenge was simple we just had to guess some passwords, the common ones.

![image](https://github.com/user-attachments/assets/8849f92d-da0f-4415-8ae0-053de34cb5df)

after few guesses we found the password which was admin123

## NFT Takeover

Here we had to gain access to a digital wallet containing an NFT
first we began with looking for nft directories and we found it in the main.js file

![image](https://github.com/user-attachments/assets/45040329-982a-4a2b-bb78-8a53919c8f52)

we navigated to the page

![image](https://github.com/user-attachments/assets/40970fcf-3452-4583-90d5-f986a196058e)

after that we went searching for sensitive information that can be use. we found a user feedback stating a seed phrase

![image](https://github.com/user-attachments/assets/378a1b82-6913-4a29-bb74-0e5e687ba253)

we used a script to convert the seed phrase into a private key 

```python
from bip_utils import Bip39SeedGenerator, Bip32Slip10Ed25519


mnemonic = "purpose betray marriage blame crunch monitor spin slide donate sport lift clutch"

# Generate seed from mnemonic
seed_generator = Bip39SeedGenerator(mnemonic)
seed = seed_generator.Generate()

# Derive private key using BIP32
bip32 = Bip32Slip10Ed25519.FromSeed(seed)
private_key = bip32.PrivateKey().Raw().ToHex()

# Print the private key
print(f"Private Key: {private_key}")

```

and that was the private key  ``` 0x5bcc3e9d38baa06e7bfaab80ae5957bbe8ef059e640311d7d6d465e6bc948e3e ```

next we entred the key on the NFT page, got athenticated and got accesss to the wallet.

![image](https://github.com/user-attachments/assets/fd29dea1-8c1b-4859-9be1-4f15271c80a3)


# 3 stars

## Login Bender 

we logged into the app using admin creds and went for the administration directory where we found Bender's email ``` bender@juice-sh.op ```

![image](https://github.com/user-attachments/assets/a2cd4daa-0141-403c-aac5-81d194d323ca)

we dont have a password so we performed a SQLi knowing that the app is vulnerbale to this attack

we changes the email inout with a sql payload ``` bender@juice-sh.op' AND '1'='1' -- ```

the payload is cloasing the eamil using a single quote and then adds AND '1'='1' which is always true and then commenting the rest using --

and we typed random characters in the input of the passwords

![image](https://github.com/user-attachments/assets/110a1dcd-df7f-47bd-827c-bea3dd15f608) ![image](https://github.com/user-attachments/assets/890985c0-5462-43c9-bdcc-867b0e0a3c82)

## Payback Time

the goal of this challenge was to get financial gain by manipulating product pricing

one of the directories we found before was /accounting

![image](https://github.com/user-attachments/assets/00a1e1e0-646b-4c32-9771-c25173484689)

we needed another user creds.
By searching a bit we found the email

![image](https://github.com/user-attachments/assets/86e390d0-a144-4542-b9b5-4b5285e8823c)

we used SQLi attack to get access to this account using the following payload ```accountant@juice-sh.op' AND '1'='1' --```

![image](https://github.com/user-attachments/assets/e6df8364-bc49-4647-851b-8ddab2ee3841)

now that we got access lets intercept the request for changing the price of a product and set it to a negative value.

![image](https://github.com/user-attachments/assets/09c3e3c4-cde2-4fb3-ba5c-bee1da0484a9)

then we purchased the item which resulted a credit to the account unstead oaf a charge .

![image](https://github.com/user-attachments/assets/d53048d8-b2b0-433e-9272-7493b0ee589e) ![image](https://github.com/user-attachments/assets/138d43b9-aa5c-496f-ac94-5ade6506a574)

## Privacy Policy Inspection

In one of the first challenges we already found the path to privacy policy

we examined the page loking for hints or something that could be exploited 

we identified that hovering over some words

![image](https://github.com/user-attachments/assets/19260a3f-e3bb-44cb-85b1-c51e6ba1aff8)

![image](https://github.com/user-attachments/assets/418c1e22-d6c4-48b7-b5de-af098323b247)

![image](https://github.com/user-attachments/assets/9184fc3a-99a2-465a-9669-4c1be27c6074)

by puting them all together we got ``` 127.0.0.1:3000wemayalsoinstructyoutorefuseallreasonablynecessaryresponsibility ```
looks like a path so we tried a looked for it ``` 127.0.0.1:3000/we/may/also/instruct/you/to/refuse/all/reasonably/necessary/responsibility ```

![image](https://github.com/user-attachments/assets/b0e60aab-aad1-425e-81b4-a93b0669b262)

we got an error but it showing us another path 

![image](https://github.com/user-attachments/assets/f9cc5686-4fdb-4b81-8743-0b4126e81810)

# 4 stars 

## Easter Egg

this challenge required exploring the application looking for an easter egg

first we explored the ftp server by nagivating to ``` 127.0.0.1:3000/ftp ```

here we found the file eastere.gg file 

![image](https://github.com/user-attachments/assets/be7c6c7f-019e-4d51-b654-b3e20912ce54)

challenge solved but we still cannot access the file 

## Poison Null Byte

we knew that only pdf and md files are downloadable through the app thats wh we couldnt get the content of eastere.gg

![image](https://github.com/user-attachments/assets/3750c4be-e81b-43a7-b004-1d819c901121)

so we tried to manipulate the URL by including nullbytes followed by an allowed file extension 127.0.0.1:3000/ftp/eastere.gg%2500.pdf

File downloaded and challenge solved 

the content of the file was checked on the challenge that follows

## Nested Easter Egg

we started by exploring the downloaded file ``` eastere.gg ```

![image](https://github.com/user-attachments/assets/5fbb31b0-69f0-41a0-8258-d3fb07ba1fe5)


we got a base64 encoded string ``` L2d1ci9xcmlmL25lci9mYi9zaGFhbC9ndXJsL3V2cS9uYS9ybmZncmUvcnR0L2p2Z3V2YS9ndXIvcm5mZ3JlL3J0dA== ```
we decoded it using CyberChef

![image](https://github.com/user-attachments/assets/33e3e940-ac62-46c8-a78e-45070923d93d)

we found a url that took us to the nested easter egg

![image](https://github.com/user-attachments/assets/8ddaa35c-1a8e-402d-9f7c-d7ac3da30a64)


# conclusion

This practical work wasn’t just about using tools like OWASP ZAP, Burp Suite, or Gobuster. It was about exploring, experimenting, and sometimes failing before finding the right approach. I navigated through the challenges with a focus on understanding the underlying security flaws. 

Each task provided practical experience and highlighted how simple misconfigurations or oversights and sometimes just the coding logic can lead to security issues. This exercise was a good way to reinforce key concepts in web application security while gaining hands-on exposure to penetration testing.
