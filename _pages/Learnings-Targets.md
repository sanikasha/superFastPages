---
layout: page
title: Learning Targets
permalink: /learningtargets/
---

<h1>Vocab</h1>
| Word     | Pseudocode | Python | Def/Purpose |
| ----------- | ----------- | ----------- | ----------- |
| Output     | DISPLAY(expression) | print(expression, end=” “) | Displays the value of expression, followed by a space. Python defaults to newline, thus the end=” “ |
| Input   | a ← INPUT() | 	a = input(prompt) | Accepts a value from the user and returns it to the variable a. |
| Assignment | a ← expression | 	a = expression | Evaluates expression and assigns the result to the variable a. |
| Lists | | [] | a way to group data into ordered sequences |
| Dictionaries | | {} | a way of grouping data into in key-value relationships |
| HTML Fragments | | | HTML fragments are portions of code used in a greater coding system that enable functionality specific to the current page |
| API | | | A Web API is an application programming interface typically for a web browser. |
| Frontend | | | Front-end web development is the development of the graphical user interface of a website, utilize HTML and JavaScript |
| Backend | | | Functionality, code that connects the web to a database, manages user connections, and powers the web application itself |
| Deployment | | | Deploying a Web Application enables a Server and Web Application to be available to users on the Internet |


<h1>Deployment Resources</h1>
| Resources     | Purpose |
| ----------- | ----------- |
| EC2 | a cloud computing platform that the PUSD district has provided for their students to serve our Web Application |
| GitHub | The leading open platform to share a code across the Internet. |
| Docker and docker-compose | Docker container prepares an environment that contains the Web Application code and all the dependencies (requirements.txt for Python) Docker is an open platform for developing, shipping, and running applications. |
| Nginx | Nginx is an open source software for web serving, reverse proxy, caching, load balancing, media streaming, and more. |

<h1>AWS</h1>
Start SSJN on Flask:
cd ~/p3t2_ssjn_flask/
source webapp/bin/activate 

Curl:
http://localhost:8032

Update from AWS:
cd ~/p3t2_ssjn_flask/
sudo docker-compose ps
sudo docker ps
git status
sudo docker-compose kill
git pull
sudo docker-compose build --no-cache
sudo docker-compose up -d


<h1>Initial Targets, Important</h1>
| Week     | Topics | Learnings |
| ----------- | ----------- | ----------- |
| 1 | Tools Setup | Create Fastpage, Creat first Jupyter notebook, Screen capture of VS Studio |
| 2 | Intro Python, Jupyter, Fastpages | Productive Blogging, Jupyter Notebook using Bash, more |
| 3 | Data Abstraction | List/Dictionaries Iteration, HTML/Markdown Fragments |



