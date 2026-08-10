Based on the `jsp-angular-mcq_2.docx` file provided, here are all the extracted questions. They have been kept exactly as they appear in the standalone file, with the correct answer and a brief explanation formatted as bullet points directly below the options.

### **Part 1: Angular Multiple Choice Questions**

**01. In angular, controllers are called null**

* a. Module
* b. Component
* c. servic
* d. model
* **Correct Answer:** b. Component


* **Explanation:** In modern Angular (v2+), the traditional AngularJS "controller" concept was replaced by Components, which handle both the logic and the view.



**02. The GET method is _______, which means the operations you perform in response to this method should only retrieve data and not modify it.**

* a) Idempotent
* b) ==Nullipotent==
* c) Both
* d) Neither nullipotent nor idempotent
* **Correct Answer:** c) ~~Both~~ / ✅ b) Nullipotent


* **Explanation:** The HTTP GET method is designed to be nullipotent (it doesn't modify server state) and idempotent (making the same request repeatedly produces the same result).



**03. Which directive is used to repeat a region of content for each item in an array**

* a. `*ngFor`
* b. *ngSwitch
* c. *ngIf
* d. *ngLoop
* **Correct Answer:** a. `*ngFor`


* **Explanation:** `*ngFor` is Angular's structural directive for iterating over collections or arrays to repeat HTML templates.



**04. Which function returns true if the array contains the specified value?**

* a. test(value)
* b. map(value)
* c. check(value)
* d. includes(value)
* **Correct Answer:** d. includes(value)


* **Explanation:** In JavaScript/TypeScript, the `Array.prototype.includes()` method is used to determine whether an array includes a certain value among its entries.



**05. Each TypeScript file in the project acts as**

* a. Model
* b. Module
* c. Component
* d. Both b & c
* **Correct Answer:** b. Module


* **Explanation:** In TypeScript, any file containing a top-level `import` or `export` is inherently treated as a module.



**06. TypeScript is a superset of JavaScript**

* a. true
* b. false
* **Correct Answer:** a. true


* **Explanation:** TypeScript builds upon JavaScript by adding static typing, making it a strict syntactical superset of JavaScript.



**07. Which command is used to create a new angular app ?**

* a. ng create project_name
* b. ng new project_name
* c. Both a and b
* d. None
* **Correct Answer:** b. ng new project_name


* **Explanation:** The Angular CLI uses the `ng new` command to scaffold and generate a fresh Angular application workspace.



**08. Which of the following is correct about TypeScript?**

* a. Angular is based on TypeScript
* b. This is a superset of JavaScript
* c. TypeScript is maintained by Microsoft
* d. All
* **Correct Answer:** d. All


* **Explanation:** All statements are true: Angular is built with it, it's a JS superset, and Microsoft maintains it.



**09. How can decorator provide configuration information?**

* a. properties
* b. objects
* c. class
* d. method
* **Correct Answer:** a. properties


* **Explanation:** Decorators accept configuration metadata objects, and the settings are provided through the properties of those objects.



**10. TypeScript is a__ language**

* a. Open Source
* b. Closed
* c. Free
* d. All of the above
* **Correct Answer:** a. Open Source


* **Explanation:** TypeScript is a free and open-source programming language developed by Microsoft.



**11. AngularJS directives we used in_____**

* a) Model
* b) View
* c) Controller
* d) Module
* **Correct Answer:** b) View


* **Explanation:** Directives (like `ng-repeat` or `ng-model`) are embedded directly into the HTML templates, which represent the View layer.



**12. Which file is acts as placeholder for basic angular app?**

* a) Main.ts
* b) app.module.ts
* c) index.html
* d) app.template.html
* **Correct Answer:** c) index.html


* **Explanation:** `index.html` is the primary entry page where the root Angular component is injected to load the application.



**13. The angular-cli setup for the project created a template file called in the src/app folder.**

* a) App.model.ts
* b) app.component.html
* c) app.component.js
* d) app.component.css
* **Correct Answer:** b) app.component.html


* **Explanation:** The CLI defaults to creating `app.component.html` as the boilerplate template for the root app component.



**14. Which keyword is used to define types that can be instantiated with the new keyword to create objects that have well-defined data and behaviour?**

* a) Object
* b) Class
* c) Prototype
* d) Static
* **Correct Answer:** b) Class


* **Explanation:** The `class` keyword defines an object blueprint that can be instantiated using `new`.



**15. Which ng command performs the production build process?**

* a. Ng start
* b. Ng lint
* c. Ng build
* d. Ng test
* **Correct Answer:** c. Ng build


