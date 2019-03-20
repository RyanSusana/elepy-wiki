# Handlers
## Table of Contents
* [What Are Handlers?](#what-are-handlers-)
* [Changing Handlers](#changing-handlers)
* [Available Handlers](#available-handlers)

## What Are Handlers?
Elepy knows the concept of Handlers. Handlers are how Elepy takes in an HTTP Request and produces an action and an HTTP Response.

Elepy has 5 handlers: CreateHandler, FindOneHandler, FindManyHandler, UpdateHandler and DeleteHandler. All* handlers have one method that they need to implement. This method has 4 params:  an HTTP Context, a Model Description, a CRUD Object and an ObjectMapper.

*Update has two separate, but similar methods for PUT and PATCH requests.

Let's take a look at a DeleteHandler:
```java
public class UserDelete implements DeleteHandler<User> {

    @Override
    public void handleDelete(HttpContext context, Crud<User> crud, ModelDescription<User> modelDescription, ObjectMapper objectMapper) {
        Object objectId = context.modelId();

        crud.getById(objectId).orElseThrow(() -> new ElepyException(String.format("No %s found", modelDescription.getName()), 404));

        crud.delete(objectId);

        context.response().status(200);
        context.response().result("OK");
    }
}
```
What's happening:
1. It get's the `modelId` from the HTTP Request
2. Looks for the object with that ID
    * If that object doesn't exist, it throws an ElepyException, which later gets transformed into a nice response message. Feel free to throw exceptions anywhere, Elepy has a global Exception handler.
3. Elepy deletes the object with that ID via the CRUD interface of that specific model
4. The status and result of the HTTP Response are set

## Changing Handlers
When configuring RestModels you have access to the five annotations: @Create, @FindOne, @FindMany, @Update and @Delete.

To change a handler for any of those functionalities, you change the handler property in the annotation and point to your new Handler class.

In the UserDelete case it would be:
```java
@RestModel(name="Users", slug="/users")
@Delete(handler = UserDelete.class)
public class User {
    private String id, username, password;

    //Getters and Setters
}
```
Elepy then tries to instantiate and inject your UserDelete class and then it swaps out the default handler to the new, custom one.

## Available Handlers
Here is a list of out-of-the-box handlers that you can extend and play around with
Create:
* DefaultCreate<T>: The default implementation
* SimpleCreate<T>: A simple way to create objects

FindOne:
* DefaultFindOne<T>: The default implementation
* MappedFindOne<T, R>: Use this class to map the result of a RestModel to another type.

FindMany:
* DefaultFindMany<T>: The default implementation
* MappedFindMany<T, R>: Use this class to map the results of a RestModel to another type.

FindOne & FindMany:
* MappedFind<T, R>: This is a combination of MappedFindMany and MappedFindMany. Use this class if you want to always map from a RestModel to another type, regardless if you are finding one or many.

Update:
* DefaultUpdate<T>:  The default implementation
* SimpleUpdate<T>: A simple way to update objects

Delete:
* DefaultDelete<T>: The default implementation
* SimpleDelete<T>: A simple way to delete objects


