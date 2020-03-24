# @RequestMapping
Mapping URI with annotated the class or method that will handle the request.

```java
@RequestMapping("/home")
public class HomeController {

    @RequestMapping("test")
    public String test() {
      ...
    }
}
```

## Available parameters
- HTTP methods as a parameter
- HTTP header that should be matched along with URI
- Multiple matching URIs

# @PathVariable
Annotation which indicates that a method parameter should be bound to a URI template variable

## @RequestMapping with @PathVariable
RequestMapping annotation can be used to handle dynamic URIs where one or more of the URI value works as a parameter. We can even specify Regular Expression for URI dynamic parameter to accept only specific type of input. It works with @PathVariable annotation through which we can map the URI variable to one of the method arguments. For example:
```java
@RequestMapping("homes/{version}")
public String getHomes(@PathVariable("version") String version) {
    ...
}
```
It's also possible to use regex.

# @RequestParam
Matches query parameters with the given type
```java
@RequestMapping("homes/{version}")
public String getHomes(@PathVariable("version" String version,
                       @RequestParam("id") int id) {
     ...
}
```

---
Refer:
- https://www.journaldev.com/3358/spring-requestmapping-requestparam-pathvariable-example
