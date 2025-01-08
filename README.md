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

# 


## Repetitive Registration

## Error Handling 

## Outdated Allowlist 

## Confidential Document 

## Bully Chatbot 

## Missing Encoding 
