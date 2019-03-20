Elepy is awesome, but more importantly, easy! This guide shows how easy Elepy can be to get started with.

### Step Zero: Basic Terminology
Elepy knows the concept of RestModels. These are in essence a regular POJO(or POKO, for Kotlin users) annotated the [@RestModel](/docs/annotations#restmodel) annotation. These are the domain objects of your CMS.

And that leads us to the next term, CMS. CMS means (Headless) Content Management System in the Elepy context. For more details of a Headless CMS is, [click here](https://en.wikipedia.org/wiki/Headless_content_management_system).

### Step One: Install Elepy with Maven
The latest versions of elepy can be found at: https://elepy.com/docs/download
#### Elepy Core
The core module of Elepy, can be installed with maven. This includes the API generation and the core functionality of Elepy. For the CMS you must include the `elepy-admin` dependency.
``` xml
<dependency>
    <groupId>com.elepy</groupId>
    <artifactId>elepy-core</artifactId>
    <version>LATEST VERSION</version>
</dependency>
```

#### Elepy Admin
This is the admin module of Elepy. It contains the powerful content management system.
``` xml
<dependency>
    <groupId>com.elepy</groupId>
    <artifactId>elepy-admin</artifactId>
    <version>LATEST VERSION</version>
</dependency>
```

### Step Two: Create and annotate your POJO's
Create your Rest Model. The only mandatory annotation is `@RestModel`. This annotation is where you describe the name and `/slug` of your model. 
``` java
@RestModel(name = "Products", slug = "/products")
public class Product {

    @Identifier
    private String productId;
    
    @Text(value = TextType.TEXTAREA, maximumLength = 100)
    private String shortDescription;
    
    @Text(TextType.HTML)//WYSIWYG editor
    private String htmlDescription;

    @PrettyName("Product Name")
    @Required
    @Unique
    private String name;

    @Number(minimum = 0)
    private BigDecimal price;

    @Number(minimum = 0)
    private int stockLeft;

    //Getters and Setters. I like to use Lombok to automate this :D
}
```
### Step Three: Configure Elepy

In the `main()` of your application is where you usually configure and start Elepy. The most important part of the configuration is the Database setup. For MongDB you need to supply Elepy with a reference to your `DB` object. This can be done with the `connectDB(DB)` method or with the `attachSingleton(Class, singleton)` method. After connecting your Database, you should start adding your RestModels with the `addModel(Class)`, `addModels(Class...)` and `addModelPackage(String)` methods. Once you do that, you might be interested in adding Extensions. The ElepyAdminPanel Extension is how you can add the Content Management System.

As you also may have noticed, the `Elepy` configuration object is of fluent nature.
``` java
public static void main(String[] args) {
    DB database = mongo.getDB("product-database");

    new Elepy()
        .attachSingleton(DB.class, database)
        .withIPAddress("localhost")
        .onPort(7777)
        .addModel(Product.class)
        //Add an Elepy extension
        //The AdminPanel/CMS is a great start :D
        .addExtension(new ElepyAdminPanel())
        .start();

}
```

### Step Four: Explore!

Once you run Elepy you get access to five basic routes:
```
GET       /products       //Find all products
POST      /products       //Create a new product
PUT       /products/:id   //Update a whole product
PATCH     /products/:id   //Update just parts of a product
DELETE    /products/:id   //Delete a product
```

You will also be able to access the admin panel at http://localhost:7777/admin.

```
username: admin
password: admin
```