# 3. Building microservices with Spring Boot
## Service design
- Decomposition guidelines:
  - Pay attention to the nouns & verbs used to describe business problem
  - Look for data cohesion: highly correlated data -> single service, separate data -> dif service
- Service granularity guidelines:
  - Start broad then refactor into smaller services
  - Focus first on how services interact
  - Change service responsibility following understanding of the problem domain
  - Signs of services that are too coarse-grained:
    - Too many responsibilities
    - Manage data across a large number of tables
    - Too many test cases
  - Signs of services that are too fine-grained:
    - Services are heavily dependent on one another
    - Services only do simple CRUD
- URL naming guidelines:
  - Specify the resource the service represent
  - Use nesting to represent relationships between resource
  - -> If URLs are too long, the service might be doing too much
  - Establish a version scheme early (eg prepend all endpoints with a version number)
- Development best practices:
  - Build a layered service
  - Avoid premature framework design & adoption which might have high maintenance cost
## Spring Boot annotations & elements
- RestController:
  - Def: class level annotation, specifying a REST-based service class
  - Parse JSON & XML input data
  - Return output data as JSON by default
- RequestMapping(value="value"):
  - Def: class/method level annotation, specifying the HTTP endpoint exposed to users
  - At class level, specifying the root URL for all endpoints exposed by the controller
  - Param: place inside {}
- GetMapping(value="value") = RequestMapping(value="value", method = RequestMethod.GET)
- -> PostMapping, PutMapping, DeleteMapping are similar
- PathVariable("name"): method param annotation, mapping the param in the URL to the method's param
- RequestBody: method param annotation, mapping the request body into an object
- ResponseEntity`<Type>`: wrapper object, representing the entire HTTP response (status code, header, body of Type)
## Localization: skipped
## Spring HATEOAS
- Add hyperlinks for a given resource
- Usage:
  - Extend the model class using RepresentationModel`<Type>`
  - In the GET handler of the class, call model.add(link). link can be built with HATEOAS link to static method.