# @Text
This annotation signifies that the value of a field is a String value. It comes with three optional properties, minimumLength, maximumLength and value(TextType). The minimumLength and maximumLength properties get asserted by the `ObjectEvaluator`. The value(or TextType) changes the way the field is presented in the CMS.

```java
@Text(minimumLength = 50, maximumLength = 350, value = TextType.MARKDOWN)
private String productDescription;
```
