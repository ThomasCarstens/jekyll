---
layout: single
title: "App for education"
excerpt: "A custom mobile app developed and implemented at the University of Cape Town."

header:
  teaser: assets/images/posts/app-for-education/framework.png
  overlay_image: assets/images/posts/app-for-education/framework.png
categories: Tech-Project
tags:
- Design-and/or-development
- Mobile app
- Ionic
- Angular
- Firebase
- Android app
- Ios app
toc: true
toc_sticky: true
date: 2018-11-11
gallery:
  - image_path: /assets/images/posts/app-for-education/app-pics/login.jpeg
    alt: "App pic 4"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/feed.jpeg
    alt: "App pic 3"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/picture-and-text.jpeg
    alt: "App pic 6"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/picture-and-expanded-text.jpeg
    alt: "App pic 5"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/sure-of-post.jpeg
    alt: "App pic 8"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/chat-layout.jpeg
    alt: "App pic 1"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/comment-with-pic.jpeg
    alt: "App pic 2"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/please-add-text.jpeg
    alt: "App pic 7"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/survey-link.jpeg
    alt: "App pic 9"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/survey-options.jpeg
    alt: "App pic 10"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/app-pics/update.jpeg
    alt: "App pic 11"
    title: "Some snapshots of the app"

gallery2:
  - image_path: /assets/images/posts/app-for-education/strategy-1.png
    alt: "App pic 12"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/concept-2.png
    alt: "App pic 13"
    title: "Some snapshots of the app"

gallery3:
  - image_path: /assets/images/posts/app-for-education/strategy-2.png
    alt: "App pic 14"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/concept-2.png
    alt: "App pic 15"
    title: "Some snapshots of the app"

gallery4:
  - image_path: /assets/images/posts/app-for-education/strategy-3.png
    alt: "App pic 16"
    title: "Some snapshots of the app"
  - image_path: /assets/images/posts/app-for-education/concept-2.png
    alt: "App pic 15"
    title: "Some snapshots of the app"
---

# ![favicon](/assets/images/favicon.jpg){: .aligned-left} App for an Engineering Undergraduate Course

Supervised by Bruce Kloot of Mechanical Engineering UCT, I designed and developed a mobile application for enhanced interaction in engineering learning and I implemented within two undergraduate courses.

## App Features

I made a video where I display the functionality of the app.
{% include video id="c5QMkaOH5u4" provider="youtube" %}


## Aim
The goal of this project was to design an online learning space as an effective means for students to interact with tutors in the Dynamics 1 course. It was envisioned that through this process, the students are better included and empowered in their own learning process. The final product was an application called Dynamics App. Using the app, students can now post a question in a feed for tutors to be notified immediately. The app is currently on the Google Playstore, Testflight on the iStore (contact me for the invite link) as well as a webapp. Such a tool did not exist in the UCT Mechanical Engineering Department, and it is well suited to a course that requires of students to grasp and apply various kinetic and kinematic concepts in a short amount of time. I am looking to expand it in other university courses.

### Time-bound:
4 months development.

### Limitations
There was no guarantee that students would even use the app. I simply thought it would be useful from my experience at UCT.


## Project Plan
The starting question here is: “Does the students’ use of the online space enhance their experience of the course?”. This question requires the existence of such a space, and a means to measure whether the online space has enhanced the students’ experience of the course. For the first part, the online space must be conceived, developed and implemented within the course; for the second part, an indicator is chosen to measure the success of this space.
This project was planned in a sequence of phases:

{%
include figure
image_path="/assets/images/posts/app-for-education/thesis-outline.png"
alt="Thesis outline"
caption="Thesis outline"
%}  

### Phase 1: Literature Review                                                        
Reviewing similar literature to select the most adequate indicator of success.

### Phase 2: Conceptualisation   
Researching the current means of learning so to select the most adapted concept for an online space.

The pilot project consisted of trialling three learning strategies to decide on a final concept.
I used Google Drive as a central repository, and I connected it to the local LMS, Vula.

{% include gallery id="gallery2" caption="First I allowed students to comment on the tutorials remotely (Google Drive)." %}

{% include gallery id="gallery3" caption="Then I allowed students to comment on a test and memo just after the test (using Google Drive) ." %}

{% include gallery id="gallery4" caption="Finally students were given the opportunity to upload their own work for tutors to comment (using Google Drive) ." %}

This process suggested that students are most involved when they are given the opportunity to show their work to the tutors.

### Phase 3: Development   
Developing this concept into an online space that can be implemented in the course.

{%
include figure
image_path="/assets/images/posts/app-for-education/framework.png"
alt="Software framework"
caption="Software framework"
%}

{%
include figure
image_path="/assets/images/posts/app-for-education/firebase-functionality.png"
alt="Firebase functionality"
caption="Firebase functionality"
%}

### Phase 4: Implementation   
Promoting the online space among students as a tool for learning.

{%
include figure
image_path="/assets/images/posts/app-for-education/App-Advert.png"
alt="App advert"
caption="App advert"
%}

### Phase 5: Iterations   
Iteratively developing the online space according to recommendations and maintenance issues.

{%
include figure
image_path="/assets/images/posts/app-for-education/wbs.png"
alt="wbs"
caption="Work Breakdown Structure"
%}

## Summary
I made a poster summarising the project.

### Poster
{%
include figure
image_path="/assets/images/posts/app-for-education/Poster.png"
alt="poster"
caption="Poster"
%}

### App screenshots
Here are some more screenshots of the app.
{% include gallery caption="Some snapshots of the app." %}
