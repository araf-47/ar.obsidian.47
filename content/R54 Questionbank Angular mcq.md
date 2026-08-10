Here are the extracted multiple-choice questions from the provided document, along with the correct answers and brief explanations.

**01. In angular, controllers are called**

- a. Module
    
- **b. Component**
    
- c. servic
    
- d. model
    

**Correct Answer:** b. Component **Explanation:** Modern Angular uses a component-based architecture where Components take on the traditional role of controllers by managing the logic and data for their associated views.

**02. The GET method is ______ which means the operations you perform in response to this method should only retrieve data and not modify it.**

- a) Idempotent
    
- **b) Nullipotent**
    
- c) Both
    
- d) Neither nullipotent nor idempotent
    

**Correct Answer:** b) Nullipotent **Explanation:** While GET is technically both, an operation that strictly reads data without causing any state modification or side-effects on the server is best described as nullipotent.

**03. Which directive is used to repeat a region of content for each item in an array**

- a. `*ngFor`
    
- b. *ngSwitch
    
- c. *ngIf
    
- d. *ngLoop


**Correct Answer:** a. `*ngFor` **Explanation:** The `*ngFor` structural directive acts as an Angular repeater, instantiating a template once per item from an iterable collection.

**04. Which function returns true if the array contains the specified value?**

- a. test(value)
    
- b. map(value)
    
- c. check(value)
    
- **d. includes (value)**


**Correct Answer:** d. includes (value) **Explanation:** In JavaScript and TypeScript, the `Array.prototype.includes()` method determines whether an array includes a certain value among its entries, returning true or false as appropriate.

**05. Each TypeScript file in the project acts as**

- a. Model
    
- **b. Module**
    
- c. Component
    
- d. Both b & c


**Correct Answer:** b. Module **Explanation:** In TypeScript, any file containing a top-level `import` or `export` is considered a module.

**06. TypeScript is a superset of JavaScript**

- **a. true**
    
- b. false

**Correct Answer:** a. true **Explanation:** TypeScript builds upon JavaScript by adding optional static typing and class-based object-oriented programming features.

**07. Which command is used to create a new angular app?**

- a. ng create project_name
    
- **b. ng new project_name**
    
- c. Both a and b
    
- d. None

**Correct Answer:** b. ng new project_name **Explanation:** The Angular CLI command `ng new` generates a new workspace and an initial Angular app.

**08. Which of the following is correct about TypeScript?**

- a. Angular is based on TypeScript
    
- b. This is a superset of JavaScript
    
- c. TypeScript is maintained by Microsoft
    
- **d. All**

**Correct Answer:** d. All **Explanation:** All of the listed statements about TypeScript are accurate facts.

**09. How can decorator provide configuration information?**

- **a. properties**
    
- b. objects
    
- c. class
    
- d. method

**Correct Answer:** a. properties **Explanation:** Decorators accept metadata objects, utilizing the properties of those objects (like `selector` or `templateUrl`) to configure the target class.

**10. TypeScript is a language**

- **a. Open Source**
    
- b. Closed
    
- c. Free
    
- d. All of the above

**Correct Answer:** a. Open Source **Explanation:** TypeScript is an open-source programming language developed and maintained by Microsoft.

**11. AngularJS directives we used in**

- a) Model
    
- **b) View**
    
- c) Controller
    
- d) Module

**Correct Answer:** b) View **Explanation:** Directives are used within HTML templates (the View) to manipulate the Document Object Model (DOM).

**12. Which file is acts as placeholder for basic angular app?**

- a) Main.ts
    
- b) app.module.ts
    
- **c) index.html**
    
- d) app.template.html

**Correct Answer:** c) index.html **Explanation:** The `index.html` file serves as the main web page where the root Angular component is injected and rendered.

**13. The angular-cli setup for the project created a template file called ______ in the src/app folder.**

- a) App.model.ts
    
- **b) app.component.html**
    
- c) app.component.js
    
- d) app.component.css

