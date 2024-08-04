	* take the same example 
* we have class dev that needs an object of type `Computer` 
* `Computer` is an interface and there are 2 implementation `Desktop` and `Laptop`
```java
public interface Computer {
	void compile();
}
```

```java
public class Laptop implements Computer{
	public Laptop(){
		System.out.println("Laptop Constructor");
	}
	@Override
	public void compile() {
		System.out.println("Compiling with 404 bugs.");
	}
}
```

```java
public class Desktop implements Computer{
	public Desktop(){
		System.out.println("Desktop constructor");
	}
	@Override
	public void compile() {
		System.out.println("Compiling with 404 bugs but faster.");
	}
}
```

```java
public class Dev {
	
	private Computer comp;

	public int getComp() {
		return comp;
	}
	public void setComp(Cmoputer comp) {
		this.comp = comp;
	}
	public void build(){
		comp.compile();
		System.out.println("working on Awsome Project");
	}
}
```

```java
public class Myapplication {
	psvm (String args[]) {
		// creating the object of IoC container
		ApplicationContext context = ClassPathXmlApplicationContext("spring.xml"); 

		Dev dev1 = context.getBean("dev");
		dev1.build();
	}
}
/* output
Error : No qualifying Bean
/*
```

```java

<beans>
	<bean id="dev" class="org.rohit.Dev" autowire="byName/byType/..."></bean>

	<bean id="comp" class="org.rohit.Desktop">
</beans>
```

- byType - searches for a bean whose type matches the type of the member variable 
- byName - searches the bean whose id matches the member variable name