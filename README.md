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



