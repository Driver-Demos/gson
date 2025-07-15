# Purpose
The `JsonAdapterAnnotationOnFieldsTest` Java file is a comprehensive suite of functional tests designed to validate the behavior of the `@JsonAdapter` annotation in the Gson library. This file is part of the `com.google.gson.functional` package and focuses on testing how the `@JsonAdapter` annotation affects serialization and deserialization processes when applied to fields. The tests cover various scenarios, including precedence rules between class-level and field-level annotations, the interaction between registered type adapters and those specified by annotations, and the behavior of custom type adapters and factories. The file also explores the use of `JsonSerializer` and `JsonDeserializer` interfaces as `@JsonAdapter` values, ensuring that custom serialization and deserialization logic is correctly applied.

The file is structured around multiple test cases, each encapsulated in a method annotated with `@Test`, which is part of the JUnit testing framework. These tests utilize the `Gson` and `GsonBuilder` classes to create instances of Gson with specific configurations, such as registered type adapters and exclusion strategies. The tests assert expected outcomes using the `Truth` assertion library, verifying that the JSON output or deserialized objects match the expected values. The file also includes several inner classes that define custom type adapters and factories, demonstrating how these components can be used to override default serialization behavior. Overall, this file serves as a detailed examination of the `@JsonAdapter` annotation's functionality within the Gson library, ensuring that it behaves as intended across a variety of use cases.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.ExclusionStrategy`
- `com.google.gson.FieldAttributes`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonDeserializationContext`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSerializationContext`
- `com.google.gson.JsonSerializer`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.annotations.JsonAdapter`
- `com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.Type`
- `java.util.Arrays`
- `java.util.Collections`
- `java.util.List`
- `org.junit.Test`


# Classes

---
### JsonAdapterAnnotationOnFieldsTest<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonAdapterAnnotationOnFieldsTest` class is a comprehensive suite of functional tests designed to verify the behavior of the `@JsonAdapter` annotation in the Gson library, particularly focusing on its precedence and interaction with other serialization and deserialization strategies. The tests cover various scenarios including class-level and field-level annotations, registered type adapters, and exclusion strategies, ensuring that the `@JsonAdapter` annotation behaves as expected in different contexts and configurations.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testClassAnnotationAdapterTakesPrecedenceOverDefault`](#JsonAdapterAnnotationOnFieldsTesttestClassAnnotationAdapterTakesPrecedenceOverDefault)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testClassAnnotationAdapterFactoryTakesPrecedenceOverDefault`](#JsonAdapterAnnotationOnFieldsTesttestClassAnnotationAdapterFactoryTakesPrecedenceOverDefault)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testRegisteredTypeAdapterTakesPrecedenceOverClassAnnotationAdapter`](#JsonAdapterAnnotationOnFieldsTesttestRegisteredTypeAdapterTakesPrecedenceOverClassAnnotationAdapter)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testFieldAnnotationTakesPrecedenceOverRegisteredTypeAdapter`](#JsonAdapterAnnotationOnFieldsTesttestFieldAnnotationTakesPrecedenceOverRegisteredTypeAdapter)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testFieldAnnotationTakesPrecedenceOverClassAnnotation`](#JsonAdapterAnnotationOnFieldsTesttestFieldAnnotationTakesPrecedenceOverClassAnnotation)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonAdapterInvokedOnlyForAnnotatedFields`](#JsonAdapterAnnotationOnFieldsTesttestJsonAdapterInvokedOnlyForAnnotatedFields)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonAdapterWrappedInNullSafeAsRequested`](#JsonAdapterAnnotationOnFieldsTesttestJsonAdapterWrappedInNullSafeAsRequested)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testNonPrimitiveFieldAnnotationTakesPrecedenceOverDefault`](#JsonAdapterAnnotationOnFieldsTesttestNonPrimitiveFieldAnnotationTakesPrecedenceOverDefault)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testPrimitiveFieldAnnotationTakesPrecedenceOverDefault`](#JsonAdapterAnnotationOnFieldsTesttestPrimitiveFieldAnnotationTakesPrecedenceOverDefault)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testFieldAnnotationWorksForParameterizedType`](#JsonAdapterAnnotationOnFieldsTesttestFieldAnnotationWorksForParameterizedType)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testOverwriteBuiltIn`](#JsonAdapterAnnotationOnFieldsTesttestOverwriteBuiltIn)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testExcludeSerializePrecedence`](#JsonAdapterAnnotationOnFieldsTesttestExcludeSerializePrecedence)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testExcludeDeserializePrecedence`](#JsonAdapterAnnotationOnFieldsTesttestExcludeDeserializePrecedence)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testExcludePrecedence`](#JsonAdapterAnnotationOnFieldsTesttestExcludePrecedence)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testDelegatingAdapterFactory`](#JsonAdapterAnnotationOnFieldsTesttestDelegatingAdapterFactory)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testDelegatingAdapterFactory_Delayed`](#JsonAdapterAnnotationOnFieldsTesttestDelegatingAdapterFactory_Delayed)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testGetAdapterDelegation`](#JsonAdapterAnnotationOnFieldsTesttestGetAdapterDelegation)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonSerializer`](#JsonAdapterAnnotationOnFieldsTesttestJsonSerializer)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonDeserializer`](#JsonAdapterAnnotationOnFieldsTesttestJsonDeserializer)

**Methods**

---
#### JsonAdapterAnnotationOnFieldsTest\.testClassAnnotationAdapterTakesPrecedenceOverDefault<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testClassAnnotationAdapterTakesPrecedenceOverDefault}} -->
The method `testClassAnnotationAdapterTakesPrecedenceOverDefault` tests that a class-level `JsonAdapter` annotation takes precedence over the default serialization and deserialization behavior in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Gson` instance is created.
    - A `Computer` object is serialized to JSON using `gson.toJson`, and the result is asserted to be `{"user":"UserClassAnnotationAdapter"}`.
    - A JSON string representing a `Computer` object is deserialized using `gson.fromJson`, and the `user.name` field of the resulting `Computer` object is asserted to be `UserClassAnnotationAdapter`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonAdapter` annotation.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testClassAnnotationAdapterFactoryTakesPrecedenceOverDefault<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testClassAnnotationAdapterFactoryTakesPrecedenceOverDefault}} -->
This method tests that a class-level JsonAdapter annotation takes precedence over the default serialization and deserialization behavior in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new Gson instance is created.
    - A Gizmo object is serialized to JSON using Gson's toJson method.
    - The resulting JSON string is asserted to be equal to a specific expected string, indicating that the class-level JsonAdapter was used.
    - A JSON string is deserialized into a Gizmo object using Gson's fromJson method.
    - The name of the part in the deserialized Gizmo object is asserted to be equal to a specific expected string, confirming the precedence of the class-level JsonAdapter.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of Gson's serialization and deserialization with class-level JsonAdapter annotations.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testRegisteredTypeAdapterTakesPrecedenceOverClassAnnotationAdapter<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testRegisteredTypeAdapterTakesPrecedenceOverClassAnnotationAdapter}} -->
