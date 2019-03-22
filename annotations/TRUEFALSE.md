# @TrueFalse
This annotation signifies that a field is a boolean. It comes with two optional properties, `trueValue` and `falseValue`. These values describe what true and false mean in the context of your application.

Example usage:
```java
@TrueFalse(trueValue = "This product can be deleted", falseValue = "This product can't be deleted")
private boolean deletable;
```
