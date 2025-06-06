# Purpose
The `JsonAdapterAnnotationOnClassesTest` Java file is a comprehensive suite of functional tests designed to validate the behavior of the `@JsonAdapter` annotation in the Gson library. This file is part of the `com.google.gson.functional` package and leverages the JUnit testing framework to ensure that custom serialization and deserialization logic, as specified by the `@JsonAdapter` annotation, is correctly applied to various classes. The tests cover a wide range of scenarios, including the invocation of custom `TypeAdapter`, `TypeAdapterFactory`, `JsonSerializer`, and `JsonDeserializer` implementations, as well as the interaction between registered adapters and those specified via annotations. The file also explores edge cases such as incorrect adapter types, null-safe handling, and the use of `InstanceCreator` for adapter instantiation.

The primary technical components of this file include the use of the Gson library's `Gson`, `GsonBuilder`, and various adapter interfaces to manipulate JSON serialization and deserialization processes. The tests verify that the `@JsonAdapter` annotation can override default behavior, handle null values gracefully, and correctly delegate to registered adapters when necessary. Additionally, the file tests the behavior of adapter factories that return null, ensuring that Gson falls back to other available factories. The file also includes tests for complex scenarios involving multiple instances of the same factory class and the use of `Gson#getDelegateAdapter` to ensure proper delegation and avoid infinite recursion. Overall, this file serves as a robust validation tool for developers using Gson's `@JsonAdapter` feature to customize JSON processing in their applications.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.common.base.Splitter`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.InstanceCreator`
- `com.google.gson.JsonDeserializationContext`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSerializationContext`
- `com.google.gson.JsonSerializer`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.annotations.JsonAdapter`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.ParameterizedType`
- `java.lang.reflect.Type`
- `java.util.List`
- `java.util.Locale`
- `org.junit.Test`


# Classes

---
### JsonAdapterAnnotationOnClassesTest<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonAdapterAnnotationOnClassesTest` class is a comprehensive suite of functional tests designed to validate the behavior of the `@JsonAdapter` annotation in the Gson library. It includes various test cases to ensure that custom serialization and deserialization logic, as specified by `@JsonAdapter`, is correctly applied to classes, fields, and enums. The tests cover scenarios such as overriding adapters, handling null values, and using different types of adapters like `TypeAdapter`, `TypeAdapterFactory`, `JsonSerializer`, and `JsonDeserializer`. Additionally, the class tests edge cases involving factory delegation and adapter creation using `InstanceCreator` and JDK Unsafe.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonAdapterInvoked`](#JsonAdapterAnnotationOnClassesTesttestJsonAdapterInvoked)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonAdapterFactoryInvoked`](#JsonAdapterAnnotationOnClassesTesttestJsonAdapterFactoryInvoked)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testRegisteredAdapterOverridesJsonAdapter`](#JsonAdapterAnnotationOnClassesTesttestRegisteredAdapterOverridesJsonAdapter)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testRegisteredSerializerOverridesJsonAdapter`](#JsonAdapterAnnotationOnClassesTesttestRegisteredSerializerOverridesJsonAdapter)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testRegisteredDeserializerOverridesJsonAdapter`](#JsonAdapterAnnotationOnClassesTesttestRegisteredDeserializerOverridesJsonAdapter)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testIncorrectTypeAdapterFails`](#JsonAdapterAnnotationOnClassesTesttestIncorrectTypeAdapterFails)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testSuperclassTypeAdapterNotInvoked`](#JsonAdapterAnnotationOnClassesTesttestSuperclassTypeAdapterNotInvoked)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testNullSafeObject`](#JsonAdapterAnnotationOnClassesTesttestNullSafeObject)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testFactoryReturningNull`](#JsonAdapterAnnotationOnClassesTesttestFactoryReturningNull)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testIncorrectJsonAdapterType`](#JsonAdapterAnnotationOnClassesTesttestIncorrectJsonAdapterType)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegatingAdapterFactory`](#JsonAdapterAnnotationOnClassesTesttestDelegatingAdapterFactory)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegatingAdapterFactory_Delayed`](#JsonAdapterAnnotationOnClassesTesttestDelegatingAdapterFactory_Delayed)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryClass`](#JsonAdapterAnnotationOnClassesTesttestDelegating_SameFactoryClass)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryInstance`](#JsonAdapterAnnotationOnClassesTesttestDelegating_SameFactoryInstance)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryClass_OnClassAndField`](#JsonAdapterAnnotationOnClassesTesttestDelegating_SameFactoryClass_OnClassAndField)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryInstance_OnClassAndField`](#JsonAdapterAnnotationOnClassesTesttestDelegating_SameFactoryInstance_OnClassAndField)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonSerializer`](#JsonAdapterAnnotationOnClassesTesttestJsonSerializer)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonDeserializer`](#JsonAdapterAnnotationOnClassesTesttestJsonDeserializer)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testAdapterCreatedByInstanceCreator`](#JsonAdapterAnnotationOnClassesTesttestAdapterCreatedByInstanceCreator)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testAdapterCreatedByJdkUnsafe`](#JsonAdapterAnnotationOnClassesTesttestAdapterCreatedByJdkUnsafe)

**Methods**

---
#### JsonAdapterAnnotationOnClassesTest\.testJsonAdapterInvoked<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonAdapterInvoked}} -->
The `testJsonAdapterInvoked` method tests the functionality of custom JSON adapters in the Gson library by serializing and deserializing objects and asserting the expected JSON output and object state.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created to handle JSON serialization and deserialization.
    - An object of class `A` is serialized to JSON, and the result is asserted to be equal to the string "jsonAdapter".
    - A `User` object is serialized to JSON, and the result is asserted to be equal to a JSON object with a combined name field.
    - A JSON string representing a `User` is deserialized, and the resulting object's fields are asserted to match the expected values.
    - An enum `Foo.BAR` is serialized to JSON, and the result is asserted to be equal to the string "bar".
    - A JSON string representing a `Foo` enum is deserialized, and the resulting enum value is asserted to be `Foo.BAZ`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of JSON serialization and deserialization using custom adapters.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testJsonAdapterFactoryInvoked<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonAdapterFactoryInvoked}} -->
