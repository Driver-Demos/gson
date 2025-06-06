# Purpose
The `NullObjectAndFieldTest` Java class is a comprehensive suite of functional tests designed to validate the behavior of the Gson library when handling null values during serialization and deserialization processes. This test class is part of the `com.google.gson.functional` package and utilizes the JUnit testing framework to ensure that Gson correctly serializes and deserializes null objects, fields, and array elements. The tests cover various scenarios, including top-level null object serialization and deserialization, explicit serialization of null fields in custom objects, and the use of custom serializers and deserializers to handle null values. The class also addresses specific issues and edge cases, such as the serialization of null-wrapped primitive members and the behavior of absent JSON elements.

The class is structured around multiple test methods, each focusing on a specific aspect of null handling in Gson. It employs the `GsonBuilder` to configure Gson instances with the `serializeNulls` option, which dictates whether null values should be included in the JSON output. The tests make use of custom classes like `ClassWithObjects`, `ClassWithMembers`, and `ClassWithNullWrappedPrimitive` to simulate real-world scenarios where objects may contain null fields. Additionally, the class includes custom serializers and deserializers, such as `ClassWithObjectsSerializer`, to demonstrate how Gson can be extended to handle null values in a customized manner. Overall, this test class serves as a critical component in ensuring the robustness and correctness of Gson's null handling capabilities.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonNull`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonSerializationContext`
- `com.google.gson.JsonSerializer`
- `com.google.gson.common.TestTypes.BagOfPrimitives`
- `com.google.gson.common.TestTypes.ClassWithObjects`
- `java.lang.reflect.Type`
- `java.util.Collection`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### NullObjectAndFieldTest<!-- {{#class:com.google.gson.functional.NullObjectAndFieldTest}} -->
- **Modifiers**: `public`
- **Description**: The `NullObjectAndFieldTest` class is a suite of functional tests designed to verify the behavior of the Gson library when handling null objects and fields during serialization and deserialization processes. It includes tests for top-level null object serialization and deserialization, explicit serialization and deserialization of nulls in various data structures such as arrays, collections, and custom objects, as well as tests for custom serialization and deserialization using type adapters. The class ensures that null values are correctly serialized and deserialized according to the Gson configuration, and it addresses specific issues and edge cases related to null handling.
- **Fields**:
    - `gsonBuilder`: `GsonBuilder` A GsonBuilder instance used to configure Gson for serialization and deserialization tests.
- **Methods**:
    - [`com.google.gson.functional.NullObjectAndFieldTest.setUp`](#NullObjectAndFieldTestsetUp)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testTopLevelNullObjectSerialization`](#NullObjectAndFieldTesttestTopLevelNullObjectSerialization)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testTopLevelNullObjectDeserialization`](#NullObjectAndFieldTesttestTopLevelNullObjectDeserialization)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNulls`](#NullObjectAndFieldTesttestExplicitSerializationOfNulls)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testExplicitDeserializationOfNulls`](#NullObjectAndFieldTesttestExplicitDeserializationOfNulls)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNullArrayMembers`](#NullObjectAndFieldTesttestExplicitSerializationOfNullArrayMembers)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testNullWrappedPrimitiveMemberSerialization`](#NullObjectAndFieldTesttestNullWrappedPrimitiveMemberSerialization)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testNullWrappedPrimitiveMemberDeserialization`](#NullObjectAndFieldTesttestNullWrappedPrimitiveMemberDeserialization)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNullCollectionMembers`](#NullObjectAndFieldTesttestExplicitSerializationOfNullCollectionMembers)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNullStringMembers`](#NullObjectAndFieldTesttestExplicitSerializationOfNullStringMembers)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testCustomSerializationOfNulls`](#NullObjectAndFieldTesttestCustomSerializationOfNulls)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testPrintPrintingObjectWithNulls`](#NullObjectAndFieldTesttestPrintPrintingObjectWithNulls)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testPrintPrintingArraysWithNulls`](#NullObjectAndFieldTesttestPrintPrintingArraysWithNulls)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testAbsentJsonElementsAreSetToNull`](#NullObjectAndFieldTesttestAbsentJsonElementsAreSetToNull)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testExplicitNullSetsFieldToNullDuringDeserialization`](#NullObjectAndFieldTesttestExplicitNullSetsFieldToNullDuringDeserialization)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testCustomTypeAdapterPassesNullSerialization`](#NullObjectAndFieldTesttestCustomTypeAdapterPassesNullSerialization)
    - [`com.google.gson.functional.NullObjectAndFieldTest.testCustomTypeAdapterPassesNullDeserialization`](#NullObjectAndFieldTesttestCustomTypeAdapterPassesNullDeserialization)

**Methods**

---
#### NullObjectAndFieldTest\.setUp<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.setUp}} -->
The setUp method initializes a GsonBuilder instance with the configuration to serialize null values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with @Before, indicating it runs before each test method in the class.
    - A new GsonBuilder instance is created and assigned to the gsonBuilder field.
    - The serializeNulls method is called on the GsonBuilder instance to configure it to include null values during serialization.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testTopLevelNullObjectSerialization<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testTopLevelNullObjectSerialization}} -->
