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

