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
### 3. Create a controller

*/src/main/java/demo/Controller.java*

```
package demo;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;

@Controller
public class Controller {

    @GetMapping("/user")
    public String userForm(Model model) {
        model.addAttribute("user", new User());
        return "user";
    }

    @PostMapping("/user")
    public String greetingSubmit(@ModelAttribute User user) {
        return "result";
    }
}
```
Spring MVC uses the @Controller annotation to automatically identify controllers. Spring's dispatcher server automatically scans the classes marked with the @Controller annotation and detects any @RequestMapping annotations.
