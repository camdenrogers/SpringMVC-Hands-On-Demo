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

@RequestParam - Annotation used by Spring to bind request parameters to a method parameter in your controller. In this case, the parameters firstName, lastName, email, and password are request parameters within the POST request. 

### Create a Model

*/src/main/java/demo/User.java*

```
package demo;

public class User {

    private String firstName;
    private String lastName;
    private String email;
    private String password;
    private int userId;
    private static int nextUserId = 1;

    public User(String firstName, String lastName, String email, String password) {
        this();
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.password = password;
    }

    public User(){
        userId = nextUserId;
        nextUserId++;
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

    public int getUserId() {
        return userId;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }
}
```
*/src/main/java/demo/UserData.java*

```
package demo;

import org.springframework.web.bind.annotation.ModelAttribute;

import java.util.ArrayList;

public class UserData {

    static ArrayList<User> users= new ArrayList<>();

    public static ArrayList<User> getAll(){
        return users;
    }

    public static void add(User newUser){
        users.add(newUser);
    }

    public static void remove(int id){
        User userToRemove = getByUserId(id);
        users.remove(userToRemove);
    }

    public static User getByUserId(int id){
        User foundUser = null;

        for(User possibleUser : users){
            if(possibleUser.getUserId() == id){
                foundUser = possibleUser;
            }
        }
        return foundUser;
    }
}

```

### Create Views

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
