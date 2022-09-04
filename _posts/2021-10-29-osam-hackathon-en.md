---
title:  "Participating in 2021 OSAM hackathon ✍"
excerpt: "I participated in 2021 OSAM hackathon! 😁"
toc: true

categories:
  - Hackathon
  - Review

last_modified_at: 2021-10-23T12:53:00-05:00
---

*한국어로 이 글을 읽고 싶다면, [여기를 클릭하세요]({{site.url}}/hackathon/osam-hackathon)*


# 🎉 Participating in OSAM hackathon

&nbsp;I've participated in **2021 OSAM hackathon** hosted by [OSAM](https://osam.kr) from this July to October.
&nbsp;To record what I've learned through this hackathon and help people who want to participate in OSAM hackathon next year, I decided to write a review of the hackathon.

## 🙌 Participant selection process

&nbsp;This year, OSAM picked up 200 participants through 3 selection criteria : **evaluation of theory**, **coding test**, and **Development Plan**.  
<p align="center">
<img src="/assets/images/osam-hackathon/selecting_participants.png" width="500">
</p>
&nbsp;40 people were selected for each of the five areas of Web, App, IoT, Cloud, and AI. If there is an area that does not meet the number of people, additional participants were selected from other areas.

### 📝 Evaluation of theory

&nbsp;
The **Evaluation of theory** is conducted by taking lectures in one of the five fields (Web, App, IoT, Cloud, AI) provided by OSAM and taking a test consisting of 40 questions.   

#### Lectures 
<p align="center">
<img src="/assets/images/osam-hackathon/lectures.PNG" width="465px">
</p>
&nbsp;Since I was intersted in **Web** area, I took the lectures about Web. The list of lectures is as follows :

- Understanding Open Source
- Learn Open Source License
- Introduction of Git & Github
- HTML & CSS
- JavaScript
- JavaScript class
- Using Vue.js to develop SPA

&nbsp;Since this hackathon was made to encourage soldiers to participate in open source activity, lectures about open source were included in the list.   

#### Study more!
&nbsp;Since lectures provided by OSAM were consisted of basic concepts only, I studied more about JS and Vue through websites below :