The method `testTopLevelNullObjectSerialization` tests the serialization of a top-level null object using Gson to ensure it outputs the string "null".
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using a `GsonBuilder` that is configured to serialize nulls.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` object is called with a `null` argument, and the result is stored in the `actual` variable.
    - An assertion is made to check that the `actual` string is equal to "null".
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method is called again with `null` and `String.class` as arguments, and the result is stored in the `actual` variable.
    - Another assertion is made to verify that the `actual` string is equal to "null".
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of Gson serialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testTopLevelNullObjectDeserialization<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testTopLevelNullObjectDeserialization}} -->
The method `testTopLevelNullObjectDeserialization` tests the deserialization of a JSON 'null' value into a Java String object using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using a GsonBuilder configured to serialize nulls.
    - The method [`fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) is called on the Gson instance to deserialize the JSON string 'null' into a Java String object.
    - An assertion is made to verify that the deserialized object is null.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the deserialization result.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testExplicitSerializationOfNulls<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNulls}} -->
The method `testExplicitSerializationOfNulls` tests the serialization of a class with a null field using Gson to ensure it explicitly includes null values in the JSON output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using a `GsonBuilder` that is configured to serialize nulls.
    - An instance of `ClassWithObjects` is created with a null value for its field.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of `Gson` is used to serialize the `ClassWithObjects` instance to a JSON string.
    - The resulting JSON string is compared to the expected JSON string `{"bag":null}` using an assertion to verify correctness.
- **Output**:
    - The method does not return a value; it performs an assertion to verify that the JSON serialization includes null values as expected.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testExplicitDeserializationOfNulls<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testExplicitDeserializationOfNulls}} -->
The method `testExplicitDeserializationOfNulls` tests the deserialization of a JSON object with a null field into a Java object using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using a `GsonBuilder` that is configured to serialize nulls.
    - The [`fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of the `Gson` instance is called with a JSON string containing a null field and the `ClassWithObjects` class type, resulting in a `ClassWithObjects` object.
    - An assertion is made to verify that the `bag` field of the deserialized `ClassWithObjects` object is null.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the `bag` field of the deserialized object is null.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testExplicitSerializationOfNullArrayMembers<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNullArrayMembers}} -->
The method `testExplicitSerializationOfNullArrayMembers` tests the serialization of a class with null array members using Gson to ensure that null arrays are explicitly serialized as `"array":null` in the resulting JSON.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using a `GsonBuilder` that is configured to serialize nulls.
    - An instance of `ClassWithMembers` is created, which presumably has a null array member.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` instance is called to serialize the `ClassWithMembers` instance into a JSON string.
    - An assertion is made to check that the resulting JSON string contains the substring `"array":null`, indicating that the null array member was explicitly serialized.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the serialization behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testNullWrappedPrimitiveMemberSerialization<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testNullWrappedPrimitiveMemberSerialization}} -->
