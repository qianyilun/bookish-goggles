## Environment
* Java 8
* Eclipse for Java EE

## Setup 

* Open Eclipse
  * Help -> install new software -> search "Spring Tool Suite" -> install 


## Configure pom.xml

* Create a **Maven** project

* Open *pom.xml*

* Configure the following "necessary" components

  ```xml
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.4.RELEASE</version> <!-- need to find the latest version -->
      <relativePath/> <!-- lookup parent from repository -->
  </parent>
  ```

  ``` xml
  <dependencies>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
  
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-test</artifactId>
          <scope>test</scope>
      </dependency>
  </dependencies>
  ```

  ``` XML
  <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
      <java.version>1.8</java.version> <!-- you may need this -->
  </properties>
  ```

  > You can download a template from [start.spring.io](https://start.spring.io/) and improve as a Maven project 

* Eclipse: right click the project --> Maven --> Update project
  * IntelliJ, no need to update (but ensure open auto-import)

#### reference

* [Spring Boot Quick Start 8 - Creating a Spring Boot project](https://youtu.be/bDtZvYAT5Sc) 



## Recommand Structure

root package：**com.example.myproject**

```java
com
  +- example
    +- myproject
      +- Application.java
      |
      +- domain
      |  +- Customer.java
      |  +- CustomerRepository.java
      |
      +- service
      |  +- CustomerService.java
      |
      +- controller
      |  +- CustomerController.java
      |
```

#### reference

* [Spring Boot系列(一)：Spring Boot 入门篇](https://zhuanlan.zhihu.com/p/24957789) 



# Start an Spring Application

* Need a Java class to hold *main* function

  * e.g. DemoApplication.java

* Annotation

  ``` java
  @SpringBootApplication
  ```

* *main* function

  ``` java
  public static void main(String[] args) {
      // suppose this class name is DemoApplication.java
      SpringApplication.run(DemoApplication.class, args);
  }
  ```

* Eclipse: run as a **Java application**

  * IntelliJ: run button

* Check out the command line to see if it has

  * ![Screen Shot 2018-09-07 at 11.09.49 PM](https://ws4.sinaimg.cn/large/0069RVTdly1fv23xtj08fj30u901yad8.jpg)

* What Spring Boot did for you when starting
  * Set up default configuration
  * Starts Spring **application context**
    * A container of **Beans**. Use getBean() when necessary.
    * "spring-boot-starter" creates the Spring application context
  * Perform class path scan
    * Based on **annotations**, to identity/classify the "duty" of different classes
      * i.e. @Service -> as a service; @Controller -> as a controller
  * Start Tomcat server

#### reference

* [Spring Boot Quick Start 9 - Starting a Spring Boot application](https://youtu.be/E7_a-kB46LU) 
* [Spring Boot Quick Start 10 - Spring Boot startup steps](https://youtu.be/h581CNFdjDc) 



# REST Controller in Spring

* Controller

  * A Java class
  * Marked with **annotations**
  * Has info about
    * What URL access?
    * What HTTP method?

* Two way to design a controller class

  1. Design as a "data facade" that includes all requests mappings into ONE major class

  2. Divide to one class as one URL mapping, which handles GET, PUT for each URL

     ```java
     @RestController
     @RequestMapping("/students") 
     // only handle http://localhost:8080/student, but can have GET/PUT methods
     public class StudentController {
         @Autowired
         private StudentService studentService;
     
         @RequestMapping(method = RequestMethod.GET)
         public Collection<StudentEntity> retrieveAllStudents() {
             return studentService.retrieveAllStudents();
         }
     
         @RequestMapping(value = "{id}", method = RequestMethod.GET)
         // url: http://localhost:8080/students/3
         public StudentEntity getStudentEntityById(@PathVariable("id") int id) {
             return studentService.retrieveStudentById(id);
         }
     
         @RequestMapping(method = RequestMethod.POST, consumes = 		MediaType.APPLICATION_JSON_VALUE)
         public void insertStudent(@RequestBody StudentEntity studentEntity) {
             studentService.insertStudent(studentEntity);
         }
     }
     ```

#### Reference

* [Learn Spring Boot (MVC) in 50 Minutes](https://www.youtube.com/watch?v=Ke7Tr4RgRTs)

