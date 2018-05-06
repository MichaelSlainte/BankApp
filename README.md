# BankApp
BankApp with Java Spring.

Autors: Michael Marques, Aleksandro Candido, Nuno Forjaz.

Introduction
The aim of this project is to build an online banking system with certain attributes. 
With the help of a Udemy course we by Le Deng we were able to build a functional online prototype  banking service with the functionality defined as per specification for this project. We also added extra functionalities such as booking appointments as well as having an savings account included. The users can choose to deposit, transfer and/or withdraw money from their accounts.  
There are many issues to tackle prior to getting the full working service. To start this project we had to create the models (classes) and relate them as described in the ERD shown in the section below.  We then had to decide , where we used bootstrap.

This system was built using the following stack

# Frontend

●	Thymeleaf
○	Java server-side template engine (easier communication between views and controllers)

●	Bootstrap
○	Framework to combine HTML, CSS and JS

●	Javascript/JQuery
○	Scripting language and JQuery Library

# Backend

●	Spring Boot
○	Framework that favours convention over configuration, largely used amongst Java community, very handy to work with MVC in Maven projects

●	Spring Security 4
○	Security services for Java-EE based applications, consistently integrated with Spring framework

●	Spring Data
○	JPA based repositories integrated with Spring Framework

●	Hibernate
○	For Data Persistence with MySQL

# Database
●	MySQL

# Setting the application ready to run
●	Create a database named onlinebanking in MySQL 
●	Set spring.datasource.url, username and password in resources/application.properties of the project
●	Create the user roles in the database onlinebanking (ROLE_USER, ROLE_ADMIN), as the application does not create it automatically.

# The Restful API

We started this project using Eclipse and installing the spring tool suite and the springsource tool suite .  By using the spring boot many of the attributes have been preset  such as some dependencies etc. We started by initiating a spring starter project creating a new project running as a spring boot app and inserting the domain models. 
The first folder created was the domain and the respective classes(Refer to ER diagrams for relationships between classes and their respective references):  

1.	User - here we inserted all of the variables and classes pertinent to this class (Username, password, email etc)
2.	PrimaryAccount  
3.	PrimaryTransaction
4.	SavingsAccount
5.	SavingsTransaction
6.	Appointments
7.	Recipient

# Next step was to create our index page.

In the resources folder we added all our design resources (css, javascript, images etc) of the pom.xml and added the dependencies such as the thymeleaf dependency. A new common folder inside the dependency directory was created and two html pages(header, index) was added. We used the “th (thymeleaf)” was used to create URL paths along with the common web design code(HTML, CSS, JS refer to code for layout).

The next step was to create a home controller in which we used another java class file inside the controller directory where we added the @controler annotation to register this class as a bin in the spring container.  We then used the @RequestMapping to register the path mapping to the specific files.  (At this step we are able to display our index page).
The sign up attribute was our next step. The initial steps were similar to the prior page with the exception of the th:action which points  to the @signup path where we include certain features such as returning “Email already exists” if the email already exists when the user attempts to sign up and the show password feature in the <div class =”checkbox”> tag using JS. For the controller part of sign up, in the home controller the com.userfront.domain.user, we then mapped the request to the the correct path where we used a GET method, then defined a model where we bind the new variable to the user method.
  
To  add the sign up functionality a persistence layer as the information is fed to our database and hibernate is needed as all the info needs to be kept(in case of a power outage ETC). In our case we used a relational database mysql. We started by adding our depencies to our pom.xml (data-jpa and test) and modifying our models. We added the entity annotation and it will be persisting into the database, we then used the @Id and the @GeneratedValue along with the @ManyToOne and the @JoinColumn where we identified the primary key(for user class was user_id) and the type of relation in our case as an example we used the appointment to user many to one.  For the PrimaryAccout to PrimaryTransaction 1-to-n we used the LAZY FetchType to boost performance,  we used the @JsonIgnore annotation to break the infinite loop when serializing primaryaccount to primaryTransactionList. This same procedure was again followed for the recipient, savings, savings transaction class(refer to ERD and code for relations between classes). With the help of springboard the hibernate configuration was quite simple when opening the application properties where we defined the jdbc, defined the username, password, datasource, and the hibernate, finally added the mysql dependency to the pom.xml.   We then created a service domain in the userfront folder and created a java interface along with a userservice implementation folder. In the userervice implementation we created another class called userserviceimplementation, we used the annotation @Service so that springboot can register it in the database where we implemented the userservice database. We then created dao folder with another interface “UserDao” where we implemented the Crud functionality using springboot which will help us create read update and delete certain data by using the “FindBy” keywords .  We then used the @Autowired annotation to wire the userDao automatically by dependency injection. 

The next step was security and its implementation using spring security.  We added the starter security dependency in our pom.xml file. We then added a new folder in the usefront domain along with a SeccurityConfig file where we added the @Config annotation so that springboot can identify that this is the configuration class, we also included the @EnableWebSeccurity. We encrypted the password using “SALT”which was used to create specific string everytime we login, for the encryption we used the @Bean annotation. When defined an @Overide method to allow permission to the requests (refer to code to see defined paths). We then added the Authority, Role and UserRole classes  to the seccurity folder needed to make spring security work, we also created a new implemented a userdetailsservice in the 

UserServiceImpl class that works as a user authentication provider. 

The next step was to add the user front page. We added an html file for the user once the user loggs in where we display all of the relevant information for the user account such as the account balace etc. Then we added a controler folder and a @RequestMapping annotation to along with user to go into the primary and the saving account with the logout option (refer to code for web design functionality). To add a deposit and withdraw functionality we needed to first  along with the deposit and withdraw transation functionality we needed to first: 

# References: 
- Spring Boot <https://projects.spring.io/spring-boot/>

- Bootstrap <http://getbootstrap.com>

- Hibernate <http://hibernate.org/orm/>

- Spring Data <http://projects.spring.io/spring-data/>

- Spring Security <https://docs.spring.io/spring-security/site/docs/5.0.3.RELEASE/reference/htmlsingle/>

- Udemy Courses <https://www.udemy.com/>

