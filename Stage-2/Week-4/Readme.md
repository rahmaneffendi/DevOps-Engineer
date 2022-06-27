# Final Task 

# 1.REPOSITORY

Before you start the task, please read this:

- Please screenshot the command - step by step

- Describe the process in your final task repository

Requirements

- Create your own repository for housy frontnend & backend

- Create your repository for the answer final task

Instructions

- Clone housy-frontend https://github.com/dumbwaysdev/housy-frontend

- Clone housy-backend https://github.com/dumbwaysdev/housy-frontend

- Change git remote to your own repository

- Create branch Development , Staging and Production

# 2.SERVER

Before you start the task, please read this:

Please screenshot the command - step by step

Describe the process in your final task repository

Requirements

Dont use App Catalog in IDCH

Server App (Frontend & Backend) or (Frontend, Backend, Database), 2 Core 2Gb RAM

Server Nginx, 1 Core 1Gb RAM

Server Monitoring, 1 Core 1Gb RAM

Server CI/CD , 1 Core 2Gb RAM

Server Database, 1 Core 1Gb RAM

For disk use default Instructions

Create multiple server with load balancing (Frontend and Backend)

Create security with ufw for all of server , adjust to your port application

Other than nginx, don't use elastic IP

# 3.USER

Before you start the task, please read this:

Please screenshot the command - step by step

Describe the process in your final task repository

Requirements

Custom user for every server with password

Instructions

Create user with password

Disable sign in without password

# 4.SSH

Before you start the task, please read this:

Please screenshot the command - step by step

Describe the process in your final task repository

Requirements

SSH Key for access the server without username & password

SSH Key for connect from one server to another server

SSH Key for access the git without username & password

Instructions

Create SSH Key with your initial name like this : alvin@dumbways

Use the same SSH Key for CI/CD

# 5.DATABASE

Before you start the task, please read this:

Please screenshot the command - step by step

Describe the process in your final task repository

Requirements

Setup database SQL with PostgreSQL

Instructions

Setup PostgreSQL with Docker

Set the volume location in /home/username/

Allow database to remote from another server

Create database housy and create table with sequelize

Alternative to convert MySQL database to PostgreSQL : https://pgloader.io

# 6.WEB SERVER

Before you start the task, please read this:

Please screenshot the command - step by step

Describe the process in your final task repository

Requirements

Web server nginx / apache2

For reserve proxy and SSL configuration

Instructions

Setup web server nginx / apache2

SSL support - Cloudflare (Don't use Certbot)

Make LoadBalancing

Reverse proxy the frontend -> https://name.studentdumbways.my.id

Reverse proxy the backend -> https://api.name.studentdumbways.my.id

Reverse proxy the nodeexporter -> https://exporter.name.studentdumbways.my.id

Reverse proxy the prometheus -> https://prometheus.name.studentdumbways.my.id

Reverse proxy the grafana -> https://monitoring.name.studentdumbways.my.id

Reverse proxy the Jenkins -> https://pipeline.name.studentdumbways.my.id

# 7.DEPLOYMENT

Before you start the task, please read this:

Please screenshot the command - step by step

Describe the process in your final task repository

Requirements

Deployment housy frontend

Deployment housy backend

Instructions

Please read the instruction for deploy the apps

Use the branch production

Deploy applications with docker

Integration dumbflix frontend, backend and database

Use command production to run the application -> not npm start

Reverse proxy the frontend -> https://name.studentdumbways.my.id

Reverse proxy the backend -> https://api.name.studentdumbways.my.id

# 8.CI/CD

Before you start the task, please read this:

- Please screenshot the command - step by step

- Describe the process in your final task repository

Requirements

- Auto deployment for applications

- Make 2 job with Pipeline for production and Use Publish Over SSH for Staging

Instructions

- Deploy CI/CD (Jenkins) tools with Docker

- Set the volume in /home/username/

- Setup job for frontend & backend

- Trigger by push

# 9.MONITORING

Before you start the task, please read this:

- Please screenshot the command - step by step

- Describe the process in your final task repository

Requirements

- Monitoring multiple server

Instructions

- Setup monitoring tools (Prometheus & Grafana) with docker

- Integration monitoring to all of servers

# 10.AUTH

Before you start the task, please read this:

Please screenshot the command - step by step

Describe the process in your final task repository

Requirements

Disable access for public content

Instructions

Disable prometheus for public

Set username and password to open the site