**Correct Answer:** b) app.component.html **Explanation:** The CLI creates `app.component.html` as the default template for the application's root component.

**14. Which keyword is used to define types that can be instantiated with the new keyword to create objects that have well-defined data and behaviour?**

- a) Object
    
- **b) Class**
    
- c) Prototype
    
- d) Static

**Correct Answer:** b) Class **Explanation:** The `class` keyword defines a blueprint for creating objects with specific properties and methods.

**15. Which ng command performs the production build process?**

- a. Ng start
    
- b. Ng lint
    
- **c. Ng build**
    
- d. Ng test

**Correct Answer:** c. Ng build **Explanation:** The `ng build` command compiles the Angular application into an output directory for deployment.

**16. Which keyword is used to identify data or types that you want to use elsewhere in the application?**

- a. Import
    
- **b. Export**
    
- c. New
    
- d. Add

**Correct Answer:** b. Export **Explanation:** The `export` keyword exposes a module's features so they can be imported and utilized in other files.

**17. Which directive can be used to set multiple style properties?**

- a) ngClass
    
- **b) ngStyle**  
    
- c) Both A and B
    
- d) None

**Correct Answer:** b) ngStyle **Explanation:** The `ngStyle` directive allows you to dynamically set multiple inline CSS styles using a key-value object.

**18. What do you mean by NPM?**

- **a) Node Package Manager**
    
- b) Node Packet Manager
    
- c) Node Project Manager
    
- d) Node Package Machine

**Correct Answer:** a) Node Package Manager **Explanation:** NPM stands for Node Package Manager, the default package manager for the Node.js JavaScript runtime environment.

**19. The decorator provides configuration information through its:**

- **a. properties**
    
- b. objects
    
- c. class
    
- d. method

**Correct Answer:** a. properties **Explanation:** Decorators read configuration settings through the properties defined in their metadata object.

**20. Which file contains the configuration details of angular development tools?**

- a) package.json
    
- b) package-lock.json
    
- c) tsconfig.json
    
- **d) angular.json**

**Correct Answer:** d) angular.json **Explanation:** `angular.json` provides workspace-wide and project-specific configuration for the Angular CLI.

**21. You can convert the numbers to strings with the ______ method**

- a. Convert
    
- **b. toString**
    
- c. numberToString
    
- d. toFixed

**Correct Answer:** b. toString **Explanation:** The `.toString()` method is a standard JavaScript function used to return a string representation of a number.

**22. You can define function in two ways:**

- **a. function expression**
    
- b. function component
    
- **c. function declaration**
    
- d. Both a & b (Correct ans: ==Both a & C==)

**Correct Answer:** a & c _(Note: The exam options present a flaw here by providing 'Both a & b' instead of the logically expected 'Both a & c'. Conceptually, functions are defined via expressions or declarations)._

**Explanation:** In JavaScript, you can define functions primarily through declarations (`function doSomething() {}`) or expressions (`const doSomething = function() {}`).

**23. TypeScript file extension is**

- a. js
    
- b. es
    
- **c. ts**
    
- d. tts

**Correct Answer:** c. ts **Explanation:** TypeScript source files end with the `.ts` extension.

**24. Angular configuration file name is:**

- a. Package.json
    
- **b. Angular.json**
    
- b. Composer.json _(Note: duplicate option letter in source)_
    
- d. Config.json

**Correct Answer:** b. Angular.json **Explanation:** `angular.json` is the central configuration file for an Angular workspace.

**25. ngModel directive is used for**

- a. One-way binding
    
- **b. Two-way binding**
    
- c. Refer element in the template

**Correct Answer:** b. Two-way binding **Explanation:** `ngModel` handles two-way data binding, syncing values between the template (UI) and the component class.

**26. Which keyword is used to define a constant value that will not change?**

- a. Final
    
- b. Let
    
- **c. Const**
    
- d. Get

**Correct Answer:** c. Const **Explanation:** In JavaScript/TypeScript, the `const` keyword declares a variable whose reference cannot be reassigned.

