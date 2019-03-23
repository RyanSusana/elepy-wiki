# @Evaluators
An evaluator, or `ObjectEvaluator`, is a way of checking if an RestModel item is valid. Whenever you create/update a RestModel item, it gets run through a list of ObjectEvaluators associated with that particular RestModel. The evaluator evaluates an item by not throwing an exception whenever an item gets through it with the `#evaluate(Object, Class)`. By default, the list contains one evaluator, Elepy's default ObjectEvaluator. This default ObjectEvaluator handles things like the `@Number`, `@Text`, `@Required` and `@DateTime`annotations. It makes sure an object doesn't violate the constraints set by those annotations.

__But__, there are ways you can create and assign your own Evaluators. Let's say you want to evaluate a Person RestModel that has an email property, and you want to validate that e-mail address.

You can use the `@Evaluators` to point to a PersonEvaluator(and maybe more, like a generic NameEvaluator) like so:

```java
@RestModel(name = "Persons", slug = "/persons")
@Evaluators(PersonEvaluator.class)
public class Person {
    private String id, firstName, lastName, email;

    //Getters and Setters. 
}
```

```java
public class PersonEvaluator implements ObjectEvaluator<Person> {

    @Inject
    private EmailValidator emailValidator;

    public void evaluate(Person person, Class<Person> cls) throws Exception {
        boolean isValid = emailValidator.isValid(person.getEmail());

        if (!isValid) {
            throw new ElepyException("Email is not valid", 400);
        }
    }
}
```