This method tests that a registered type adapter for a class takes precedence over a class-level annotation adapter when serializing and deserializing JSON using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using GsonBuilder, registering a custom type adapter (RegisteredUserAdapter) for the User class.
    - A Computer object is serialized to JSON using the Gson instance, and the resulting JSON is asserted to be equal to a specific string indicating the use of the RegisteredUserAdapter.
    - A JSON string is deserialized into a Computer object using the Gson instance, and the user name of the resulting object is asserted to be equal to a specific string indicating the use of the RegisteredUserAdapter.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testFieldAnnotationTakesPrecedenceOverRegisteredTypeAdapter<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testFieldAnnotationTakesPrecedenceOverRegisteredTypeAdapter}} -->
This method tests that a field-level JsonAdapter annotation takes precedence over a registered TypeAdapter for serialization and deserialization of a Part object within a Gadget class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using GsonBuilder, registering a TypeAdapter for the Part class that throws AssertionError for both read and write methods.
    - A Gadget object is serialized to JSON using the Gson instance, and the resulting JSON string is asserted to be equal to '{"part":"PartJsonFieldAnnotationAdapter"}'.
    - A JSON string representing a Gadget object is deserialized back into a Gadget instance using the Gson instance, and it is asserted that the part name is 'PartJsonFieldAnnotationAdapter'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the precedence of field-level JsonAdapter annotations over registered TypeAdapters.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testFieldAnnotationTakesPrecedenceOverClassAnnotation<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testFieldAnnotationTakesPrecedenceOverClassAnnotation}} -->
This method tests that a field-level JsonAdapter annotation takes precedence over a class-level JsonAdapter annotation during serialization and deserialization using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created.
    - A Computer2 object is serialized to JSON using Gson, and the resulting JSON string is compared to the expected value using an assertion.
    - A JSON string is deserialized into a Computer2 object using Gson, and the resulting object's user name is compared to the expected value using an assertion.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of Gson serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testJsonAdapterInvokedOnlyForAnnotatedFields<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonAdapterInvokedOnlyForAnnotatedFields}} -->
The method `testJsonAdapterInvokedOnlyForAnnotatedFields` tests that the `JsonAdapter` annotation is only applied to fields that are explicitly annotated with it during JSON deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created.
    - A JSON string `{'part1':'name','part2':{'name':'name2'}}` is defined.
    - The JSON string is deserialized into a `GadgetWithTwoParts` object using the `Gson.fromJson` method.
    - The method asserts that the `name` field of `part1` in the deserialized object is equal to `PartJsonFieldAnnotationAdapter`, indicating that the `JsonAdapter` was applied.
    - The method asserts that the `name` field of `part2` in the deserialized object is equal to `name2`, indicating that no `JsonAdapter` was applied to this field.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonAdapter` annotation.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testJsonAdapterWrappedInNullSafeAsRequested<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonAdapterWrappedInNullSafeAsRequested}} -->
The method `testJsonAdapterWrappedInNullSafeAsRequested` tests the behavior of a Gson adapter when handling null values in JSON serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new Gson instance is created.
    - A JSON string `{'part':null}` is defined.
    - The JSON string is deserialized into a `GadgetWithOptionalPart` object using Gson.
    - An assertion checks that the `part` field of the deserialized object is null.
    - The object is serialized back to a JSON string using Gson.
    - An assertion checks that the serialized JSON string does not contain the string 'PartJsonFieldAnnotationAdapter'.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of Gson with null-safe adapters.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testNonPrimitiveFieldAnnotationTakesPrecedenceOverDefault<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testNonPrimitiveFieldAnnotationTakesPrecedenceOverDefault}} -->
This method tests that a non-primitive field's JsonAdapter annotation takes precedence over the default serialization and deserialization behavior.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created.
    - A GadgetWithOptionalPart object is serialized to JSON using Gson, expecting the output to use the PartJsonFieldAnnotationAdapter for the 'part' field.
    - The JSON string is asserted to be equal to '{"part":"PartJsonFieldAnnotationAdapter"}'.
    - The JSON string '{'part':'foo'}' is deserialized back into a GadgetWithOptionalPart object using Gson.
    - The deserialized object's 'part' field's name is asserted to be 'PartJsonFieldAnnotationAdapter'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testPrimitiveFieldAnnotationTakesPrecedenceOverDefault<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testPrimitiveFieldAnnotationTakesPrecedenceOverDefault}} -->
The method `testPrimitiveFieldAnnotationTakesPrecedenceOverDefault` tests that a `JsonAdapter` annotation on a primitive field takes precedence over the default serialization and deserialization behavior in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created.
    - A `GadgetWithPrimitivePart` object is serialized to JSON using `gson.toJson`, and the result is stored in the `json` variable.
    - An assertion checks that the serialized JSON string is equal to `{"part":"42"}`.
    - The JSON string is deserialized back into a `GadgetWithPrimitivePart` object using `gson.fromJson`.
    - An assertion checks that the `part` field of the deserialized object is equal to `42`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonAdapter` annotation on a primitive field.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testFieldAnnotationWorksForParameterizedType<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testFieldAnnotationWorksForParameterizedType}} -->
The method `testFieldAnnotationWorksForParameterizedType` tests the functionality of the `@JsonAdapter` annotation for a parameterized type field in a class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated.
    - A `Gizmo2` object is created with a list containing a `Part` object, and it is serialized to JSON using `gson.toJson()`.
    - The resulting JSON string is asserted to be equal to `{"part":"GizmoPartTypeAdapterFactory"}`.
    - A `Gizmo2` object is deserialized from a JSON string using `gson.fromJson()`.
    - The name of the first `Part` object in the `part` list of the deserialized `Gizmo2` object is asserted to be equal to `GizmoPartTypeAdapterFactory`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `@JsonAdapter` annotation for parameterized types.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testOverwriteBuiltIn<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testOverwriteBuiltIn}} -->
The `testOverwriteBuiltIn` method tests the ability to overwrite built-in type adapters using the `@JsonAdapter` annotation in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create an instance of `BuiltInOverwriting` and set its field `f` to a `JsonPrimitive` with the value `true`.
    - Serialize the `BuiltInOverwriting` object to JSON using Gson and assert that the resulting JSON string matches the expected format with the serialized value from `JsonElementAdapter`.
    - Deserialize a JSON string into a `BuiltInOverwriting` object and assert that the field `f` is equal to the deserialized value from `JsonElementAdapter`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testExcludeSerializePrecedence<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testExcludeSerializePrecedence}} -->