- [The Modern Javascript Tutorial](https://javascript.info)
- [Official tutorial of Vue.js](https://vuejs.org/v2/guide/index.html)

&nbsp;Because I studied in advance like this, I was able to save a lot of time when I participated in Hackathon later. 👍 

#### Test
&nbsp;The test was consisted of 40 questions, and the time was limited to 60 minutes. Because problems were only about basic concepts, the test was very easy. I scored 97 out of 100.

### 👨‍💻 Coding Test
&nbsp;Coding Test was conducted at **[Programmers](https://programmers.co.kr/competitions/1585/2021-practice-coding)**

&nbsp;The test consisted of four questions. First two problems were kind of easy problems about string, and later two problems were so hard that I couldn't even figure out what they were about... 😅 The time limit was two hours. I got 177.6 out of 400...😇

### 📈 Development Plan
&nbsp;In development plan, I had to write about the project that I want to work on. The plan form was given as follows :

- Name of the project
- A general outline of the project
- Development plan & purpose
- The expected effects and prospects

&nbsp;I wrote about a web service that supports soldiers reading book. 

### 🥳 Successed to participate in the hackathon!

<p align="center">
<img src="/assets/images/osam-hackathon/success.png" width="600px">
</p>

&nbsp;On August 27, 2021, the results of the selection of Hackathon participants were posted on OSAM's notice board. I didn't expect much because I didn't do well on the coding test and there would be many applicants in the Web field, but fortunately, I was able to participate in the hackathon. 🙌    

## 🔥 Working on Project

&nbsp;You can check the **Handover** project I participated in [**here**](https://github.com/osamhack2021/Web_Handover_Handover).

### 👨‍👨‍👦 Collaborating with Team members
&nbsp;**Team Handover** were consisted of 3 Frontend developer, 2 Backend developer, and 1 designer. As there were many team members, it was very important to set up a collaboration method well. Thanks to the leader of the team, we could create a very good collaboration environment through Slack and Notion.

<p align="center">
<img src="/assets/images/osam-hackathon/slack.png">
</p>

Our team mainly communicated through Slack, and formed a channel as above. Some characteristic channels are as follows :

- **#dev-record** : On this channel, we wrote the time we started and finished developing everyday so that we could check what others are working on, and cheer up each other. 🙌

<p align="center">
<img src="/assets/images/osam-hackathon/dev-record.png" width=600px>
</p>

- **#update-github** : It is a channel using a github bot on the slack. If any of the team members was engaged in activities such as pushing a commit to Handover's repo or creating an issue, the contents could also be checked on the slack.
- **#update-notion** : Similar to #update-github, if someone modifies Handover's Notion, the content can be checked on the slack.

In the case of **Notion**, it was used as a library to share documents to refer to together. It contained a list of open-source text editors surveyed at Handover's planning stage, and API-related documents prepared by backend developers for frontend developers.

<p align="center">
<img src="/assets/images/osam-hackathon/notion.png" width=500px>
</p>

In addition, through meetings at **zoom** every weekend, we shared curent progress of each other. We also used **Google Slides** and **Google Docs** when working on submissions.

### 🔧 Development process
&nbsp;Since this was the first time I've ever participated in Web development, I couldn't follow up every process of our team...😥 So I'm going to write only about the part I worked on.

#### Hello, React 😂
&nbsp;Although I studied Vue hard to participate in Hackathon, our project was developed using **React**.

&nbsp;Since our team's frontend developers except me knew how to use React, our team decided to use React. Fortunately, backend developers started developing first, and I was given about two weeks to study React waiting for backend developers. In addition, I had to study the Material-UI, Sass, and Redux that we decided to use in the project. It's been a really busy two weeks.

<p align="center">
<img src="/assets/images/osam-hackathon/develop1.png" width=600px>
<br>
<i>I studied hard writing to do list every day..</i>
</p>

#### Making a layout
&nbsp; First of all, frontend team produced a layout of pages as the design provided by the designer. In consideration of me, the team leader assigned me with the production of simple login, registration, and recovery pages. It took quite a while for me to get used to web development. 😂

&nbsp I made a layout of login, registration, recovery, profile, profile setting page. (Design of the pages were changed later though...)

<p align="center">
<img src="/assets/images/osam-hackathon/develop2.png" width=600px>
<br>
<i>Initial layout of Login Page</i>
</p>

#### Implementing functions

&nbsp; Since backend development was almost finished as frontend developers almost finished making layouts, frontend developers started to **implement functions** of each pages. Although I started React hard, I couldn't work on pages by myself...😥 Codes of pages that I worked on were almost written by using the code of the boilerplate or referring to the team member's code. Still, I successed to make most of the pages I made the layout work well with dummy data.

#### Connecting with Backend
&nbsp; It was really hard for me to connect the backend and the frontend using APIs made by backend developers, since it was the first time I'm working with API. 🤯 I have worked on registeration page, profile setting pages, and profile page.

## 🌟 Submissions

&nbsp; You can check out the repository of Handover project [here](https://github.com/osamhack2021/Web_Handover_Handover).
&nbsp; Also, you can check out the video showing how Handover works [here](https://drive.google.com/file/d/149TNAh23DhGnmvNqapcNVphTsnZ--FoD/view). (It's in Korean 😅)

## 🚀 Epilogue

&nbsp;
OSAM Hackathon became a great vitality in my boring military life. I was able to learn so many things and meet a new world for about three months. Thanks to the participation of Hackathon, I started blogs, gained the courage to participate in many competitions in the future, and became motivated to study harder. I am very grateful to the team members and mentors with OSAM for holding such a good competition. If I have another opportunity to participate in such a competition in the future, I will challenge without hesitation. 🤗

## 🎊 We won the CNO award!

<p align="center">
<img src="/assets/images/osam-hackathon/OSAM_award.PNG" width="600px">
</p>

&nbsp; On November 11, 2021, the results of 2021 OSAM Hackathon were finally announced. My Handover team won the **Chief of Naval Operations Award**. 🙌
Of course, I was happy to receive the award, but I felt a little ashamed because I didn't contribute much to the development of the project. I should work harder thinking that I was just lucky this time. 🏃‍♂️