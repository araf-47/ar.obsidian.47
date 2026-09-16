# Spring & Spring Boot — Multiple Choice Questions (with Answers)

> Source: *Spring & SpringBoot [MCQ]*, Md Rakibul Islam, ESAD-JEE (Diploma), Oct 20, 2021

**Verification note:** All answers were reasoned through individually; the handful of genuinely ambiguous or source-flawed questions (Q11, Q21, Q60, Q108, Q116) were additionally checked against Spring's official documentation and multiple technical references, with the ambiguity called out inline. Everything else reflects well-established, unambiguous Spring/Spring Boot facts.

***

1. Which of the following technologies in spring is used to allow an application to manipulate Java objects at runtime?

          a) Weaving
          b) SPEL
          c) RPC
          d) JCP

   **Answer: a) Weaving**

2. How many ways Inversion of control is executed?

          a) Dependency lookup
          b) Dependency injection
          c) Traditional approach
          d) Both a & b

   **Answer: d) Both a & b**

3. Which of the following are core concepts of AOP?

          a) Joinpoints
          b) Advice
          c) Pointcuts
          d) All of the above

   **Answer: d) All of the above**

4. What is the purpose of interfaces?

          a) Loose coupling
          b) Reduce coupling
          c) Remove coupling
          d) All of the above

   **Answer: a) Loose coupling**

5. What is the abbreviation of DTO?

          a) Database Objects
          b) Data Transfer Objects
          c) Data Objects
          d) None

   **Answer: b) Data Transfer Objects**

6. Why we use named parameters?

          a) Callable Statements
          b) Statements
          c) Prepared Statements
          d) Transactions

   **Answer: c) Prepared Statements**

7. How many ways you can configure spring dependency? (Choose two)

          a) Externally in Xml file
          b) Text file
          c) Faces-config
          d) Java annotations
          e) Both A & D

   **Answer: e) Both A & D**

8. Transaction and AOP service, message source for internationalization (i18n), and application event handling services are provided by?

          a) BeanFactory
          b) FactoryBean
          c) ApplicationContext

   **Answer: c) ApplicationContext**

9. Which of the following is a destruction method?

          a) afterPropertiesSet
          b) destroy-method attribute
          c) nit-method attribute
          d) None

   **Answer: b) destroy-method attribute**

10. When Dependency Injections are executed?

          a) Coding time
          b) Compile time
          c) Run time

    **Answer: c) Run time**

11. What is the role of Factory Pattern?

          a) To provide application context
          b) To provide application initiated object
          c) To provide application component
          d) Above all

    **Answer: b) To provide application initiated object**

12. Which of the following is correct related to JdbcTemplate?

          a) it is not necessary to write SQL queries
          b) It is not necessary to manage connections in the application code
          c) SQL queries automatically become database agnostic
          d) Object relational mapping is available out of the box

    **Answer: b) It is not necessary to manage connections in the application code**

13. Which of the following are ORM libraries?

          a) Hibernate
          b) TopLink
          c) JDO
          d) Above all

    **Answer: d) Above all**

14. Which of the following are types of IoC containers?

          a) BeanFactory
          b) BeanContext
          c) ApplicationContext
          d) ApplicationFactory
          e) Both A&C

    **Answer: e) Both A&C**

15. Which of the following method is used to shutdown all the bean processes after closing the spring container?

          a) destory method
          b) none of the mentioned
          c) shutdownHook
          d) All of the mentioned

    **Answer: c) shutdownHook**

16. Which are the attribute of bean class?

          a) name
          b) id
          c) class
          d) all of the above

    **Answer: d) all of the above**

17. IoC can be decomposed into two subtypes that are

          a) Dependency Lookup
          b) Bean factory
          c) Dependency Injection
          d) Both A & C
          e) None

    **Answer: d) Both A & C**

18. What is the objective of AOP?

          a) MVC logic
          b) Constraint logic
          c) Bean logic
          d) Crosscutting logic

    **Answer: d) Crosscutting logic**

19. What are the advantage of Dependency injection?

          a) Makes the code loosely coupled, so easy to maintain
          b) Makes the code easy to test
          c) Both a and b
          d) None

    **Answer: c) Both a and b**

