# Annotations
This is a guide to the many available annotations of Elepy.

# Table of Annotations
* [Field Annotations](#field-annotations)
    * [@Identifier](#identifier)
    * [@Unique](#unique)
    * [@Required](#required)
    * [@Searchable](#searchable)
    * [@Uneditable](#uneditable)
    * [@PrettyName](#prettyname)
    * [@TrueFalse](#truefalse)
    * [@Number](#number)
    * [@Text](#text)
    * [@DateTime](#datetime)
    * [@Importance](#importance)
    * [@Hidden](#hidden)
* [RestModel Annotations](#restmodel-annotations)
    * [@RestModel](#restmodel)
    * [@Create](#create)
    * [@Find](#find)
    * [@Update](#update)
    * [@Delete](#delete)
    * [@Dao](#dao)
    * [@DaoProvider](#daoprovider)
    * [@IdProvider](#idprovider)


# Annotations

## Field Annotations
Field annotations can be marked on any field in your RestModel. 

### Identifier
This annotation signifies that a field is the identifying field of a RestModel. A RestModel can only have one `@Identifier`. Furthermore, the supported Identifier types are String, Long or Integer. 
If no @Identifier is used, Elepy will look for a field with the name 'id', or annotated with `@JsonProperty("id")`

### Unique
This annotation signifies that a field is unique. It uses `IntegrityEvaluator` and the `Crud` method `#searchInField(Field, String)` to test the uniqueness of a field.

### Required
This annotation signifies that a field is required in all circumstances. If no value is provided for this field in an update or create, an error should be thrown and displayed in a Restful response. This gets handled by the `ObjectEvaluator`

### Searchable
This annotation signifies that a field is searchable, and should be considered implemented in the `Crud` interface. When you mark a field as searchable, you say that a field should be able to be queried for.

By default, all @Searchable fields can be queried for by specifying a 'q' query parameter in a GET request.

### Uneditable
This annotation signifies that a field can only be set once. If you try to update the field, an error should be thrown. This error gets thrown by the `ObjectUpdateEvaluator` and gets shown in the Restful Response.

### PrettyName
This annotation gives a field a pretty name, `@PrettyName("a nice name")`. Pretty names get shown in error messages and on the CMS.

### TrueFalse
This annotation signifies that a field is a boolean. It comes with two optional properties, `trueValue` and `falseValue`. These values describe what true and false mean in the context of your application.

Example usage:
```java
@TrueFalse(trueValue = "This product can be deleted", falseValue = "This product can't be deleted")
private boolean deletable;
```
### Number
This annotation signifies that a field is a number. It comes with three optional properties, minimum, maximum and value(NumberType). The minimum and maximum properties get asserted by the `ObjectEvaluator'

Example usage
```java
@Number(minimum = 0, maximum = 1000, value = NumberType.DECIMAL)
private BigDecimal price;
```
### Text
This annotation signifies that the value of a field is a String value. It comes with three optional properties, minimumLength, maximumLength and value(TextType). The minimumLength and maximumLength properties get asserted by the `ObjectEvaluator`. The value(or TextType) changes the way the field is presented in the CMS.

```java
@Text(minimumLength = 50, maximumLength = 350, value = TextType.MARKDOWN)
private String productDescription;
```
### DateTime
This annotation signifies that the value of a field is a Date value. It comes with three optional properties, includeTime, minimumDate and maximumDate. 


_More about @DateTime coming soon..._

### Importance
This annotation defines the order of a field in the CMS. The higher the importance, the higher it's listed in the CMS.

Negative valued @Importance fields(like `@Importance(-5)`) don't get displayed in the table view of your data.

### Hidden
This annotation signifies that a field should be hidden from the CMS.

 
## RestModel Annotations
### RestModel
This annotation is the only one you __need__ to mark your POJO as valid Elepy model. If you don't add this annotation, Elepy will not recognize your model. The __required__ properties are `slug` and `name`. The optional properties are `description`, `defaultSortField` and `defaultSortDirection`.

```
name: What do you call the model? e.g 'Products'
slug: What is the URI of the model? e.g '/products'

description: A brief description of the model
defaultSortField: What field do you sort on by default?
defaultSortDirection: How do you sort the model by default? ASCENDING or DESCENDING?
```
### Create
_coming soon..._

### Find
_coming soon..._ 

### Update
_coming soon..._

### Delete
_coming soon..._