The `testExcludeSerializePrecedence` method tests that a serialization exclusion strategy takes precedence over a `JsonAdapter` annotation during serialization, but not during deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created with a serialization exclusion strategy that skips all fields.
    - An instance of `DelegatingAndOverwriting` is created and its fields are set.
    - The object is serialized to JSON using the `Gson` object, and the result is asserted to be an empty JSON object `{}` due to the exclusion strategy.
    - The JSON string `{"f":1,"f2":2,"f3":3}` is deserialized into a `DelegatingAndOverwriting` object using the `Gson` object.
    - Assertions are made to verify that the fields `f` and `f2` are correctly deserialized, and that the `JsonAdapter` for `f3` is used, resulting in `f3` being equal to `JsonElementAdapter.DESERIALIZED`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of serialization and deserialization with exclusion strategies and `JsonAdapter` annotations.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.addSerializationExclusionStrategy`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderaddSerializationExclusionStrategy)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testExcludeDeserializePrecedence<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testExcludeDeserializePrecedence}} -->
The method `testExcludeDeserializePrecedence` tests that a deserialization exclusion strategy takes precedence over `@JsonAdapter` annotations in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created with a deserialization exclusion strategy that skips all fields.
    - An instance of `DelegatingAndOverwriting` is created and its fields are set with specific values.
    - The object is serialized to JSON using the `Gson` instance, and the output is verified to ensure that `@JsonAdapter` annotations are respected during serialization.
    - The JSON string `{"f":1,"f2":2,"f3":3}` is deserialized into a `DelegatingAndOverwriting` object using the `Gson` instance.
    - Assertions are made to verify that all fields of the deserialized object are `null`, confirming that the exclusion strategy took precedence over `@JsonAdapter` annotations.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the Gson library with exclusion strategies.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.addDeserializationExclusionStrategy`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderaddDeserializationExclusionStrategy)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testExcludePrecedence<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testExcludePrecedence}} -->
The `testExcludePrecedence` method tests that an exclusion strategy in Gson has higher precedence over the `@JsonAdapter` annotation for both serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created with an exclusion strategy that skips all fields but not classes.
    - An instance of `DelegatingAndOverwriting` is created and its fields are set with values.
    - The object is serialized to JSON using the `Gson` object, and the result is asserted to be an empty JSON object `{}`.
    - The JSON string `{"f":1,"f2":2,"f3":3}` is deserialized into a `DelegatingAndOverwriting` object using the `Gson` object.
    - Assertions are made to ensure that all fields of the deserialized object are `null`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the exclusion strategy in Gson.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setExclusionStrategies`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetExclusionStrategies)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testDelegatingAdapterFactory<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testDelegatingAdapterFactory}} -->
The `testDelegatingAdapterFactory` method tests the functionality of a custom `TypeAdapterFactory` that delegates serialization and deserialization to a default adapter while appending a custom suffix to the serialized and deserialized values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `WithDelegatingFactory<String>` object is deserialized from a JSON string using `Gson.fromJson`, and it is asserted that the field `f` equals 'test-custom'.
    - The same deserialization is performed using a `TypeToken` to specify the type, and it is again asserted that the field `f` equals 'test-custom'.
    - A `WithDelegatingFactory<String>` object is created and its field `f` is set to 'value'.
    - The object is serialized to JSON using `Gson.toJson`, and it is asserted that the resulting JSON string equals '{"f":"value-custom"}'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom `TypeAdapterFactory`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testDelegatingAdapterFactory\_Delayed<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testDelegatingAdapterFactory_Delayed}} -->
The `testDelegatingAdapterFactory_Delayed` method tests the serialization and deserialization of a `WithDelayedDelegatingFactory` object using a custom `TypeAdapterFactory` that appends '-custom' to the field value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `WithDelayedDelegatingFactory` object is deserialized from a JSON string using `Gson.fromJson`, and it is asserted that the field `f` equals 'test-custom'.
    - A `WithDelayedDelegatingFactory` object is created, its field `f` is set to 'value', and it is serialized to JSON using `Gson.toJson`, asserting that the result equals '{"f":"value-custom"}'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior of serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testGetAdapterDelegation<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testGetAdapterDelegation}} -->
The `testGetAdapterDelegation` method tests the custom serialization and deserialization behavior of the `GetAdapterDelegation` class using a `TypeAdapterFactory`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created.
    - The [`fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson) method of `Gson` is used to deserialize a JSON string into a `GetAdapterDelegation` object, and it is asserted that the field `f` is deserialized with a custom suffix `-custom`.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of `Gson` is used to serialize a `GetAdapterDelegation` object into a JSON string, and it is asserted that the field `f` is serialized with a custom suffix `-custom`.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts the correctness of custom serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testJsonSerializer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonSerializer}} -->
The `testJsonSerializer` method tests the serialization and deserialization of a class using a custom JSON serializer with Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - The method deserializes a JSON string `{"f":[1,2,3]}` into an instance of `WithJsonSerializer` class, verifying that the field `f` is correctly deserialized to a list `[1, 2, 3]`.
    - The method serializes a new instance of `WithJsonSerializer` to JSON, verifying that the custom serializer is used, which always returns `{"f":true}`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)


