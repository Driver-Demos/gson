
## Files
- **[Intercept.java](interceptors/Intercept.java.driver.md)**: The `Intercept.java` file defines an annotation used to specify interceptors for class instances after deserialization by Gson, allowing for post-processing such as validation.
- **[InterceptorFactory.java](interceptors/InterceptorFactory.java.driver.md)**: The `InterceptorFactory.java` file in the `gson` codebase provides a type adapter factory that implements the `@Intercept` annotation to allow post-deserialization processing of JSON objects.
- **[JsonPostDeserializer.java](interceptors/JsonPostDeserializer.java.driver.md)**: The `JsonPostDeserializer.java` file defines an interface for inspecting or modifying an object after it has been deserialized by Gson.
