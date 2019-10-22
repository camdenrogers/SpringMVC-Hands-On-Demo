# SpringMVC-Hands-On-Demo
Code and instructions for completing Spring MVC Demo.

### 1. Download the Repository

### 2. Create the build.gradle file in the root directory

```
plugins {
	id 'org.springframework.boot' version '2.1.8.RELEASE'
	id 'io.spring.dependency-management' version '1.0.8.RELEASE'
	id 'java'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '1.8'

repositories {
	     mavenCentral()
}

dependencies {
	     implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	     implementation 'org.springframework.boot:spring-boot-starter-web'
	     testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```