---
#### JsonAdapterAnnotationOnFieldsTest\.testJsonDeserializer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.testJsonDeserializer}} -->
The `testJsonDeserializer` method tests the functionality of a custom JSON deserializer for a field in a class using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created.
    - The [`fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson) method of `Gson` is used to deserialize a JSON string into an instance of `WithJsonDeserializer`, which uses a custom deserializer that always returns the list `[3, 2, 1]`.
    - An assertion checks that the deserialized list `f` is equal to `[3, 2, 1]`.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of `Gson` is used to serialize an instance of `WithJsonDeserializer` with a list `[4, 5, 6]` back to JSON.
    - An assertion checks that the serialized JSON string is equal to `{"f":[4,5,6]}`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom deserializer.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest`](#JsonAdapterAnnotationOnFieldsTest)  (Base Class)



---
### Gadget<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gadget}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Gadget` class is a private, static, and final class that represents a gadget with a single `Part` field, which is annotated with `@JsonAdapter` to specify a custom JSON serialization and deserialization behavior using the `PartJsonFieldAnnotationAdapter` class.
- **Fields**:
    - `part`: `Part` A final field of type `Part` that is annotated with `@JsonAdapter` to use `PartJsonFieldAnnotationAdapter` for JSON operations.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gadget.Gadget`](#GadgetGadget)

**Methods**

---
#### Gadget\.Gadget<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gadget.Gadget}} -->
The `Gadget` constructor initializes a `Gadget` object with a specified `Part` object.
- **Inputs**:
    - `part`: A `Part` object that is used to initialize the `part` field of the `Gadget` class.
- **Control Flow**:
    - The constructor takes a `Part` object as an argument.
    - It assigns the provided `Part` object to the `part` field of the `Gadget` instance.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `Gadget` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gadget`](#JsonAdapterAnnotationOnFieldsTest.Gadget)  (Base Class)



---
### Gizmo<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Gizmo` class is a private, static, and final class that represents a component with a single field, `part`, which is of type `Part`. The class uses a `JsonAdapter` annotation to specify a custom type adapter factory, `GizmoPartTypeAdapterFactory`, for JSON serialization and deserialization of the `part` field, ensuring that the `part` field is processed using this specific adapter when converting to and from JSON.
- **Fields**:
    - `part`: `Part` A final field of type `Part` that represents a component of the Gizmo, annotated with `JsonAdapter` to use a custom type adapter factory for JSON operations.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo.Gizmo`](#GizmoGizmo)

**Methods**

---
#### Gizmo\.Gizmo<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo.Gizmo}} -->
The Gizmo constructor initializes a Gizmo object with a given Part object.
- **Inputs**:
    - `part`: A Part object that is used to initialize the Gizmo's part field.
- **Control Flow**:
    - The constructor takes a Part object as an argument.
    - It assigns the provided Part object to the Gizmo's part field.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo`](#JsonAdapterAnnotationOnFieldsTest.Gizmo)  (Base Class)



---
### Part<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Part}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Part` class is a simple, immutable data structure that represents a component with a single attribute, `name`, which is a string. It is used within the context of JSON serialization and deserialization tests, particularly in conjunction with Gson's `JsonAdapter` annotation to demonstrate how custom serialization and deserialization can be applied to fields of this type.
- **Fields**:
    - `name`: `String` A final string field that holds the name of the part.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Part.Part`](#PartPart)

**Methods**

---
#### Part\.Part<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Part.Part}} -->
The constructor initializes a Part object with a given name.
- **Modifiers**: `public`
- **Inputs**:
    - `name`: A String representing the name of the Part.
- **Control Flow**:
    - Assigns the input parameter 'name' to the instance variable 'name' of the Part object.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the Part class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Part`](#JsonAdapterAnnotationOnFieldsTest.Part)  (Base Class)



---
### PartJsonFieldAnnotationAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `PartJsonFieldAnnotationAdapter` class is a private static inner class that extends `TypeAdapter<Part>` to provide custom serialization and deserialization logic for `Part` objects when used with Gson. It overrides the `write` and `read` methods to handle JSON conversion, specifically writing a fixed string "PartJsonFieldAnnotationAdapter" during serialization and creating a new `Part` object with the same string during deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter.write`](#PartJsonFieldAnnotationAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter.read`](#PartJsonFieldAnnotationAdapterread)

**Methods**

---
#### PartJsonFieldAnnotationAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter.write}} -->
The `write` method writes a fixed string value to a `JsonWriter` object.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `out`: A `JsonWriter` object to which the method writes a string value.
    - `part`: A `Part` object, which is not used in the method's logic.
- **Control Flow**:
    - The method calls the [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method on the `JsonWriter` object `out`, passing the string "PartJsonFieldAnnotationAdapter" as an argument.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter`](#JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter)  (Base Class)


---
#### PartJsonFieldAnnotationAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader` and returns a new `Part` object with a fixed name.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method reads the next JSON string from the `JsonReader` using `in.nextString()` and assigns it to a variable `unused`.
    - It then returns a new `Part` object initialized with the string "PartJsonFieldAnnotationAdapter".
- **Output**:
    - A `Part` object with the name "PartJsonFieldAnnotationAdapter".
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter`](#JsonAdapterAnnotationOnFieldsTest.PartJsonFieldAnnotationAdapter)  (Base Class)



---
### GizmoPartTypeAdapterFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GizmoPartTypeAdapterFactory}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `GizmoPartTypeAdapterFactory` class is a private static inner class that implements the `TypeAdapterFactory` interface, providing a custom `TypeAdapter` for serializing and deserializing objects of type `Part` with a fixed string value "GizmoPartTypeAdapterFactory".
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GizmoPartTypeAdapterFactory.create`](#GizmoPartTypeAdapterFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### GizmoPartTypeAdapterFactory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GizmoPartTypeAdapterFactory.create}} -->
The `create` method in the `GizmoPartTypeAdapterFactory` class returns a new `TypeAdapter` instance for serializing and deserializing objects of type `Part` with a fixed string value.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class, used for JSON serialization and deserialization.
    - `type`: A `TypeToken` representing the type of the object for which the `TypeAdapter` is being created.
- **Control Flow**:
    - The method returns a new anonymous `TypeAdapter` instance.
    - The `write` method of the `TypeAdapter` writes a fixed string "GizmoPartTypeAdapterFactory" to the `JsonWriter`.
    - The `read` method of the `TypeAdapter` reads a string from the `JsonReader` and returns a new `Part` object initialized with the fixed string "GizmoPartTypeAdapterFactory".
- **Output**:
    - A `TypeAdapter<T>` instance that serializes and deserializes objects of type `Part` with a fixed string value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GizmoPartTypeAdapterFactory`](#JsonAdapterAnnotationOnFieldsTest.GizmoPartTypeAdapterFactory)  (Base Class)



---
### Computer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Computer` class is a simple, immutable class that represents a computer associated with a specific user. It contains a single field, `user`, which is a reference to a `User` object, indicating the user associated with this computer. The class is designed to be used in scenarios where a computer needs to be linked to a user, and it is part of a larger test suite for JSON serialization and deserialization using Gson.
- **Fields**:
    - `user`: `User` A final field representing the user associated with this computer.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer.Computer`](#ComputerComputer)

**Methods**

---
#### Computer\.Computer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer.Computer}} -->
The `Computer` constructor initializes a `Computer` object with a given `User` object.
- **Inputs**:
    - `user`: A `User` object that is assigned to the `user` field of the `Computer` class.
- **Control Flow**:
    - The constructor takes a `User` object as a parameter.
    - It assigns the provided `User` object to the `user` field of the `Computer` instance.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `Computer` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer`](#JsonAdapterAnnotationOnFieldsTest.Computer)  (Base Class)



---
### User<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.User}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `User` class is a simple data structure representing a user with a single field, `name`, which is a `String`. It is annotated with `@JsonAdapter`, indicating that a custom JSON adapter, `UserClassAnnotationAdapter`, is used for serialization and deserialization of this class when working with JSON data using Gson.
- **Fields**:
    - `name`: `String` A final String field representing the name of the user.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.User.User`](#UserUser)

**Methods**

---
#### User\.User<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.User.User}} -->
The `User` constructor initializes a `User` object with a given name.
- **Modifiers**: `private`
- **Inputs**:
    - `name`: A `String` representing the name of the user.
- **Control Flow**:
    - The constructor assigns the provided `name` argument to the `name` field of the `User` object.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `User` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.User`](#JsonAdapterAnnotationOnFieldsTest.User)  (Base Class)



---
### UserClassAnnotationAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `UserClassAnnotationAdapter` class is a private static inner class that extends `TypeAdapter<User>`, providing custom serialization and deserialization logic for the `User` class. It overrides the `write` method to output a fixed string "UserClassAnnotationAdapter" when serializing a `User` object, and the `read` method to return a new `User` object with the name "UserClassAnnotationAdapter" when deserializing.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter.write`](#UserClassAnnotationAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter.read`](#UserClassAnnotationAdapterread)

**Methods**

---
#### UserClassAnnotationAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter.write}} -->
The `write` method writes a fixed string value "UserClassAnnotationAdapter" to the provided `JsonWriter` object.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - `user`: A `User` object, which is not used in this method.
- **Control Flow**:
    - The method calls `out.value()` with the string "UserClassAnnotationAdapter" to write this value to the `JsonWriter`.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter`](#JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter)  (Base Class)


---
#### UserClassAnnotationAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader` and returns a new `User` object with a predefined name.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method reads the next JSON string from the `JsonReader` using `in.nextString()` and assigns it to a local variable `unused`.
    - A new `User` object is created with the name "UserClassAnnotationAdapter" and returned.
- **Output**:
    - A `User` object with the name "UserClassAnnotationAdapter".
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter`](#JsonAdapterAnnotationOnFieldsTest.UserClassAnnotationAdapter)  (Base Class)



---
### Computer2<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer2}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Computer2` class is a private, static, and final class that encapsulates a `User` object, with a specific `JsonAdapter` annotation applied to the `user` field to override the default serialization and deserialization behavior defined by the `User` class's own `JsonAdapter` annotation.
- **Fields**:
    - `user`: `User` A final field of type `User` that is annotated with `JsonAdapter(UserFieldAnnotationAdapter.class)` to customize its JSON serialization and deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer2.Computer2`](#Computer2Computer2)

**Methods**

---
#### Computer2\.Computer2<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer2.Computer2}} -->
The `Computer2` constructor initializes a `Computer2` object with a given `User` object, assigning it to the `user` field.
- **Inputs**:
    - `user`: A `User` object that is assigned to the `user` field of the `Computer2` instance.
- **Control Flow**:
    - The constructor takes a `User` object as a parameter.
    - The `user` field of the `Computer2` instance is set to the provided `User` object.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `Computer2` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Computer2`](#JsonAdapterAnnotationOnFieldsTest.Computer2)  (Base Class)



---
### UserFieldAnnotationAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `UserFieldAnnotationAdapter` class is a specialized `TypeAdapter` for the `User` class, designed to handle JSON serialization and deserialization by overriding the default behavior with a custom implementation that writes and reads a fixed string value, "UserFieldAnnotationAdapter", instead of the actual `User` object data.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter.write`](#UserFieldAnnotationAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter.read`](#UserFieldAnnotationAdapterread)

**Methods**

---
#### UserFieldAnnotationAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter.write}} -->
The `write` method writes a fixed string value "UserFieldAnnotationAdapter" to the provided `JsonWriter`.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - `user`: A `User` object, which is not used in this method.
- **Control Flow**:
    - The method calls `out.value()` with the string "UserFieldAnnotationAdapter" to write this value to the `JsonWriter`.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter`](#JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter)  (Base Class)


---
#### UserFieldAnnotationAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader` and returns a new `User` object with a predefined name.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method reads the next JSON string from the `JsonReader` using `in.nextString()` and assigns it to a variable `unused`.
    - A new `User` object is created with the name "UserFieldAnnotationAdapter" and returned.
- **Output**:
    - A `User` object with the name "UserFieldAnnotationAdapter".
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter`](#JsonAdapterAnnotationOnFieldsTest.UserFieldAnnotationAdapter)  (Base Class)



---
### RegisteredUserAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `RegisteredUserAdapter` class is a private static final inner class that extends `TypeAdapter<User>`, providing custom serialization and deserialization logic for `User` objects. It overrides the `write` method to output a fixed string "RegisteredUserAdapter" and the `read` method to return a new `User` object with the name "RegisteredUserAdapter".
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter.write`](#RegisteredUserAdapterwrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter.read`](#RegisteredUserAdapterread)

**Methods**

---
#### RegisteredUserAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter.write}} -->
The `write` method writes a fixed string value "RegisteredUserAdapter" to a `JsonWriter` object.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - `user`: A `User` object, which is not used in this method.
- **Control Flow**:
    - The method calls `out.value()` with the string "RegisteredUserAdapter" to write this value to the `JsonWriter`.
- **Output**:
    - The method does not return any value; it writes a string to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter`](#JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter)  (Base Class)


---
#### RegisteredUserAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader` and returns a new `User` object with a predefined name.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method reads the next JSON string from the `JsonReader` object `in` and assigns it to a local variable `unused`.
    - A new `User` object is created with the name "RegisteredUserAdapter" and returned.
- **Output**:
    - A `User` object with the name "RegisteredUserAdapter".
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter`](#JsonAdapterAnnotationOnFieldsTest.RegisteredUserAdapter)  (Base Class)



---
### GadgetWithTwoParts<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithTwoParts}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `GadgetWithTwoParts` class is a private, static, and final class that represents a gadget composed of two parts, `part1` and `part2`. The class utilizes the `JsonAdapter` annotation on `part1` to specify a custom JSON serialization and deserialization behavior using the `PartJsonFieldAnnotationAdapter`, while `part2` does not have any specific JSON adapter annotation, implying default serialization and deserialization behavior.
- **Fields**:
    - `part1`: `Part` This field represents the first part of the gadget and uses a custom JSON adapter for serialization and deserialization.
    - `part2`: `Part` This field represents the second part of the gadget and does not use a custom JSON adapter, implying default serialization and deserialization behavior.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithTwoParts.GadgetWithTwoParts`](#GadgetWithTwoPartsGadgetWithTwoParts)

**Methods**

---
#### GadgetWithTwoParts\.GadgetWithTwoParts<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithTwoParts.GadgetWithTwoParts}} -->
The `GadgetWithTwoParts` constructor initializes a `GadgetWithTwoParts` object with two `Part` objects, assigning them to `part1` and `part2` fields.
- **Modifiers**: ``
- **Inputs**:
    - `part1`: The first `Part` object to be assigned to the `part1` field of the `GadgetWithTwoParts` object.
    - `part2`: The second `Part` object to be assigned to the `part2` field of the `GadgetWithTwoParts` object.
- **Control Flow**:
    - The constructor takes two parameters, `part1` and `part2`, both of type `Part`.
    - It assigns the `part1` parameter to the `part1` field of the `GadgetWithTwoParts` object.
    - It assigns the `part2` parameter to the `part2` field of the `GadgetWithTwoParts` object.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `GadgetWithTwoParts` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithTwoParts`](#JsonAdapterAnnotationOnFieldsTest.GadgetWithTwoParts)  (Base Class)



---
### GadgetWithOptionalPart<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithOptionalPart}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `GadgetWithOptionalPart` class is a private, static, and final class that represents a gadget with an optional part, utilizing a JSON adapter for custom serialization and deserialization of its `part` field.
- **Fields**:
    - `part`: `Part` A final field of type `Part` that is annotated with `@JsonAdapter` to use `PartJsonFieldAnnotationAdapter` for custom JSON serialization and deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithOptionalPart.GadgetWithOptionalPart`](#GadgetWithOptionalPartGadgetWithOptionalPart)

**Methods**

---
#### GadgetWithOptionalPart\.GadgetWithOptionalPart<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithOptionalPart.GadgetWithOptionalPart}} -->
The `GadgetWithOptionalPart` constructor initializes a `GadgetWithOptionalPart` object with a given `Part` object, which can be null.
- **Modifiers**: `private`
- **Inputs**:
    - `part`: A `Part` object that can be optionally null, used to initialize the `part` field of the `GadgetWithOptionalPart` instance.
- **Control Flow**:
    - The constructor takes a `Part` object as an argument.
    - It assigns the provided `Part` object to the `part` field of the `GadgetWithOptionalPart` instance.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `GadgetWithOptionalPart` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithOptionalPart`](#JsonAdapterAnnotationOnFieldsTest.GadgetWithOptionalPart)  (Base Class)



---
### GadgetWithPrimitivePart<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithPrimitivePart}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `GadgetWithPrimitivePart` class is a private, static, and final class that represents a gadget with a single primitive long field named `part`. This field is annotated with `@JsonAdapter`, which specifies a custom type adapter factory (`LongToStringTypeAdapterFactory`) for converting the long value to a string during JSON serialization and deserialization. The class has a private constructor that initializes the `part` field.
- **Fields**:
    - `part`: `long` A final long field representing a part of the gadget, annotated with @JsonAdapter for custom JSON serialization and deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithPrimitivePart.GadgetWithPrimitivePart`](#GadgetWithPrimitivePartGadgetWithPrimitivePart)

**Methods**

---
#### GadgetWithPrimitivePart\.GadgetWithPrimitivePart<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithPrimitivePart.GadgetWithPrimitivePart}} -->
The `GadgetWithPrimitivePart` constructor initializes an instance of the class with a specified long value for its `part` field.
- **Modifiers**: `private`
- **Inputs**:
    - `part`: A long value that is used to initialize the `part` field of the `GadgetWithPrimitivePart` instance.
- **Control Flow**:
    - The constructor takes a single long argument named `part`.
    - It assigns the value of the `part` argument to the instance's `part` field.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `GadgetWithPrimitivePart` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GadgetWithPrimitivePart`](#JsonAdapterAnnotationOnFieldsTest.GadgetWithPrimitivePart)  (Base Class)



---
### LongToStringTypeAdapterFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `LongToStringTypeAdapterFactory` class is a custom implementation of the `TypeAdapterFactory` interface, designed to handle the serialization and deserialization of `Long` and `long` types in JSON using the Gson library. It provides a static `TypeAdapter` for `Long` that converts `Long` values to their string representation when writing to JSON and reads them back as `Long` when deserializing from JSON. This factory ensures that any field annotated with `@JsonAdapter(LongToStringTypeAdapterFactory.class)` will use this adapter for `Long` and `long` types.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory.write`](#LongToStringTypeAdapterFactorywrite)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory.read`](#LongToStringTypeAdapterFactoryread)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory.create`](#LongToStringTypeAdapterFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### LongToStringTypeAdapterFactory\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory.write}} -->
The `write` method writes a `Long` value to a `JsonWriter` as a string.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object to which the `Long` value will be written.
    - [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `Long` object representing the value to be written to the `JsonWriter`.
- **Control Flow**:
    - The method calls `out.value()` with the string representation of the `Long` value, converting the `Long` to a string using `value.toString()` before writing.
- **Output**:
    - The method does not return any value; it writes the `Long` value to the `JsonWriter` as a string.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory`](#JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory)  (Base Class)


---
#### LongToStringTypeAdapterFactory\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory.read}} -->
The `read` method reads the next JSON value from the `JsonReader` and returns it as a `Long`.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the next JSON value is read.
- **Control Flow**:
    - The method calls `in.nextLong()` to read the next JSON value from the `JsonReader` and convert it to a `Long`.
- **Output**:
    - The method returns a `Long` representing the next JSON value read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory`](#JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory)  (Base Class)


---
#### LongToStringTypeAdapterFactory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory.create}} -->
The `create` method in `LongToStringTypeAdapterFactory` returns a `TypeAdapter` for `Long` types or throws an exception if the type is not `Long`.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class, used for JSON serialization and deserialization.
    - `type`: A `TypeToken` representing the type for which a `TypeAdapter` is to be created.
- **Control Flow**:
    - Retrieve the raw type from the `TypeToken` using `type.getRawType()` and store it in `cls`.
    - Check if `cls` is assignable from `Long.class`; if true, return the `ADAPTER` cast to `TypeAdapter<T>`.
    - Check if `cls` is assignable from `long.class`; if true, return the `ADAPTER` cast to `TypeAdapter<T>`.
    - If neither condition is met, throw an `IllegalStateException` indicating that a non-long field was annotated with `@JsonAdapter(LongToStringTypeAdapterFactory.class)`.
- **Output**:
    - Returns a `TypeAdapter<T>` for `Long` types or throws an `IllegalStateException` if the type is not `Long`.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory`](#JsonAdapterAnnotationOnFieldsTest.LongToStringTypeAdapterFactory)  (Base Class)



---
### Gizmo2<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Gizmo2` class is a private, static, and final class that represents a collection of `Part` objects, with a custom JSON adapter specified for serialization and deserialization using the `Gizmo2PartTypeAdapterFactory`. This class is used to demonstrate the precedence of field-level `JsonAdapter` annotations over other type adapters in the context of JSON processing with Gson.
- **Fields**:
    - `part`: `List<Part>` A list of `Part` objects annotated with `JsonAdapter` to use `Gizmo2PartTypeAdapterFactory` for JSON serialization and deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2.Gizmo2`](#Gizmo2Gizmo2)

**Methods**

---
#### Gizmo2\.Gizmo2<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2.Gizmo2}} -->
The Gizmo2 constructor initializes a Gizmo2 object with a list of Part objects.
- **Inputs**:
    - `part`: A List of Part objects that will be assigned to the Gizmo2 instance's part field.
- **Control Flow**:
    - The constructor takes a List of Part objects as an argument.
    - It assigns this list to the instance variable 'part' of the Gizmo2 object.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the Gizmo2 class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2`](#JsonAdapterAnnotationOnFieldsTest.Gizmo2)  (Base Class)



---
### Gizmo2PartTypeAdapterFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2PartTypeAdapterFactory}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Gizmo2PartTypeAdapterFactory` class is a private static inner class that implements the `TypeAdapterFactory` interface, providing a custom `TypeAdapter` for serializing and deserializing objects of type `Part` within the `Gizmo2` class. It overrides the `create` method to return a `TypeAdapter` that writes a fixed string "GizmoPartTypeAdapterFactory" during serialization and reads a JSON string to return a list containing a single `Part` object with the same fixed name during deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2PartTypeAdapterFactory.create`](#Gizmo2PartTypeAdapterFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### Gizmo2PartTypeAdapterFactory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2PartTypeAdapterFactory.create}} -->
The `create` method in `GizmoPartTypeAdapterFactory` returns a custom `TypeAdapter` for serializing and deserializing objects of type `T` with a fixed string value.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of `Gson` used for creating the `TypeAdapter`.
    - `type`: A `TypeToken` representing the type `T` for which the `TypeAdapter` is being created.
- **Control Flow**:
    - The method returns a new instance of an anonymous `TypeAdapter` class.
    - The `write` method of the `TypeAdapter` writes a fixed string "GizmoPartTypeAdapterFactory" to the `JsonWriter`.
    - The `read` method reads a string from the `JsonReader` and returns a new `Part` object with the name "GizmoPartTypeAdapterFactory".
- **Output**:
    - A `TypeAdapter<T>` that serializes and deserializes objects of type `T` with a fixed string value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.Gizmo2PartTypeAdapterFactory`](#JsonAdapterAnnotationOnFieldsTest.Gizmo2PartTypeAdapterFactory)  (Base Class)



---
### BuiltInOverwriting<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.BuiltInOverwriting}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `BuiltInOverwriting` class is a private static class that demonstrates the use of the `@JsonAdapter` annotation to specify a custom `TypeAdapter` for a `JsonElement` field, allowing the overwriting of built-in adapters in Gson serialization and deserialization processes.
- **Fields**:
    - `f`: `JsonElement` A `JsonElement` field annotated with `@JsonAdapter` to use `JsonElementAdapter` for custom serialization and deserialization.


---
### JsonElementAdapter<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `JsonElementAdapter` class is a custom `TypeAdapter` for the `JsonElement` type, designed to override the default serialization and deserialization behavior by providing hardcoded values. It serializes any `JsonElement` to a fixed string "serialized hardcoded" and deserializes any JSON input to a fixed `JsonPrimitive` with the value "deserialized hardcoded".
- **Fields**:
    - `DESERIALIZED`: `JsonPrimitive` A static final `JsonPrimitive` representing the hardcoded deserialized value.
    - `SERIALIZED`: `String` A static final `String` representing the hardcoded serialized value.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter.read`](#JsonElementAdapterread)
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter.write`](#JsonElementAdapterwrite)

**Methods**

---
#### JsonElementAdapter\.read<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter.read}} -->
The `read` method skips the current JSON value in the `JsonReader` and returns a predefined `JsonElement` constant.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which JSON data is being read.
- **Control Flow**:
    - The method calls `in.skipValue()` to skip the current JSON value in the `JsonReader`.
    - It then returns the constant `DESERIALIZED`, which is a predefined `JsonElement`.
- **Output**:
    - A `JsonElement` object, specifically the constant `DESERIALIZED`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter`](#JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter)  (Base Class)


---
#### JsonElementAdapter\.write<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter.write}} -->
The `write` method writes a hardcoded string value to a `JsonWriter` object.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object to which the serialized data is written.
    - [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `JsonElement` object that is not used in this method.
- **Control Flow**:
    - The method calls the [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method on the `JsonWriter` object `out`, passing a hardcoded string `SERIALIZED` as the argument.
- **Output**:
    - The method does not return any value; it writes a hardcoded string to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter`](#JsonAdapterAnnotationOnFieldsTest.JsonElementAdapter)  (Base Class)



---
### DelegatingAndOverwriting<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.DelegatingAndOverwriting}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `DelegatingAndOverwriting` class is a private static class that demonstrates the use of the `@JsonAdapter` annotation to specify custom serialization and deserialization behavior for its fields using different `TypeAdapterFactory` implementations. It includes fields with both delegating and non-delegating adapters to test various scenarios in JSON processing.
- **Fields**:
    - `f`: `Integer` An Integer field annotated with a delegating adapter factory for custom JSON processing.
    - `f2`: `JsonElement` A JsonElement field annotated with a delegating adapter factory for custom JSON processing.
    - `f3`: `JsonElement` A JsonElement field annotated with a non-delegating adapter for custom JSON processing.


---
### DelegatingAdapterFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.DelegatingAndOverwriting.DelegatingAdapterFactory}} -->
- **Modifiers**: `static`
- **Description**: The `DelegatingAdapterFactory` class is a static inner class that implements the `TypeAdapterFactory` interface, providing a mechanism to create a `TypeAdapter` by delegating the creation process to the `Gson` instance's `getDelegateAdapter` method. This allows for the customization of serialization and deserialization processes by leveraging the existing adapter infrastructure within Gson.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.DelegatingAndOverwriting.DelegatingAdapterFactory.create`](#DelegatingAdapterFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### DelegatingAdapterFactory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.DelegatingAndOverwriting.DelegatingAdapterFactory.create}} -->
The `create` method returns a `TypeAdapter` for a given type using the Gson instance's delegate adapter.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the Gson class used to obtain the delegate adapter.
    - `type`: A TypeToken representing the type for which a TypeAdapter is to be created.
- **Control Flow**:
    - The method calls `gson.getDelegateAdapter` with `this` and `type` as arguments to obtain the delegate adapter for the specified type.
- **Output**:
    - A `TypeAdapter<T>` for the specified type, obtained from the Gson instance's delegate adapter.
- **Functions called**:
    - [`com.google.gson.Gson.getDelegateAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.DelegatingAndOverwriting.DelegatingAdapterFactory`](#JsonAdapterAnnotationOnFieldsTest.DelegatingAndOverwriting.DelegatingAdapterFactory)  (Base Class)



---
### WithDelegatingFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithDelegatingFactory}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithDelegatingFactory` class is a generic container class that utilizes a custom `TypeAdapterFactory` to handle JSON serialization and deserialization with the Gson library. It contains a single field `f` of generic type `T`, which is annotated with `@JsonAdapter` to specify the use of the nested `Factory` class for custom JSON processing. The `Factory` class implements `TypeAdapterFactory` and provides a custom `TypeAdapter` that appends "-custom" to serialized and deserialized string values, demonstrating how to extend Gson's default behavior.
- **Fields**:
    - `f`: `T` A generic field of type `T` that is serialized and deserialized using a custom `TypeAdapter` defined in the nested `Factory` class.


---
### Factory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation.Factory}} -->
- **Modifiers**: `static`
- **Description**: The `Factory` class is a static inner class that implements the `TypeAdapterFactory` interface, providing a mechanism to create custom `TypeAdapter` instances for JSON serialization and deserialization using the Gson library. It specifically customizes the behavior of reading and writing `String` values by appending "-custom" to the serialized and deserialized strings, demonstrating how to extend Gson's functionality with custom logic.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation.Factory.create`](#Factorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### Factory\.create<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation.Factory.create}} -->
The `create` method in the `Factory` class returns a custom `TypeAdapter` for a given type that appends '-custom' to serialized and deserialized string values.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class used to obtain the delegate adapter.
    - `type`: A `TypeToken<T>` representing the type for which the `TypeAdapter` is being created.
- **Control Flow**:
    - The method begins by obtaining a delegate `TypeAdapter<String>` using `Gson.getAdapter(type)` for the specified type.
    - A new `TypeAdapter<String>` is created and returned, which overrides the [`read`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.read) and [`write`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.write) methods.
    - In the [`read`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.read) method, the delegate's [`read`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.read) method is called, and '-custom' is appended to the result before returning it.
    - In the [`write`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.write) method, '-custom' is appended to the value before passing it to the delegate's [`write`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.write) method.
- **Output**:
    - Returns a `TypeAdapter<T>` that customizes the serialization and deserialization of strings by appending '-custom'.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create.read`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.read)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create.write`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate.write)
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation.Factory`](#JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation.Factory)  (Base Class)



---
### WithDelayedDelegatingFactory<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithDelayedDelegatingFactory}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithDelayedDelegatingFactory` class is a private static class that demonstrates the use of a custom `TypeAdapterFactory` to handle JSON serialization and deserialization with a delayed delegation approach. It uses a nested `Factory` class to create a `TypeAdapter` for `String` fields, which appends "-custom" to the serialized and deserialized values, showcasing how to customize JSON processing using Gson's `@JsonAdapter` annotation.
- **Fields**:
    - `f`: `String` A String field annotated with @JsonAdapter to use the custom Factory for JSON serialization and deserialization.


---
### GetAdapterDelegation<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `GetAdapterDelegation` class is a private static class that demonstrates the use of a custom `TypeAdapterFactory` to modify the serialization and deserialization behavior of a field annotated with `@JsonAdapter`. It uses the `Gson.getAdapter` method to obtain a delegate adapter and appends "-custom" to the serialized and deserialized string values.
- **Fields**:
    - `f`: `String` A string field annotated with `@JsonAdapter` to use a custom `TypeAdapterFactory` for serialization and deserialization.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation.GetAdapterDelegation`](#GetAdapterDelegationGetAdapterDelegation)

**Methods**

---
#### GetAdapterDelegation\.GetAdapterDelegation<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation.GetAdapterDelegation}} -->
The `GetAdapterDelegation` constructor initializes an instance of the class by setting the field `f` to the provided string argument.
- **Inputs**:
    - `f`: A string that is assigned to the instance variable `f` of the `GetAdapterDelegation` class.
- **Control Flow**:
    - The constructor takes a single string argument `f`.
    - The instance variable `this.f` is assigned the value of the argument `f`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `GetAdapterDelegation` class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation`](#JsonAdapterAnnotationOnFieldsTest.GetAdapterDelegation)  (Base Class)



---
### WithJsonSerializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonSerializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithJsonSerializer` class is a private static class that demonstrates the use of a custom JSON serializer for a list of integers using the Gson library. It contains a field `f` which is a list of integers annotated with `@JsonAdapter`, specifying a custom serializer `Serializer` that always serializes the list to a JSON primitive value of `true`, regardless of the list's contents.
- **Fields**:
    - `f`: `List<Integer>` A list of integers annotated with @JsonAdapter to use a custom serializer that always serializes the list to true.


---
### Serializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonSerializer.Serializer}} -->
- **Modifiers**: `static`
- **Description**: The `Serializer` class is a static inner class that implements the `JsonSerializer` interface for serializing a `List<Integer>` into a JSON element, specifically returning a JSON primitive with a boolean value of `true` regardless of the input list.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonSerializer.Serializer.serialize`](#Serializerserialize)

**Methods**

---
#### Serializer\.serialize<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonSerializer.Serializer.serialize}} -->
The `serialize` method converts a list of integers into a JSON element, specifically a JSON primitive with a boolean value of true.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: A list of integers to be serialized.
    - `typeOfSrc`: The type of the source object to be serialized.
    - `context`: The context for serialization, providing methods to serialize other types.
- **Control Flow**:
    - The method takes three parameters: a list of integers (`src`), a type (`typeOfSrc`), and a serialization context (`context`).
    - It returns a new `JsonPrimitive` object with a boolean value of `true`, regardless of the input list.
- **Output**:
    - A `JsonElement` object, specifically a `JsonPrimitive` with a boolean value of true.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonSerializer.Serializer`](#JsonAdapterAnnotationOnFieldsTest.WithJsonSerializer.Serializer)  (Base Class)



---
### WithJsonDeserializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `WithJsonDeserializer` class is a private static class that demonstrates the use of a custom JSON deserializer for a field annotated with `@JsonAdapter`. It contains a list of integers `f` that is deserialized using the custom `Deserializer` class, which implements the `JsonDeserializer` interface to always return a fixed list of integers `[3, 2, 1]` regardless of the input JSON.
- **Fields**:
    - `f`: `List<Integer>` A list of integers that is deserialized using a custom deserializer.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer.WithJsonDeserializer`](#WithJsonDeserializerWithJsonDeserializer)

**Methods**

---
#### WithJsonDeserializer\.WithJsonDeserializer<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer.WithJsonDeserializer}} -->
The `WithJsonDeserializer` constructor initializes an instance of the class with a list of integers.
- **Inputs**:
    - `f`: A list of integers to be assigned to the instance variable `f`.
- **Control Flow**:
    - Assigns the input list `f` to the instance variable `this.f`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the class.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer`](#JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer)  (Base Class)



---
### Deserializer<!-- {{#class:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer.Deserializer}} -->
- **Modifiers**: `static`
- **Description**: The `Deserializer` class is a static inner class that implements the `JsonDeserializer` interface for deserializing JSON elements into a list of integers. It overrides the `deserialize` method to return a fixed list of integers `[3, 2, 1]`, regardless of the input JSON.
- **Methods**:
    - [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer.Deserializer.deserialize`](#Deserializerdeserialize)

**Methods**

---
#### Deserializer\.deserialize<!-- {{#callable:com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer.Deserializer.deserialize}} -->
The `deserialize` method returns a fixed list of integers [3, 2, 1] regardless of the input JSON element.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the object to deserialize to.
    - `context`: A `JsonDeserializationContext` that provides the context for deserialization.
- **Control Flow**:
    - The method does not utilize the input parameters and directly returns a fixed list of integers [3, 2, 1].
- **Output**:
    - A `List<Integer>` containing the integers 3, 2, and 1.
- **See also**: [`com.google.gson.functional.JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer.Deserializer`](#JsonAdapterAnnotationOnFieldsTest.WithJsonDeserializer.Deserializer)  (Base Class)