**27. Two-way bindings are used with HTML ______ elements**

- a. Table
    
- **b. Form**
    
- c. Div
    
- d. Heading

**Correct Answer:** b. Form **Explanation:** Two-way binding (like `ngModel`) is designed primarily for form input elements (inputs, selects, textareas).

**28. Which type of web application requires a lot of bandwidth?**

- a. One-page
    
- b.Single_page
    
- c. Multiple-page
    
- **d.round-trip**

**Correct Answer:** d. round-trip **Explanation:** Round-trip (multi-page) applications necessitate loading complete HTML pages from the server upon every interaction, increasing bandwidth usage.

**29. Which command starts the Angular development tools:**

- a. Ng new
    
- **b. Ng serve**
    
- c. Ng run
    
- d. Ng start

**Correct Answer:** b. Ng serve **Explanation:** The `ng serve` command builds the app and launches a local development server.

**30. In angular, Default root module name is**

- a. module.ts
    
- **b. app.module.ts**
    
- c. module.js
    
- d. app.module.js

**Correct Answer:** b. app.module.ts **Explanation:** By default, the Angular CLI creates the application's root module inside `app.module.ts`.

**31. Which object oriented terms not supported by Typescript?**

- A. Abstract class
    
- B. Classes
    
- C. Interfaces
    
- D. Modules

**Explanation/Note:** TypeScript natively supports _all_ of the concepts listed in options A through D. This question appears to be flawed, as there is no correct answer among the provided choices.

**32. How do you install the npm package?**

- **a) npm install PackageName**
    
- b) npm-install PackageName
    
- c) npm PackageName
    
- d) Ng create new appName

**Correct Answer:** a) npm install PackageName **Explanation:** `npm install` is the standard Node Package Manager command to download and install a package.

**33. Which keyboard command is used to terminate any angular process**

- **a. Ctrl+c**
    
- b. Ctrl+p
    
- c. Ctrl+z
    
- d. Ctrl+d

**Correct Answer:** a. Ctrl+c **Explanation:** `Ctrl+C` sends an interrupt signal to stop processes running in a terminal, such as an active `ng serve` session.

**34. How do you apply command to check node version?**

- a. nodejs-v
    
- b. nodejs
    
- **c. node -v**
    
- d. node-version

**Correct Answer:** c. node-v **Explanation:** While the exact spacing in a terminal is `node -v`, option C most closely represents the correct command flag to check the Node runtime version.

**35. Angular works on what page?**

- a. Round trip application
    
- **b. Single page application //best**
    
- c. Both a & b
    
- d. none

**Correct Answer:** b. Single page application **Explanation:** Angular is specifically optimized for building Single Page Applications (SPAs) where views update without full page reloads.

**36. How can Angular module provide configuration information through the properties?**

- a. @Component decorator.
    
- b. @Model decorator.
    
- **c. @NgModule decorator.**
    
- d. @Module decorator.

**Correct Answer:** c. @NgModule decorator. **Explanation:** The `@NgModule` decorator defines an Angular module and accepts a metadata object containing its configuration properties.

**37. Which models represent just data passed from the component to the template?**

- **a. View models**
    
- b. Domain models
    
- c. Service models
    
- d. None

**Correct Answer:** a. View models **Explanation:** View models are data structures tailored specifically for the UI view, separate from backend domain data.

**38. The style of development that Angular supports is derived through the use of ______ pattern?**

- a. pattern
    
- **b. Model-View-Controller**
    
- c. User-Logic-Model
    
- d. Model-Template-Controller

**Correct Answer:** b. Model-View-Controller **Explanation:** Angular's architecture stems from the MVC (or MVVM) design pattern, separating logical components from the UI template.

**39. Which of the following directive allows us to use form?**

- a. ng-include
    
- **b. ng-form**
    
- c. ng-bind
    
- d. ng-attach

