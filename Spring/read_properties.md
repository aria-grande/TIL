# Configuration properties in Spring
Read [this](https://www.javadevjournal.com/spring-boot/configuration-properties-in-spring-boot/)
https://www.concretepage.com/spring-5/spring-value#Technologies

## @Value
This annotation can be used for injecting values into fields in Spring-managed beans. Read [more](https://www.baeldung.com/spring-value-annotation)
```java
@Value("${serviceName}")
private String serviceName;   // value from configuration will be assigned
```

It does not work with static variable
```java
@Value("${serviceName}")
private static String serviceName;   // null
```