The method `testJsonAdapterFactoryInvoked` tests the invocation of a custom `JsonAdapterFactory` for serialization and deserialization of a class `C` using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Gson` instance is created.
    - An object of class `C` is serialized to JSON using `gson.toJson`, and the result is asserted to be equal to the string "jsonAdapterFactory".
    - A JSON string "bar" is deserialized into an object of class `C` using `gson.fromJson`, and the `value` field of the resulting object is asserted to be equal to "jsonAdapterFactory".
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonAdapterFactory`.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testRegisteredAdapterOverridesJsonAdapter<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testRegisteredAdapterOverridesJsonAdapter}} -->
The method `testRegisteredAdapterOverridesJsonAdapter` tests that a registered `TypeAdapter` for class `A` overrides the `JsonAdapter` annotation when serializing an object of class `A` to JSON.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapter` for class `A` is created with overridden `write` and `read` methods to handle JSON serialization and deserialization.
    - A `Gson` instance is created using `GsonBuilder`, registering the `TypeAdapter` for class `A`.
    - An object of class `A` is serialized to JSON using the `Gson` instance.
    - The resulting JSON string is asserted to be equal to the string "registeredAdapter".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the `TypeAdapter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testRegisteredSerializerOverridesJsonAdapter<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testRegisteredSerializerOverridesJsonAdapter}} -->
This method tests that a registered JsonSerializer for class A overrides the default JsonAdapter for serialization, but the default JsonAdapter is used for deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JsonSerializer for class A is created that always serializes objects to the string 'registeredSerializer'.
    - A Gson instance is created with this serializer registered for class A.
    - An object of class A is serialized to JSON using the Gson instance, and it is asserted that the output is '"registeredSerializer"'.
    - An object of class A is deserialized from the string 'abcd' using the Gson instance, and it is asserted that the deserialized object's value is 'jsonAdapter'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testRegisteredDeserializerOverridesJsonAdapter<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testRegisteredDeserializerOverridesJsonAdapter}} -->
The method tests that a registered deserializer for class A overrides the default JsonAdapter deserializer, while the JsonAdapter serializer remains in use.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JsonDeserializer for class A is created that returns a new instance of A with the value 'registeredDeserializer'.
    - A Gson instance is created with the deserializer registered for class A.
    - An instance of A is serialized to JSON using the Gson instance, and it is asserted that the output is '"jsonAdapter"', indicating the JsonAdapter serializer is used.
    - A JSON string 'abcd' is deserialized into an instance of A using the Gson instance, and it is asserted that the value of the resulting object is 'registeredDeserializer', indicating the registered deserializer is used.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson deserialization and serialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testIncorrectTypeAdapterFails<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testIncorrectTypeAdapterFails}} -->
The method `testIncorrectTypeAdapterFails` tests that serializing an object with an incorrect type adapter using Gson throws a `ClassCastException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Gson` instance is created.
    - An instance of `ClassWithIncorrectJsonAdapter` is created with the value "bar".
    - The `assertThrows` method is used to verify that a `ClassCastException` is thrown when attempting to serialize the object using `gson.toJson(obj)`.
- **Output**:
    - The method does not return any value; it asserts that a `ClassCastException` is thrown during the execution of the test.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testSuperclassTypeAdapterNotInvoked<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testSuperclassTypeAdapterNotInvoked}} -->
The method `testSuperclassTypeAdapterNotInvoked` verifies that the superclass type adapter is not invoked when serializing an instance of class `B` using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new Gson instance.
    - Serialize an instance of class `B` with the value "bar" to JSON using the Gson instance.
    - Assert that the resulting JSON string does not contain the string "jsonAdapter".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testNullSafeObject<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testNullSafeObject}} -->
The `testNullSafeObject` method tests the serialization and deserialization behavior of the `NullableClass` using Gson, ensuring that null values are handled correctly.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - The method deserializes the JSON string "null" into a `NullableClass` object and asserts that the result is null.
    - It then deserializes the JSON string "\"ignored\"" into a `NullableClass` object and asserts that the result is not null.
    - The method serializes a null `NullableClass` object to JSON and asserts that the result is the string "null".
    - Finally, it serializes a new instance of `NullableClass` to JSON and asserts that the result is the string "\"nullable\"".
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior of Gson with `NullableClass`.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testFactoryReturningNull<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testFactoryReturningNull}} -->
The `testFactoryReturningNull` method tests the behavior of Gson when a `TypeAdapterFactory` returns `null`, indicating it cannot handle a type, and verifies that Gson falls back to a reflection-based adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created.
    - The method asserts that deserializing the string "null" to `WithNullReturningFactory.class` results in `null`.
    - It asserts that serializing `null` with `WithNullReturningFactory.class` results in the string "null".
    - A `TypeToken` for `WithNullReturningFactory<String>` is created and used to deserialize the string "a", asserting the result is "custom-read:a".
    - It asserts that deserializing "null" with the `stringTypeArg` results in `null`.
    - It asserts that serializing a `WithNullReturningFactory` with value "b" results in "custom-write:b".
    - It asserts that serializing `null` with the `stringTypeArg` results in "null".
    - A `TypeToken` for `WithNullReturningFactory<Integer>` is created and used to deserialize a JSON object with `t` set to 1, asserting the result is 1.
    - It asserts that serializing a `WithNullReturningFactory` with value 2 results in a JSON object with `t` set to 2.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the expected behavior of Gson's serialization and deserialization processes with a custom `TypeAdapterFactory`.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testIncorrectJsonAdapterType<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testIncorrectJsonAdapterType}} -->