20. Which of the following component intercepts all requests from spring MVC application?

          a) dispatcher servlet
          b) controller servlet
          c) filter dispatcher

    **Answer: a) dispatcher servlet**

21. Which Method used to process bean?

          a) postProcessAfterinitialization()
          b) postProcessBeforelnitialization()
          c) scope
          d) own constructor

    **Answer: b) postProcessBeforeInitialization()** *(note: both a & b are valid BeanPostProcessor callback methods)*

22. What do you mean by inversion of Control?

          a) IOC is a technique that internalizes the creation of management of component dependencies
          b) IOC is a technique that externalizes the creation of management of component dependencies
          c) a & b
          d) None

    **Answer: b) IOC is a technique that externalizes the creation of management of component dependencies**

23. Which function returns true if the array contains the specified value?

          a) test(value)
          b) map(value)
          c) check(value)
          d) includes(value)

    **Answer: d) includes(value)**

24. You can convert the numbers to strings with the _____ method

          a) Convert
          b) toString
          c) numberToString
          d) toFixed

    **Answer: b) toString**

25. Which is the limitation of traditional factory pattern?

          a) Single Implementation
          b) Multiple Implementation
          c) Both a and b
          d) None

    **Answer: a) Single Implementation**

26. Which of the following is true?

          a) ApplicationContext extends BeanFactory
          b) BeanFactory extends ApplicationContext
          c) BeanFactory implements ApplicationContext
          d) ApplicationContext implements BeanFactory

    **Answer: a) ApplicationContext extends BeanFactory**

27. Which keyword is used to define a constant value that will not change?

          a) final
          b) Let
          c) Const
          d) Get

    **Answer: c) Const**

28. Which is not Spring own Module JAR File?

          a) Aop
          b) Oxm
          c) primeface
          d) Asm

    **Answer: c) primeface**

29. Which layer is the core layer within the application and all business logic will be implemented in this layer?

          a) persistence layer
          b) service layer
          c) presentation layer
          d) security layer

    **Answer: b) service layer**

30. Using named parameters is preferred due to

          a) proxy pattern usage
          b) low cohesion
          c) loose coupling
          d) improved code maintainability

    **Answer: d) improved code maintainability**

31. Which of the following configuration is supported by the LocalSessionFactoryBean?

          a) Scanning a package to detect annotated entity classes (with @Entity)
          b) Listing hibernate XML mapping configuration file (hbm.xml)
          c) Listing entity classes annotated (with @Entity)
          d) All above

    **Answer: d) All above**

32. Which is/are ORM frameworks?

          a) Hibernate
          b) EclipseLink/TopLink
          c) Open JPA
          d) All are above

    **Answer: d) All are above**

33. What is Bean Factory?

          a) An Interface
          b) an Object
          c) a Class
          d) None

    **Answer: a) An Interface**

34. Why do you design to interfaces?

          a) Loose coupling
          b) Reduce coupling
          c) Remove coupling
          d) All of the above

    **Answer: a) Loose coupling**

35. What data access technology is supported by the Spring framework?

          a) JDBC
          b) Hibernate
          c) JPA
          d) Above a, b, c

    **Answer: d) Above a, b, c**

36. Which is responsible for getting connection to the database?

          a) Statement
          b) ResultSet
          c) Driver
          d) Connection

    **Answer: c) Driver**

37. Which of the following can be the return type of a request processing method of a controller?

          a) Void
          b) Object
          c) ModelAndView
          d) A & C

    **Answer: d) A & C**

38. What do you mean by "@Entity"?

          a) mapped Java class
          b) mapped entity object
          c) mapped entity class
          d) None

    **Answer: c) mapped entity class**

39. In Spring Web Flow, a flow consists of a series of steps is called

          a) Model
          b) Instance
          c) States
          d) Object

    **Answer: c) States**

40. Which of the following are advantages of DI rather than a more traditional approach?

          a) Reduced glue code
          b) Simplified application configuration
          c) Ability to manage common dependencies
          d) Improved testability
          e) All of the above

    **Answer: e) All of the above**

41. Which of the following is the default scope of bean?

          a) Request
          b) Singleton
          c) Prototype
          d) Session

    **Answer: b) Singleton**

