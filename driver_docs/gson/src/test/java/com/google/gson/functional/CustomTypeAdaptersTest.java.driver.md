# Purpose
The `CustomTypeAdaptersTest` Java file is a comprehensive suite of functional tests designed to validate the functionality of custom serializers and deserializers within the Gson library. This file is part of the `com.google.gson.functional` package and leverages the JUnit testing framework to ensure that custom type adapters are correctly implemented and invoked during the serialization and deserialization processes. The primary focus of these tests is to verify that custom logic can be applied to specific data types, such as `ClassWithCustomTypeConverter`, `BagOfPrimitives`, and [`Foo`](#FooFoo), among others, by registering custom `JsonSerializer` and `JsonDeserializer` implementations with a `GsonBuilder`.

The file contains a variety of test cases that cover different scenarios, including the serialization and deserialization of primitive types, nested objects, collections, and maps. It also tests the behavior of custom type adapters when dealing with null values and subclass hierarchies. Additionally, the file includes tests for ensuring that custom adapters are not erroneously applied to subclasses unless explicitly specified. The use of custom type adapters is demonstrated through the implementation of classes like `FooTypeAdapter`, `StringHolderTypeAdapter`, and `DateTypeAdapter`, which provide specific serialization and deserialization logic for their respective types. Overall, this file serves as a critical component in ensuring the robustness and flexibility of the Gson library's type adapter functionality.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.common.base.Splitter`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.InstanceCreator`
- `com.google.gson.JsonDeserializationContext`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSerializationContext`
- `com.google.gson.JsonSerializer`
- `com.google.gson.common.TestTypes.BagOfPrimitives`
- `com.google.gson.common.TestTypes.ClassWithCustomTypeConverter`
- `com.google.gson.reflect.TypeToken`
- `java.lang.reflect.Type`
- `java.util.Date`
- `java.util.HashMap`
- `java.util.HashSet`
- `java.util.List`
- `java.util.Map`
- `java.util.Set`
- `org.junit.Before`
- `org.junit.Ignore`
- `org.junit.Test`


# Classes

---
### CustomTypeAdaptersTest<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest}} -->
- **Modifiers**: `public`
- **Description**: The `CustomTypeAdaptersTest` class is a comprehensive suite of functional tests designed to validate the behavior of custom serializers and deserializers using the Gson library. It includes tests for various scenarios such as custom serialization and deserialization of specific classes, handling of nested objects, and ensuring that custom adapters are correctly applied or not applied to subclasses and primitive types. The class also tests the serialization and deserialization of collections and maps with custom adapters, and verifies that custom adapters are not invoked for null values. Additionally, it includes tests for registering type hierarchy adapters, particularly for handling `Date` objects.
- **Fields**:
    - `builder`: `GsonBuilder` A `GsonBuilder` instance used to configure and create `Gson` objects for testing custom type adapters.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.setUp`](#CustomTypeAdaptersTestsetUp)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomSerializers`](#CustomTypeAdaptersTesttestCustomSerializers)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomDeserializers`](#CustomTypeAdaptersTesttestCustomDeserializers)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.disable_testCustomSerializersOfSelf`](#CustomTypeAdaptersTestdisable_testCustomSerializersOfSelf)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.disable_testCustomDeserializersOfSelf`](#CustomTypeAdaptersTestdisable_testCustomDeserializersOfSelf)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomNestedSerializers`](#CustomTypeAdaptersTesttestCustomNestedSerializers)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomNestedDeserializers`](#CustomTypeAdaptersTesttestCustomNestedDeserializers)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomTypeAdapterDoesNotAppliesToSubClasses`](#CustomTypeAdaptersTesttestCustomTypeAdapterDoesNotAppliesToSubClasses)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomTypeAdapterAppliesToSubClassesSerializedAsBaseClass`](#CustomTypeAdaptersTesttestCustomTypeAdapterAppliesToSubClassesSerializedAsBaseClass)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.createGsonObjectWithFooTypeAdapter`](#CustomTypeAdaptersTestcreateGsonObjectWithFooTypeAdapter)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomSerializerInvokedForPrimitives`](#CustomTypeAdaptersTesttestCustomSerializerInvokedForPrimitives)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomDeserializerInvokedForPrimitives`](#CustomTypeAdaptersTesttestCustomDeserializerInvokedForPrimitives)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomByteArraySerializer`](#CustomTypeAdaptersTesttestCustomByteArraySerializer)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomByteArrayDeserializerAndInstanceCreator`](#CustomTypeAdaptersTesttestCustomByteArrayDeserializerAndInstanceCreator)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForCollectionElementSerializationWithType`](#CustomTypeAdaptersTesttestCustomAdapterInvokedForCollectionElementSerializationWithType)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForCollectionElementSerialization`](#CustomTypeAdaptersTesttestCustomAdapterInvokedForCollectionElementSerialization)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForCollectionElementDeserialization`](#CustomTypeAdaptersTesttestCustomAdapterInvokedForCollectionElementDeserialization)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForMapElementSerializationWithType`](#CustomTypeAdaptersTesttestCustomAdapterInvokedForMapElementSerializationWithType)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForMapElementSerialization`](#CustomTypeAdaptersTesttestCustomAdapterInvokedForMapElementSerialization)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForMapElementDeserialization`](#CustomTypeAdaptersTesttestCustomAdapterInvokedForMapElementDeserialization)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testEnsureCustomSerializerNotInvokedForNullValues`](#CustomTypeAdaptersTesttestEnsureCustomSerializerNotInvokedForNullValues)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testEnsureCustomDeserializerNotInvokedForNullValues`](#CustomTypeAdaptersTesttestEnsureCustomDeserializerNotInvokedForNullValues)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.testRegisterHierarchyAdapterForDate`](#CustomTypeAdaptersTesttestRegisterHierarchyAdapterForDate)

**Methods**

---
#### CustomTypeAdaptersTest\.setUp<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.setUp}} -->
The `setUp` method initializes a `GsonBuilder` instance before each test is executed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with `@Before`, indicating it runs before each test method in the class.
    - A new instance of `GsonBuilder` is assigned to the `builder` field.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomSerializers<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomSerializers}} -->