The method `testIncorrectJsonAdapterType` tests that an `IllegalArgumentException` is thrown when attempting to serialize an object with an invalid `@JsonAdapter` type using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Gson` instance is created.
    - An instance of `WithInvalidAdapterClass` is created.
    - The method `assertThrows` is used to verify that an `IllegalArgumentException` is thrown when `gson.toJson(obj)` is called.
    - The exception message is asserted to be equal to a specific error message indicating the invalid `@JsonAdapter` type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testDelegatingAdapterFactory<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegatingAdapterFactory}} -->
The `testDelegatingAdapterFactory` method tests the serialization and deserialization of a `WithDelegatingFactory` object using Gson with a custom `TypeAdapterFactory` that delegates to a default adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `WithDelegatingFactory<String>` object is deserialized from a JSON string using Gson and the `WithDelegatingFactory` class, and its field `f` is asserted to be equal to 'de'.
    - The same deserialization is performed using a `TypeToken` for `WithDelegatingFactory<String>`, and the field `f` is again asserted to be 'de'.
    - A `WithDelegatingFactory<String>` object is created with the value 'se', serialized to JSON using Gson, and the resulting JSON string is asserted to be '{"custom":{"f":"se"}}'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testDelegatingAdapterFactory\_Delayed<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegatingAdapterFactory_Delayed}} -->
The method `testDelegatingAdapterFactory_Delayed` tests the serialization and deserialization of a `WithDelayedDelegatingFactory` object using a custom `TypeAdapterFactory` with delayed delegate adapter retrieval.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `WithDelayedDelegatingFactory` object is deserialized from a JSON string using `Gson.fromJson`, and its field `f` is asserted to be equal to 'de'.
    - A `WithDelayedDelegatingFactory` object is created with the field `f` set to 'se', and it is serialized to a JSON string using `Gson.toJson`, which is then asserted to be equal to '{"custom":{"f":"se"}}'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testDelegating\_SameFactoryClass<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryClass}} -->
The `testDelegating_SameFactoryClass` method tests the behavior of Gson's `getDelegateAdapter` when different instances of the same factory class are used, ensuring that both factories are utilized during serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering a `WithDelegatingFactory.Factory` as a type adapter factory.
    - A JSON string is deserialized into a `WithDelegatingFactory` object using the `Gson` instance, expecting the custom factory to be applied twice, resulting in nested `"custom"` keys.
    - An assertion checks that the deserialized object's field `f` is equal to "de".
    - A `WithDelegatingFactory` object is serialized back to JSON using the `Gson` instance, expecting the custom factory to be applied twice, resulting in nested `"custom"` keys.
    - An assertion checks that the serialized JSON string matches the expected nested structure.
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior of the Gson serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testDelegating\_SameFactoryInstance<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryInstance}} -->
The method `testDelegating_SameFactoryInstance` tests the behavior of Gson's `getDelegateAdapter` when the same instance of a factory is used for both [`registerTypeAdapterFactory`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory) and [`registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter).
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `WithDelegatingFactory.Factory` is created and assigned to the variable `factory`.
    - A `Gson` object is created using `GsonBuilder`, registering the `factory` instance as both a `TypeAdapterFactory` and an `InstanceCreator` for `WithDelegatingFactory.Factory`.
    - The method deserializes a JSON string `{"custom":{"f":"de"}}` into a `WithDelegatingFactory` object using the `gson` instance, and asserts that the field `f` of the deserialized object equals "de".
    - A `WithDelegatingFactory` object is created with the value "se" and serialized back to JSON using the `gson` instance, asserting that the resulting JSON string is `{"custom":{"f":"se"}}`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior of Gson's serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testDelegating\_SameFactoryClass\_OnClassAndField<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryClass_OnClassAndField}} -->
This method tests the behavior of Gson's delegate adapter when the same factory class is used on both a class and its field, ensuring proper serialization and deserialization with custom adapters.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created with a custom TypeAdapter for String that appends '-str' to the string during serialization and deserialization.
    - The method deserializes a JSON string into an instance of WithDelegatingFactoryOnClassAndField, expecting the custom String adapter to modify the field value to 'de-str'.
    - An assertion checks that the deserialized field value is 'de-str'.
    - A new instance of WithDelegatingFactoryOnClassAndField is created with the field value 'se'.
    - The method serializes this instance back to JSON, expecting the custom String adapter to modify the field value to 'se-str'.
    - An assertion checks that the serialized JSON matches the expected structure with 'se-str' as the field value.
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior of Gson's serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testDelegating\_SameFactoryInstance\_OnClassAndField<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testDelegating_SameFactoryInstance_OnClassAndField}} -->
The method `testDelegating_SameFactoryInstance_OnClassAndField` tests the behavior of Gson's `getDelegateAdapter` when the same factory instance is used for both a class and its field, ensuring proper serialization and deserialization without infinite recursion.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `WithDelegatingFactoryOnClassAndField.Factory` instance is created.
    - A `Gson` object is built using `GsonBuilder`, registering a custom `TypeAdapter` for `String` and the factory instance for `WithDelegatingFactoryOnClassAndField.Factory`.
    - The method deserializes a JSON string into a `WithDelegatingFactoryOnClassAndField` object using the `Gson` instance, expecting the field `f` to be deserialized with the custom `String` adapter.
    - An assertion checks that the deserialized field `f` equals 'de-str'.
    - A `WithDelegatingFactoryOnClassAndField` object is created with 'se' as the field value.
    - The method serializes this object back to JSON using the `Gson` instance, expecting the field `f` to be serialized with the custom `String` adapter.
    - An assertion checks that the serialized JSON matches the expected structure with 'se-str' as the field value.
- **Output**:
    - The method does not return any value; it performs assertions to verify correct behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testJsonSerializer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonSerializer}} -->
The `testJsonSerializer` method tests the serialization and deserialization of a `WithJsonSerializer` object using Gson, verifying the use of a custom serializer.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - The method deserializes a JSON string `{"f":"test"}` into a `WithJsonSerializer` object using Gson's [`fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson) method.
    - An assertion checks that the field `f` of the deserialized object equals "test".
    - The method serializes a new `WithJsonSerializer` object into a JSON string using Gson's [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method.
    - An assertion checks that the serialized JSON string equals "true", indicating the use of a custom serializer.
- **Output**:
    - The method does not return any value; it performs assertions to verify correct behavior.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testJsonDeserializer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testJsonDeserializer}} -->