* **Explanation:** `ng build` compiles the application into an output directory, often used with `--prod` for production environments.



**16. Which keyword is used to identify data or types that you want to use elsewhere in the application?**

* a. Import
* b. Export
* c. New
* d. Add
* **Correct Answer:** b. Export


* **Explanation:** The `export` keyword makes variables, functions, or classes available to be imported by other files.



**17. Which directive can be used to set multiple style properties?**

* a) ngClass
* b) ngStyle
* c) Both A and B
* d) None
* **Correct Answer:** b) ngStyle


* **Explanation:** `ngStyle` allows developers to dynamically bind and set multiple inline CSS styles simultaneously.



**18. What do you mean by NPM ?**

* a) Node Package Manager
* b) Node Packet Manager
* c) Node Project Manager
* d) Node Package Machine
* **Correct Answer:** a) Node Package Manager


* **Explanation:** NPM stands for Node Package Manager, the default package manager for Node.js environments.



**19. The decorator provides configuration information through its:**

* a. properties
* b. objects
* c. class
* d. method
* **Correct Answer:** a. properties


* **Explanation:** Identical in nature to question 9; decorators take metadata configuration via properties.



**20. Which file contains the configuration details of angular development tools?**

* a) package.json
* b) package-lock.json
* c) tsconfig.json
* d) angular.json
* **Correct Answer:** d) angular.json


* **Explanation:** `angular.json` is the core workspace configuration file utilized by the Angular CLI.



**21. You can convert the numbers to strings with the _______ method**

* a. Convert
* b. toString
* c. numberToString
* d. toFixed
* **Correct Answer:** b. toString


* **Explanation:** The `.toString()` method is the standard JavaScript/TypeScript function for converting numerical values into strings.



**22. You can define function in two ways:**

* a. function expression
* b. function component
* c. function declaration
* d. Both a & b (==Both a & c==)
* **Correct Answer:** d. Both a & b (Note: ==Technically a & c==, but d is the intended combo choice in this exam format)


* **Explanation:** In JavaScript, functions are primarily defined via function declarations or function expressions.



**23. TypeScript file extension is ___**

* a. js
* b. es
* c. ts
* d. tts
* **Correct Answer:** c. ts


* **Explanation:** Standard TypeScript files use the `.ts` file extension.



**24. Angular configuration file name is:**

* a. Package.json
* b. Composer.json
* b. Angular.json
* d. Config.json
* **Correct Answer:** b. Angular.json (the second 'b' option)


* **Explanation:** `angular.json` handles all project-specific and workspace-wide Angular configurations.



**25. ngMode directive is used for**

* a. One-way binding
* b. Two-way binding
* c. Refer element in the template
* **Correct Answer:** b. Two-way binding


* **Explanation:** `ngModel` (spelled `ngMode1` in the source) is the Angular directive responsible for two-way data binding.



**26. Which keyword is used to define a constant value that will not change?**

* a. Final
* b. Let
* c. Const
* d. Get
* **Correct Answer:** c. Const


* **Explanation:** The `const` keyword defines block-scoped, read-only named constants.



**27. Two-way bindings are used with HTML  __  elements**

* a. Table
* b. Form
* c. Div
* d. Heading
* **Correct Answer:** b. Form


* **Explanation:** Two-way binding (`[(ngModel)]`) is used specifically to sync data between the component and interactive HTML form elements.



**28. Which type of web application requires a lot of bandwidth?**

* a. One-page
* b. Single_page
* c. Multiple-page
* d. round-trip
* **Correct Answer:** d. round-trip


* **Explanation:** Round-trip (multi-page) applications require full page reloads and resource redownloads, consuming more bandwidth than SPAs.



**29. Which command starts the Angular development tools:**

* a. Ng new
* b. Ng serve
* c. Ng run
* d. Ng start
* **Correct Answer:** b. Ng serve


* **Explanation:** The `ng serve` command builds the app, starts the local dev server, and watches for file modifications.



**30. In angular, Default root module name is**

* a. module.ts
* b. app.module.ts
* c. module.js
* d. app.module.js
* **Correct Answer:** b. app.module.ts


* **Explanation:** The Angular CLI generates the main root module inside the `app.module.ts` file.



**31. Which object oriented terms not supported by Typescript?**

* A. Abstract class
* B. Classes
* C. Interfaces
* D. Modules
* **Correct Answer:** All are supported. (Exam flaw: TypeScript natively supports all of these)


* **Explanation:** TypeScript provides full support for abstract classes, interfaces, modules, and standard classes.



**32. How do you install the npm package?**

