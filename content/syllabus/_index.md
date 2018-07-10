---
title: "Syllabus"
description: "This is the course syllabus. It contains important course information from including things like grading and contact policies."
categories: ["Syllabus"]
weight: 1
---

# CS 512 (aka 519) Data Science Tools and Programming

## 4 Credits

## Description
Accessing and distributing data in the cloud; relational and non-relational databases; map reduction; cloud data processing; load balancing; types of data-stores used in the cloud; data processing.

### Instructor: Justin Wolford
wolfordj@oregonstate.edu

### Course Learning Outcomes
1. Use appropriate tools to access and store distributed data
1. Design programs to analyze distributed data
1. Evaluate various storage and access options for large data sets
1. Evaluate existing programs to find and remove bottelnecks in data processing
1. Understand differences between relational and non-relational databases
1. Use tools to clean and transform datasets for use in database systems
1. Create visualizations of large data sets

### Required Materials
None. All additional resources will be online tutorials, articles or books.

## Weekly Course Calendar

1. Review, Overview and Tools \[1\]
    * Python
    * Google Cloud Setup
2. Relational Databases \[5\]
    * Cloud SQL using MySQL
3. Data cleaning for use in databases \[6\]
    * Cloud Dataprep
4. Data visualization \[7\]
    * Matplotlib
5. Project
6. NoSQL Databases \[5\]\[3\]
    * Google Bigtable
    * Google BigQuery
7. Map Reduce \[2\]\[4\]
    * Google DataProc
    * Spark
8. Map Reduce Continued
9. Project
10. Buffer Week

## Grading
| Percentage    |   Grade |
--------------  |----------
93              | A
90              | A-
87              | B+
83              | B
80              | B
77              | C+
73              | C
70              | C-
67              | D+
63              | D
60              | D-
0               | F

## Grade Weights
Final Project 30% \
Homeworks 70%

## Late Policy
Assignments are not accepted late. If you need an extension for any reason the request must be submitted at least 72 hours in advance, typically a 48 hours is the maximum extension, but no documentation is required. If you need an **emergency** extension it must be requested within 48 hours *after* the assignment was due and must be accompanied by documentation supporting the request (eg. doctors note, visit summary from the ER, police report etc.). As long as there is supporting documentation these are generally granted for up to a 48 hour extension. Longer extensions are handled on a case by case basis.

## Fixing Work
Sometimes you need to make changes to a program or an assignment to get it to run correctly. You will have 7 days from when an assignment is graded to resubmit the assignment for a maximum grade of 70%. These can only be minor changes to get a program to run. You can't write a program from scratch and still get 70% credit.

## Assignments
There will generally be an assignment every week. They are graded on correctness only. A program that fails to run will typically get no credit, even if all you had to do was add a `:` to make it run. If you want feedback on specific choices you made in your program you can post the code and the specific questions to the discussion board 48 hours after the assignment is due and the instructor and TAs can provide additional feedback there that you and other classmates can benefit from.

### Assignment format
Unless otherwise specified all files should be be submitted as `.py` files if they are code files or as `.pdf` files if they are written documents. You should always submit all of the `.py` files you wrote for a project even if we will not be running them so we have a record of your program if we need to come back and look at it later. Files should **not** be zipped because that makes them hard to view in the Canvas grading tool. If we want a zipped file set we will ask for it specifically.

## Final Project
This class will have a final project. This will require you to do calculations, visualization and analysis of a very large data set, ideally in the tens to hundreds of millions of records. More details will be released on this later in the course.

## Incoming Expectations
This course is made for data science students who have completed CS511, the *Introduction to Python Programming for Statistics* course. You will be expected to use many third party programs and will need to be comfortable doing basic tasks using a command line. The emphasis of this course is on the data science tools and on programming. There should be many opportunities to use more advanced statistical methods, but they will not be covered in this course.

## Tools
This course will primarily be about using Googles suite of cloud and big data tools. These tools are generally based on Python 2.7 however other tools will likely leverage Python 3.6. This isn't a fun place to be in but we can deal with it.

Ideally, if you can get [Anaconda](anaconda.org) installed and running with two different environments, one running Python 2.7 and the other running Python 3.6 you will be ahead of the curve.

