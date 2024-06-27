```cmd
https://github.com/Ankitkushwaha90/for_react_spring_get_post_fetch_data_from_mongodb
```
```java
package com.MongoSpring.MongoSpring.Controller;


// import org.apache.catalina.filters.CorsFilter;
import org.springframework.beans.factory.annotation.Autowired;
// import org.springframework.boot.web.servlet.FilterRegistrationBean;
// import org.springframework.context.annotation.Bean;
import org.springframework.web.bind.annotation.*;
// import org.springframework.web.cors.CorsConfiguration;
// import org.springframework.web.cors.UrlBasedCorsConfigurationSource;

import com.MongoSpring.MongoSpring.Model.Student;
import com.MongoSpring.MongoSpring.Repository.StudentRepo;

// import jakarta.servlet.FilterRegistration;

import java.util.List;
import java.util.Optional;

@RestController
@RequestMapping("/api")
@CrossOrigin("*")
public class MainController {

    @Autowired
    StudentRepo studentRepo;

    // Create a new student
    @PostMapping("/students")
    public Student addStudent(@RequestBody Student student) {
        return studentRepo.save(student);
    }

    // Get all students
    @GetMapping("/students")
    public List<Student> getAllStudents() {
        return studentRepo.findAll();
    }
    // @GetMapping("/users")
    // public List<User> getAllUsers() {
    //     // Logic to fetch all users
    // }

    // Get a student by ID
    @GetMapping("/students/{id}")
    public Student getStudentById(@PathVariable String id) {
        Optional<Student> student = studentRepo.findById(id);
        if (student.isPresent()) {
            return student.get();
        } else {
            throw new RuntimeException("Student not found with id " + id);
        }
    }

    // Update a student by ID
    @PutMapping("/students/{id}")
    public Student updateStudent(@PathVariable String id, @RequestBody Student studentDetails) {
        Student student = studentRepo.findById(id).orElseThrow(() -> new RuntimeException("Student not found with id " + id));

        student.setName(studentDetails.getName());
        student.setAge(studentDetails.getAge());

        return studentRepo.save(student);
    }

    // Delete a student by ID
    @DeleteMapping("/students/{id}")
    public String deleteStudent(@PathVariable String id) {
        studentRepo.deleteById(id);
        return "Student deleted with id " + id;
    }

    // Find students by name
    @GetMapping("/students/name/{name}")
    public List<Student> getStudentsByName(@PathVariable String name) {
        return studentRepo.findByName(name);
    }

    // @Bean
    // public FilterRegistration coresFilter(){
    //     UrlBasedCorsConfigurationSource Source = new UrlBasedCorsConfigurationSource();

    //     CorsConfiguration corsConfiguration = new CorsConfiguration();
    //     corsConfiguration.setAllowCredentials(true);
    //     corsConfiguration.addAllowedHeader("*");
    //     corsConfiguration.addAllowedHeader("Authorization");
    //     corsConfiguration.addAllowedHeader("content-Type");
    //     corsConfiguration.addAllowedHeader("Accept");
    //     corsConfiguration.addAllowedHeader("POST");
    //     corsConfiguration.addAllowedHeader("GET");
    //     corsConfiguration.addAllowedHeader("DELETE");
    //     corsConfiguration.addAllowedHeader("PUT");
    //     corsConfiguration.addAllowedHeader("OPTIONS");
    //     corsConfiguration.setMaxAge(3600L);

    //     Source.registerCorsConfiguration("/**", corsConfiguration);

    //     FilterRegistrationBean bean = new FilterRegistrationBean(new CorsFilter(Source));

    //     return bean;
    // }
}
```
