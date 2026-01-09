Step 1 — Generate Maven Wrapper (one time)

Run this locally in the root of your Java project (where pom.xml exists):

mvn -N wrapper:wrapper


This creates:

mvnw
mvnw.cmd
.mvn/
└── wrapper/
├── maven-wrapper.jar
└── maven-wrapper.properties


📌 Commit these files to Git:

git add mvnw mvnw.cmd .mvn
git commit -m "Add Maven Wrapper"
git push

🧪 Step 2 — Verify locally

From the project root:

chmod +x mvnw
./mvnw -version
./mvnw clean compile


If this works locally → it will work in Jenkins.

---
Step 1: Create a Dockerfile

In the same folder as your docker-compose.yml, create a file named Dockerfile:

FROM jenkins/jenkins:lts

USER root
RUN apt-get update && apt-get install -y docker.io

USER jenkins

Step 2: Update your docker-compose.yml

Replace:

image: jenkins/jenkins:lts


with:

build: .

✅ Final version (fixed)
services:
jenkins:
build: .
container_name: jenkins-demo
ports:
- "8080:8080"
- "50000:50000"
volumes:
- jenkins_home:/var/jenkins_home
- /var/run/docker.sock:/var/run/docker.sock
environment:
- JAVA_OPTS=-Djenkins.install.runSetupWizard=true
user: root
restart: unless-stopped
networks:
- jenkins-net

networks:
jenkins-net:
driver: bridge

volumes:
jenkins_home:
name: jenkins_demo_home

Step 3: Rebuild Jenkins

Run:

docker-compose down
docker-compose up --build -d

Step 4: Verify Docker works inside Jenkins
docker exec -it jenkins-demo bash
docker --version
docker ps


If both work → 🎉 you’re done.