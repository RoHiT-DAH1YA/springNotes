
```java
package com.group.sampleProject;  
  
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  
  
@SpringBootApplication  
public class SampleProjectApplication {  
  
    public static void main(String[] args) {  
       SpringApplication.run(SampleProjectApplication.class, args);  
    }  
  
}

```

```java
package com.group.sampleProject;  
  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.RestController;  
  
@RestController  
public class Hello {  
  
    @RequestMapping("/")  
    public String greet() {  
        return "Hello world, Welcome SEAMAN!!! to spring demo";  
    }  
}
```


@SpringBootApplication ->
	tells java it is a spring application
@RestController("path/of/the/request/") ->
	tells that it is taking http request for the path defined
@RequestMapping("path/to/request/") ->
	this is added on top of functions. Request Mapping handles all type of requests like get put post delete etc. To handle a specific use
	@GetMapping, @PostMapping, @DeleteMapping, etc.