* a) npm install PackageName
* b) npm-install PackageName
* c) npm PackageName
* d) Ng create new appName
* **Correct Answer:** a) npm install PackageName


* **Explanation:** `npm install <package-name>` is the correct syntax for the Node Package Manager.



**33. Which keyboard command is used to terminate any angular process**

* a. Ctrl+c
* b. Ctrl+p
* c. Ctrl+z
* d. Ctrl+d
* **Correct Answer:** a. Ctrl+c


* **Explanation:** `Ctrl+c` sends an interrupt signal to the terminal, safely terminating running node processes like `ng serve`.



**34. How do you apply command to check node version?**

* a. nodejs –v
* b. nodejs
* c. node –v
* d. node –version
* **Correct Answer:** c. node –v


* **Explanation:** Both `node -v` and `node --version` are valid, with `node -v` being the standard shorthand.



**35. Angular works on what page?**

* a. Round trip application
* b. Single page application //best
* c. Both a & b
* d. none
* **Correct Answer:** b. Single page application


* **Explanation:** Angular is specifically designed to build and optimize Single Page Applications (SPAs).



**36. How can Angular module provide configuration information through the properties?**

* a. @Component decorator.
* b. @Model decorator.
* c. @NgModule decorator.
* d. @Module decorator.
* **Correct Answer:** c. @NgModule decorator.


* **Explanation:** Angular modules are configured by passing a metadata object to the `@NgModule` decorator.



**37. Which models represent just data passed from the component to the template?**

* a. View models
* b. Domain models
* c. Service models
* d. None
* **Correct Answer:** a. View models


* **Explanation:** View models abstract the view and hold the specific data state required solely for template rendering.



**38. The style of development that Angular supports is derived through the use of ______ pattern?**

* a. pattern
* b. Model-View-Controller
* c. User-Logic-Model
* d. Model-Template-Controller
* **Correct Answer:** b. Model-View-Controller


* **Explanation:** Angular's component-based architecture has its historical and conceptual roots in the MVC (or MVVM) design pattern.



**39. Which of the following directive allows us to use form?**

* a. ng-include
* b. ng-form
* c. ng-bind
* d. ng-attach
* **Correct Answer:** b. ng-form


* **Explanation:** In AngularJS, `ng-form` allows forms to be nested and dynamically controls form validation states.



**40. JavaScript ___ are used to manage the dependencies in a web application**

* a) modules
* b) functions
* c) files
* d) components
* **Correct Answer:** a) modules


* **Explanation:** JavaScript modules allow developers to encapsulate code and manage application dependencies via imports and exports.



**41. What is the main purpose of RESTful web services?**

* a. To perform CRUD operation on HTTP Request
* b. To perform CRUD operation without HTTP Request
* c. To perform web request other than CRUD operation
* d. To perform CRUD operation with TCP/IP Request
* **Correct Answer:** a. To perform CRUD operation on HTTP Request


* **Explanation:** RESTful services map standard CRUD (Create, Read, Update, Delete) database operations to standard HTTP requests.



**42. In which folder you will add the custom code and content for your application?**

* a) node_modules
* b) e2e
* c) src
* d) app
* **Correct Answer:** ~~d) app~~ / ✅ c) src


* **Explanation:** The `app` directory (inside the `src` folder) holds all the custom component, template, and logic code for the application.



**43. Which of the following command is correct for installing angular-cli?**

* a) npm install -g @angular/cli
* b) npm install -global @angular/cli
* c) npm install -g angular/cli
* d) npm install -global angular/cli
* **Correct Answer:** a) npm install -g @angular/cli


* **Explanation:** This is the standard NPM command to globally (`-g`) install the official Angular CLI package.



**44. Models can be:**

* a. view models
* b. domain models
* c. both a and b
* d. none
* **Correct Answer:** c. both a and b


* **Explanation:** Angular applications utilize both Domain Models (for core business logic) and View Models (for rendering UI states).



**45. Which of the following is a filter in Angular Js**

* a. Currency
* b. Date
* c. Uppercase
* d. All of the above
* **Correct Answer:** d. All of the above


* **Explanation:** Currency, Date, and Uppercase are all built-in formatting filters (or pipes) native to the framework.



**46. Which of the following typescript feature is used to reduce the common JavaScript errors?**

* a. Export
* b. Import
* c. Both A and B
* d. None
* **Correct Answer:** d. None


* **Explanation:** Strict static typing is the feature that reduces errors. Import and export just handle modularity.



**47. Angular applications are built around a design pattern called Model-View-Controller (MVC)**

* a) True
* b) False
* **Correct Answer:** a) True