The `testJsonDeserializer` method tests the functionality of a custom JSON deserializer for the `WithJsonDeserializer` class using the Gson library.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new instance of `Gson`.
    - Deserialize a JSON string `{"f":"test"}` into an instance of `WithJsonDeserializer` using the custom deserializer, which sets the field `f` to "123".
    - Assert that the field `f` of the deserialized object is equal to "123".
    - Serialize a new `WithJsonDeserializer` object with field `f` set to "abc" back to JSON using the default serializer.
    - Assert that the serialized JSON string is `{"f":"abc"}`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom deserializer and serializer.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testAdapterCreatedByInstanceCreator<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testAdapterCreatedByInstanceCreator}} -->
The method `testAdapterCreatedByInstanceCreator` tests the creation of a Gson adapter using an `InstanceCreator` to serialize an object to a custom JSON string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `CreatedByInstanceCreator.Serializer` with the string "custom".
    - Create a `Gson` object using `GsonBuilder`, registering a type adapter for `CreatedByInstanceCreator.Serializer` using an `InstanceCreator` that returns the previously created serializer.
    - Serialize a new `CreatedByInstanceCreator` object to JSON using the `Gson` instance.
    - Assert that the resulting JSON string is equal to "custom".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)


---
#### JsonAdapterAnnotationOnClassesTest\.testAdapterCreatedByJdkUnsafe<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.testAdapterCreatedByJdkUnsafe}} -->
The method `testAdapterCreatedByJdkUnsafe` tests the serialization of a `CreatedByJdkUnsafe` object using Gson and verifies that the resulting JSON string is "false".
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new Gson instance.
    - Serialize a new `CreatedByJdkUnsafe` object to JSON using Gson.
    - Assert that the resulting JSON string is equal to "false".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest`](#JsonAdapterAnnotationOnClassesTest)  (Base Class)



---
### WithNullReturningFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithNullReturningFactory` class is a generic container class that holds an object of type `T` and is annotated with `@JsonAdapter` to use a custom `TypeAdapterFactory` called `NullReturningFactory`. This factory is designed to conditionally return a `TypeAdapter` for parameterized types where the type argument is `String`, allowing for custom serialization and deserialization logic. If the type argument is not `String`, the factory returns `null`, indicating that it cannot handle the type, and Gson should try a different factory instead.
- **Fields**:
    - `t`: `T` A generic field of type `T` that holds the value contained in the `WithNullReturningFactory` instance.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory.WithNullReturningFactory`](#WithNullReturningFactoryWithNullReturningFactory)

**Methods**

---
#### WithNullReturningFactory\.WithNullReturningFactory<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory.WithNullReturningFactory}} -->
The constructor `WithNullReturningFactory` initializes an instance of the class with a given value of type `T`.
- **Modifiers**: `public`
- **Inputs**:
    - `t`: The input parameter `t` is a generic type `T` that represents the value to be assigned to the instance variable `t` of the class.
- **Control Flow**:
    - The constructor takes a single parameter `t` of generic type `T`.
    - It assigns the value of `t` to the instance variable `this.t`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory`](#JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory)  (Base Class)



---
### NullReturningFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory.NullReturningFactory}} -->
- **Modifiers**: `static`
- **Description**: The `NullReturningFactory` class is a static inner class that implements the `TypeAdapterFactory` interface, designed to conditionally return a `TypeAdapter` for parameterized types where the first type argument is `String`. If the type is not parameterized or the first type argument is not `String`, it returns `null`, allowing Gson to try other factories. This class is used to demonstrate the behavior of a factory that can return `null` to indicate it cannot handle a type, and it provides custom serialization and deserialization logic for `WithNullReturningFactory<String>` instances.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory.NullReturningFactory.create`](#NullReturningFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### NullReturningFactory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory.NullReturningFactory.create}} -->
The `create` method attempts to create a `TypeAdapter` for a given `TypeToken` if it is a parameterized type with a `String` as its first type argument.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class, used for JSON serialization and deserialization.
    - `type`: A `TypeToken` representing the type for which a `TypeAdapter` is to be created.
- **Control Flow**:
    - Check if the type represented by `TypeToken` is a raw (non-parameterized) type; if so, return `null`.
    - Cast the type to `ParameterizedType` and check if the first actual type argument is `String`; if not, return `null`.
    - Create a `TypeAdapter` for `WithNullReturningFactory<String>` that customizes the `write` and `read` methods for JSON serialization and deserialization.
    - Return the created `TypeAdapter`.
- **Output**:
    - Returns a `TypeAdapter<T>` for `WithNullReturningFactory<String>` if the conditions are met, otherwise returns `null`.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory.NullReturningFactory`](#JsonAdapterAnnotationOnClassesTest.WithNullReturningFactory.NullReturningFactory)  (Base Class)



---
### A<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `A` class is a private static class annotated with `@JsonAdapter`, which uses a custom `JsonAdapter` for serialization and deserialization of its instances. It contains a single final field `value` and a nested static final class `JsonAdapter` that extends `TypeAdapter<A>`, providing custom implementations for the `write` and `read` methods to handle JSON conversion.
- **Fields**:
    - `value`: `String` A final string field that holds the value for an instance of class A.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.A`](#AA)

**Methods**

---
#### A\.A<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.A}} -->
The constructor `A(String value)` initializes an instance of class `A` by setting its `value` field to the provided string argument.
- **Inputs**:
    - `value`: A `String` that is used to initialize the `value` field of the `A` class instance.
- **Control Flow**:
    - The constructor takes a single `String` argument named `value`.
    - It assigns the provided `value` to the instance variable `this.value`.
- **Output**:
    - This constructor does not return any value as it is a constructor for initializing objects of class `A`.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A`](#JsonAdapterAnnotationOnClassesTest.A)  (Base Class)



---
### JsonAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.JsonAdapter}} -->
- **Modifiers**: `static`, `final`
- **Description**: The `JsonAdapter` class is a static final inner class extending `TypeAdapter<A>`, designed to handle the serialization and deserialization of objects of type `A` using the Gson library. It overrides the `write` and `read` methods to provide custom behavior, where it writes a fixed string "jsonAdapter" to the `JsonWriter` and reads a string from the `JsonReader`, returning a new instance of `A` initialized with "jsonAdapter".
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.JsonAdapter.write`](#JsonAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.JsonAdapter.read`](#JsonAdapterread)

**Methods**

---
#### JsonAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.JsonAdapter.write}} -->
The `write` method writes a fixed string value "jsonAdapter" to the provided `JsonWriter` output stream.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): An instance of class `A`, which is not used in this method.
- **Control Flow**:
    - The method calls `out.value("jsonAdapter")` to write the string "jsonAdapter" to the `JsonWriter` output.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.JsonAdapter`](#JsonAdapterAnnotationOnClassesTest.A.JsonAdapter)  (Base Class)


---
#### JsonAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.JsonAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader` and returns a new instance of class `A` with a fixed value.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method reads the next JSON string from the `JsonReader` using `in.nextString()` and assigns it to a local variable `unused`.
    - It then returns a new instance of class `A` initialized with the string "jsonAdapter".
