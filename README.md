# SpringMVC-Hands-On-Demo
Code and instructions for completing Spring MVC Demo.

### Download the Repository

### Create a controller

*/src/main/java/demo/DemoController.java*

```
package demo;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class DemoController {

    @GetMapping("")
    public String home(Model model){
        model.addAttribute("users",UserData.getAll());
        return "home";
    }

    @GetMapping("/add")
    public String userForm(Model model) {
        //model.addAttribute("user", new User());
        return "addUser";
    }

    @PostMapping("/add")
    public String greetingSubmit(@RequestParam String firstName, @RequestParam String lastName, @RequestParam String email, @RequestParam String password) {
        User newUser = new User(firstName,lastName,email,password);
        UserData.add(newUser);
        return "redirect:";
    }
}
```

@Controller - Annotation used by Spring so its dispatcher server can automatically identify controllers

@RequestMapping - Annotation used by Spring to map web requests onto handler classes and methods depending on the URI. @PostMapping and @GetMapping are annotations that map POST and GET requests.



### Create a User model class as a Plain Old Java Object (POJO) called User.java

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
<a href="/demo">Submit another message</a>
</body>
</html>
```

### Make the application executable

*/src/main/java/demo/Application.java*


```
package demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Create a class to handle storage and access to User objects. This is not practical, but it mimics a database and will help understand MVC better so that when you start using a database, Spring and MVC make a little more sense.