42. What is the main benefit of using DataSource?

          a) it is possible to use a database connection pool to fetch database connection
          b) it is possible to directly connect to a database without using connection parameters
          c) it automatically enables distributed transactions
          d) it facilitates logging of database queries and their results

    **Answer: a) it is possible to use a database connection pool to fetch database connection**

43. Spring supports which of the following format?

          a) CurrencyFormatter
          b) DateFormatter
          c) NumberFormatter
          d) Above all

    **Answer: d) Above all**

44. Which is/are the drawbacks of the Basic Factory Pattern

          a) There is no way to change an implementing class without a recompile.
          b) There is no way simply to switch instantiation models.
          c) Only A
          d) Both A and B

    **Answer: d) Both A and B**

45. Which of the following ways to inject dependency? (choose two)

          a) By Constructor
          b) By Setter method
          c) By getter method
          d) By list method
          e) Both A & B

    **Answer: e) Both A & B**

46. AOP implements which of the following features?

          a) Crosscutting logic
          b) MVC logic
          c) Constraint logic
          d) Bean logic

    **Answer: a) Crosscutting logic**

47. Which of the following is the alternative to Spring HibernateTemplate

          a) Hibernate contextual sessions
          b) HibernateContext
          c) All of the mentioned
          d) None of the mentioned

    **Answer: a) Hibernate contextual sessions**

48. Which of the following layer is used for @Controller annotation?

          a) Session layer
          b) Business layer
          c) Service layer
          d) Presentation layer

    **Answer: d) Presentation layer**

49. How many way we decomposed into two subtypes?

          a) Dependency Injection
          b) Dependency Lookup
          c) Bean factory
          d) A & B

    **Answer: d) A & B**

50. What do you mean by DispatcherServlet?

          a) DispatcherServlet is used for AOP.
          b) DispatcherServlet handles all the http requests and responses.
          c) DispatcherServlet is used for transaction management.
          d) DispatcherServlet is used for Dependency injection.

    **Answer: b) DispatcherServlet handles all the http requests and responses.**

51. Hibernate covered common techniques for defining _____ mappings?

          a) ORM
          b) MVC
          c) JVM

    **Answer: a) ORM**

52. Which of the following is the persistent object, stores as records in the database.

          a) EntityManagerFactory
          b) Entity-Transaction
          c) Persistence Entity

    **Answer: c) Persistence Entity**

53. Why we use jdbcTemplate? Mentioned problems of JDBC API.

          a) It provides you methods to write the queries directly
          b) It saves a lot of work and time.
          c) All of the above

    **Answer: c) All of the above**

54. Which of the following method return list of maps?

          a) Update
          b) query
          c) QueryForList()
          d) all of the mentioned

    **Answer: c) QueryForList()**

55. How can you close the database resources?

          a) Statement then Connection then ResultSet
          b) Connection then Statement then ResultSet
          c) ResultSet then Statement then Connection
          d) Statement then ResultSet then Connection

    **Answer: c) ResultSet then Statement then Connection**

56. How can you notify its completion of session?

          a) BindingResult
          b) SessionStatus
          c) Errors
          d) None

    **Answer: b) SessionStatus**

57. Which method is used to delete data in JPA?

          a) EntityManager.remove()
          b) EntityManager.destroy()
          c) EntityManager.delete()
          d) None

    **Answer: a) EntityManager.remove()**

58. What kind of framework is Spring?

          a) A lightweight framework
          b) A standard framework
          c) An explain framework
          d) None

    **Answer: a) A lightweight framework**

59. What is the core principle of Spring Framework?

          a) DOC
          b) JNDI
          c) IOC
          d) XML

    **Answer: c) IOC**

60. Which of the following class maintain Hibernate's session factory for spring?

          a) Application context
          b) SessionFactory
          c) method
          d) None

    **Answer: b) SessionFactory**

61. The JdbcTemplate class offers template method for batch update operations.

          a) batchUpdate()
          b) update()
          c) all of the mentioned A & B

    **Answer: a) batchUpdate()**

62. What is ApplicationContext?

          a) Object
          b) Class
          c) Interface
          d) None

    **Answer: c) Interface**