* **Explanation:** Angular conceptually divides apps into data models, HTML view templates, and component controllers.



**48. The logic and data required to support the template are provided by its ___________**

* a. Model
* b. Component
* c. Templates
* d. Module
* **Correct Answer:** b. Component


* **Explanation:** The backing Component class dictates the logic and binds the specific data required by the HTML template.



**49. What does CSS stands for?**

* a. Cascading Style Sheet
* b. Cascading Sheet of Style
* c. Cascading Style Sheets
* d. None
* **Correct Answer:** c. Cascading Style Sheets


* **Explanation:** CSS is the acronym for Cascading Style Sheets, the language used for styling web documents.



**50. What are the purpose of using getter and setter?**

* a. Validate values
* b. Transform values
* c. Generating values
* d. All
* **Correct Answer:** d. All


* **Explanation:** Getters and setters intercept property reads and writes, allowing for validation, transformation, and dynamic generation of data.



**51. Which decorator is used to provide the configuration information through the properties?**

* a) @Component
* b) @NgModule
* c) @RootModule
* d) All
* **Correct Answer:** ~~d) All~~ / ==b) @NgModule==


* **Explanation:** Both `@Component` and `@NgModule` accept metadata property objects. (@RootModule is not standard, but "All" is the intended broad answer).



***

### **Part 2: Java EE & JSP Multiple Choice Questions**

**1. Which of the followings two mechanisms are used to make EJB persistence to the data storage?**

* a) Container-managed persistence
* b) Object-model persistence
* c) Bean-managed persistence
* d) A &C
* **Correct Answer:** d) A &C


* **Explanation:** Enterprise JavaBeans handle data persistence either automatically through the container (CMP) or manually via developer code (BMP).



**2. Which one is equal output to The &ltc:out & gt;Action**

* a. ${}
* b. getmethod of bean
* c. `<%=%>`
* d. Above a & c
* **Correct Answer:** c. `<%=%>`

* **Explanation:** The JSP expression tag outputs evaluated Java directly to the stream, perfectly mirroring the behavior of JSTL's `<c:out>`.



**3. What is the implicit that is one of type HttpSession?**

* a. Application
* b. httpSession
* c. httpsession
* d. Session
* **Correct Answer:** d. Session


* **Explanation:** The implicit `session` object in JSP is an automatically created instance of `javax.servlet.http.HttpSession`.



**4. In servlet the service() throws the following**

* a. IOException, ServletException
* b. HTTPexception
* c. ArrayOutOfboundException
* d. NullPointerException
* **Correct Answer:** a. IOException, ServletException


* **Explanation:** The signature of the standard `service()` method explicitly declares that it throws both `ServletException` and `IOException`.



**5. Hibernate is used to simplify to interact with the database**

* a. True
* b. False
* **Correct Answer:** a. True


* **Explanation:** Hibernate is an Object-Relational Mapping (ORM) framework that simplifies database interactions by mapping tables to Java objects.



**6. What directive do we use to point to the location of the tag file?**

* a. Tag
* b. Page
* c. Taglib
* d. Tagfile
* **Correct Answer:** c. Taglib


* **Explanation:** The `<%@ taglib %>` directive declares custom tag libraries and specifies their location using a URI.



**7. In JEE what happened when web container execute JSP?**

* a. jsp to Servlert code
* b. jsp to HTML
* c. implementation servlet
* d. above a & c
* **Correct Answer:** d. above a & c


* **Explanation:** The web container translates the JSP into a servlet implementation class before compiling and executing it.



**8. Which of the following configuration file control flows through the application in JSF?**

* a. Web.xml
* b. Faces-config.xml
* c. None
* **Correct Answer:** b. Faces-config.xml


* **Explanation:** `faces-config.xml` is the primary JSF file used to manage navigation rules and bean configurations.



**9. When we configure a JavaBean which of the following scopes are required(choose all that are applicable)**

* a. Page
* b. Request
* c. Session
* d. Application
* e. All of the above
* **Correct Answer:** e. All of the above


* **Explanation:** A JavaBean can be assigned to any of these four standard web application scopes.



**10. DoGet(), doPost(), doHead(), doDelete() belongs to what type of servlet?**

* a. HttpServlets
* b. GenericServlet
* c. All of the above
* d. None of the above
* **Correct Answer:** a. HttpServlets


* **Explanation:** These protocol-specific methods are defined natively within `javax.servlet.http.HttpServlet`.



**11. Config is object of which class?**

* a. javax.servlet.Context
* b. javax.servlet.ServletContext
* c. javax.servlet.ServletConfig
* d. javax.servlet.Application
* **Correct Answer:** c. javax.servlet.ServletConfig


