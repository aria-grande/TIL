# Mockito

## @Mock vs @InjectMocks
- @Mock is mocking a class
- @InjectMocks is mocking a class and inject mocked dependencies
Let's look at the example below.
```java
@RunWith(PowerMockRunner.class)
class User {
  private Address address;
  private String name;
}
```
### 1. @Mock
```java
// Test
@RunWith(PowerMockRunner.class)
class UserTest {
  @Mock
  private User mockUser;
}
```
In this case, `Address` of `mockUser` will be `null`.

### 2. @InjectMocks
```java
@RunWith(PowerMockRunner.class)
class UserTest {
  @InjectMocks
  private User mockUser;
}
```
In this case, still `Address` of `mockUser` will be `null`, because `Address` is not mocked.


```java
@RunWith(PowerMockRunner.class)
class UserTest {
  @InjectMocks
  private User mockUser;
  
  @Mock
  private Address mockAddress;
}
```
In this case, `mockUser` will have `mockAddress` inside of it.

Ref: https://howtodoinjava.com/mockito/mockito-mock-injectmocks/