The method tests the serialization of a class with a null-wrapped primitive member using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created with the 'serializeNulls' option enabled using a GsonBuilder.
    - An instance of ClassWithNullWrappedPrimitive is created, which has a Long field initialized to null by default.
    - The Gson instance is used to serialize the ClassWithNullWrappedPrimitive instance to a JSON string.
    - The resulting JSON string is checked to ensure it contains the key-value pair '"value":null', confirming that null values are serialized.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON serialization result.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testNullWrappedPrimitiveMemberDeserialization<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testNullWrappedPrimitiveMemberDeserialization}} -->
The method tests the deserialization of a JSON object with a null value for a wrapped primitive member using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using a GsonBuilder with the serializeNulls option enabled.
    - A JSON string representing an object with a null value for a 'value' field is defined.
    - The JSON string is deserialized into an instance of ClassWithNullWrappedPrimitive using Gson's fromJson method.
    - An assertion is made to verify that the 'value' field of the deserialized object is null.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the deserialization behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testExplicitSerializationOfNullCollectionMembers<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNullCollectionMembers}} -->
This method tests the serialization of null collection members in a class using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using a GsonBuilder that is configured to serialize nulls.
    - An instance of ClassWithMembers is created, which contains a collection member that is null by default.
    - The instance is serialized to JSON using the Gson instance.
    - The resulting JSON string is checked to ensure it contains the expected representation of the null collection member, specifically checking for the presence of '"col":null'.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testExplicitSerializationOfNullStringMembers<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testExplicitSerializationOfNullStringMembers}} -->
This method tests the serialization of a class with null string members using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a Gson instance using the GsonBuilder configured to serialize nulls.
    - Instantiate an object of ClassWithMembers, which has a null string member by default.
    - Serialize the object to JSON using Gson's toJson method.
    - Assert that the resulting JSON string contains the key-value pair "str":null, indicating that the null string member was serialized explicitly.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testCustomSerializationOfNulls<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testCustomSerializationOfNulls}} -->
The method `testCustomSerializationOfNulls` tests the custom serialization of null fields in a `ClassWithObjects` instance using a registered type adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by registering a custom serializer `ClassWithObjectsSerializer` for the `ClassWithObjects` class using `gsonBuilder.registerTypeAdapter`.
    - A `Gson` instance is created from the `gsonBuilder`.
    - An instance of `ClassWithObjects` is created with a `BagOfPrimitives` object as its parameter.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` instance is called to serialize the `ClassWithObjects` instance, storing the result in the `actual` variable.
    - The expected JSON string `{"bag":null}` is defined in the `expected` variable.
    - An assertion is made to check if the `actual` serialized JSON string is equal to the `expected` string.
- **Output**:
    - The method does not return any value but asserts that the serialized JSON string matches the expected output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testPrintPrintingObjectWithNulls<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testPrintPrintingObjectWithNulls}} -->
The method `testPrintPrintingObjectWithNulls` tests the serialization of a class with null members using Gson with and without the [`serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls) option.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `GsonBuilder` instance.
    - Create a `Gson` instance from the `GsonBuilder` without the [`serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls) option.
    - Serialize an instance of `ClassWithMembers` and assert that the result is an empty JSON object `{}`.
    - Create a `Gson` instance from the `GsonBuilder` with the [`serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls) option enabled.
    - Serialize an instance of `ClassWithMembers` again and assert that the result contains the string `"str":null`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of Gson serialization with null values.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.GsonBuilder.serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testPrintPrintingArraysWithNulls<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testPrintPrintingArraysWithNulls}} -->