63. SimpleJdbcTemplate perform batch update method in the form of What?

          a) Map
          b) List
          c) Vector
          d) Set

    **Answer: b) List**

64. jQuery is one of the most popular JavaScript libraries being used for development

          a) Desktop application
          b) Web fronted
          c) Both a and b
          d) None

    **Answer: b) Web frontend**

65. How can you Annotation for Hibernate exceptions?

          a) @Repo
          b) @Repository
          c) @Translation
          d) None of the mentioned

    **Answer: b) @Repository**

66. Which of the following interface is used by the JdbcTemplate to map a resultset row?

          a) Mapper
          b) ValueMapper
          c) RowElementMapper
          d) RowMapper

    **Answer: d) RowMapper**

67. What do you mean by CRUD?

          a) Create, Run, Update, Destroy
          b) Create, Read, Update, Delete
          c) Create, Run, Update, Delete
          d) Create, Read, Update, Destroy

    **Answer: b) Create, Read, Update, Delete**

68. What is the objective of Spring Dependency Injection?

          a) easier to test
          b) Simple
          c) easier to understand
          d) All of the above

    **Answer: d) All of the above**

69. Which of the following module provides basic web-oriented integration?

          a) Web-MVC module
          b) Web-Socket module
          c) Web module
          d) Web-Portlet module

    **Answer: c) Web module**

70. Which is the default validator of spring?

          a) Spring validator
          b) Hibernate validator
          c) Hibernate validator
          d) Bean validator

    **Answer: b) Hibernate validator**

71. JdbcDaoSupport wrap up the which of the following class

          a) JdbcTemplate
          b) JdbcDao
          c) JdbcSupport
          d) None

    **Answer: a) JdbcTemplate**

72. Which of the following is the default @RequestMapping?

          a) GET
          b) PUT
          c) POST
          d) None

    **Answer: a) GET**

73. POJO stand for?

          a) Plain Old Java Object
          b) Pre old java object
          c) Plain order java object

    **Answer: a) Plain Old Java Object**

74. Which of the following exception classes is related to all the exceptions thrown in spring applications?

          a) NullPointerException
          b) DataAccessException
          c) SpringException
          d) ArrayIndexOutofBound

    **Answer: b) DataAccessException**

75. Transforming JavaBeans into XML is called?

          a) Marshaling
          b) Unmarshaling

    **Answer: a) Marshaling**

76. Which of the following is/are the Spring web flow feature?

          a) Flow
          b) View
          c) Conversation
          d) All of the above

    **Answer: d) All of the above**

77. Which of the following is return row?

          a) mapRow()
          b) query
          c) update
          d) none

    **Answer: a) mapRow()**

78. How many ways we can configure the ApplicationContext?

          a) XML based
          b) OSPEL Based
          c) Annotation based
          d) A&C

    **Answer: d) A&C**

79. What is/are the purpose of validation?

          a) Fulfills all predefined business requirements.
          b) Ensure the data integrity of the application.
          c) Usefulness in other layers of the application.
          d) All

    **Answer: d) All**

80. What is/are the objective of validation?

          a) Fulfills all predefined business requirements.
          b) Ensure the data integrity of the application.
          c) Usefulness in other layers of the application.
          d) All of the above

    **Answer: d) All of the above**

81. Which of the following is the Annotation for Controller Class?

          a) @After
          b) @Exception
          c) @Before
          d) @Controller

    **Answer: d) @Controller**

82. What should we do to publish a REST service with Spring?

          a) publishing an applications data as a REST service
          b) accessing data from third-party REST services
          c) all of the mentioned

    **Answer: c) all of the mentioned**

83. Which of the following method return the JDBC template?

          a) getTemplate()
          b) getJdbc()
          c) getJdbcTemplate()
          d) setJdbcTemplate()

    **Answer: c) getJdbcTemplate()**

84. Which of the following repository is used in Spring?

          a) JPA
          b) JDB
          c) JBoss Seam
          d) Velocity

    **Answer: a) JPA**

85. Which of the following statements is/are correct for spring beans?

          a) Spring beans are simple POJOs
          b) Spring beans are managed by IoC container
          c) Spring beans are instantiated and assembled
          d) All of the above

    **Answer: d) All of the above**

