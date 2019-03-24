# Download

## Elepy 2
Elepy 2 is the latest version of Elepy, [and is currently in BETA](https://github.com/RyanSusana/elepy/projects/2). The latest version can be downloaded with Maven:

```xml
<dependency>
    <groupId>com.elepy</groupId>
    <artifactId>elepy-basic</artifactId>
    <version>2.0.0-beta-4</version>
</dependency>
```
## Elepy 1
Elepy 1.8.0 is the most stable non-beta release of Elepy. To use it, you must include these two dependencies.
### Elepy Core
The core module of Elepy, can be installed with maven. This includes the API generation and the core functionality of Elepy. For the CMS you must include the `elepy-admin` dependency.
``` xml
<dependency>
    <groupId>com.elepy</groupId>
    <artifactId>elepy-core</artifactId>
    <version>1.8.0</version>
</dependency>
```

### Elepy Admin
This is the admin module of Elepy. It contains the powerful content management system.
``` xml
<dependency>
    <groupId>com.elepy</groupId>
    <artifactId>elepy-admin</artifactId>
    <version>1.8.0</version>
</dependency>
```