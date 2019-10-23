# SpringMVC-Hands-On-Demo
These are the steps required to create a basic application with the Model-View-Controller (MVC) pattern. In this application, we will be able to create users, and see the full list of users and their details.

### Prerequisites
1. Gradle installed on your computer (I will be using Gradle and this repo is set up using Gradle, but you can also use  Maven)

2. An IDE with Gradle integration (Preferably IntelliJ)

### 1. Download Repository and Import Project into IDE
<br/>

### 2. Create Controller

@Controller - Annotation used by Spring so its dispatcher server can automatically identify controllers

@RequestMapping - Annotation used by Spring to map web requests onto handler classes and methods depending on the URI. @PostMapping and @GetMapping are annotations that map POST and GET requests.

@RequestParam - Annotation used by Spring to bind request parameters to a method parameter in your controller. In this case, the parameters firstName, lastName, email, and password are request parameters within the POST request. 

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
<br/>
<br/>

### 3. Create Models

This is just a Plain Old Java Object (POJO) that will represent the data we are working with for this demo application. 

*/src/main/java/demo/User.java*

```
package demo;

public class User {

    private String firstName;
    private String lastName;
    private String email;
    private String password;

    public User(String firstName, String lastName, String email, String password) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.password = password;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```
<br/>
<br/>

This class handles storage and access to User objects. This is not practical, but it mimics a database and will help understand MVC better so that when you start using a database, Spring and MVC make a little more sense.

*/src/main/java/demo/UserData.java*

```
package demo;

import java.util.ArrayList;

public class UserData {

    static ArrayList<User> users= new ArrayList<>();

    public static ArrayList<User> getAll(){
        return users;
    }

    public static void add(User newUser){
        users.add(newUser);
    }
}
```
<br/>
<br/>

### 4. Create Views

Our views are using Thymeleaf as the template engine

*/src/main/resources/templates/add.html*

```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Handling Form Submission</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<h1>Form</h1>
<form action="#" th:action="@{/add}" th:object="${user}" method="post">
    <p>First Name: <input type="text" name="firstName"></p>
    <p>Last Name: <input type="text" name="lastName"></p>
    <p>Email: <input type="text" name="email"></p>
    <p>Password: <input type="text" name="password"></p>
    <p><input type="submit" value="Add User"></p>
</form>
</body>
</html>
```
*/src/main/resources/templates/home.html*

```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
    <body>
    <table>
        <thead>
            <tr>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Email</th>
                <th>Password</th>
            </tr>
        </thead>
        <tbody>
            <!--
            <tr th:if="${users.empty}">
                <td colspan="2"> No Users to Display</td>
            </tr>
            -->
            <tr th:each="user : ${users}">
                <td><span th:text="${user.firstName}"> First Name </span></td>
                <td><span th:text="${user.lastName}"> Last Name </span></td>
                <td><span th:text="${user.email}"> Email </span></td>
                <td><span th:text="${user.password}"> Password </span></td>
            </tr>
        </tbody>
    </table>
    <a href="/add">Add a User</a>
    </body>
</html>
```
