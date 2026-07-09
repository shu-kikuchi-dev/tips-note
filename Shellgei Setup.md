# **Shellgei Setup**

### Premise

* installed Git
* installed Docker
* installed Docker desktop



There are numerous ways of setup the environment for shellgei. Since shellgei is handeld with Linux, we also use Linux in this setup.



The important purposes of this setup are:



* Keep clean your local machine
* High reproducibility
* Robust
* Easy to setup



We will get those good characteristics through the combination of Doker and Git.



Simply put, Docker is a platform to handle the virtual machine with high reproducibility, meaning you call each environment you made with Docker, Container. Those containers are completely separated from other containers and your local machine as all virtual machine platforms do.



But, one significance is existing, that is Image for docker. Image is a file that describing all information about the container. This file is named Dockerfile uniformly as we do as .gitignore. We name .gitignore to .gitignore whenever, for any circumstances.



### Section 1. Setup

##### Step 0. Concept

We will use Docker and Git to get the strength I enumerated above. Docker has a role to keep your local machine clean, give high reproducibility through Image with using virtual environment.



And, Git put it in the Internet for usefulness. It is very convenient that you can download some configuration files and easily reproduce the completely same environment as you did before.



##### Step 1. Prepare the directory

You can put your repository in arbitrary directory. For example, if you have your own workspace you usually use, put the folder named "shellgei-study" or something like that there.



##### Step 2. Make some files

You have to create below files:

* .gitignore
* docker-compose.yml

To make those files with unique extensions, you better open the directory you made in Step 1. with VS Code. In VS Code's explorer, just make new file and name it as above.

&#x20;

.gitignore will decide what kind of file will be rejected and what will go through the censorship. docker-compose.yml will do some routine command typing we set for us.



For instance, you can set those files like:



<.gitignore>{

\# --- OS specific files ---

.DS\_Store

Thumbs.db

db.sqlite3



\# --- Editor/IDE specific ---

.vscode/

.idea/

\*.swp

\*\~



\# --- Shellgei temporary outputs ---

tmp\*

\*.out

\*.tmp

\*.png

\*.jpg

\*.gif

\*.pdf



\# --- Docker ---

.env

}



<docker-compose.yml>{

services:

&#x20; shellgei:

&#x20;   image: theoldmoon0602/shellgeibot:latest

&#x20;   container\_name: shellgei-env\_26-07-09

&#x20;   volumes:

&#x20;     - ./src:/src

&#x20;   working\_dir: /src

&#x20;   tty: true

&#x20;   stdin\_open: true

&#x20;   command: /bin/bash

}



Adding some explanation about docker-compose.yml, it will decide what Image we use. In this sample .yml file, we use theoldmoon0602/shellgeibot. This Image is provided from the official(?). That setting is so professional as unreachable by our beginners' wisdom. There is no way not to use the official one, especially for beginners.



And, We set the name of container, the directory we want to volume, the working directory and so on.



Volume is a quite important concept of Docker. When we use numerous containers to manage numerous conditions, it is troublesome to install Editor one by one. Especially when you have your own personal settings you always do, the situation get more worse.



We just want to change executing environment for each situation, but we do not want to change editor environment.



To dodge this problem, we volume the work directory that you put your source files. Through volume, you can synchronize your local machine's file contents of one directory to one directory of your virtual machine. So, we need to set the both directory and we did that in the example.



\[- ./src:/src] simply means, \[- {your local machine directory}:{your virtual machine directory}



And, at the line \[working\_dir: /src], you set the work directory of your virtual machine.



##### Step 3. Open your Docker Desktop

Just click your Docker Desktop icon, it will boot your docker in back ground. Click the button shaped "^" you see at the right of the task bar to check Docker was started. If you see the icon of Docker, it indicates you are going well.



##### Step 4. Launch the environment

Execute these command in your local machine, at the directory you put the file docker-compose.yml.



> docker-compose up -d	# This will take a long time for the first time execution

> docker-compose exec shellgei bash



Now, you are in your virtual machine. Try below command:



> echo "Hello Shellgei" | echo-sd



You will see a funny print.



### Section 2. In your daily works

Just execute below commands in order after turn on the docker.



> docker-compose up -d

> docker-compose exec shellgei bash



When you want to quit, execute below:



> exit

> docker-compose stop