The `testCustomSerializers` method tests the serialization of a `ClassWithCustomTypeConverter` object using a custom serializer registered with Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using a `GsonBuilder` with a custom `JsonSerializer` registered for `ClassWithCustomTypeConverter`.
    - The custom serializer converts an instance of `ClassWithCustomTypeConverter` into a `JsonObject` with properties `bag` set to 5 and `value` set to 25.
    - A new instance of `ClassWithCustomTypeConverter` is created.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` object is used to serialize the `ClassWithCustomTypeConverter` instance.
    - An assertion checks that the serialized JSON string is equal to `{"bag":5,"value":25}`.
- **Output**:
    - The method does not return any value, but it asserts that the serialized JSON string matches the expected output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomDeserializers<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomDeserializers}} -->
The `testCustomDeserializers` method tests the custom deserialization of a JSON string into an instance of `ClassWithCustomTypeConverter` using a registered `JsonDeserializer`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, with a custom `JsonDeserializer` registered for `ClassWithCustomTypeConverter`.
    - The custom deserializer extracts the 'bag' value from the JSON object and uses it to create a new `ClassWithCustomTypeConverter` instance.
    - A JSON string `{"bag":5,"value":25}` is deserialized into a `ClassWithCustomTypeConverter` object using the `Gson` instance.
    - An assertion checks that the `intValue` of the `BagOfPrimitives` object within the deserialized `ClassWithCustomTypeConverter` is equal to 5.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonPrimitive.getAsInt`](../../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.disable\_testCustomSerializersOfSelf<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.disable_testCustomSerializersOfSelf}} -->
The `disable_testCustomSerializersOfSelf` method tests the equality of JSON serialization between a custom Gson object and a basic Gson object for a `Foo` object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a custom Gson object using `createGsonObjectWithFooTypeAdapter()` which registers a type adapter for `Foo` class.
    - Create a basic Gson object using the default constructor.
    - Instantiate a `Foo` object with specific values (1 and 2L).
    - Serialize the `Foo` object to JSON using both the custom Gson and the basic Gson.
    - Assert that the JSON strings produced by both Gson objects are equal.
- **Output**:
    - The method does not return any value; it performs an assertion to check the equality of two JSON strings.
- **Functions called**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.createGsonObjectWithFooTypeAdapter`](#CustomTypeAdaptersTestcreateGsonObjectWithFooTypeAdapter)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.disable\_testCustomDeserializersOfSelf<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.disable_testCustomDeserializersOfSelf}} -->
The `disable_testCustomDeserializersOfSelf` method tests the deserialization of a `Foo` object using a custom deserializer and compares it to the expected values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object with a custom `Foo` type adapter is created using `createGsonObjectWithFooTypeAdapter()`.
    - A basic `Gson` object is instantiated without any custom type adapters.
    - A `Foo` object `expectedFoo` is created with specific key and value.
    - The `expectedFoo` object is serialized into a JSON string using the basic `Gson` object.
    - The JSON string is deserialized back into a `Foo` object `newFooObject` using the custom `Gson` object.
    - Assertions are made to ensure that the `key` and `value` of `newFooObject` match those of `expectedFoo`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.createGsonObjectWithFooTypeAdapter`](#CustomTypeAdaptersTestcreateGsonObjectWithFooTypeAdapter)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomNestedSerializers<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomNestedSerializers}} -->
The `testCustomNestedSerializers` method tests the serialization of a `ClassWithCustomTypeConverter` object using a custom serializer for the `BagOfPrimitives` class, ensuring the JSON output matches the expected format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, with a custom `JsonSerializer` registered for the `BagOfPrimitives` class that always returns a `JsonPrimitive` with the value `6`.
    - A `ClassWithCustomTypeConverter` object named `target` is instantiated.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` object is called with `target` as the argument, converting it to a JSON string.
    - An assertion checks that the resulting JSON string is equal to `{"bag":6,"value":10}`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON serialization output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomNestedDeserializers<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomNestedDeserializers}} -->
The `testCustomNestedDeserializers` method tests the deserialization of a JSON string into a `ClassWithCustomTypeConverter` object using a custom deserializer for the `BagOfPrimitives` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using a `GsonBuilder` with a custom `JsonDeserializer` registered for the `BagOfPrimitives` class.
    - The custom deserializer converts a JSON integer into a `BagOfPrimitives` object with the integer value set for both integer fields and default values for other fields.
    - A JSON string `{"bag":7,"value":25}` is deserialized into a `ClassWithCustomTypeConverter` object using the `Gson` instance.
    - An assertion checks that the `intValue` of the `BagOfPrimitives` object within the deserialized `ClassWithCustomTypeConverter` is equal to 7.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonPrimitive.getAsInt`](../../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomTypeAdapterDoesNotAppliesToSubClasses<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomTypeAdapterDoesNotAppliesToSubClasses}} -->