**Correct Answer:** b. ng-form **Explanation:** In early versions of Angular (AngularJS), `ng-form` was used to instantiate a form object.

**40. JavaScript ______ are used to manage the dependencies in a web application**

- **a) modules**
    
- b) functions
    
- c) files
    
- d) components

**Correct Answer:** a) modules **Explanation:** ES6 Modules allow JavaScript code to export and import dependencies securely across different files.

**41. What is the main purpose of RESTful web services?**

- **a. To perform CRUD operation on HTTP Request**
    
- b. To perform CRUD operation without HTTP Request
    
- c. To perform web request other than CRUD operation
    
- d. To perform CRUD operation with TCP/IP Request

**Correct Answer:** a. To perform CRUD operation on HTTP Request **Explanation:** RESTful services map CRUD (Create, Read, Update, Delete) operations directly to standard HTTP methods (POST, GET, PUT, DELETE).

**42. In which folder you will add the custom code and content for your application?**

- a) node_modules
    
- b) e2e
    
- **c) src**
    
- d) app

**Correct Answer:** c) src **Explanation:** The `src` directory contains the source code (including the `app` folder) for the Angular application being developed.

**43. Which of the following command is correct for installing angular-cli?**

- **a) npm install -g @angular/cli**
    
- b) npm install -global @angular/cli
    
- c) npm install -g angular/cli
    
- d) npm install -global angular/cli

**Correct Answer:** a) npm install -g @angular/cli **Explanation:** This is the correct terminal command to install the Angular CLI globally via NPM.

**44. Models can be:**

- a. view models
    
- b. domain models
    
- **c. both a and b**
    
- d. none

**Correct Answer:** c. both a and b **Explanation:** A codebase can implement both view models (for the UI state) and domain models (for the core business data).

**45. Which of the following is a filter in Angular Js**

- a. Currency
    
- b. Date
    
- c. Uppercase
    
- **d. All of the above**

**Correct Answer:** d. All of the above **Explanation:** In AngularJS (version 1.x), Currency, Date, and Uppercase were all built-in filters (which are now called Pipes in modern Angular).

**46. Which of the following typescript feature is used to reduce the common JavaScript errors?**

- a. Export
    
- b. Import
    
- c. Both A and B
    
- **d. None**

**Correct Answer:** d. None **Explanation:** The primary TypeScript feature used to reduce common JavaScript errors is _static typing_, which is not listed as an option here. (Export and Import manage module visibility, not type safety).

**47. Angular applications are built around a design pattern called Model-View-Controller (MVC)**

- **a) True**
    
- b) False

**Correct Answer:** a) True **Explanation:** Angular utilizes MVC-inspired architecture to decouple logic, templates, and data.

**48. The logic and data required to support the template are provided by its**

- a. Model
    
- **b. Component**
    
- c. Templates
    
- d. Module

**Correct Answer:** b. Component **Explanation:** The component class encapsulates the logic and state data that the HTML template displays and binds to.

**49. What does CSS stands for?**

- a. Cascading Style Sheet
    
- b. Cascading Sheet of Style
    
- **c. Cascading Style Sheets**
    
- d. None

**Correct Answer:** c. Cascading Style Sheets **Explanation:** CSS is the acronym for Cascading Style Sheets.

**50. What are the purpose of using getter and setter?**

- a. Validate values
    
- b. Transform values
    
- c. Generating values
    
- **d. All**

**Correct Answer:** d. All **Explanation:** Getters and setters intercept property access, allowing you to validate data before assignment, transform data on retrieval, or dynamically generate computed values.

**51. Which decorator is used to provide the configuration information through the properties?**

- **a) @Component**
    
- b) @NgModule
    
- c) @RootModule
    
- d) All

**Correct Answer:** a) @Component **Explanation:** The `@Component` decorator is the most common decorator used to define property configuration (like selectors and styles) for Angular elements. _(Note: While @NgModule also accepts properties, @Component is the standard expectation for generic questions of this type unless specifying modules)._