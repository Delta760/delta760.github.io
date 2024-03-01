---
toc: true
comments: false
layout: post
title: College Board Final Individual
description: My reflection on my work for CPT Project
courses: { compsci: {week: 1} }
type: tangibles
---

## Condensed project overview
We created a game centering around a sort of turn based combat against an invisible AI. The player has the opportunity to either move or attack one of the postions he ajacent to or move to an ajacent space. The game will notify you if the AI is within one space of you and if you hit it you win. However, if the AI hits you before you hit it you will lose. The game will store your wins on the global leaderboard (we ran out of time to do this automatically but we can store wins) and you can choose different classes to enhance your expierence.

## My Feature
My feature in the project is ordering and creating the main menu screens as well as the implementation of the JWT tokens in order to differentiate not only admins and players but also individual users.

[Link to where I got my Collegboard Requirments](https://apcentral.collegeboard.org/media/pdf/ap-csp-student-task-directions.pdf)

| Collegeboard Requirements | Me |
|------------------|------------------|
| Instructions for input from one of the following: the user, a device, an online datas stream, a file.  | Our Project takes input from the player on where they want to move and attack.  |
| Use of at least one list (or other collection type) to represent a collectino of data that is stored and used to manage program complexity and help fulfill the users purpose.  | An example of a collection of data that is stored is of the collection of class abilities as well as indivual user data such as wins and password. <a><img src="https://i.postimg.cc/NjnY9pG6/Screen-Shot-2024-03-01-at-11-28-18-AM.png"></a>
| At least one procedure that contirubted to the program's intened purpose where you have defined: the name, return type, one or more parameters:  | This procedure has a name(read), a return(response), and parameters(self): <a><img src="https://i.postimg.cc/LsVTQ0qf/Screen-Shot-2024-03-01-at-11-31-47-AM.png"></a>  |
| An algorithm that includes sequencing, selection, and iteration that is in the body of the selected procedure  | This function shows the sequencing, selection, and iteration through a list of meme images: <a><img src="https://i.postimg.cc/rpnkXj30/Screen-Shot-2024-03-01-at-11-38-16-AM.png"></a>  |
| Calls to your student-developed prodcedure:  | calling queryImages: <a><img src="https://i.postimg.cc/pTJKL9QF/Screen-Shot-2024-03-01-at-11-41-00-AM.png"></a>  |
| Instructions for output (tactile, audible, visual, or ) based on input and program functionality  | This code is the fetch that displays the user data that was used in the leaderboard screen: <a><img src="https://i.postimg.cc/Kz14dRqb/Screen-Shot-2024-03-01-at-11-44-30-AM.png"></a>  |

# Component B: Video

[Link to Video](https://drive.google.com/file/d/1ZfDdQ5x0vMFbANHlCg8nE2eyQTTgQG3Z/view?usp=sharing)


| Collegboard Requirements | My Video |
|------------------|------------------|
| Input to program  | Seen in video, login in which gives the user the jwt token  |
| At least one aspect of the functionality of your program| When the token is removed you cannot acces the leaderboard (403 error)  |
| Output produced by program:  | When you have the jwt token coordinated to your user you can access the leaderboard.  |
| My video does not have: | any distinguishing information and voice narration  |
| My video is | a .webmb, less than 1 minute in length, less than 30MB in file size.  |