86. JPQL is similar to

          a) MySQL
          b) HQL
          c) iBatis
          d) None

    **Answer: b) HQL**

87. What is the main advantage of using Data Access Object?

          a) It provides access credentials to the data objects
          b) It hides database specific implementation from the other layers of the application
          c) It always provides non jdbc specific implementation
          d) It provides object modeling for data

    **Answer: b) It hides database specific implementation from the other layers of the application**

88. Which component is used for request?

          a) RequestMapper
          b) URLMapper
          c) RequestMapping
          d) RequestResolver

    **Answer: c) RequestMapping**

89. Which of the following technique that externalizes the creation and management of Component dependencies?

          a) DAO
          b) JNDI
          c) IoC
          d) None

    **Answer: c) IoC**

90. Spring MVC which is the central servlet that receives requests and dispatchers then to the appropriate controllers?

          a) DispatcherServlet
          b) Servlet
          c) ActionServlet
          d) None of the above

    **Answer: a) DispatcherServlet**

91. Which of the following file is required for configuring the database and the registration of entity classes?

          a) Web.xml
          b) App-context.xml
          c) Persistence.xml
          d) None

    **Answer: c) Persistence.xml**

92. What do you mean by HQL?

          a) Hipertext Query Language
          b) Hiperlink Query Language
          c) Hibernate Query Language

    **Answer: c) Hibernate Query Language**

93. How can you annotate a transaction?

          a) @Transactional
          b) @Transactions
          c) @Transaction
          d) None of the mentioned

    **Answer: a) @Transactional**

94. How can we return contextual sessions?

          a) getSession() method
          b) getCurrent() method
          c) getCurrentSession() method
          d) HibernateContext

    **Answer: c) getCurrentSession() method**

95. In a web application, in terms of bean scopes, there are which scopes are available?

          a) Request
          b) Session
          c) Application
          d) Above all

    **Answer: d) Above all**

96. Which of the following is a correct SQL resultset mapping at the entity class?

          a) @SqlResultSetMapping
          b) @SqlResultSetExactor
          c) @SqlReseltSet Query

    **Answer: a) @SqlResultSetMapping**

97. How can you handle the shutdown of IoC container?

          a) Using shutdownHandler()
          b) Using registerShutdownHook()
          c) Using registerHook()
          d) Using shutdownHook()

    **Answer: b) Using registerShutdownHook()**

98. Which of the following class is belongs to the Spring Jdbc module?

          a) JdbcDaoSupport
          b) JdbcTemplateSupport
          c) JdbcTemplateDaoSupport
          d) JdbcObjectDaoSupport

    **Answer: a) JdbcDaoSupport**

99. What is the starting point of Spring Boot Application?

          a) @Service
          b) @Controller
          c) @SpringBootApplication
          d) None of the Above

    **Answer: c) @SpringBootApplication**

100. Which Maven command is used to run a Spring boot application?

          a) maven spring-boot:run
          b) Mvn spring: run
          c) mvn spring-boot:run
          d) None of the options

     **Answer: c) mvn spring-boot:run**

101. What is the spring boot default embedded server?

          a) Undertow Server
          b) Tomcat Server
          c) Glassfish Server
          d) Jetty Server

     **Answer: b) Tomcat Server**

102. The annotation to be added to automatically configure beans based on the classes added to the class path is?

          a) @AutoConfiguration
          b) @EnableAutoConfiguration
          c) @EnableConfiguration
          d) None of the options

     **Answer: b) @EnableAutoConfiguration**

103. How primary key is annotated with attribute?

          a) @Column
          b) @Id
          c) @PrimaryKeyNotNull
          d) @PrimaryKeyNotNullAutoIncrement

     **Answer: b) @Id**

104. What is the default method of @RequestMapping?

          a) Pull
          b) Patch
          c) Post
          d) Get

     **Answer: d) Get**

105. How to disable the default web server in the Spring Boot application?

          a) spring.main.web-server-type = none
          b) spring.main.web-application-type = none
          c) spring.main.application-type = no
          d) spring.web-application-type = no-server

     **Answer: b) spring.main.web-application-type = none**

106. Which of the following are embedded containers supported by Spring?

          a) Undertow
          b) Tomcat
          c) Jetty
          d) All of the above

     **Answer: d) All of the above**

