# Purpose
The `TypeAdapterRuntimeTypeWrapperTest` class is a unit test suite designed to validate the behavior of custom type adapters in the Gson library, specifically focusing on serialization and deserialization processes. This code provides a narrow functionality, primarily testing how Gson handles different scenarios when custom `JsonSerializer` and `JsonDeserializer` implementations are registered for a base class and its subclass. The tests ensure that the correct serialization strategy is applied, whether it be a custom serializer, a reflective adapter, or a combination of both, depending on the configuration of type adapters.

The class contains several test methods, each targeting a specific aspect of Gson's type adapter behavior. These tests cover scenarios such as preferring a custom serializer over a reflective adapter, handling multiple deserializers, and ensuring backward compatibility when a subclass has its own deserializer. The tests utilize the `GsonBuilder` to register type adapters and verify the serialized JSON output using assertions. The class also includes a test for cyclic dependencies, demonstrating Gson's ability to handle types that reference themselves during serialization. Overall, this file is a collection of test cases that ensure the robustness and flexibility of Gson's type adapter mechanism.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonDeserializationContext`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSerializer`
- `com.google.gson.TypeAdapter`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.Type`
- `org.junit.Test`


# Classes

---
### TypeAdapterRuntimeTypeWrapperTest<!-- {{#class:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest}} -->
- **Modifiers**: `public`
- **Description**: The `TypeAdapterRuntimeTypeWrapperTest` class is a test suite designed to verify the behavior of Gson's type adapter mechanism, particularly focusing on how custom `JsonSerializer` and `JsonDeserializer` implementations interact with the default reflective serialization and deserialization processes. It includes various test cases to ensure that when custom serializers or deserializers are registered for a base class, they are preferred over the reflective adapters for subclasses, unless specific backward compatibility or delegation rules apply. The tests also cover scenarios involving cyclic dependencies and future adapters.
- **Methods**:
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonSerializer`](#TypeAdapterRuntimeTypeWrapperTesttestJsonSerializer)
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_ReflectiveSerializerDelegate`](#TypeAdapterRuntimeTypeWrapperTesttestJsonDeserializer_ReflectiveSerializerDelegate)
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_CustomSerializerDelegate`](#TypeAdapterRuntimeTypeWrapperTesttestJsonDeserializer_CustomSerializerDelegate)
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_ReflectiveTreeSerializerDelegate`](#TypeAdapterRuntimeTypeWrapperTesttestJsonDeserializer_ReflectiveTreeSerializerDelegate)
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_JsonSerializerDelegate`](#TypeAdapterRuntimeTypeWrapperTesttestJsonDeserializer_JsonSerializerDelegate)
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_SubclassBackwardCompatibility`](#TypeAdapterRuntimeTypeWrapperTesttestJsonDeserializer_SubclassBackwardCompatibility)
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testGsonFutureAdapter`](#TypeAdapterRuntimeTypeWrapperTesttestGsonFutureAdapter)

**Methods**

---
#### TypeAdapterRuntimeTypeWrapperTest\.testJsonSerializer<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonSerializer}} -->
The `testJsonSerializer` method tests the serialization of a `Container` object using a custom `JsonSerializer` for the `Base` class, ensuring the output JSON matches the expected string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, with a custom `JsonSerializer` registered for the `Base` class that serializes any `Base` object to the JSON string "serializer".
    - A `Container` object is serialized to JSON using the `Gson` object.
    - The resulting JSON string is asserted to be equal to the expected string `{"b":"serializer"}`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest`](#TypeAdapterRuntimeTypeWrapperTest)  (Base Class)


---
#### TypeAdapterRuntimeTypeWrapperTest\.testJsonDeserializer\_ReflectiveSerializerDelegate<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_ReflectiveSerializerDelegate}} -->
The method `testJsonDeserializer_ReflectiveSerializerDelegate` tests the serialization behavior of Gson when a `JsonDeserializer` is registered for a base class without a custom serializer.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder`, registering a `JsonDeserializer` for the `Base` class.
    - A `Container` object, which contains a `Base` type field initialized with a `Subclass` instance, is serialized to JSON using the `Gson` instance.
    - The resulting JSON string is asserted to be equal to `{"b":{"f":"test"}}`, verifying that the reflective adapter is used for serialization.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest`](#TypeAdapterRuntimeTypeWrapperTest)  (Base Class)


---
#### TypeAdapterRuntimeTypeWrapperTest\.testJsonDeserializer\_CustomSerializerDelegate<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_CustomSerializerDelegate}} -->
This method tests the serialization of a Container object using a custom TypeAdapter for the Base class that overrides the default reflective serialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using GsonBuilder, where a custom TypeAdapter for the Base class is registered to handle serialization by writing 'custom delegate' as the value.
    - Another TypeAdapter for the Base class is registered, which is a Deserializer that throws an AssertionError when its deserialize method is called.
    - A Container object is serialized to JSON using the configured Gson instance.
    - An assertion checks that the resulting JSON string is equal to '{"b":"custom delegate"}'.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest`](#TypeAdapterRuntimeTypeWrapperTest)  (Base Class)


---
#### TypeAdapterRuntimeTypeWrapperTest\.testJsonDeserializer\_ReflectiveTreeSerializerDelegate<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_ReflectiveTreeSerializerDelegate}} -->
The method `testJsonDeserializer_ReflectiveTreeSerializerDelegate` tests the serialization behavior of Gson when multiple `JsonDeserializer` instances are registered for a base class, which fall back to reflective serialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder`, registering two `JsonDeserializer` instances for the `Base` class, both of which fall back to reflective serialization.
    - A `Container` object, which contains a `Base` reference to a `Subclass` instance, is serialized to JSON using the `Gson` instance.
    - The resulting JSON string is asserted to be equal to `{"b":{"f":"test"}}`, verifying that reflective serialization was used for the `Subclass` instance.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest`](#TypeAdapterRuntimeTypeWrapperTest)  (Base Class)


---
#### TypeAdapterRuntimeTypeWrapperTest\.testJsonDeserializer\_JsonSerializerDelegate<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_JsonSerializerDelegate}} -->
The method `testJsonDeserializer_JsonSerializerDelegate` tests the behavior of Gson serialization when a `JsonSerializer` is registered as a delegate for a base class, ensuring it is preferred over the reflective adapter for a subclass.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, where a `JsonSerializer` is registered for the `Base` class to return a `JsonPrimitive` with the value "custom delegate".
    - A `JsonDeserializer` is also registered for the `Base` class, but it is not used in this test.
    - A `Container` object, which contains a `Base` field initialized with a `Subclass` instance, is serialized to JSON using the `Gson` object.
    - The resulting JSON string is asserted to be equal to `{"b":"custom delegate"}` using `assertThat`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest`](#TypeAdapterRuntimeTypeWrapperTest)  (Base Class)


---
#### TypeAdapterRuntimeTypeWrapperTest\.testJsonDeserializer\_SubclassBackwardCompatibility<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testJsonDeserializer_SubclassBackwardCompatibility}} -->
This method tests the backward compatibility of Gson's JSON deserialization when a JsonDeserializer is registered for a subclass and a JsonSerializer is registered for its base class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using GsonBuilder, registering a JsonDeserializer for Subclass that throws an AssertionError and a JsonSerializer for Base that returns a JsonPrimitive with the value 'base'.
    - A Container object is serialized to JSON using the Gson instance.
    - An assertion checks that the resulting JSON string is equal to '{"b":{"f":"test"}}', indicating that the reflective adapter for Subclass was used.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest`](#TypeAdapterRuntimeTypeWrapperTest)  (Base Class)


---
#### TypeAdapterRuntimeTypeWrapperTest\.testGsonFutureAdapter<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.testGsonFutureAdapter}} -->
The `testGsonFutureAdapter` method tests the serialization of a cyclic object structure using Gson to ensure it correctly handles future adapters.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create an instance of `CyclicBase` named `b`.
    - Assign a new `CyclicSub` object with an integer value of 2 to the field `f` of `b`.
    - Serialize the object `b` to a JSON string using Gson.
    - Assert that the resulting JSON string is equal to the expected string `{"f":{"i":2}}`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the JSON serialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest`](#TypeAdapterRuntimeTypeWrapperTest)  (Base Class)



---
### Base<!-- {{#class:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.Base}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Base` class is a simple, private static class used as a base type in the `TypeAdapterRuntimeTypeWrapperTest` for testing purposes, particularly in scenarios involving JSON serialization and deserialization with Gson.


---
### Subclass<!-- {{#class:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.Subclass}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Subclass` is a private static class that extends the `Base` class and contains a single string field `f` initialized to "test". It is used within the `TypeAdapterRuntimeTypeWrapperTest` class to demonstrate serialization and deserialization behaviors in various test cases.
- **Fields**:
    - `f`: `String` A string field initialized to "test".
- **Extends/Implements**:
    - [`com.google.gson.functional.UncategorizedTest.Base`](UncategorizedTest.java.driver.md#Base)


---
### Container<!-- {{#class:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.Container}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Container` class is a simple private static class that contains a single field `b`, which is an instance of the `Base` class initialized with a `Subclass` object. This class is used in the context of testing JSON serialization and deserialization behaviors with the Gson library, particularly focusing on how different type adapters and serializers are applied to the `Base` and `Subclass` types.
- **Fields**:
    - `b`: `Base` A field of type `Base` initialized with an instance of `Subclass`, used for testing serialization behavior.


---
### Deserializer<!-- {{#class:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.Deserializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Deserializer` class is a private static inner class that implements the `JsonDeserializer` interface for the `Base` class, but its `deserialize` method is intentionally left unimplemented, throwing an `AssertionError` to indicate it is not needed for the test cases in which it is used.
- **Methods**:
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.Deserializer.deserialize`](#Deserializerdeserialize)

**Methods**

---
#### Deserializer\.deserialize<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.Deserializer.deserialize}} -->
The `deserialize` method is a placeholder that throws an `AssertionError` indicating it is not needed for the test.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the object to deserialize to.
    - `context`: A `JsonDeserializationContext` that provides the context for deserialization.
- **Control Flow**:
    - The method immediately throws an `AssertionError` with the message 'not needed for this test'.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.Deserializer`](#TypeAdapterRuntimeTypeWrapperTest.Deserializer)  (Base Class)



---
### CyclicBase<!-- {{#class:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.CyclicBase}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `CyclicBase` class is a simple private static class that contains a single field, `f`, which is a reference to another instance of `CyclicBase`, allowing for the creation of cyclic data structures.
- **Fields**:
    - `f`: `CyclicBase` A reference to another instance of `CyclicBase`, enabling cyclic references.


---
### CyclicSub<!-- {{#class:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.CyclicSub}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `CyclicSub` class is a private static subclass of `CyclicBase` that represents a cyclic structure with an integer field `i`, which is initialized through its constructor.
- **Fields**:
    - `i`: `int` An integer field representing a value associated with the `CyclicSub` instance.
- **Methods**:
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.CyclicSub.CyclicSub`](#CyclicSubCyclicSub)
- **Extends/Implements**:
    - [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.CyclicBase`](#TypeAdapterRuntimeTypeWrapperTest.CyclicBase)

**Methods**

---
#### CyclicSub\.CyclicSub<!-- {{#callable:com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.CyclicSub.CyclicSub}} -->
The `CyclicSub` constructor initializes an instance of the `CyclicSub` class by setting its integer field `i` to the provided value.
- **Modifiers**: `public`
- **Inputs**:
    - `i`: An integer value used to initialize the `i` field of the `CyclicSub` instance.
- **Control Flow**:
    - The constructor takes an integer parameter `i`.
    - The integer parameter `i` is assigned to the instance variable `this.i`.
- **Output**:
    - The constructor does not return any value as it is used to initialize an object of the `CyclicSub` class.
- **See also**: [`com.google.gson.functional.TypeAdapterRuntimeTypeWrapperTest.CyclicSub`](#TypeAdapterRuntimeTypeWrapperTest.CyclicSub)  (Base Class)



