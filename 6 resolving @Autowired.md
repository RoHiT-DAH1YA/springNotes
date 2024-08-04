- in [[5 spring first app and DI - types]] we saw how construction, setter and field injection works. But how do spring knows which class/interface we are refering to?
- in prev example we had `Dev` and `Laptop`. lets add an interface `computer` to it. and let two class implement computer and lets request a bean of type computer.

```java
public interface Computer {
	void compile();
}
```

```java
@Component
public class Laptop implements Computer{
	@Override
	public void compile() {
		System.out.println("Compiling with 404 bugs.");
	}
}
```

```java
@Component
public class Desktop implements Computer{
	@Override
	public void compile() {
		System.out.println("Compiling with 404 bugs but faster.");
	}
}
```

```java
@Component
public class Dev {
	@Autowired
	private Computer comp;
	
	public void build(){
		comp.compile();
		System.out.println("working on Awsome Project");
	}
}
```

```java
@SpringBootApplication
public class Myapplication {
	psvm (String args[]) {
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

- this will give error as spring will not be able to resolve which implementation of Computer is to be used? Desktop or Laptop?

#### Method - 1 use @Primary
- use @Primary annotation on top of the class that is preferred in case of confusion

```java
@Component
@Primary  // <<<------------
public class Laptop implements Computer{
	@Override
	public void compile() {
		System.out.println("Compiling with 404 bugs.");
	}
}
```

```java
@Component
public class Dev {
	@Autowired
	private Computer comp;
	
	public void build(){
		comp.compile();
		System.out.println("working on Awsome Project");
	}
}
```

> please don't mention on @Primary on top of more than one class. it just fails its purpose

#### Method - 2 @Qualifier
- adding @Qualifier("bean_name") on top of the object we want to inject object into will create the bean of the given name.

```java
@Component
public class Dev {
	@Autowired
	@Qualifier("lapotp")  // yes first letter is small intentionally
	private Computer comp;
	
	public void build(){
		comp.compile();
		System.out.println("working on Awsome Project");
	}
}
```