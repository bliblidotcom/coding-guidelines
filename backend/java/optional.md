# Java Optional

Did you know that in Java 8, there is class java.util.Optional. Optional is a container class for wrapping nullable value. With Optional, 

- we can operate to wrapped value without being scared about NullPointerException.
- we don't need to check null using IF anymore.
- we can transform wrapped value to another value easily.
- the logic flow is more easy to read.

So, start from now, please abused java.util.Optional class. I give you some examples how to use java.util.Optional class.

## Null Check

```java
// If style

String name = customer.getName();
if (name == null) {
  name = "";
}
```

```java
// Optional style

String name = Optional.ofNullable(customer.getName())
    .orElse("");
```

## If Logic

```java
// If style

Customer user = findCustomerById("id");
if (user == null) {
  user = createNewUser("id");
}
```

```java
// Optional style

Customer user = Optional.ofNullable(findCustomerById("id"))
    .orElseGet(() -> createNewUser("id"));
```
