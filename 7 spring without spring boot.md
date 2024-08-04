
1. create a starter java application with nothing just remember to add maven
2. add `Spring Context` dependency from Maven repository to `pom.xml` file and reload it
3. Now create following files

```java
public class Dev {
	public void build(){
		System.out.println("Working on some Awsome Project.");
	}
}
```

```java
public class App {  
    public static void main( String[] args )  
    {  
  
        ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");  
		Dev obj = context.getBean(Dev.class);
		obj.build();
    }  
}
```

- we are telling main to create `ApplicationContext` using `spring.xml`
- but we need to create `spring.xml` by ourselves
- We need to create this file (acc. to intellij) main > java > resources > spring.xml
- Sample spring . xml

```java
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:util="http://www.springframework.org/schema/util"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd"> 
       <!-- bean definitions here -->  
       
    <bean id="dev" class="org.eccentric.Dev">  
    </bean>
</beans>
```

## Ways to create - object
```java
main() {
...
	Dev obj = context.getBean(Dev.class); // using class bame
	Dev obj = context.getBean("dev"); // using bean id
...
}
```

### Multiple beans
- we can have multiple beans for same class.
- basically multiple objects of same class in IoC
- to do so we can create two beans in xml using different bean id
```java
<beans>
	<bean id="dev" class="org.eccentric.Dev">  
    </bean>
    <bean id="dev1" class="org.eccentric.Dev">  
    </bean>
</bean>
```

```java
main() {
...
	Dev obj = context.getBean("dev"); // bean 1
	Dev obj = context.getBean("dev1"); // bean 2
...
}
```

## object creation
- objects for each bean is created even if they were not used at all.
- for two beans of same class. 2 objects are called. i.e. constructor is called 2 times
- you can confirm it 
```java
public class Dev {
	public Dev() {
		System.out.println("In Dev's constructor.");
	}
	public void build(){
		System.out.println("Working on some Awsome Project.");
	}
}
```

```java
<beans>
	<bean id="dev" class="org.eccentric.Dev">  
    </bean>
    <bean id="dev1" class="org.eccentric.Dev">  
    </bean>
</bean>
```

```java
main() {
...
	Dev obj = context.getBean("dev"); // bean 1
	Dev obj = context.getBean("dev1"); // bean 2
...
}
```

# initialize variables with default values
- there are 2 ways :
	- setter injection
	- constructor injection
- say `Dev`   has `age` variable and we want spring to initialize it on its own
## (setter injection in spring) 
- **Note - you need to create getters and setter for each new variable you want spring to initialise**
```java
public class Dev {
	int age;
	public int getAge() {
		return age;
	}
	public void setAge(int age){
		this.age = age;
	}
	public Dev() {
		System.out.println("In Dev's constructor.");
	}
	public void build(){
		System.out.println("Working on some Awsome Project.");
	}
}
```

```java
<beans>
	<bean id="dev" name="org.rohit.Dev"> 
		<property name="age" value="12" />
	</bean>
</beans>
```

## Constructor injection in spring
- initialising age using constructor
```java
public class Dev {
	int age;
	public Dev() {
		System.out.println("In Dev's constructor.");
	}
	public Dev(int age) {
		this.age = age;
	}
	public Dev(int age, int salary) {
		}
	public void build(){
		System.out.println("Working on some Awsome Project.");
	}
}
```

```java
<beans>
	<bean id="dev" name="org.rohit.Dev"> 
		<constructor-arg value="14"/>
		// <constructor-arg index="1" value="50"> // for salary
	</bean>
</beans>
```

- note that we haven't used any name property in `<constructor-arg>` its because we have only one constructor with one argument.
- we can use `name="name_of_arg"` 
- we can also use `index="index_of_arg"` if required

#### till no we were initialising only primitive type
- to initialise secondary types we use ref

```java
public class Dev {
	private Computer com;
	private int age;
	public Dev() {
		System.out.println("In Dev's constructor.");
	}
	public Dev(int age) {
		this.age = age;
	}
	public Dev(int age, Computer com) {
		this.age = age;
		this.com = com;
	}
	public void build(){
		System.out.println("Working on some Awsome Project.");
	}
}
```
```java
<beans>
	<bean id="laptop1" name="org.rohit.Laptop"/>
	<bean id="dev" name="org.rohit.Dev">
		<constructor-arg name="age" value="18"/>
		<constructor-arg name="comp" ref="laptop1"/>
	</bean>
</beans>
```

