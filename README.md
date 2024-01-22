# app-property


server.port=8081
server.servlet.context-path=/REST

spring.datasource.url = jdbc:mysql://localhost:3306/emp
spring.datasource.username = root
spring.datasource.password = 12345
spring.jpa.hibernate.ddl-auto = none




CURD
------------------------------------------------------------

package com.example.SpringRest.Controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import com.example.SpringRest.Entity.Student;
import com.example.SpringRest.Repository.StudentRepository;

@RestController
public class StudentController {
	
	@Autowired
	StudentRepository repo;           //using student repository which we have extended
 
	

	@GetMapping("/students")                                      			// get all Students
	public List<Student> getAllStudents(){	
	List<Student> students= repo.findAll();	
		return students;			
	}




   
	@GetMapping("/students/{id}")				                            // get student by id
		public Student getStudent(@PathVariable int id ){
		
		Student student = repo.findById(id).get();		
		return student;
	}
	

	@PostMapping("/students/add")
												// add new student
	public void CreateStudent(@RequestBody Student student) {	
		repo.save(student);
			
	}
		
	@PutMapping("/students/update/{id}")                              			   //Update
	public Student UpdateStudent (@PathVariable int id) {
	Student student =  repo.findById(id).get();
	student.setName("Anushka");
	student.setPercentage(90);
	repo.save(student);
	return student;
		
	}
	
		
	@DeleteMapping("/students/delete/{id}")					                  //delete
	
	public void RemovStudent(@PathVariable int id) {
	Student student=repo.findById(id).get();
		
		repo.delete(student);
			
	}

}