The method `testCustomTypeAdapterDoesNotAppliesToSubClasses` tests that a custom type adapter registered for a base class does not apply to its subclass when serializing objects using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering a custom `JsonSerializer` for the `Base` class that serializes the `baseValue` property.
    - An instance of `Base` is created and serialized to JSON using the `Gson` object, and the resulting JSON is asserted to contain the property `value`.
    - An instance of `Derived` (a subclass of `Base`) is created and serialized to JSON using the same `Gson` object, and the resulting JSON is asserted to contain the property `derivedValue`, indicating that the custom serializer for `Base` does not apply to `Derived`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom type adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomTypeAdapterAppliesToSubClassesSerializedAsBaseClass<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomTypeAdapterAppliesToSubClassesSerializedAsBaseClass}} -->
This method tests if a custom type adapter for a base class is applied when serializing a subclass as the base class using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created with a custom type adapter registered for the Base class, which serializes the baseValue property into a JSON object.
    - An instance of the Base class is created and serialized to JSON, and the resulting JSON is asserted to contain the 'value' property.
    - An instance of the Derived class is created, cast to the Base class, and serialized to JSON, and the resulting JSON is asserted to contain the 'value' property and not contain the 'derivedValue' property.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom type adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.createGsonObjectWithFooTypeAdapter<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.createGsonObjectWithFooTypeAdapter}} -->
The method `createGsonObjectWithFooTypeAdapter` creates and returns a `Gson` object configured with a custom type adapter for the `Foo` class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - A new `GsonBuilder` instance is created.
    - The [`registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter) method is called on the `GsonBuilder` instance to register a custom type adapter for the `Foo` class, using `FooTypeAdapter`.
    - The [`create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate) method is called on the `GsonBuilder` instance to build and return a `Gson` object.
- **Output**:
    - A `Gson` object configured with a custom type adapter for the `Foo` class is returned.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomSerializerInvokedForPrimitives<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomSerializerInvokedForPrimitives}} -->
The method `testCustomSerializerInvokedForPrimitives` tests the invocation of a custom serializer for primitive boolean types using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, with a custom serializer registered for the primitive `boolean` type, which converts `true` to `1` and `false` to `0`.
    - The method asserts that serializing `true` as a primitive `boolean` results in the string "1".
    - The method asserts that serializing `true` as a `Boolean` object results in the string "true".
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom serializer.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomDeserializerInvokedForPrimitives<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomDeserializerInvokedForPrimitives}} -->
The method `testCustomDeserializerInvokedForPrimitives` tests the functionality of a custom deserializer for primitive boolean values using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, with a custom deserializer registered for the `boolean.class` type.
    - The custom deserializer converts a JSON integer to a boolean by checking if the integer is not zero.
    - The method asserts that deserializing the JSON string "1" to a boolean results in `Boolean.TRUE`.
    - The method asserts that deserializing the JSON string "true" to a `Boolean` object also results in `Boolean.TRUE`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom deserializer.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.JsonElement.getAsInt`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsInt)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomByteArraySerializer<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomByteArraySerializer}} -->
The method `testCustomByteArraySerializer` tests the serialization of a byte array into a JSON string using a custom serializer in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, with a custom `JsonSerializer` registered for `byte[]` type.
    - The custom serializer converts a byte array into a `JsonPrimitive` by appending each byte as a character to a `StringBuilder`.
    - A byte array `data` is defined with values from 0 to 9.
    - The byte array is serialized to a JSON string using the `Gson` object.
    - An assertion checks that the resulting JSON string is equal to the string "0123456789".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.append`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectionappend)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomByteArrayDeserializerAndInstanceCreator<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomByteArrayDeserializerAndInstanceCreator}} -->
