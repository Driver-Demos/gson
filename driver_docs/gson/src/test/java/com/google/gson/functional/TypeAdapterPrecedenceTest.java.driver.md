# Purpose
The `TypeAdapterPrecedenceTest` Java class is a unit test suite designed to evaluate the precedence and behavior of different type adapters in the Gson library, a popular JSON serialization/deserialization library. This class is part of the `com.google.gson.functional` package and uses the JUnit testing framework to define a series of tests that explore how Gson handles multiple type adapters registered for the same class, [`Foo`](#FooFoo). The tests specifically focus on the order of precedence between streaming and non-streaming type adapters, as well as hierarchical and non-hierarchical adapters, to ensure that the correct adapter is used during JSON serialization and deserialization processes.

The class contains several test methods, each registering different combinations of `JsonSerializer`, `JsonDeserializer`, and `TypeAdapter` instances for the [`Foo`](#FooFoo) class using a `GsonBuilder`. These methods verify the output of the `toJson` and `fromJson` methods of the `Gson` object to ensure that the expected adapter is applied based on the registration order. The [`Foo`](#FooFoo) class is a simple data structure with a single `name` field, and the custom adapters append specific strings to the `name` to indicate which adapter was used. This test suite is crucial for developers using Gson to understand and control the behavior of type adapters, ensuring that their JSON processing logic behaves as intended.
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
- `com.google.gson.JsonSerializationContext`
- `com.google.gson.JsonSerializer`
- `com.google.gson.TypeAdapter`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.Type`
- `org.junit.Test`


# Classes

---
### TypeAdapterPrecedenceTest<!-- {{#class:com.google.gson.functional.TypeAdapterPrecedenceTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `TypeAdapterPrecedenceTest` class is a test suite designed to verify the precedence and behavior of different type adapters in the Gson library when serializing and deserializing objects of the `Foo` class. It includes various test cases that register multiple type adapters and type hierarchy adapters for the same class and checks which adapter is used in different scenarios, ensuring that the most recently registered adapter takes precedence. The class uses the JUnit framework for testing and employs custom serializers, deserializers, and type adapters to demonstrate the precedence rules in Gson.
- **Methods**:
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testNonstreamingFollowedByNonstreaming`](#TypeAdapterPrecedenceTesttestNonstreamingFollowedByNonstreaming)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingFollowedByStreaming`](#TypeAdapterPrecedenceTesttestStreamingFollowedByStreaming)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testSerializeNonstreamingTypeAdapterFollowedByStreamingTypeAdapter`](#TypeAdapterPrecedenceTesttestSerializeNonstreamingTypeAdapterFollowedByStreamingTypeAdapter)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingFollowedByNonstreaming`](#TypeAdapterPrecedenceTesttestStreamingFollowedByNonstreaming)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingHierarchicalFollowedByNonstreaming`](#TypeAdapterPrecedenceTesttestStreamingHierarchicalFollowedByNonstreaming)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingFollowedByNonstreamingHierarchical`](#TypeAdapterPrecedenceTesttestStreamingFollowedByNonstreamingHierarchical)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingHierarchicalFollowedByNonstreamingHierarchical`](#TypeAdapterPrecedenceTesttestStreamingHierarchicalFollowedByNonstreamingHierarchical)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.testNonstreamingHierarchicalFollowedByNonstreaming`](#TypeAdapterPrecedenceTesttestNonstreamingHierarchicalFollowedByNonstreaming)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter`](#TypeAdapterPrecedenceTestnewTypeAdapter)

**Methods**

---
#### TypeAdapterPrecedenceTest\.testNonstreamingFollowedByNonstreaming<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testNonstreamingFollowedByNonstreaming}} -->
The method `testNonstreamingFollowedByNonstreaming` tests the precedence of non-streaming serializers and deserializers registered for the `Foo` class in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering two serializers and two deserializers for the `Foo` class, with the second serializer and deserializer expected to take precedence.
    - The method asserts that serializing a `Foo` object with the name "foo" results in the string "foo via serializer 2", indicating that the second serializer is used.
    - The method asserts that deserializing the string "foo" into a `Foo` object results in a `Foo` object with the name "foo via deserializer 2", indicating that the second deserializer is used.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.testStreamingFollowedByStreaming<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingFollowedByStreaming}} -->