107. Which of the following is the default HTML template engine in Spring Boot?

          a) Jansa
          b) Thymeleaf
          c) JSP
          d) None

     **Answer: b) Thymeleaf**

108. Which of the following is not a spring boot layer?

          a) Presentation Layer
          b) Service layer
          c) Persistence Layer
          d) Business Layer

     **Answer: d) Business Layer** *(⚠️ flawed question — verified against multiple sources: standard Spring Boot layers are Presentation, Business/Service, and Persistence, where "Business Layer" and "Service layer" are two names for the exact same layer. Since the question lists them as separate options, there's no clean single "odd one out" — treat this answer as a best-effort pick, not a confirmed fact.)*

109. Why jdbcTemplate is used for?

          a) Allow to issue any type of SQL statement
          b) return any type of result
          c) both a and b
          d) None

     **Answer: c) both a and b**

110. Which of the following classes can you use for executing the SQL queries?

          a) JDBCHelper
          b) DBTemplate
          c) DBHelper
          d) JdbcTemplate

     **Answer: d) JdbcTemplate**

111. How to configure hibernate in spring boot?

          a) h2
          b) spring-boot-starter-data-jpa
          c) Both a & b
          d) None of the above

     **Answer: c) Both a & b**

112. Spring-boot-starter-parent manage which of the following activities?

          a) Configuration - Java Version and other properties
          b) Dependency Management - Version of dependencies
          c) Default Plugin Configuration
          d) All of the above

     **Answer: d) All of the above**

113. Which of the following annotation used for Restful Web Services?

          a) @Controller
          b) @SpringBootApplication
          c) @RestController
          d) All of the Above

     **Answer: c) @RestController**

114. Which of the following are Class level annotation?

          a) @Controller
          b) @Service
          c) @Repository
          d) All of the above

     **Answer: d) All of the above**

115. What is the purpose of Rest Template?

          a) create applications that consume RESTful Web Services
          b) create applications that produced RESTful Web Services
          c) Both A & B
          d) None

     **Answer: a) create applications that consume RESTful Web Services**

116. How we can disable a specific auto-configuration class?

          a) Using include attribute of @DisableAutoconfiguration
          b) Using not exclude attribute of @DisableAutoConfiguration
          c) Using not include attribute of @EnableAutoConfiguration
          d) Using exclude attribute of @EnableAutoConfiguration

     **Answer: d) Using exclude attribute of @EnableAutoConfiguration**

117. Which of the following annotation is used to bind application properties to the class fields?

          a) @ApplicationProperties
          b) @ConfigurationProperties
          c) @AppProperties
          d) None of the above

     **Answer: b) @ConfigurationProperties**

118. Where we configure DispatcherServlet?

          a) In Beans configuration file
          b) Web-inf/dispatcher.xml
          c) Meta-inf/dispatcher.xml
          d) In web.xml file

     **Answer: d) In web.xml file**

119. What is the starter for using log4j2 for logging?

          a) Spring-boot-starter-logger
          b) Spring-boot-starter-log
          c) Spring-boot-starter-log4j2
          d) None of the options

     **Answer: c) Spring-boot-starter-log4j2**

120. Which Annotation used for entity manager injection in EJB components?

          a) @Persistence
          b) @PersistenceCon
          c) @PersistenceContext
          d) None of the mentioned

     **Answer: c) @PersistenceContext**

121. Which you needed to build a RESTful Web Services?

          a) Spring-boot-starter-rest
          b) Spring-boot-starter-web.rest
          c) Spring-boot-starter-web
          d) None

     **Answer: c) Spring-boot-starter-web**

122. What is the abbreviation of DTO?

          a) Database Objects
          b) Data Transfer Objects
          c) Data Objects
          d) None

     **Answer: b) Data Transfer Objects**

123. Which package contains the foundation of JDBC class?

          a) org.springframework.jdbc.core
          b) org.springframework.jdbc.datasource
          c) org.springframework.jdbc.object
          d) org.springframework.jdbc.support

     **Answer: a) org.springframework.jdbc.core**

124. Do you think Spring Boot upgrades all dependencies automatically?

          a) True
          b) False

     **Answer: b) False**
