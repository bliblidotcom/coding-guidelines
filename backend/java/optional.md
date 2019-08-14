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

## Operation to Nullable Value

```java
// If style

String nameUpper = customer.getName();
if (nameUpper != null) {
  nameUpper = nameUpper.toUpperCase();
} else {
  nameUpper = "";
}
```

```java
// Optional style

String nameUpper = Optional.ofNullable(customer.getName())
    .map(String::toUpperCase)
    .orElse("");
```

## Nested If Checking

```java
// If style

String country = "Indonesia";
if (customer.getAddress() != null) {
  if (customer.getAddress().getCountry() != null) {
    country = customer.getAddress().getCountry();
  }
}
```

```java
// Optional style

String country = Optional.ofNullable(customer.getAddress())
    .map(Address::getCountry)
    .orElse("Indonesia");
```

## Check and Throw Exception

```java
// If style

String name = customer.getName();
if (name == null) {
  throw new IllegalArgumentException("Name is null");
}
```

```java
// Optional style

String name = Optional.ofNullable(customer.getName())
    .orElseThrow(() -> new IllegalArgumentException("Name is null"));
```

## If Check and Do Something

```java
// If style

if (customer.getAddress() != null) {
  if (customer.getAddress().getCountry() != null) {
    // do something
    System.out.println(customer.getAddress().getCountry());
  }
}
```

```java
// Optional style

Optional.ofNullable(customer.getAddress())
    .map(Address::getCountry)
    .ifPresent(System.out::println);
```

## Nested Object

```java
// If style

Long cashBalance = 0L;
if (customer.getWallet() != null) {
  if (customer.getWallet().getBalance() != null) {
    cashBalance = customer.getWallet().getBalance().getCashBalance();
  }
}
```

```java
// Optional style

Long cashBalance = Optional.ofNullable(customer.getWallet())
    .map(Wallet::getBalance)
    .map(WalletBalance::getCashBalance)
    .orElse(0L);
```

## If Filter

```java
// If style

Long bonus = 0L;
if (Type.PREMIUM.equals(customer.getType())) {
  if (customer.getWallet() != null) {
    if (customer.getWallet().getBalance() != null) {
      bonus = customer.getWallet().getBalance().getCashBalance() * 10 / 100;
    }
  }
}
```

```java
// Optional style

Long bonus = Optional.of(customer)
    .filter(value -> Type.PREMIUM.equals(value.getType()))
    .map(Customer::getWallet)
    .map(Wallet::getBalance)
    .map(balance -> balance.getCashBalance() * 10 / 100)
    .orElse(0L);
```