The `testStreamingFollowedByStreaming` method tests the precedence of type adapters in Gson when multiple streaming type adapters are registered for the same class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering two type adapters for the `Foo` class, with the second adapter expected to take precedence.
    - The method asserts that serializing a `Foo` object with the name "foo" results in the JSON string "foo via type adapter 2", indicating that the second type adapter is used.
    - The method asserts that deserializing the string "foo" into a `Foo` object results in a `Foo` object with the name "foo via type adapter 2", again indicating that the second type adapter is used.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson type adapter precedence.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter`](#TypeAdapterPrecedenceTestnewTypeAdapter)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.testSerializeNonstreamingTypeAdapterFollowedByStreamingTypeAdapter<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testSerializeNonstreamingTypeAdapterFollowedByStreamingTypeAdapter}} -->
This method tests the precedence of a non-streaming type adapter followed by a streaming type adapter in Gson serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using GsonBuilder, registering a non-streaming serializer, a non-streaming deserializer, and a streaming type adapter for the Foo class.
    - The method asserts that serializing a Foo object with the name 'foo' using Gson results in the string '"foo via type adapter"'.
    - The method asserts that deserializing the string 'foo' into a Foo object using Gson results in a Foo object with the name 'foo via type adapter'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of Gson serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter`](#TypeAdapterPrecedenceTestnewTypeAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.testStreamingFollowedByNonstreaming<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingFollowedByNonstreaming}} -->
The method `testStreamingFollowedByNonstreaming` tests the precedence of streaming and non-streaming type adapters in Gson serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering a type adapter, a serializer, and a deserializer for the `Foo` class.
    - The method asserts that serializing a `Foo` object with the name "foo" results in the string "foo via serializer" using the registered serializer.
    - The method asserts that deserializing the string "foo" into a `Foo` object results in a `Foo` object with the name "foo via deserializer" using the registered deserializer.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter`](#TypeAdapterPrecedenceTestnewTypeAdapter)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.testStreamingHierarchicalFollowedByNonstreaming<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingHierarchicalFollowedByNonstreaming}} -->
The method tests the precedence of a streaming hierarchical type adapter followed by non-streaming type adapters for serialization and deserialization of a 'Foo' object using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using GsonBuilder, registering a type hierarchy adapter for 'Foo' with a type adapter, followed by a serializer and a deserializer for 'Foo'.
    - The method asserts that serializing a 'Foo' object with the name 'foo' results in the string '"foo via serializer"', indicating that the non-streaming serializer takes precedence over the streaming type adapter.
    - The method asserts that deserializing the string 'foo' into a 'Foo' object results in a 'Foo' object with the name 'foo via deserializer', indicating that the non-streaming deserializer takes precedence over the streaming type adapter.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson configuration.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter`](#TypeAdapterPrecedenceTestnewTypeAdapter)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.testStreamingFollowedByNonstreamingHierarchical<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingFollowedByNonstreamingHierarchical}} -->
The method `testStreamingFollowedByNonstreamingHierarchical` tests the precedence of type adapters and type hierarchy adapters in Gson serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering a type adapter and two type hierarchy adapters for the `Foo` class.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` object is called with a `Foo` object, and the result is asserted to be equal to a string indicating the use of the type adapter.
    - The [`fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of the `Gson` object is called with a JSON string and the `Foo` class, and the result's `name` field is asserted to be equal to a string indicating the use of the type adapter.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `Gson` object.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter`](#TypeAdapterPrecedenceTestnewTypeAdapter)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.testStreamingHierarchicalFollowedByNonstreamingHierarchical<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testStreamingHierarchicalFollowedByNonstreamingHierarchical}} -->
The method tests the precedence of streaming and non-streaming hierarchical type adapters in Gson serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using GsonBuilder, registering three type hierarchy adapters for the Foo class: a serializer, a deserializer, and a type adapter.
    - The method asserts that serializing a Foo object with the name 'foo' results in the JSON string '"foo via type adapter"', indicating that the type adapter takes precedence.
    - The method asserts that deserializing the string 'foo' into a Foo object results in a Foo object with the name 'foo via type adapter', again showing the precedence of the type adapter.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the Gson configuration.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter`](#TypeAdapterPrecedenceTestnewTypeAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.testNonstreamingHierarchicalFollowedByNonstreaming<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.testNonstreamingHierarchicalFollowedByNonstreaming}} -->
The method `testNonstreamingHierarchicalFollowedByNonstreaming` tests the precedence of non-streaming hierarchical and non-hierarchical type adapters in Gson serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering both hierarchical and non-hierarchical serializers and deserializers for the `Foo` class.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the `Gson` object is called with a `Foo` object, and the result is asserted to be equal to the expected serialized string using the non-hierarchical serializer.
    - The [`fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of the `Gson` object is called with a JSON string, and the resulting `Foo` object's `name` is asserted to be equal to the expected deserialized string using the non-hierarchical deserializer.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer`](#TypeAdapterPrecedenceTestnewSerializer)
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer`](#TypeAdapterPrecedenceTestnewDeserializer)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.newSerializer<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.newSerializer}} -->
The `newSerializer` method creates a new instance of a `JsonSerializer` for the `Foo` class that appends a given name to the serialized output.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `name`: A `String` that will be appended to the serialized output of a `Foo` object.
- **Control Flow**:
    - The method returns an anonymous instance of `JsonSerializer<Foo>`.
    - The `serialize` method of this `JsonSerializer` is overridden to concatenate the `name` field of the `Foo` object with the provided `name` argument, separated by ' via ', and return it as a `JsonPrimitive`.
- **Output**:
    - An instance of `JsonSerializer<Foo>` that serializes a `Foo` object by appending the provided name to its `name` field.
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.newDeserializer<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.newDeserializer}} -->
The `newDeserializer` method creates a new `JsonDeserializer` for the `Foo` class that appends a specified name to the deserialized string.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `name`: A `String` that will be appended to the deserialized `Foo` object's name.
- **Control Flow**:
    - The method returns an anonymous inner class that implements `JsonDeserializer<Foo>`.
    - The `deserialize` method of this anonymous class is overridden to create a new `Foo` object.
    - The `deserialize` method concatenates the JSON element's string value with ' via ' and the provided `name` argument to form the `Foo` object's name.
- **Output**:
    - A `JsonDeserializer<Foo>` that deserializes a JSON element into a `Foo` object with a modified name.
- **Functions called**:
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)


---
#### TypeAdapterPrecedenceTest\.newTypeAdapter<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.newTypeAdapter}} -->
The `newTypeAdapter` method creates a new `TypeAdapter` for the `Foo` class that appends a specified name to the serialized and deserialized string values.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `name`: A `String` that is appended to the `Foo` object's name during serialization and deserialization.
- **Control Flow**:
    - The method returns an anonymous `TypeAdapter` instance for the `Foo` class.
    - The `read` method of the `TypeAdapter` reads a string from the `JsonReader`, appends ' via ' and the provided `name`, and constructs a new `Foo` object with this modified string.
    - The `write` method of the `TypeAdapter` writes the `Foo` object's name, appended with ' via ' and the provided `name`, to the `JsonWriter`.
- **Output**:
    - A `TypeAdapter<Foo>` instance that customizes the serialization and deserialization of `Foo` objects by appending a specified name to their string representation.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest`](#TypeAdapterPrecedenceTest)  (Base Class)



---
### Foo<!-- {{#class:com.google.gson.functional.TypeAdapterPrecedenceTest.Foo}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Foo` class is a simple, private static class that encapsulates a single final field, `name`, which is a `String`. It is used within the `TypeAdapterPrecedenceTest` class to demonstrate serialization and deserialization behavior with different type adapters in the Gson library.
- **Fields**:
    - `name`: `String` A final String field that stores the name associated with the Foo instance.
- **Methods**:
    - [`com.google.gson.functional.TypeAdapterPrecedenceTest.Foo.Foo`](#FooFoo)

**Methods**

---
#### Foo\.Foo<!-- {{#callable:com.google.gson.functional.TypeAdapterPrecedenceTest.Foo.Foo}} -->
The `Foo` constructor initializes a `Foo` object with a given name.
- **Modifiers**: `private`
- **Inputs**:
    - `name`: A `String` representing the name to be assigned to the `Foo` object.
- **Control Flow**:
    - The constructor assigns the provided `name` to the `name` field of the `Foo` object.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `Foo` class.
- **See also**: [`com.google.gson.functional.TypeAdapterPrecedenceTest.Foo`](#TypeAdapterPrecedenceTest.Foo)  (Base Class)