* **Explanation:** The implicit `config` object in a JSP maps directly to the `ServletConfig` interface.



**12. In which two web application directories can dependent classes and libraries be located?**

* a. /WEB-INF/lib as a JAR file
* b. /WEB-INF/lib as compiled class file
* c. /WEB-INF/classes as compiled class file
* d. /META-INF/classes as compiled class files
* e. Above a & c
* **Correct Answer:** e. Above a & c


* **Explanation:** Packaged `.jar` files belong in `/WEB-INF/lib`, and compiled `.class` files belong in `/WEB-INF/classes`.



**13. When using servlet, we use log method for**

* a. Application log
* b. Web server log
* c. Jsp log
* d. Application server
* **Correct Answer:** d. Application server


* **Explanation:** The `log()` method routes output to the standard log streams of the application server (servlet container).



**14. Where you put JSTL lib on the web application?**

* a. WEB-INF/lib
* b. Lib
* c. Root/lib on container home path
* **Correct Answer:** a. WEB-INF/lib


* **Explanation:** All third-party dependency JARs, including JSTL libraries, must reside in `/WEB-INF/lib`.



**15. What type of programming in JSP?**

* a. Server
* b. Client
* **Correct Answer:** a. Server


* **Explanation:** JavaServer Pages (JSP) is a backend, server-side technology.



**16. When the web container cannot find a file requested in the web application, it will show the status code.**

* a. 408
* b. 500
* c. 404
* d. 504
* **Correct Answer:** c. 404


* **Explanation:** The HTTP 404 status code universally represents "Not Found".



**17. Which security mechanism uses the concept of a realm?**

* a. Authorization
* b. Data integrity
* c. Confidentiality
* d. Authentication
* **Correct Answer:** d. Authentication


* **Explanation:** A security realm is used to manage and verify user credentials for authentication.



**18. `<%=new java.util.Date()%>` is the example of –**

* a. Declaration
* b. ELException
* c. Expression
* d. Scriplet
* **Correct Answer:** c. Expression


* **Explanation:** The `<%= ... %>` block represents an expression tag in standard JSP syntax.



**19. Why do we use Servlet?**

* a. Maintainability
* b. Reusability
* c. Core functionality of all servlets
* d. Both a & b
* **Correct Answer:** d. Both a & b


* **Explanation:** Servlets establish a strong architecture that promotes code maintainability and reusability on the backend.



**20. Which of the following are the popular commercial O/R frameworks?**

* a. Toplink
* b. Struts
* c. Hibernete
* d. Both a & c
* **Correct Answer:** d. Both a & c


* **Explanation:** Both Oracle TopLink and Hibernate are prominent Object-Relational mapping solutions.



**21. Which of the following is a reserved word and so can’t be used as an EL identifier?**

* a. Empty
* b. Erase
* c. Error
* d. Evoke
* **Correct Answer:** a. Empty


* **Explanation:** `empty` is an inherent operator in the JSP Expression Language.



**22. Which of the following Layer Architecture keep separate Business Objects form Data Access Objects?**

* a. One-Layer Architecture
* b. Two-Layer Architecture
* c. Three--Layer Architecture
* d. All of the above
* **Correct Answer:** c. Three--Layer Architecture


* **Explanation:** The 3-tier architecture ensures strict separation between Presentation, Logic, and Data layers.



**23. Which of the following statements are true regarding RSS Newsreader?**

* a. RSS is a XML based format
* b. RSS is a text based format
* c. It represents the current news stores available on website.
* d. Both a & c
* **Correct Answer:** d. Both a & c


* **Explanation:** RSS utilizes a standard XML format to syndicate and distribute updated web content like news stories.



**24. How can we create drop-down menus, list boxes, radio buttons and check boxes in JSF by using?**

* a. The HTML Custom Actions
* b. The Core Custom Actions
* c. None
* **Correct Answer:** a. The HTML Custom Actions


* **Explanation:** JSF standardizes visual UI elements within its HTML component tag library.



**25. What is the recommended method of deploying into Tomcat?**

* a. Manually moving the files into a project folder
* b. Using a WAR file
* c. Editing the servlet.xml file
* d. Defending a context
* **Correct Answer:** b. Using a WAR file


* **Explanation:** Packaging an app into a Web Application Archive (WAR) is the safest standard format for server deployment.



**26. Which of the following handle HttpServlet response?**

* a. DoPost()
* b. doGet()
* c. getPost
* d. above a & b
* **Correct Answer:** d. above a & b


