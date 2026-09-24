
# Architecture summary

**Initial architecture consist of 3 layers (Presentation, Application, and Data).<br>**
> **Presentation** layer provides 2 types of access, standard ***Web*** access (Admin & Doctor Dashboard) and any other Frontend Apps and Modules via ***ReST APIs***.

> **Application** layer consist of ***Controller***, ***Service***, and ***Repository***
>
> This project use ***Spring Boot*** as the framework so Spring's annotations and pattern will be used as a standard.
> + **@Controller** for Thymeleaf-based Web Access
> + **@RestController** for JSON-based ReST API Access
> + **@Service** for business logic (Controllers must get through this Service, not direct to Repository and Data
> + **@Repository** for accessing Data Layer (extends JpaRepository for MySQL, MongoRepository for MongoDB)

> **Data** layer use 2 Database Systems
> + **MySQL** for standard data storage
> + **@Entity** used for MySQL Models (POJO for MySQL Tables)<br>
> + **MongoDB** for prescription data storage
> + **@Document** used for MongoDB Models (POJO for MongoDB Documents)



# Numbered flow of data and control

> 1. Web User (Admin & Doctor) access Dashboard via http url in the browser, web page served by embedded http server in Spring Boot. 
> 2. The request handled by @Controller classes which then return Thymeleaf generated html as a response.
> 3. If there is any process that require data retrieval or data manipulation, request in step 1 and 2 will also access Service Layer from @Service classes that handle business logic.
> 4. Service Layer able to access data by calling (query) methods from @Repository classes, in this case there are 2 kinds of Repository, @JpaRepository and @MongoRepository.
> 5. Repository responsible to handle access to database systems (MySQL & MongoDB). MySQL is used as the standard for data storage, meanwhile MongoDB used for prescriptions data only. 
> 6. Database tables (RDMBS) or documents (NoSQL) represented by models.
> 7. The models defined by @Entity annotation for MySQL Model and accessed via JpaRepository, on the other hand @Document annotation is used for MongoDB Model which accessed via MongoRepository.

> 1. Step 1 alternatively can be achieved from other Frontend Apps such as Mobile Apps or other Web Application that serve the page but for business logic and data access, they need to access ReST APIs.
> 2. ReST API requests are handled by @RestController classes which then orchestrate the business logic and data access the same way as Web User (Admin & Doctor) through Service Layer (step 3-7).
