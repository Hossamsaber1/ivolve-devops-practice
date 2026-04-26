# Lab 1: Building and Packaging Java Applications with Gradle

## Overview
This lab demonstrates how to build, test, package, and run a Java application using Gradle on Ubuntu Linux.

You will learn how to:

- Install Java
- Install Gradle
- Install Git
- Clone project source code
- Run unit tests
- Build JAR artifact
- Run the application
- Verify output

---

## Requirements

| Tool | Version |
|------|---------|
| Ubuntu | 22.04+ |
| Java | 17+ |
| Gradle | 8.8 |
| Git | Latest |

---

## Step 1: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 2: Install Java 17

```bash
sudo apt install openjdk-17-jdk -y
java -version
```

## Step 3: Install Git

```bash
sudo apt install git -y
git --version
```

## Step 4: Install Latest Gradle

```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
echo 'source "$HOME/.sdkman/bin/sdkman-init.sh"' >> ~/.bashrc
source ~/.bashrc
sdk install gradle 8.8
sdk default gradle 8.8
gradle -v
```

## Step 5: Clone Project

```bash
git clone https://github.com/Ibrahim-Adel15/build1.git
cd build1
```

## Step 6: Run Unit Tests

```bash
gradle test
```

## Step 7: Build Application

```bash
gradle build
```

## Step 8: Verify Output

```bash
ls build/libs/
```

Expected:

```text
ivolve-app.jar
```

## Step 9: Run Application

```bash
java -jar build/libs/ivolve-app.jar
```

## Useful Commands

```bash
gradle clean
gradle clean test build
which gradle
pwd
```

## CI/CD Example (Jenkins)

```groovy
pipeline {
  agent any
  stages {
    stage('Test') {
      steps { sh 'gradle test' }
    }
    stage('Build') {
      steps { sh 'gradle build' }
    }
  }
}
```

## Final Result

```text
BUILD SUCCESSFUL
Artifact Generated: build/libs/ivolve-app.jar
```

## Author

Hossam Saber  
DevOps | Cloud | Infrastructure Engineer

