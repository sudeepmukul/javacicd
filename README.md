# Q1 — Java CI/CD using Jenkins Freestyle, GitHub and Maven

## Files
- `src/main/java/App.java`: Java application
- `pom.xml`: Maven build/package configuration

## 1. Check prerequisites
On the Windows machine running Jenkins, verify:
```powershell
git --version
java -version
mvn -version
```
Jenkins must be able to access Git, Java and Maven in its own PATH.

## 2. Push project to GitHub
Create an empty GitHub repository named `q1-java-freestyle`. Open a terminal in this folder:
```powershell
git init
git add .
git commit -m "Add Java CI project"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/q1-java-freestyle.git
git push -u origin main
```
Replace the username/repository URL with your own.

## 3. Create Jenkins Freestyle job
1. Open Jenkins at `http://localhost:8080` (if that is your configured address).
2. Select **New Item** → enter `Q1-Java-Freestyle` → **Freestyle project** → OK.
3. Under **Source Code Management**, select **Git**, enter the repository URL, and set branch to `*/main`.
4. Under **Build Triggers**, select **Poll SCM** and enter `H/2 * * * *` to check for changes periodically.
5. Under **Build Steps**, add **Execute Windows batch command**:
   ```bat
   mvn -B clean package
   ```
6. Under **Post-build Actions**, archive artifacts using `target/*.jar`.
7. Save → **Build Now** → open **Console Output** and confirm `BUILD SUCCESS`.

## 4. Demonstrate a source change
Edit the print message, then:
```powershell
git add .
git commit -m "Update Java message"
git push
```
Wait for polling or click **Build Now**. Show the new build and JAR artifact.

## Result
Jenkins checks out the Java project from GitHub, compiles it and packages it as a JAR using Maven.