- **Output**:
    - An instance of class `A` initialized with the string "jsonAdapter".
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A.JsonAdapter`](#JsonAdapterAnnotationOnClassesTest.A.JsonAdapter)  (Base Class)



---
### C<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `C` class is a private static class that is annotated with `@JsonAdapter`, using a custom `JsonAdapterFactory` to handle JSON serialization and deserialization. It contains a single final field `value` and provides a constructor to initialize this field. The `JsonAdapterFactory` is an inner static final class implementing `TypeAdapterFactory`, which creates a `TypeAdapter` for the `C` class, overriding the `write` and `read` methods to handle JSON operations by outputting and reading a fixed string value, respectively.
- **Fields**:
    - `value`: `String` A final String field that holds the value for an instance of the C class.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C.C`](#CC)

**Methods**

---
#### C\.C<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C.C}} -->
The constructor `C` initializes an instance of class `C` by setting its `value` field to the provided string argument.
- **Inputs**:
    - `value`: A string that is used to initialize the `value` field of the `C` class instance.
- **Control Flow**:
    - The constructor takes a single string argument named `value`.
    - It assigns the provided `value` to the instance variable `this.value`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of class `C`.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C`](#JsonAdapterAnnotationOnClassesTest.C)  (Base Class)



---
### JsonAdapterFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C.JsonAdapterFactory}} -->
- **Modifiers**: `static`, `final`
- **Description**: The `JsonAdapterFactory` class is a static final implementation of the `TypeAdapterFactory` interface, designed to create custom `TypeAdapter` instances for JSON serialization and deserialization using the Gson library. It provides a specific implementation for the `create` method, which returns a `TypeAdapter` that writes a fixed string "jsonAdapterFactory" during serialization and reads a fixed string to create a new instance of class `C` during deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C.JsonAdapterFactory.create`](#JsonAdapterFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### JsonAdapterFactory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C.JsonAdapterFactory.create}} -->
The `create` method returns a custom `TypeAdapter` for a given type that writes a fixed string and reads a fixed object.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class used for JSON serialization and deserialization.
    - `type`: A `TypeToken` representing the type for which the `TypeAdapter` is being created.
- **Control Flow**:
    - The method returns a new instance of an anonymous `TypeAdapter` class.
    - The `write` method of the `TypeAdapter` writes the fixed string "jsonAdapterFactory" to the `JsonWriter`.
    - The `read` method of the `TypeAdapter` reads a string from the `JsonReader` and returns a new instance of class `C` with the value "jsonAdapterFactory".
- **Output**:
    - A `TypeAdapter<T>` instance that writes a fixed string and reads a fixed object.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.C.JsonAdapterFactory`](#JsonAdapterAnnotationOnClassesTest.C.JsonAdapterFactory)  (Base Class)



---
### B<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.B}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `B` class is a private static final class that extends the `A` class, providing a constructor that takes a `String` value and passes it to the superclass `A` constructor.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.B.B`](#BB)
- **Extends/Implements**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.A`](#JsonAdapterAnnotationOnClassesTest.A)

**Methods**

---
#### B\.B<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.B.B}} -->
The constructor B initializes an instance of class B by calling the superclass constructor with a given string value.
- **Modifiers**: ``
- **Inputs**:
    - `value`: A string value that is passed to the superclass constructor.
- **Control Flow**:
    - The constructor B is called with a single string argument 'value'.
    - The constructor calls the superclass constructor using 'super(value)' to initialize the superclass part of the object.
- **Output**:
    - There is no explicit output as this is a constructor, but it initializes an instance of class B.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.B`](#JsonAdapterAnnotationOnClassesTest.B)  (Base Class)



---
### ClassWithIncorrectJsonAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.ClassWithIncorrectJsonAdapter}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `ClassWithIncorrectJsonAdapter` class is a simple class that contains a single final field `value` of type `String`. It is annotated with `@JsonAdapter` using `A.JsonAdapter.class`, which is not the correct type adapter for this class, leading to a `ClassCastException` when attempting to serialize or deserialize instances of this class using Gson.
- **Fields**:
    - `value`: `String` A final String field that holds the value for the class.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.ClassWithIncorrectJsonAdapter.ClassWithIncorrectJsonAdapter`](#ClassWithIncorrectJsonAdapterClassWithIncorrectJsonAdapter)

**Methods**

---
#### ClassWithIncorrectJsonAdapter\.ClassWithIncorrectJsonAdapter<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.ClassWithIncorrectJsonAdapter.ClassWithIncorrectJsonAdapter}} -->
The constructor `ClassWithIncorrectJsonAdapter` initializes an instance of the class with a given string value.
- **Modifiers**: ``
- **Inputs**:
    - `value`: A string that is assigned to the instance variable `value` of the class.
- **Control Flow**:
    - The constructor takes a single string argument `value`.
    - It assigns the provided `value` to the instance variable `value` of the class.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.ClassWithIncorrectJsonAdapter`](#JsonAdapterAnnotationOnClassesTest.ClassWithIncorrectJsonAdapter)  (Base Class)



---
### User<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.User}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `User` class represents a user with a first name and last name, and is annotated with `@JsonAdapter` to specify a custom JSON serialization and deserialization behavior using the `UserJsonAdapter` class.
- **Fields**:
    - `firstName`: `String` The first name of the user.
    - `lastName`: `String` The last name of the user.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.User.User`](#UserUser)

**Methods**

---
#### User\.User<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.User.User}} -->
The `User` constructor initializes a `User` object with a given first name and last name.
- **Inputs**:
    - `firstName`: A `String` representing the first name of the user.
    - `lastName`: A `String` representing the last name of the user.
- **Control Flow**:
    - The constructor assigns the provided `firstName` to the `firstName` field of the `User` object.
    - The constructor assigns the provided `lastName` to the `lastName` field of the `User` object.
- **Output**:
    - This constructor does not return a value as it is used to instantiate a `User` object.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.User`](#JsonAdapterAnnotationOnClassesTest.User)  (Base Class)



---
### UserJsonAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.UserJsonAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `UserJsonAdapter` class is a private static class that extends `TypeAdapter<User>` to provide custom serialization and deserialization logic for `User` objects. It overrides the `write` method to serialize a `User` object by combining the `firstName` and `lastName` fields into a single `name` field in JSON format. Conversely, it overrides the `read` method to deserialize a JSON object by splitting the `name` field back into `firstName` and `lastName` fields, creating a new `User` object with these values.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.UserJsonAdapter.write`](#UserJsonAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.UserJsonAdapter.read`](#UserJsonAdapterread)

**Methods**

---
#### UserJsonAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.UserJsonAdapter.write}} -->
The `write` method serializes a `User` object into JSON format by combining the user's first and last names into a single 'name' field.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - `user`: A `User` object containing the first and last names to be serialized.
- **Control Flow**:
    - Begin writing a JSON object using `out.beginObject()`.
    - Write a JSON field named 'name' using `out.name("name")`.
    - Combine the `firstName` and `lastName` of the `user` object with a space in between and write it as the value of the 'name' field using `out.value(user.firstName + " " + user.lastName)`.
    - End the JSON object using `out.endObject()`.
- **Output**:
    - The method does not return a value; it writes the serialized JSON representation of the `User` object to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.UserJsonAdapter`](#JsonAdapterAnnotationOnClassesTest.UserJsonAdapter)  (Base Class)


---
#### UserJsonAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.UserJsonAdapter.read}} -->
The `read` method deserializes a JSON object containing a user's full name into a `User` object with separate first and last names.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object used to read the JSON input.
- **Control Flow**:
    - The method begins by calling `in.beginObject()` to start reading a JSON object.
    - It reads the next name in the JSON object using `in.nextName()`, which is stored in an unused variable.
    - The method then reads the next string value, which is expected to be a full name, and splits it into parts using a space as the delimiter with `Splitter.on(" ").splitToList(in.nextString())`.
    - It calls `in.endObject()` to finish reading the JSON object.
    - Finally, it returns a new `User` object, using the first and second elements of the `nameParts` list as the first and last names, respectively.
- **Output**:
    - A `User` object with the first and last names extracted from the JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.UserJsonAdapter`](#JsonAdapterAnnotationOnClassesTest.UserJsonAdapter)  (Base Class)



---
### NullableClass<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClass}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `NullableClass` is a private static class annotated with `@JsonAdapter`, which specifies a custom JSON adapter (`NullableClassJsonAdapter`) for serialization and deserialization. This class is used to demonstrate the handling of null values in JSON serialization and deserialization using Gson, where the adapter ensures that null values are correctly processed and represented as "nullable" when serialized.


---
### NullableClassJsonAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `NullableClassJsonAdapter` is a private static class that extends `TypeAdapter` for the `NullableClass` type, providing custom serialization and deserialization logic for JSON processing using the Gson library. It writes a fixed string "nullable" when serializing a `NullableClass` instance and creates a new `NullableClass` instance when deserializing, ignoring the actual JSON content.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter.write`](#NullableClassJsonAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter.read`](#NullableClassJsonAdapterread)

**Methods**

---
#### NullableClassJsonAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter.write}} -->
The `write` method writes a fixed string value "nullable" to the provided `JsonWriter`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `out`: A `JsonWriter` object to which the method writes the string value.
    - [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `NullableClass` object, which is not used in the method logic.
- **Control Flow**:
    - The method calls `out.value("nullable")` to write the string "nullable" to the `JsonWriter` object.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter`](#JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter)  (Base Class)


---
#### NullableClassJsonAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader` and returns a new instance of `NullableClass`.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method reads the next JSON string from the `JsonReader` using `in.nextString()` and assigns it to a local variable `unused`.
    - A new instance of `NullableClass` is created and returned.
- **Output**:
    - A new instance of `NullableClass`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter`](#JsonAdapterAnnotationOnClassesTest.NullableClassJsonAdapter)  (Base Class)



---
### Foo<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.Foo}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Foo` class is a private static enum that defines two constants, `BAR` and `BAZ`, and is annotated with `@JsonAdapter(FooJsonAdapter.class)`, indicating that it uses a custom JSON adapter for serialization and deserialization.


---
### FooJsonAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.FooJsonAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `FooJsonAdapter` class is a private static inner class that extends `TypeAdapter<Foo>` to provide custom serialization and deserialization logic for the `Foo` enum type. It overrides the `write` method to serialize a `Foo` enum value to its lowercase string representation using the US locale, and the `read` method to deserialize a string back to a `Foo` enum value by converting it to uppercase using the US locale.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.FooJsonAdapter.write`](#FooJsonAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.FooJsonAdapter.read`](#FooJsonAdapterread)

**Methods**

---
#### FooJsonAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.FooJsonAdapter.write}} -->
The `write` method serializes a `Foo` enum value to a JSON string in lowercase using a `JsonWriter`.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `Foo` enum value to be serialized.
- **Control Flow**:
    - The method calls `out.value()` with the `name()` of the `Foo` enum value converted to lowercase using `Locale.US`.
- **Output**:
    - The method writes the lowercase name of the `Foo` enum value to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.FooJsonAdapter`](#JsonAdapterAnnotationOnClassesTest.FooJsonAdapter)  (Base Class)


---
#### FooJsonAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.FooJsonAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader`, converts it to uppercase, and returns the corresponding `Foo` enum value.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method reads the next JSON string from the `JsonReader` using `in.nextString()`.
    - The string is converted to uppercase using `toUpperCase(Locale.US)`.
    - The method returns the `Foo` enum value corresponding to the uppercase string using `Foo.valueOf()`.
- **Output**:
    - Returns a `Foo` enum value corresponding to the uppercase version of the JSON string read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.FooJsonAdapter`](#JsonAdapterAnnotationOnClassesTest.FooJsonAdapter)  (Base Class)



---
### WithInvalidAdapterClass<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithInvalidAdapterClass}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `WithInvalidAdapterClass` is a private static final class that is incorrectly annotated with `@JsonAdapter(Integer.class)`, which is not a valid type for a `JsonAdapter`. This class is used to demonstrate error handling when an invalid adapter is specified, as it will throw an `IllegalArgumentException` when serialization is attempted with Gson.
- **Fields**:
    - `value`: `String` A final string field initialized to "a".


---
### WithDelegatingFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactory}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithDelegatingFactory` class is a generic container class that utilizes a custom `TypeAdapterFactory` to handle JSON serialization and deserialization using Gson. It wraps an object of type `T` and provides a factory class that delegates the serialization and deserialization process to a delegate adapter, while adding custom behavior to handle JSON objects with a specific structure.
- **Fields**:
    - `f`: `T` A generic field of type `T` that holds the value to be serialized or deserialized.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactory.WithDelegatingFactory`](#WithDelegatingFactoryWithDelegatingFactory)

**Methods**

---
#### WithDelegatingFactory\.WithDelegatingFactory<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactory.WithDelegatingFactory}} -->
The `WithDelegatingFactory` constructor initializes an instance of the class with a given value of type `T`.
- **Inputs**:
    - `f`: A generic parameter of type `T` used to initialize the instance variable `f`.
- **Control Flow**:
    - The constructor takes a single parameter `f` of type `T`.
    - It assigns the value of `f` to the instance variable `this.f`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `WithDelegatingFactory` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactory`](#JsonAdapterAnnotationOnClassesTest.WithDelegatingFactory)  (Base Class)



---
### Factory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField.Factory}} -->
- **Modifiers**: `static`
- **Description**: The `Factory` class is a static inner class that implements the `TypeAdapterFactory` interface, providing a mechanism to create custom `TypeAdapter` instances for JSON serialization and deserialization using the Gson library. It customizes the serialization and deserialization process by wrapping the delegate adapter with additional logic to handle JSON objects with a specific structure, ensuring that the JSON data is encapsulated within a "custom" object.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField.Factory.create`](#Factorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### Factory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField.Factory.create}} -->
The `create` method returns a custom `TypeAdapter` that wraps a delegate adapter to perform custom serialization and deserialization with a 'custom' JSON object wrapper.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class used to obtain the delegate adapter.
    - `type`: A `TypeToken` representing the type for which the adapter is being created.
- **Control Flow**:
    - Obtain a delegate `TypeAdapter` for the specified type using `gson.getDelegateAdapter` with the current factory and type.
    - Return a new `TypeAdapter` instance with overridden [`read`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.read) and [`write`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.write) methods.
    - In the [`read`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.read) method, begin reading a JSON object, assert that the next name is 'custom', read the object using the delegate adapter, and end the object.
    - In the [`write`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.write) method, begin writing a JSON object, write the name 'custom', write the object using the delegate adapter, and end the object.
- **Output**:
    - A `TypeAdapter<T>` that performs custom serialization and deserialization by wrapping the delegate adapter with a 'custom' JSON object.
- **Functions called**:
    - [`com.google.gson.Gson.getDelegateAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create.read`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.read)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create.write`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.write)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField.Factory`](#JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField.Factory)  (Base Class)



---
### WithDelayedDelegatingFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelayedDelegatingFactory}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithDelayedDelegatingFactory` class is a private static class that is used to demonstrate the use of a custom `TypeAdapterFactory` for JSON serialization and deserialization using Gson. It contains a single field `f` and a nested static `Factory` class that implements `TypeAdapterFactory`. The `Factory` class provides a custom `TypeAdapter` that delegates serialization and deserialization to a delegate adapter obtained from Gson, while wrapping the JSON object with a custom key `"custom"`. This class is primarily used for testing the behavior of delayed delegation in Gson's adapter factories.
- **Fields**:
    - `f`: `String` A string field used to store data within the `WithDelayedDelegatingFactory` class.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelayedDelegatingFactory.WithDelayedDelegatingFactory`](#WithDelayedDelegatingFactoryWithDelayedDelegatingFactory)

**Methods**

---
#### WithDelayedDelegatingFactory\.WithDelayedDelegatingFactory<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelayedDelegatingFactory.WithDelayedDelegatingFactory}} -->
The `WithDelayedDelegatingFactory` constructor initializes an instance with a given string value.
- **Inputs**:
    - `f`: A string value used to initialize the instance variable `f`.
- **Control Flow**:
    - The constructor takes a single string argument `f`.
    - It assigns the input string `f` to the instance variable `this.f`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the class `WithDelayedDelegatingFactory`.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelayedDelegatingFactory`](#JsonAdapterAnnotationOnClassesTest.WithDelayedDelegatingFactory)  (Base Class)



---
### WithDelegatingFactoryOnClassAndField<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithDelegatingFactoryOnClassAndField` class is a private static class that demonstrates the use of a custom `TypeAdapterFactory` for JSON serialization and deserialization using Gson. It is annotated with `@JsonAdapter` to specify a factory class for handling JSON operations. The class contains a single field `f` which is also annotated with `@JsonAdapter`, indicating that the same factory class is used for both the class and the field. The nested `Factory` class implements `TypeAdapterFactory` to provide custom serialization and deserialization logic, wrapping the default delegate adapter to add a custom JSON object structure.
- **Fields**:
    - `f`: `String` A string field annotated with @JsonAdapter to use the Factory class for JSON operations.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField.WithDelegatingFactoryOnClassAndField`](#WithDelegatingFactoryOnClassAndFieldWithDelegatingFactoryOnClassAndField)

**Methods**

---
#### WithDelegatingFactoryOnClassAndField\.WithDelegatingFactoryOnClassAndField<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField.WithDelegatingFactoryOnClassAndField}} -->
The constructor `WithDelegatingFactoryOnClassAndField` initializes an instance of the class with a given string value for its field `f`.
- **Inputs**:
    - `f`: A string value used to initialize the field `f` of the class.
- **Control Flow**:
    - The constructor takes a single string argument `f`.
    - It assigns the value of `f` to the instance variable `this.f`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField`](#JsonAdapterAnnotationOnClassesTest.WithDelegatingFactoryOnClassAndField)  (Base Class)



---
### WithJsonSerializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonSerializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithJsonSerializer` class is a private static class that is annotated with `@JsonAdapter`, indicating that it uses a custom serializer for JSON serialization. The class contains a single field `f` of type `String`, which is initialized to an empty string. The nested static `Serializer` class implements the `JsonSerializer` interface for `WithJsonSerializer`, providing a custom serialization method that always returns a JSON primitive with the value `true`, regardless of the actual content of the `WithJsonSerializer` instance.
- **Fields**:
    - `f`: `String` A string field initialized to an empty string.


---
### Serializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer}} -->
- **Modifiers**: `static`
- **Description**: The `Serializer` class is a static inner class that implements the `JsonSerializer` interface for the `CreatedByJdkUnsafe` class, providing a custom serialization mechanism that returns a JSON primitive based on the `wasInitialized` field, which is set to `true` by default but is intended to be left at its default value of `false` when instantiated using JDK Unsafe.
- **Fields**:
    - `wasInitialized`: `boolean` A boolean field that is set to true by default, but intended to be false when instantiated using JDK Unsafe.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer.Serializer`](#SerializerSerializer)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer.serialize`](#Serializerserialize)

**Methods**

---
#### Serializer\.Serializer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer.Serializer}} -->
The `Serializer` constructor is designed to throw an `AssertionError` if called, indicating it should not be used.
- **Modifiers**: `public`
- **Inputs**:
    - `i`: An integer parameter that is not used in the method.
- **Control Flow**:
    - The method immediately throws an `AssertionError` with the message 'should not be called'.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer`](#JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer)  (Base Class)


---
#### Serializer\.serialize<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer.serialize}} -->
The `serialize` method converts a `CreatedByJdkUnsafe` object into a JSON primitive representing the `wasInitialized` boolean field.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The `CreatedByJdkUnsafe` object to be serialized.
    - `typeOfSrc`: The specific type of the source object, `CreatedByJdkUnsafe`.
    - `context`: The context for serialization, providing additional serialization capabilities.
- **Control Flow**:
    - The method directly returns a new `JsonPrimitive` object initialized with the value of the `wasInitialized` field.
- **Output**:
    - A `JsonElement` representing the `wasInitialized` field as a JSON primitive.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer`](#JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe.Serializer)  (Base Class)



---
### WithJsonDeserializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithJsonDeserializer` class is a private static class that is annotated with `@JsonAdapter`, indicating that it uses a custom deserializer for JSON deserialization. It contains a single field `f` and a nested static class `Deserializer` that implements the `JsonDeserializer` interface to provide custom deserialization logic, which always sets the field `f` to the string "123" regardless of the input JSON.
- **Fields**:
    - `f`: `String` A string field that is set during deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer.WithJsonDeserializer`](#WithJsonDeserializerWithJsonDeserializer)

**Methods**

---
#### WithJsonDeserializer\.WithJsonDeserializer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer.WithJsonDeserializer}} -->
The `WithJsonDeserializer` constructor initializes an instance of the class by setting the field `f` with the provided string argument.
- **Inputs**:
    - `f`: A string that is used to initialize the field `f` of the `WithJsonDeserializer` class.
- **Control Flow**:
    - The constructor takes a single string argument `f`.
    - It assigns the value of `f` to the instance variable `this.f`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `WithJsonDeserializer` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer`](#JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer)  (Base Class)



---
### Deserializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer.Deserializer}} -->
- **Modifiers**: `static`
- **Description**: The `Deserializer` class is a static inner class that implements the `JsonDeserializer` interface for the `WithJsonDeserializer` class, providing a custom deserialization logic that always returns a new `WithJsonDeserializer` instance with the field value set to "123".
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer.Deserializer.deserialize`](#Deserializerdeserialize)

**Methods**

---
#### Deserializer\.deserialize<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer.Deserializer.deserialize}} -->
The `deserialize` method creates a new `WithJsonDeserializer` object with a fixed string value "123".
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the object to deserialize to.
    - `context`: A `JsonDeserializationContext` that provides the context for deserialization.
- **Control Flow**:
    - The method is called with three parameters: `json`, `typeOfT`, and `context`.
    - A new instance of `WithJsonDeserializer` is created with the string "123" as its constructor argument.
    - The newly created `WithJsonDeserializer` object is returned.
- **Output**:
    - Returns a new `WithJsonDeserializer` object initialized with the string "123".
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer.Deserializer`](#JsonAdapterAnnotationOnClassesTest.WithJsonDeserializer.Deserializer)  (Base Class)



---
### CreatedByInstanceCreator<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByInstanceCreator}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `CreatedByInstanceCreator` class is a private static class that is used in conjunction with the Gson library to demonstrate the use of a custom serializer through the `@JsonAdapter` annotation. It contains a nested static class `Serializer` that implements the `JsonSerializer` interface, allowing for custom serialization of `CreatedByInstanceCreator` instances into JSON format. The `Serializer` class requires a string value upon instantiation, which is used as the serialized JSON output.
- **Fields**:
    - `value`: `String` A string value used in the serialization process.


---
### CreatedByJdkUnsafe<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnClassesTest.CreatedByJdkUnsafe}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `CreatedByJdkUnsafe` class is a private static class that is used to demonstrate the creation of a JSON adapter using JDK Unsafe mechanisms. It contains a nested static `Serializer` class that implements the `JsonSerializer` interface for serializing instances of `CreatedByJdkUnsafe`. The serializer has a boolean field `wasInitialized` which is set to `true` by default, but the JDK Unsafe mechanism leaves it at its default value `false`. The serializer's constructor is designed to throw an error if called, ensuring it is not used directly.
- **Fields**:
    - `wasInitialized`: `boolean` A boolean field in the Serializer class, defaulting to true, but intended to be left at false by JDK Unsafe.