You may also find it useful to install the [Google Cloud SDK](https://cloud.google.com/sdk/) but you should be aware this can be a little challenging.

## Real World Stuff
The Google set of tools are professional tools used in industry. This is awesome because it means that employers will be excited you know how to use it. It also means that Google requires cash money to use it. As part of the class you will get $50 in Google cloud credit. This should be plenty to get through the course. But you need to be careful. If you leave a service running, get something stuck in an infinite loop or accidentally request to use a cluster of 1000 servers instead of 10 you might quickly burn through that budget.

The instructor will do what they can to help in that sort of situation, but if you do something wrong and it eats up all your credit you **may** need to pay for additional computation time if Google is unable to provide additional credit.

## Getting Help With Tools
Speaking of challenges, when you run into trouble, please seek help. When it comes to software configuration issues like installing Anaconda or the Google SDK if you do the wrong thing to solve a problem it can make it harder to fix.

Try to follow the online documentation. If it does not work, don't improvise unless you are confident in your skills. It is better to come to the message board and ask for help. When you do please post:

* The steps you have taken
* The last thing you did that seemed to work correctly
* The full error message, this might be very long. If it is more than a page there are sites like [Pastebin.com](pastebin.com) that are designed for posting and sharing code snippets and errors.
* Where else you have looked for solutions so I don't point you to something you already looked at

## Communications
There are several ways to communicate in an online class, they all have different purposes.

### Message Board
We will use Piazza as a discussion platform. This is where you should post well prepared questions, both technical and theoretical about the content and assignments. You should follow similar steps to *Getting Help With Tools* when asking questions here.

You should not ask about any personal information on Piazza. For example it is not the place to ask about why you lost points on an assignment or to request an extension for an assignment.

### Email

All emails to the instructor or the TA should have, as the first 7 characters in the email title \[CS519\] or \[CS512\]. This makes sure it goes to the right email box. If it does not have this tag at the beginning of an email it may get overlooked. 

#### Instructor
You should email the instructor about general class concerns, extension requests or about issues you are unable to resolve with the TA. In general questions about the assignment or help with troubleshooting should go to Piazza where they can help other students. If you email the instructor these questions they might just ask you to post them to Piazza.

If you **did** post a question to Piazza and no one has answered it in 24 hours during weekdays then you can email the instructor to call attention to it and they will come answer it on Piazza. In general the instructor tries to answer questions before this but sometimes they are missed.

#### TA
You should email the TA grade related questions. If you do not understand why you got a deduction or think that they may have missed something while grading contact them and CC the instructor. The instructor will not look at or change grades until you have contacted the TA first. The TA will know better why they graded something the way they did than the instructor.

If, after emailing the TA, they are unable to resolve your issue then you should email the instructor, forwarding your exchange with the TA.

### Office Hours
The TAs will hold regular office hours for general troubleshooting and questions. This is often a good place to get help working through error messages.

The instructor will meet online with students by appointment. The office hours are held online using WebEx.

## Expected Response Time
These times only apply to the weekday. The instructor will try to be available on the weekend but it should not be expected.

|Medium |Time   |
--------|-------
Email   |48 Hours
Message Board|24 Hours
Grades  | 1 Week

If you do not get a response in the above listed times, email again and include the tag \[second attempt\] after the course tag in the email title and it will get more urgent treatment. If you use this tag and the above listed times *have not elapsed* the instructor might be a little grumpy.

As an example if you email on Friday at 4pm, you might not get a response till Tuesday at 4pm. This is a upper bound. Responses will usually come more quickly but sometimes things happen and it takes awhile to get back to you.

Grades usually come back within a week but some of these assignments can be complex so you might see a couple assignments which take longer.

## Difference with On Campus Classes
In an on campus class about 1/2 to 1/3 of the class would be the instructor lecturing at you. The rest of the time would be used to do in class examples and work as small groups. This is where you would test your understanding of the topics and ask your group mates for help. It is also where you would help your fellow students. If you were totally stuck the instructor would help.

In principle online learning should be about the same. But instead of a classroom you have a message board. You should be active on the message board to help and get help from your classmates. When everyone gets stuck the instructor can help get the class unstuck. But the value of the class comes in your ability to get help from other people learning the same thing at the same time and having an instructor to help guide that learning. If you are not active on the discussion board you will get much less out of the class.

## Plagiarism
Keeping with the idea of needing to communicate with your classmates, you will need to share code with each other to communicate ideas and to explain problems. That said, you should only share what is needed. This is good practice in general. Having to look through an entire file to find a single function is not helpful when you could have just posted the functions.

You will also get great help from your classmates. If you use a code fix or suggestion from them you need to do two things.

1. You need to cite who it came from, that means you need to, in your code, add a comment saying that the code was not your original code and say what student or 3rd party provided it.
1. You need to document what the code is doing. So you should write roughly a sentence per line of code explaining what the snippet is doing. So if you were to say, use an entire 100 line file provided by a student you would need to write something around a 2,000 word essay describing what the code is doing.

When giving help, don't give more help than is needed. Try to keep answers deep in depth but narrow in focus. Address the problem the student is asking about and address it well, but keep from giving away too much about topics they might not have run into yet.


## Accommodations
Accommodations for students with disabilities are determined and approved by Disability Access Services (DAS). If you, as a student, believe you are eligible for accommodations but have not obtained approval please contact DAS immediately at 541-737-4098 or at [http://ds.oregonstate.edu](http://ds.oregonstate.edu). DAS notifies students and faculty members of approved academic accommodations and coordinates implementation of those accommodations. While not required, students and faculty members are encouraged to discuss details of the implementation of individual accommodations.