The method `testCustomByteArrayDeserializerAndInstanceCreator` tests the deserialization of a JSON string into a byte array using a custom deserializer in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` is instantiated and a custom `JsonDeserializer` for `byte[]` is registered, which converts a JSON string into a byte array by parsing each character as a byte.
    - A `Gson` object is created from the `GsonBuilder`.
    - A JSON string `"'0123456789'"` is defined and deserialized into a `byte[]` using the `Gson` object.
    - An expected byte array `{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}` is defined.
    - A loop iterates over the deserialized byte array, asserting that each element matches the corresponding element in the expected array.
- **Output**:
    - The method does not return a value; it performs assertions to verify that the deserialized byte array matches the expected byte array.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomAdapterInvokedForCollectionElementSerializationWithType<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForCollectionElementSerializationWithType}} -->
This method tests if a custom type adapter is correctly invoked for serializing elements of a collection with a specified type.
- **Modifiers**: `@Test`, `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using GsonBuilder, registering a custom type adapter for the StringHolder class.
    - A Type object representing a Set of StringHolder is created using TypeToken.
    - A StringHolder object is instantiated with the values "Jacob" and "Tomaw".
    - A HashSet is created and the StringHolder object is added to it.
    - The set is serialized to JSON using the Gson object and the specified Type.
    - An assertion checks if the resulting JSON string contains the expected serialized form "Jacob:Tomaw".
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correct behavior of the custom adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomAdapterInvokedForCollectionElementSerialization<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForCollectionElementSerialization}} -->
This method tests if a custom type adapter is correctly invoked for serializing elements of a collection using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using GsonBuilder, registering a custom type adapter for the StringHolder class.
    - A StringHolder object is instantiated with the values 'Jacob' and 'Tomaw'.
    - A HashSet is created and the StringHolder object is added to it.
    - The HashSet is serialized to JSON using the Gson object.
    - An assertion checks if the resulting JSON string contains the expected serialized format 'Jacob:Tomaw'.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correct behavior of the custom adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomAdapterInvokedForCollectionElementDeserialization<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForCollectionElementDeserialization}} -->
This method tests whether a custom type adapter is correctly invoked for deserializing elements of a collection.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using GsonBuilder, registering a custom type adapter for the StringHolder class.
    - A TypeToken is used to define the type of a Set containing StringHolder objects.
    - The Gson object is used to deserialize a JSON string representing a set of StringHolder objects.
    - Assertions are made to verify that the set contains exactly one StringHolder object and that its fields are correctly populated.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.size`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructorsize)
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.iterator`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoriterator)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomAdapterInvokedForMapElementSerializationWithType<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForMapElementSerializationWithType}} -->
This method tests if a custom type adapter is correctly invoked for serializing map elements of type `StringHolder` with a specified type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering a custom type adapter `StringHolderTypeAdapter` for the `StringHolder` class.
    - A `Type` object `mapType` is created to represent a map with `String` keys and `StringHolder` values.
    - A `StringHolder` object `holder` is instantiated with the values "Jacob" and "Tomaw".
    - A `Map` object `mapOfHolders` is created and the `holder` is added to it with the key "foo".
    - The map is serialized to a JSON string using the `Gson` object and the specified `mapType`.
    - An assertion checks that the resulting JSON string contains the expected serialized form of the map element, "foo":"Jacob:Tomaw".
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correct serialization of a map element using a custom adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomAdapterInvokedForMapElementSerialization<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForMapElementSerialization}} -->
This method tests if a custom type adapter is correctly invoked for serializing map elements of type `StringHolder` using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder`, registering a custom type adapter `StringHolderTypeAdapter` for the `StringHolder` class.
    - A `StringHolder` object is instantiated with the values "Jacob" and "Tomaw".
    - A `Map` is created and the `StringHolder` object is added to it with the key "foo".
    - The map is serialized to JSON using the `Gson` object.
    - An assertion checks that the resulting JSON string contains the expected serialized form of the `StringHolder` object, "foo":"Jacob:Tomaw".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correct behavior of the custom adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testCustomAdapterInvokedForMapElementDeserialization<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testCustomAdapterInvokedForMapElementDeserialization}} -->
The method tests if a custom adapter is correctly invoked for deserializing map elements into `StringHolder` objects using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created with a custom type adapter registered for `StringHolder` class using `GsonBuilder`.
    - A `Type` object representing a map with `String` keys and `StringHolder` values is created using `TypeToken`.
    - The JSON string "{'foo':'Jacob:Tomaw'}" is deserialized into a `Map<String, StringHolder>` using the `Gson` object and the specified `Type`.
    - An assertion checks that the size of the resulting map is 1.
    - The `StringHolder` object associated with the key 'foo' is retrieved from the map.
    - Assertions verify that the `part1` and `part2` fields of the `StringHolder` object are 'Jacob' and 'Tomaw', respectively.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.size`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructorsize)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testEnsureCustomSerializerNotInvokedForNullValues<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testEnsureCustomSerializerNotInvokedForNullValues}} -->
