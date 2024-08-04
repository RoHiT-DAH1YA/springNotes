## Steps
1. config spring - you don't want spring to handle every object but only the objects you were asked to take care of.

## Example

#### Iteration - 1
```java
public class Dev {
	public void build(){
		System.out.println("working on Awsome Project");
	}
}
```

```java
@SpringBootApplication
public class Myapplication {
	psvm (String args[]) {
		SpringApplication.run(MyApplication.class, args);

		Dev dev1 = new Dev();
		dev1.build();
	}
}

/* output
Working on Awsome Project
/*
```
- here we are creating the object by ourselves by conventional way
- lets see how to make spring to do it
#### Iteration - 2
- remember the IoC container in JVM is of type ApplicationContext

```java  
// File Not changed
public class Dev {
	public void build(){
		System.out.println("working on Awsome Project");
	}
}
```

```java
@SpringBootApplication
public class Myapplication {
	public static void main (String args[]) {
		// creating the object of IoC container
		ApplicationContext context = SpringApplication.run(MyApplication.class, args);

		Dev dev1 = context.getBean(Dev.class);
		dev1.build();
	}
}
/* output
Error : No qualifying Bean
/*
```

-> see we first created the object of IoC container 
-> and used that container to create the object of dev using `.getBean(Dev.class)`
- But right now it will give error as we haven't define that 

- to resolve this error use @Component on top of Dev class

```java  
@Component
public class Dev {
	public void build(){
		System.out.println("working on Awsome Project");
	}
}
```

> @Component - tells spring that its a bean or class supposed to be handled by it

### Iteration - 3
- Giving machines to the devs is an obvious choice so lets create a class `Laptop`

```java
public class Laptop {
	public void compile() {
		System.out.println("Compiling with 404 bugs.");
	}
}
```

```java
@Component
public class Dev {
	private Laptop laptop = new Laptop();
	public void build(){
		laptop.compile();
		System.out.println("working on Awsome Project");
	}
}
```

```java
// not changed
main(){...}
/*
Compiling with 404 bugs.
Working on Awsome Project.
*/
```

### Iteration - 4 (Field Injection)
- we want spring to create an object of laptop itself and connect it in the dev class


```java
@Component
public class Laptop {
	public void compile() {
		System.out.println("Compiling with 404 bugs.");
	}
}
```

```java
@Component
public class Dev {
	@Autowire
	private Laptop laptop;
	
	public void build(){
		laptop.compile();
		System.out.println("working on Awsome Project");
	}
}
```

```java
// not changed
main() {...}
/*
Compiling with 404 bugs.
Working on Awsome Project.
*/
```

1. you needs to add `@Component` in begining of `Laptop` class
2. and you add `@Autowire` to connect them behind the scenes
- otherwise you had to create a new object of IoC and then add that to laptop some what like laptop = context.getBean(Laptop.class) something

### Iteration - 5 (constructor Injection)

```java
@Component
public class Laptop {
	public void compile() {
		System.out.println("Compiling with 404 bugs.");
	}
}
```

```java
@Component
public class Dev {
	
	private Laptop laptop;

	// @Autowired // optional here - only for constructor injection
	public Dev(Laptop laptop) {
		this.laptop = laptop;
	}
	
	public void build(){
		laptop.compile();
		System.out.println("working on Awsome Project");
	}
}
```

```java
// not changed
main() {...}
/*
Compiling with 404 bugs.
Working on Awsome Project.
*/
```
> @Autowired in the case of constructor injection is optional

### Iteration - 5 (setter Injection)

```java
@Component
public class Laptop {
	public void compile() {
		System.out.println("Compiling with 404 bugs.");
	}
}
```

```java
@Component
public class Dev {
	
	private Laptop laptop;

	@Autowired
	public void setLaptop(Laptop laptop){
		this.laptop = laptop;
	}
	
	public void build(){
		laptop.compile();
		System.out.println("working on Awsome Project");
	}
}
```

```java
// not changed
main() {...}
/*
Compiling with 404 bugs.
Working on Awsome Project.
*/
```

#### @Autowired resolution
- till now there was only one `Laptop` type i.e. laptop class.
- So @autowired just needed to search `Laptop` type of bean in the Ioc and all set.