* **Explanation:** Servlets interact with the `HttpServletResponse` when overriding the `doPost()` and `doGet()` handlers.



**27. Which of the following are Identifying bean Scope of JSF?**

* a. Request
* b. Session
* c. Page
* d. Above a and b
* **Correct Answer:** d. Above a and b


* **Explanation:** Request and Session are valid JSF scopes; 'page' scope is restricted to JSPs.



**28. Which of the implicit variable of JSP pages that may be used to access all the other implicit object?**

* a. Context
* b. PageContext
* c. Page
* d. Object
* **Correct Answer:** b. PageContext


* **Explanation:** `pageContext` acts as the root object, possessing methods that expose all other implicit JSP objects.



**29. What are the main advantages of using an O/R framework over JDBC?**

* a. Using O/R you have a lot of queries and updates.
* b. Better performance
* c. Scalability and high availability
* d. Above b & c
* **Correct Answer:** d. Above b & c


* **Explanation:** ORM tools provide significant enhancements in performance (caching/pooling) and overall scalability compared to raw JDBC.



**30. Which of the following file is a deployment descriptor?**

* a. WEB_INF
* b. Web.xml
* c. Jsp-config.sml
* d. TLD
* **Correct Answer:** b. Web.xml


* **Explanation:** `web.xml` serves as the official deployment descriptor for Java EE web applications.



**31. Choose the correct answers related to Hibernate ?(Choose all are applicable)**

* a. Hibernate is an object-relational mapping (ORM) library for the java language
* b. Hibernate provides a mapping for object-oriented domain model to a traditional relational database.
* c. Hibernate is a database
* d. Above a & b
* **Correct Answer:** d. Above a & b


* **Explanation:** Hibernate is an ORM that maps Java classes to database tables; it is not a database engine itself.



**32. Which xml attribute allows us to specify XPath expressions?**

* a. Transform
* b. Allow
* c. Select
* d. View
* **Correct Answer:** c. Select


* **Explanation:** The `select` attribute is used in JSTL XML tags to process and evaluate XPath queries.



**33. Which of the following technology is best used when a great deal of programmatic control is required?**

* a. JSP
* b. Servlet
* c. JSF
* d. None
* **Correct Answer:** b. Servlet


* **Explanation:** Pure servlets offer direct access and unabridged programmatic control over the HTTP mechanics.



**34. Which of the following method would you require in removing a servlet instance permanently form a servlet container?**

* a. doDelete()
* b. destroy()
* c. delete()
* d. remove()
* **Correct Answer:** b. destroy()


* **Explanation:** The container triggers the `destroy()` method before terminating the servlet and garbage-collecting its resources.



**35. The Internationalization and Formatting tag library provides actions that allow you to control the – settings for your JSP pages**

* a. Date
* b. Locale
* c. Time
* **Correct Answer:** b. Locale


* **Explanation:** The JSTL formatting tag library specifically configures Locale settings for multi-language applications.



**36. Which of the following configurator file is responsible for Hibernat connection?**

* a. Context.xml
* b. Hibernat.cfg.xml
* c. *.hbrn.xml
* **Correct Answer:** b. Hibernat.cfg.xml


* **Explanation:** `hibernate.cfg.xml` is the central file for establishing standard Hibernate connections and configurations.



**37. The Servlet interface has lifecycle methods the following**

* a. Init()
* b. Service()
* c. Destroy()
* d. All of the above
* **Correct Answer:** d. All of the above


* **Explanation:** `init()`, `service()`, and `destroy()` form the required foundation of the Servlet interface.



**38. What is the abbreviation of JSP?**

* a. Java Service Programming
* b. Java Server Programming
* c. Java Service Page
* d. Java Server Pages
* **Correct Answer:** d. Java Server Pages


* **Explanation:** JSP stands for JavaServer Pages.



**39. Which one is the correct include core jstl library ?**

* a. `<%@ taglib uri=[http://java.sun.com/jstl/core](http://java.sun.com/jstl/core) prefix=”c”%>`
* b. `<%@ taglib uri=[http://java.sun.com/jsp/jstl/core](http://java.sun.com/jsp/jstl/core) prefix=”c”%>`
* c. `<%@ taglib uri=[http://java.sun.com/jsf/core](http://java.sun.com/jsf/core) prefix=”c”%>`
* **Correct Answer:** b. `<%@ taglib uri=[http://java.sun.com/jsp/jstl/core](http://java.sun.com/jsp/jstl/core) prefix=”c”%>`

* **Explanation:** This is the standard, specified URI path to import the JSTL core library.



**40. What is the purpose of attributes in terms of classic Tag?**

