what ever is your starting class
you can do it in two ways

#### spring boot - 1
```java
@SpringBootApplication  
public class FirstWebAppApplication {  
    public static void main(String[] args) {  
       SpringApplication.run(FirstWebAppApplication.class, args);  
    }  
}
```
spring boot - 2
```java
@SpringBootApplication  
public class FirstWebAppApplication {  
    public static void main(String[] args) {  
	       Application context = SpringApplication.run(FirstWebAppApplication.class, args);  
    }  
}
```
#### SPRING
```java
public class App {  
    public static void main( String[] args )  
    {  
        ApplicationContext context = new 
		    ClassPathXmlApplicationContext("spring.xml");  
    }  
}
```

`resources > spring.xml`
**Go to 7 for more information**
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:util="http://www.springframework.org/schema/util"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd"> <!-- bean definitions here -->  
  
    <bean id="dev" class="org.eccentric.Dev">  
    </bean>  
    <bean id="dev1" class="org.eccentric.Dev">  
    </bean>  
  
    <bean id="laptop" class="org.eccentric.Laptop">  
    </bean>  
</beans>
```