The method `testPrintPrintingArraysWithNulls` tests the serialization of arrays containing null values using Gson with and without the [`serializeNulls`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls) option.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `GsonBuilder` instance.
    - Create a `Gson` instance from the `GsonBuilder` without the [`serializeNulls`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls) option.
    - Serialize an array containing a null value using the `Gson` instance and store the result.
    - Assert that the serialized result matches the expected JSON string `["1",null,"3"]`.
    - Create a new `Gson` instance from the `GsonBuilder` with the [`serializeNulls`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls) option enabled.
    - Serialize the same array again using the new `Gson` instance and store the result.
    - Assert that the serialized result still matches the expected JSON string `["1",null,"3"]`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of JSON serialization.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.serializeNulls`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testAbsentJsonElementsAreSetToNull<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testAbsentJsonElementsAreSetToNull}} -->
The method `testAbsentJsonElementsAreSetToNull` verifies that absent JSON elements are set to their default values or null when deserialized into a Java object using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated.
    - The JSON string `"{array:[1,2,3]}"` is deserialized into an instance of `ClassWithInitializedMembers`.
    - Assertions are made to verify that the `array` field has a length of 3 and its second element is 2.
    - Assertions are made to check that `str1` is equal to its default value, `str2` is null, `int1` is equal to its default value, `int2` is 0, `bool1` is equal to its default value, and `bool2` is false.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization behavior.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testExplicitNullSetsFieldToNullDuringDeserialization<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testExplicitNullSetsFieldToNullDuringDeserialization}} -->
This method tests that explicitly setting a field to null in a JSON string results in the field being set to null during deserialization using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new Gson instance is created.
    - A JSON string with a field explicitly set to null is defined.
    - The JSON string is deserialized into an instance of ObjectWithField using Gson.
    - An assertion checks that the 'value' field of the deserialized object is null.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the deserialization behavior.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testCustomTypeAdapterPassesNullSerialization<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testCustomTypeAdapterPassesNullSerialization}} -->
The method `testCustomTypeAdapterPassesNullSerialization` tests that a custom type adapter for `ObjectWithField` serializes its fields as null, ensuring that the serialized JSON does not contain the field's value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using a `GsonBuilder` with a custom type adapter registered for `ObjectWithField` that serializes any instance to null.
    - An instance of `ObjectWithField` is created and its `value` field is set to "value1".
    - The `ObjectWithField` instance is serialized to JSON using the `Gson` instance.
    - An assertion is made to ensure that the resulting JSON does not contain the string "value1".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the custom type adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.functional.ReflectionAccessFilterTest.testBlockAllPartial.serialize`](ReflectionAccessFilterTest.java.driver.md#testBlockAllPartialserialize)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)


---
#### NullObjectAndFieldTest\.testCustomTypeAdapterPassesNullDeserialization<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.testCustomTypeAdapterPassesNullDeserialization}} -->
The method tests that a custom type adapter for deserialization in Gson can handle null values by returning null for a non-null JSON input.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using a GsonBuilder, which registers a custom type adapter for the ObjectWithField class that always deserializes to null.
    - A JSON string representing an object with a field is defined.
    - The JSON string is deserialized into an ObjectWithField instance using the Gson instance.
    - An assertion checks that the deserialized ObjectWithField instance is null.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the custom deserialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.functional.UncategorizedTest.BaseTypeAdapter.deserialize`](UncategorizedTest.java.driver.md#BaseTypeAdapterdeserialize)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest`](#NullObjectAndFieldTest)  (Base Class)



---
### ClassWithInitializedMembers<!-- {{#class:com.google.gson.functional.NullObjectAndFieldTest.ClassWithInitializedMembers}} -->
- **Modifiers**: `public`, `static`
- **Description**: The `ClassWithInitializedMembers` is a Java class that demonstrates the use of field initializers and a no-argument constructor to set default values for its fields. It includes both initialized and uninitialized fields, with the latter being set to default values as per the Java Virtual Machine (JVM) specification. This class is used in tests to verify the behavior of serialization and deserialization processes, particularly in handling null values and default field values.
- **Fields**:
    - `MY_STRING_DEFAULT`: `String` A public static final String initialized to "string".
    - `MY_INT_DEFAULT`: `int` A private static final int initialized to 2.
    - `MY_BOOLEAN_DEFAULT`: `boolean` A private static final boolean initialized to true.
    - `array`: `int[]` An integer array that is not initialized, defaulting to null.
    - `str1`: `String` A String initialized to MY_STRING_DEFAULT in the constructor.
    - `str2`: `String` A String that is not initialized, defaulting to null.
    - `int1`: `int` An integer initialized to MY_INT_DEFAULT.
    - `int2`: `int` An integer that is not initialized, defaulting to 0 as per JVM spec.
    - `bool1`: `boolean` A boolean initialized to MY_BOOLEAN_DEFAULT.
    - `bool2`: `boolean` A boolean that is not initialized, defaulting to false as per JVM spec.
- **Methods**:
    - [`com.google.gson.functional.NullObjectAndFieldTest.ClassWithInitializedMembers.ClassWithInitializedMembers`](#ClassWithInitializedMembersClassWithInitializedMembers)

**Methods**

---
#### ClassWithInitializedMembers\.ClassWithInitializedMembers<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.ClassWithInitializedMembers.ClassWithInitializedMembers}} -->
The constructor `ClassWithInitializedMembers` initializes the `str1` field to a default string value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor is invoked when an instance of `ClassWithInitializedMembers` is created.
    - The field `str1` is assigned the value of `MY_STRING_DEFAULT`, which is a static final string constant.
- **Output**:
    - The constructor does not return any value as it is used to initialize an object of the class.
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest.ClassWithInitializedMembers`](#NullObjectAndFieldTest.ClassWithInitializedMembers)  (Base Class)



---
### ClassWithNullWrappedPrimitive<!-- {{#class:com.google.gson.functional.NullObjectAndFieldTest.ClassWithNullWrappedPrimitive}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithNullWrappedPrimitive` is a simple private static class designed to encapsulate a single `Long` field named `value`, which can be null. This class is used in tests to verify the serialization and deserialization behavior of null-wrapped primitive types using Gson.
- **Fields**:
    - `value`: `Long` A `Long` field that can hold a null value, used to test serialization and deserialization of null-wrapped primitives.


---
### ClassWithMembers<!-- {{#class:com.google.gson.functional.NullObjectAndFieldTest.ClassWithMembers}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithMembers` class is a simple data structure that contains three fields: a string, an integer array, and a collection of strings, which are used to test serialization and deserialization of null values in JSON using the Gson library.
- **Fields**:
    - `str`: `String` A string field that can be serialized or deserialized as null.
    - `array`: `int[]` An integer array field that can be serialized or deserialized as null.
    - `col`: `Collection<String>` A collection of strings that can be serialized or deserialized as null.


---
### ClassWithObjectsSerializer<!-- {{#class:com.google.gson.functional.NullObjectAndFieldTest.ClassWithObjectsSerializer}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithObjectsSerializer` is a private static class that implements the `JsonSerializer` interface for the `ClassWithObjects` type, providing a custom serialization strategy that always serializes the `bag` field as `null` in the resulting JSON object.
- **Methods**:
    - [`com.google.gson.functional.NullObjectAndFieldTest.ClassWithObjectsSerializer.serialize`](#ClassWithObjectsSerializerserialize)

**Methods**

---
#### ClassWithObjectsSerializer\.serialize<!-- {{#callable:com.google.gson.functional.NullObjectAndFieldTest.ClassWithObjectsSerializer.serialize}} -->
The `serialize` method creates a JSON object with a single key 'bag' set to a null value.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `src`: An instance of ClassWithObjects to be serialized.
    - `typeOfSrc`: The specific type of the source object being serialized.
    - `context`: The context for serialization, providing methods to serialize other objects.
- **Control Flow**:
    - Create a new JsonObject instance named 'obj'.
    - Add a key 'bag' to 'obj' with a value of JsonNull.INSTANCE, representing a null value in JSON.
    - Return the JsonObject 'obj'.
- **Output**:
    - A JsonElement representing a JSON object with a single key 'bag' set to null.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
- **See also**: [`com.google.gson.functional.NullObjectAndFieldTest.ClassWithObjectsSerializer`](#NullObjectAndFieldTest.ClassWithObjectsSerializer)  (Base Class)



---
### ObjectWithField<!-- {{#class:com.google.gson.functional.NullObjectAndFieldTest.ObjectWithField}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ObjectWithField` class is a simple static inner class with a single field, `value`, which is a `String` initialized to an empty string. It is used in the context of testing serialization and deserialization behaviors, particularly focusing on handling null values and custom type adapters in the Gson library.
- **Fields**:
    - `value`: `String` A String field initialized to an empty string, used to test serialization and deserialization.


