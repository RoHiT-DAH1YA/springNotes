# Inversion of control - IoC
##### Principle ->
>  spring says you take care of business logic and I will take care of object creation, handling and destruction.

- We are giving the control to spring - inversing the control
- implementation of Ioc is Dependency Injection
- Ioc is principle and DI is implementation

## Dependency Injection
there are three type of DI
1. constructor
2. setter 
3. field - not advised
go to Notes - 5 for more info

## IoC container
- it is the container in the JVM where spring creates and stores all those objects.
> remember that the IoC container that spring creates inside JVM is of type `ApplicationContext` which is an interface
