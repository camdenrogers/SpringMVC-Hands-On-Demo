# SpringMVC-Hands-On-Demo
Code and instructions for completing Spring MVC Demo.

### 1. Download the Repository

### 2. Create the build.gradle file in the root directory


*build.gradle*
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
### Create a controller

*/src/main/java/demo/DemoController.java*

```
package demo;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;

@Controller
public class DemoController {

    @GetMapping("/demo")
    public String userForm(Model model) {
        model.addAttribute("user", new User());
        return "user";
    }

    @PostMapping("/demo")
    public String greetingSubmit(@ModelAttribute User user) {
        return "result";
    }
}
```
Spring MVC uses the @Controller annotation to automatically identify controllers. Spring's dispatcher server automatically scans the classes marked with the @Controller annotation and detects any @RequestMapping annotations.

### Create a Plain Old Java Object (POJO) called User.java

*/src/main/java/demo/User.java*


```
package demo;

public class User {

    private String username;
    private String password;
    private String email;

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    private String phone;


    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

### Create the view

*src/main/resources/templates/demo.html*

```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Handling Form Submission</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<h1>Form</h1>
<form action="#" th:action="@{/demo}" th:object="${user}" method="post">
    <p>Username: <input type="text" th:field="*{username}" /></p>
    <p>Password: <input type="text" th:field="*{password}" /></p>
    <p>Email: <input type="text" th:field="*{email}" /></p>
    <p>Phone: <input type="text" th:field="*{phone}" /></p>
    <p><input type="submit" value="Submit" /> <input type="reset" value="Reset" /></p>
</form>
</body>
</html>
```

### Create the result view

*src/main/resources/templates/result.html*

```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Handling Form Submission</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<h1>Result</h1>
<p th:text="'username: ' + ${user.username}" />
<p th:text="'password: ' + ${user.password}" />
<p th:text="'email: ' + ${user.email}" />
<p th:text="'phone: ' + ${user.phone}" />
<a href="/user">Submit another message</a>
</body>
</html>
```

### Make the application executable

*/src/main/java/demo/Application.java*


```
package profile;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```