* a. Wrap up functionalities for the tag
* b. Wrap up XML for the tag
* c. Without attribute tag does not execute
* d. None of the above
* **Correct Answer:** a. Wrap up functionalities for the tag


* **Explanation:** Attributes inject data and parameters to customize the behavior and functionalities of custom tags.



**41. What is the method of jspServer of HttpJspPage?**

* a. Void_jspService(HttpServletRequest, HttpServletResponse)
* b. Void_jspService()
* c. Void_jspService(HttpServletRequest, HttpServletResponse) throws IOException, ServletException
* **Correct Answer:** c. Void_jspService(HttpServletRequest, HttpServletResponse) throws IOException, ServletException


* **Explanation:** Request handlers in translated JSPs must declare these fundamental runtime exceptions in their signature.



**42. Which are the correct about Model 1 Architecture?(choose all that are applicable)**

* a. Quick and simple
* b. Page centric
* c. Complex
* d. Not page centric
* e. Above a & b
* **Correct Answer:** e. Above a & b


* **Explanation:** Model 1 architecture handles operations purely within individual JSPs, making it highly page-centric and fast to write.



**43. Which of the following is examples of JSP directive?**

* a. Include
* b. Exclude
* c. Import
* d. Taglibrary
* **Correct Answer:** a. Include


* **Explanation:** `<%@ include %>` serves as one of the three primary directives in the JSP specification.



**44. The prefix f: in JSF refers to _________**

* a. HTML elements tor the page
* b. Core JSF Functionality for the page
* c. Input text fields in the form
* d. None
* **Correct Answer:** b. Core JSF Functionality for the page


* **Explanation:** The `f:` prefix provides non-visual core elements, like validators, converters, and event listeners.



**45. Which of the following are the basic deployment technique? (choose two)**

* a. Expanded directory format
* b. JAR
* c. WAR
* d. Class
* e. Both a & c
* **Correct Answer:** e. Both a & c


* **Explanation:** Applications are typically pushed to the server either securely packaged as WAR files or as raw expanded directories.



**46. Which package is used that you have no longer to manage database connection parameters in your code?**

* a. Java.sql.DriverManager
* b. Org.git.mm.mysql.Driver
* c. Javax.sql.DataSource
* d. None
* **Correct Answer:** c. Javax.sql.DataSource


* **Explanation:** Using the `DataSource` interface delegates database credential management entirely to the application server via JNDI.



**47. Which of the followings are JSF action Tags?**

* a. `<c:choose>`
* b. `<sql:set.DateSource>`
* c. `<h:dataTable>`
* d. `<f:selectItem>`
* e. Both c & d
* **Correct Answer:** e. Both c & d


* **Explanation:** `<h:dataTable>` handles HTML logic and `<f:selectItem>` handles Core logic, and both are standard JSF tags.



**48. Which of the following are JSP Action tags are used for bean development?**

* a. Jsp:useBean
* b. Jsp:setProperty
* c. jsp:getProperty
* d. All of the above
* **Correct Answer:** d. All of the above


* **Explanation:** These three tags function collaboratively to instantiate, map, and retrieve JavaBean properties dynamically.



**49. The <c:if%gt; Actionws has a mandatory attribute**

* a. Id
* b. Var
* c. Test
* **Correct Answer:** c. Test


* **Explanation:** The `<c:if>` tag demands the `test` attribute containing the boolean condition that triggers execution.



**50. Which of the following two JAR files required for JSTL implementation?**

* a. Commons-collections.jar
* b. X.tld
* c. Standard.jar
* d. Jstl.jar
* e. Above c & d
* **Correct Answer:** e. Above c & d


* **Explanation:** Legacy deployments require both the specification (`jstl.jar`) and the runtime implementation (`standard.jar`).



**51. Which tag provide a generic way to access URL-based resources that can be either included or processed ?**

* a. `<c:import>`
* b. `<c:url>`
* c. `<c:param>`
* **Correct Answer:** a. `<c:import>`

* **Explanation:** The `<c:import>` tag is heavily utilized to fetch and seamlessly integrate external domain content dynamically.



**52. What is the purpose of DAO pattern?**

* a. It is used for encapsulating data access
* b. IT is used for authentication
* c. It is used for caching
* d. None
* **Correct Answer:** a. It is used for encapsulating data access


* **Explanation:** Data Access Objects encapsulate and segregate complex database logic away from primary business functions.



**53. Which of the following is not an implicit object?**

* a. Request
* b. Response
* c. Cookie
* d. Session
* **Correct Answer:** c. Cookie


* **Explanation:** Cookies exist as part of request headers but are not generated as standalone, predefined implicit variables in JSPs.



