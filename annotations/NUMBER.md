# @Number
This annotation signifies that a field is a number. It comes with three optional properties, minimum, maximum and value(NumberType). The minimum and maximum properties get asserted by the `ObjectEvaluator'

Example usage
```java
@Number(minimum = 0, maximum = 1000, value = NumberType.DECIMAL)
private BigDecimal price;
```