This method tests that a custom serializer for the `DataHolder` class is not invoked when serializing a `DataHolderWrapper` object containing a non-null `DataHolder`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using a `GsonBuilder`, which registers a custom serializer for the `DataHolder` class using `DataHolderSerializer`.
    - A `DataHolderWrapper` object is instantiated with a `DataHolder` containing the string "abc".
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` object is called to serialize the `DataHolderWrapper` object into a JSON string.
    - An assertion is made to check that the resulting JSON string is equal to `{"wrappedData":{"myData":"abc"}}`, ensuring the custom serializer is not invoked for null values.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testEnsureCustomDeserializerNotInvokedForNullValues<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testEnsureCustomDeserializerNotInvokedForNullValues}} -->
This method tests that a custom deserializer is not invoked when a JSON field is null.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using a GsonBuilder, which registers a custom deserializer for the DataHolder class.
    - A JSON string with a null value for the 'wrappedData' field is defined.
    - The JSON string is deserialized into a DataHolderWrapper object using the Gson instance.
    - An assertion checks that the 'wrappedData' field of the resulting DataHolderWrapper object is null.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)


---
#### CustomTypeAdaptersTest\.testRegisterHierarchyAdapterForDate<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.testRegisterHierarchyAdapterForDate}} -->
The method `testRegisterHierarchyAdapterForDate` tests the serialization and deserialization of `Date` and `java.sql.Date` objects using a custom type hierarchy adapter in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder` with a registered type hierarchy adapter for `Date` using `DateTypeAdapter`.
    - The method asserts that serializing a `Date` object with time 0 results in the JSON string "0".
    - The method asserts that serializing a `java.sql.Date` object with time 0 also results in the JSON string "0".
    - The method asserts that deserializing the JSON string "0" into a `Date` object results in a `Date` object with time 0.
    - The method asserts that deserializing the JSON string "0" into a `java.sql.Date` object results in a `java.sql.Date` object with time 0.
- **Output**:
    - The method does not return any value; it uses assertions to verify the correctness of serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest`](#CustomTypeAdaptersTest)  (Base Class)



---
### Base<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.Base}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Base` class is a simple static inner class with a single integer field `baseValue` initialized to 2, serving as a base class for potential inheritance in the context of custom serialization and deserialization tests.
- **Fields**:
    - `baseValue`: `int` An integer field initialized to 2, representing a base value for the class.


---
### Derived<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.Derived}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Derived` class is a private static inner class that extends the `Base` class, adding an additional integer field `derivedValue` initialized to 3. It is used to demonstrate the behavior of custom type adapters in serialization and deserialization processes, particularly in the context of subclassing and type hierarchy in the `CustomTypeAdaptersTest` class.
- **Fields**:
    - `derivedValue`: `int` An integer field initialized to 3, used to demonstrate subclass serialization behavior.