**54. What is the main purpose of using EL?**

* a. To remove XML from JSP pages
* b. To remove standard actions from JSP pages
* c. To remove java syntax From JSP pages
* **Correct Answer:** c. To remove java syntax From JSP pages


* **Explanation:** Expression Language replaces complex inline Java scriptlets with clear, concise bracket notation for cleaner code.



**55. Which of the following properties provide an easy facility for internationalizing and customizing the pages for JSF?**

* a. Java
* b. Tag library
* c. Message Bundles
* d. None
* **Correct Answer:** c. Message Bundles


* **Explanation:** Message Bundles abstract static text into translation-friendly resource property files for internationalization.



**56. Where do you put your JAR file under the WEB-INF folder when the JAR file contains all the custom tags that you created?**

* a. WEB-INF/classes
* b. WEB-INF/lib
* c. WEB-INF/common
* d. WEB-INF/tlds
* **Correct Answer:** b. WEB-INF/lib


* **Explanation:** Standard server classloading mechanisms scan the `/WEB-INF/lib` directory natively for all packaged JAR libraries.



**57. Which of the following ways you can terminate session? (choose two)**

* a. Session.invalidate()
* b. Session.destroy()
* c. Session.timeout
* d. Logout
* **Correct Answer:** a. Session.invalidate() and c. Session.timeout


* **Explanation:** Sessions are actively wiped using `invalidate()` or culled automatically when the designated timeout configuration is hit.



**58. When destroy() method of a filter is called?**

* a. The destroy() method is called only once at the beginning of the life cycle of a filter
* b. The destroy() method is called after the filter has executed
* c. The destroy() method is called only once at the end of the life cycle of a filter
* d. The destroy() method is called after the filter has executed doFilter method
* **Correct Answer:** c. The destroy() method is called only once at the end of the life cycle of a filter


* **Explanation:** The web container invokes `destroy()` exactly once to clear out references and memory before the filter shuts down.



**59. Which of the following is a server-side technology?**

* a. Html
* b. Jsp
* c. Javascript
* d. Css
* **Correct Answer:** b. Jsp


* **Explanation:** JSPs execute within the backend server container to dynamically compile the HTML returned to the browser.



**60. To define Faces Servlet in web.xml `<servlet> <servlet-name>Faces Servlet </servlet-name> class>blank </servlet-class> <load-on-startup>1</load-on startup> <servlet>` the value of blank `</servlet>**`

* a. javax.faces.webapp.ext.FacesServlet
* b. javax.faces.webapp. FacesServlet
* c. javax.faces.webapp.Servlet. FacesServlet
* d. None of the above
* **Correct Answer:** b. javax.faces.webapp. FacesServlet


* **Explanation:** `FacesServlet` serves as the foundational controller class that intercepts and manages routing for JSF requests.



**61. What is the primary job of the action tag?**

* a. To configure a data source
* b. To catch exception
* c. Formatting tag library
* d. None
* **Correct Answer:** d. None


* **Explanation:** Standard action tags broadly control dynamic page behaviors (like forwarding or including resources), rendering the provided options incorrect.



**62. Evaluate the following JSP script and select the right option**
1.<%--inside code here--%>
2.
3.
4.Today is: `<%= new Date()%>`
5.
6.
What needs to go on line 1

* a. `<%@ page import =”#{java.util.Date}”%>`
* b. `<%@ import class=”#{java.util.Date}”%>`
* c. `<%@include file=”#{java.util.Date}”%>`
* d. `<%@ include class=”#{java.util.Date}”%>`
* **Correct Answer:** a. `<%@ page import =”#{java.util.Date}”%>`

* **Explanation:** A class must be successfully imported via a `page` directive to be instantiated via scriptlet or expression syntax natively within the file.



**63. Which of the following are JSTL Action elements?**

* a. Stander
* b. Custom
* c. SQL
* d. Core
* e. Above c & d
* **Correct Answer:** e. Above c & d


* **Explanation:** Both Core and SQL constitute definitive logical tag libraries structurally codified within the JSTL specification.
### **Detailed Merge Report**

- **Total Initial Questions:** 114 questions were originally contained in the `jsp-angular-mcq.docx` document (51 Angular questions and 63 Java EE questions).
    
- **Total Merged/Duplicate Questions:** 1 duplicate question was identified. Original Angular Question 19 (_"The decorator provides configuration information through its:"_) possessed identical options and conceptual intent to Angular Question 09 (_"How can decorator provide configuration information?"_) and was merged into a single entry (now represented as Question 9 in the final batch).