- **Extends/Implements**:
    - [`com.google.gson.functional.UncategorizedTest.Base`](UncategorizedTest.java.driver.md#Base)


---
### Foo<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.Foo}} -->
- **Modifiers**: `public`, `static`
- **Description**: The `Foo` class is a simple data structure that encapsulates two fields: an integer `key` and a long `value`, providing constructors for initializing these fields with default or specified values.
- **Fields**:
    - `key`: `int` An integer field that holds a key value.
    - `value`: `long` A long field that holds a value associated with the key.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.Foo.Foo`](#FooFoo)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.Foo.Foo`](#FooFoo)

**Methods**

---
#### Foo\.Foo<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.Foo.Foo}} -->
The `Foo` constructor initializes a `Foo` object with default values of 0 for both its `key` and `value` fields.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor calls another constructor of the same class `Foo` with parameters `0` and `0L`.
- **Output**:
    - A new instance of the `Foo` class with `key` set to 0 and `value` set to 0L.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.Foo`](#CustomTypeAdaptersTest.Foo)  (Base Class)


---
#### Foo\.Foo<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.Foo.Foo}} -->
The `Foo` constructor initializes a `Foo` object with specified `key` and `value` attributes.
- **Modifiers**: `public`
- **Inputs**:
    - `key`: An integer representing the key to be assigned to the `Foo` object.
    - `value`: A long integer representing the value to be assigned to the `Foo` object.
- **Control Flow**:
    - The constructor assigns the provided `key` to the `key` field of the `Foo` object.
    - The constructor assigns the provided `value` to the `value` field of the `Foo` object.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `Foo` class.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.Foo`](#CustomTypeAdaptersTest.Foo)  (Base Class)



---
### FooTypeAdapter<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.FooTypeAdapter}} -->
- **Modifiers**: `public`, `static`, `final`
- **Description**: The `FooTypeAdapter` class is a custom type adapter for the `Foo` class, implementing both `JsonSerializer` and `JsonDeserializer` interfaces to facilitate the serialization and deserialization of `Foo` objects using Gson. It provides methods to convert `Foo` objects to and from JSON representation, leveraging the context provided by Gson for the actual conversion process.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.FooTypeAdapter.deserialize`](#FooTypeAdapterdeserialize)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.FooTypeAdapter.serialize`](#FooTypeAdapterserialize)

**Methods**

---
#### FooTypeAdapter\.deserialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.FooTypeAdapter.deserialize}} -->
The [`deserialize`](../../../../../../main/java/com/google/gson/JsonDeserializationContext.java.driver.md#JsonDeserializationContextdeserialize) method uses the provided `JsonDeserializationContext` to convert a `JsonElement` into an object of the specified type.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the object to be deserialized into.
    - `context`: A `JsonDeserializationContext` used to perform the deserialization.
- **Control Flow**:
    - The method calls the [`deserialize`](../../../../../../main/java/com/google/gson/JsonDeserializationContext.java.driver.md#JsonDeserializationContextdeserialize) method of the `JsonDeserializationContext` object, passing the `json` and `typeOfT` as arguments.
    - The result of the `context.deserialize` call is returned.
- **Output**:
    - Returns an instance of type `Foo` that is deserialized from the provided JSON data.
- **Functions called**:
    - [`com.google.gson.JsonDeserializationContext.deserialize`](../../../../../../main/java/com/google/gson/JsonDeserializationContext.java.driver.md#JsonDeserializationContextdeserialize)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.FooTypeAdapter`](#CustomTypeAdaptersTest.FooTypeAdapter)  (Base Class)


---
#### FooTypeAdapter\.serialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.FooTypeAdapter.serialize}} -->
The [`serialize`](../../../../../../main/java/com/google/gson/JsonSerializationContext.java.driver.md#JsonSerializationContextserialize) method serializes a `Foo` object into a `JsonElement` using the provided `JsonSerializationContext`.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The `Foo` object to be serialized.
    - `typeOfSrc`: The specific type of the source object, `Foo`, to be serialized.
    - `context`: The `JsonSerializationContext` used to serialize the `Foo` object.
- **Control Flow**:
    - The method calls the [`serialize`](../../../../../../main/java/com/google/gson/JsonSerializationContext.java.driver.md#JsonSerializationContextserialize) method of the `JsonSerializationContext` with the `src` and `typeOfSrc` as arguments.
- **Output**:
    - A `JsonElement` representing the serialized form of the `Foo` object.
- **Functions called**:
    - [`com.google.gson.JsonSerializationContext.serialize`](../../../../../../main/java/com/google/gson/JsonSerializationContext.java.driver.md#JsonSerializationContextserialize)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.FooTypeAdapter`](#CustomTypeAdaptersTest.FooTypeAdapter)  (Base Class)



---
### StringHolder<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.StringHolder}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `StringHolder` class is a utility class designed to hold two string parts, `part1` and `part2`, which can be initialized either by passing a single string with parts separated by a colon or by directly providing the two parts as separate strings.
- **Fields**:
    - `part1`: `String` Holds the first part of the string.
    - `part2`: `String` Holds the second part of the string.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolder.StringHolder`](#StringHolderStringHolder)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolder.StringHolder`](#StringHolderStringHolder)

**Methods**

---
#### StringHolder\.StringHolder<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.StringHolder.StringHolder}} -->
The `StringHolder` constructor initializes an instance by splitting a given string on the colon character and assigning the resulting parts to two instance variables.
- **Modifiers**: `public`
- **Inputs**:
    - `string`: A string input that is expected to contain two parts separated by a colon (':').
- **Control Flow**:
    - The method uses the `Splitter` class from the Guava library to split the input string on the colon character (':').
    - The resulting list of strings is stored in the variable `parts`.
    - The first element of the list (`parts.get(0)`) is assigned to the instance variable `part1`.
    - The second element of the list (`parts.get(1)`) is assigned to the instance variable `part2`.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of the `StringHolder` class.
- **Functions called**:
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolder`](#CustomTypeAdaptersTest.StringHolder)  (Base Class)


---
#### StringHolder\.StringHolder<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.StringHolder.StringHolder}} -->
The `StringHolder` constructor initializes an instance with two string parts, `part1` and `part2`, provided as arguments.
- **Modifiers**: `public`
- **Inputs**:
    - `part1`: The first part of the string to be held by the `StringHolder` instance.
    - `part2`: The second part of the string to be held by the `StringHolder` instance.
- **Control Flow**:
    - The constructor assigns the value of `part1` to the instance variable `this.part1`.
    - The constructor assigns the value of `part2` to the instance variable `this.part2`.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of the `StringHolder` class.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolder`](#CustomTypeAdaptersTest.StringHolder)  (Base Class)



---
### StringHolderTypeAdapter<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `StringHolderTypeAdapter` class is a custom type adapter for the `StringHolder` class, implementing the `JsonSerializer`, `JsonDeserializer`, and `InstanceCreator` interfaces to facilitate the serialization and deserialization of `StringHolder` objects to and from JSON using the Gson library. It provides methods to create instances of `StringHolder`, serialize `StringHolder` objects into JSON format, and deserialize JSON back into `StringHolder` objects, handling the conversion of the `part1` and `part2` fields of `StringHolder` into a single string separated by a colon.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter.createInstance`](#StringHolderTypeAdaptercreateInstance)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter.deserialize`](#StringHolderTypeAdapterdeserialize)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter.serialize`](#StringHolderTypeAdapterserialize)

**Methods**

---
#### StringHolderTypeAdapter\.createInstance<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter.createInstance}} -->
The `createInstance` method creates and returns a new `StringHolder` object initialized with a default string value.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: A `Type` object representing the type information for which an instance is to be created.
- **Control Flow**:
    - The method creates a new `StringHolder` object by calling its constructor with the string "unknown:thing".
    - The method returns the newly created `StringHolder` object.
- **Output**:
    - A `StringHolder` object initialized with the string "unknown:thing".
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter`](#CustomTypeAdaptersTest.StringHolderTypeAdapter)  (Base Class)


---
#### StringHolderTypeAdapter\.deserialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter.deserialize}} -->
The `deserialize` method converts a `JsonElement` into a `StringHolder` object by extracting the string value from the JSON element.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: A `JsonElement` representing the JSON data to be deserialized.
    - `type`: A `Type` object representing the type of the object to deserialize to, though it is not used in this method.
    - `context`: A `JsonDeserializationContext` that provides the context for deserialization, though it is not used in this method.
- **Control Flow**:
    - The method extracts the string value from the `JsonElement` using `src.getAsString()`.
    - A new `StringHolder` object is created using the extracted string value.
    - The `StringHolder` object is returned.
- **Output**:
    - A `StringHolder` object initialized with the string extracted from the `JsonElement`.
- **Functions called**:
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter`](#CustomTypeAdaptersTest.StringHolderTypeAdapter)  (Base Class)


---
#### StringHolderTypeAdapter\.serialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter.serialize}} -->
The `serialize` method converts a `StringHolder` object into a `JsonElement` by concatenating its `part1` and `part2` fields with a colon separator.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: A `StringHolder` object containing two string parts, `part1` and `part2`, to be serialized.
    - `typeOfSrc`: The `Type` of the source object, which is `StringHolder` in this context.
    - `context`: A `JsonSerializationContext` that can be used for custom serialization of complex objects.
- **Control Flow**:
    - Concatenate the `part1` and `part2` fields of the `StringHolder` object with a colon `:` separator to form a single string.
    - Create a new `JsonPrimitive` object using the concatenated string.
- **Output**:
    - Returns a `JsonPrimitive` object representing the serialized form of the `StringHolder` object as a JSON element.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.StringHolderTypeAdapter`](#CustomTypeAdaptersTest.StringHolderTypeAdapter)  (Base Class)



---
### DataHolder<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.DataHolder}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `DataHolder` class is a simple container for a single `String` field named `data`, which is initialized through the constructor and is immutable due to the `final` keyword.
- **Fields**:
    - `data`: `String` A final String field that holds the data passed during the instantiation of the DataHolder object.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolder.DataHolder`](#DataHolderDataHolder)

**Methods**

---
#### DataHolder\.DataHolder<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.DataHolder.DataHolder}} -->
The `DataHolder` constructor initializes a new instance of the `DataHolder` class with a specified string data.
- **Modifiers**: `public`
- **Inputs**:
    - `data`: A `String` representing the data to be held by the `DataHolder` instance.
- **Control Flow**:
    - The constructor assigns the input `data` to the instance variable `this.data`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `DataHolder` class.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolder`](#CustomTypeAdaptersTest.DataHolder)  (Base Class)



---
### DataHolderWrapper<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.DataHolderWrapper}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `DataHolderWrapper` class is a simple container that wraps an instance of the `DataHolder` class, providing a way to encapsulate the `DataHolder` object within another object. This class is designed to hold a final reference to a `DataHolder` instance, ensuring that the wrapped data cannot be changed once the `DataHolderWrapper` is constructed.
- **Fields**:
    - `wrappedData`: `DataHolder` A final field that holds the reference to the wrapped `DataHolder` instance.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolderWrapper.DataHolderWrapper`](#DataHolderWrapperDataHolderWrapper)

**Methods**

---
#### DataHolderWrapper\.DataHolderWrapper<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.DataHolderWrapper.DataHolderWrapper}} -->
The `DataHolderWrapper` constructor initializes a new instance by wrapping a given `DataHolder` object.
- **Modifiers**: `public`
- **Inputs**:
    - `data`: A `DataHolder` object that is to be wrapped by the `DataHolderWrapper`.
- **Control Flow**:
    - Assigns the provided `DataHolder` object to the `wrappedData` field of the `DataHolderWrapper` instance.
- **Output**:
    - A new instance of `DataHolderWrapper` with the `wrappedData` field set to the provided `DataHolder` object.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolderWrapper`](#CustomTypeAdaptersTest.DataHolderWrapper)  (Base Class)



---
### DataHolderSerializer<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.DataHolderSerializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `DataHolderSerializer` class is a private static class that implements the `JsonSerializer` interface for the `DataHolder` type, providing a custom serialization mechanism to convert `DataHolder` objects into JSON format by adding a property named "myData" with the value of the `data` field from the `DataHolder` instance.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolderSerializer.serialize`](#DataHolderSerializerserialize)

**Methods**

---
#### DataHolderSerializer\.serialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.DataHolderSerializer.serialize}} -->
The `serialize` method converts a `DataHolder` object into a JSON representation with a single property 'myData' containing the data from the `DataHolder`.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The `DataHolder` object to be serialized into JSON.
    - `typeOfSrc`: The specific type of the source object, which is `DataHolder` in this context.
    - `context`: The `JsonSerializationContext` used for the serialization process, allowing for custom serialization logic.
- **Control Flow**:
    - Create a new `JsonObject` instance named `obj`.
    - Add a property to `obj` with the key 'myData' and the value being the `data` field from the `src` `DataHolder` object.
    - Return the `JsonObject` `obj` as the serialized JSON representation of the `DataHolder`.
- **Output**:
    - A `JsonElement` representing the serialized form of the `DataHolder` object, specifically a `JsonObject` with a single property 'myData'.
- **Functions called**:
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolderSerializer`](#CustomTypeAdaptersTest.DataHolderSerializer)  (Base Class)



---
### DataHolderDeserializer<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.DataHolderDeserializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `DataHolderDeserializer` class is a private static inner class that implements the `JsonDeserializer` interface for the `DataHolder` type, providing custom deserialization logic to convert JSON data into `DataHolder` objects. It checks for the presence of a "data" field in the JSON object and assigns its value to the `DataHolder` instance, or assigns `null` if the field is absent or null.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolderDeserializer.deserialize`](#DataHolderDeserializerdeserialize)

**Methods**

---
#### DataHolderDeserializer\.deserialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.DataHolderDeserializer.deserialize}} -->
The `deserialize` method converts a JSON element into a `DataHolder` object by extracting a string value from the JSON if available.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the object to deserialize to, though it is not used in this method.
    - `context`: A `JsonDeserializationContext` that provides the context for deserialization, though it is not used in this method.
- **Control Flow**:
    - Convert the input `JsonElement` to a `JsonObject`.
    - Retrieve the 'data' element from the `JsonObject`.
    - Check if the 'data' element is null or a JSON null; if so, return a new `DataHolder` with null data.
    - If the 'data' element is not null, extract its string value and return a new `DataHolder` with this string.
- **Output**:
    - Returns a `DataHolder` object containing the string value extracted from the 'data' element of the JSON, or null if the 'data' element is absent or null.
- **Functions called**:
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.isJsonNull`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementisJsonNull)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.DataHolderDeserializer`](#CustomTypeAdaptersTest.DataHolderDeserializer)  (Base Class)



---
### DateTypeAdapter<!-- {{#class:com.google.gson.functional.CustomTypeAdaptersTest.DateTypeAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `DateTypeAdapter` class is a private static inner class that implements both `JsonSerializer<Date>` and `JsonDeserializer<Date>` interfaces to provide custom serialization and deserialization logic for `Date` objects in JSON format. It converts `Date` objects to their long representation (milliseconds since epoch) for serialization and reconstructs `Date` objects from long values during deserialization, handling both `java.util.Date` and `java.sql.Date` types.
- **Methods**:
    - [`com.google.gson.functional.CustomTypeAdaptersTest.DateTypeAdapter.deserialize`](#DateTypeAdapterdeserialize)
    - [`com.google.gson.functional.CustomTypeAdaptersTest.DateTypeAdapter.serialize`](#DateTypeAdapterserialize)

**Methods**

---
#### DateTypeAdapter\.deserialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.DateTypeAdapter.deserialize}} -->
The `deserialize` method converts a JSON element into a `Date` or `java.sql.Date` object based on the specified type.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object indicating the type of the object to be deserialized, either `Date.class` or `java.sql.Date.class`.
    - `context`: A `JsonDeserializationContext` that provides the context for deserialization.
- **Control Flow**:
    - Check if `typeOfT` is equal to `Date.class`.
    - If true, create and return a new `Date` object using the long value obtained from `json.getAsLong()`.
    - If false, create and return a new `java.sql.Date` object using the long value obtained from `json.getAsLong()`.
- **Output**:
    - Returns a `Date` object if `typeOfT` is `Date.class`, otherwise returns a `java.sql.Date` object.
- **Functions called**:
    - [`com.google.gson.JsonElement.getAsLong`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsLong)
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.DateTypeAdapter`](#CustomTypeAdaptersTest.DateTypeAdapter)  (Base Class)


---
#### DateTypeAdapter\.serialize<!-- {{#callable:com.google.gson.functional.CustomTypeAdaptersTest.DateTypeAdapter.serialize}} -->
The `serialize` method converts a `Date` object into a `JsonPrimitive` containing its time in milliseconds.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The `Date` object to be serialized.
    - `typeOfSrc`: The specific type of the source object, which is `Date` in this context.
    - `context`: The `JsonSerializationContext` that can be used for serialization of complex objects.
- **Control Flow**:
    - The method takes a `Date` object as input and calls its `getTime()` method to retrieve the time in milliseconds since the epoch.
    - It then creates a new `JsonPrimitive` object using this time value.
- **Output**:
    - A `JsonElement` representing the serialized form of the `Date` object, specifically a `JsonPrimitive` containing the time in milliseconds.
- **See also**: [`com.google.gson.functional.CustomTypeAdaptersTest.DateTypeAdapter`](#CustomTypeAdaptersTest.DateTypeAdapter)  (Base Class)



