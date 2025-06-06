# Purpose
The provided Java source code file is a comprehensive suite of functional tests for the Gson library, specifically focusing on the serialization and deserialization of various object types. The file is part of the `com.google.gson.functional` package and utilizes JUnit for testing. It includes a series of test cases that validate the correct behavior of Gson when handling different data structures, such as primitive types, arrays, nested objects, and classes with special characteristics like transient fields, static fields, and private constructors. The tests cover a wide range of scenarios, including handling of null values, empty collections, and deeply nested structures, ensuring that Gson can serialize and deserialize these structures accurately.

The file defines a class `ObjectTest` that contains multiple test methods annotated with `@Test`, each designed to verify a specific aspect of Gson's functionality. The tests make use of various helper classes, such as `BagOfPrimitives`, `Nested`, and `ClassWithArray`, to simulate real-world data structures. The setup and teardown methods, annotated with `@Before` and `@After`, respectively, ensure that the environment is correctly configured before each test and restored afterward. The file also includes tests for edge cases, such as handling of duplicate fields and serialization of anonymous and local classes, which are crucial for maintaining the robustness of the Gson library. Overall, this file serves as a critical component in ensuring the reliability and correctness of Gson's JSON processing capabilities.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.ExclusionStrategy`
- `com.google.gson.FieldAttributes`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.InstanceCreator`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonIOException`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSerializer`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.common.TestTypes.ArrayOfObjects`
- `com.google.gson.common.TestTypes.BagOfPrimitiveWrappers`
- `com.google.gson.common.TestTypes.BagOfPrimitives`
- `com.google.gson.common.TestTypes.ClassWithArray`
- `com.google.gson.common.TestTypes.ClassWithNoFields`
- `com.google.gson.common.TestTypes.ClassWithObjects`
- `com.google.gson.common.TestTypes.ClassWithTransientFields`
- `com.google.gson.common.TestTypes.Nested`
- `com.google.gson.common.TestTypes.PrimitiveArray`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.EOFException`
- `java.lang.reflect.Type`
- `java.util.ArrayList`
- `java.util.Collection`
- `java.util.Date`
- `java.util.HashMap`
- `java.util.List`
- `java.util.Locale`
- `java.util.Map`
- `java.util.TimeZone`
- `org.junit.After`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### ObjectTest<!-- {{#class:com.google.gson.functional.ObjectTest}} -->
- **Modifiers**: `public`
- **Description**: The `ObjectTest` class is a comprehensive suite of functional tests for JSON serialization and deserialization using the Gson library. It includes a variety of test cases to validate the correct handling of different data structures, such as primitives, arrays, nested objects, and classes with transient fields. The class also tests edge cases like null values, empty strings, and deeply nested JSON objects. Additionally, it verifies the behavior of Gson with static fields, anonymous classes, and custom serialization/deserialization strategies. The setup and teardown methods ensure consistent test environments by managing time zones and locales.
- **Fields**:
    - `gson`: `Gson` An instance of Gson used for JSON serialization and deserialization.
    - `oldTimeZone`: `TimeZone` Stores the original default time zone to restore after tests.
    - `oldLocale`: `Locale` Stores the original default locale to restore after tests.
- **Methods**:
    - [`com.google.gson.functional.ObjectTest.setUp`](#ObjectTestsetUp)
    - [`com.google.gson.functional.ObjectTest.tearDown`](#ObjectTesttearDown)
    - [`com.google.gson.functional.ObjectTest.testJsonInSingleQuotesDeserialization`](#ObjectTesttestJsonInSingleQuotesDeserialization)
    - [`com.google.gson.functional.ObjectTest.testJsonInMixedQuotesDeserialization`](#ObjectTesttestJsonInMixedQuotesDeserialization)
    - [`com.google.gson.functional.ObjectTest.testBagOfPrimitivesSerialization`](#ObjectTesttestBagOfPrimitivesSerialization)
    - [`com.google.gson.functional.ObjectTest.testBagOfPrimitivesDeserialization`](#ObjectTesttestBagOfPrimitivesDeserialization)
    - [`com.google.gson.functional.ObjectTest.testBagOfPrimitiveWrappersSerialization`](#ObjectTesttestBagOfPrimitiveWrappersSerialization)
    - [`com.google.gson.functional.ObjectTest.testBagOfPrimitiveWrappersDeserialization`](#ObjectTesttestBagOfPrimitiveWrappersDeserialization)
    - [`com.google.gson.functional.ObjectTest.testClassWithTransientFieldsSerialization`](#ObjectTesttestClassWithTransientFieldsSerialization)
    - [`com.google.gson.functional.ObjectTest.testClassWithTransientFieldsDeserialization`](#ObjectTesttestClassWithTransientFieldsDeserialization)
    - [`com.google.gson.functional.ObjectTest.testClassWithTransientFieldsDeserializationTransientFieldsPassedInJsonAreIgnored`](#ObjectTesttestClassWithTransientFieldsDeserializationTransientFieldsPassedInJsonAreIgnored)
    - [`com.google.gson.functional.ObjectTest.testClassWithNoFieldsSerialization`](#ObjectTesttestClassWithNoFieldsSerialization)
    - [`com.google.gson.functional.ObjectTest.testClassWithNoFieldsDeserialization`](#ObjectTesttestClassWithNoFieldsDeserialization)
    - [`com.google.gson.functional.ObjectTest.testClassWithDuplicateFields`](#ObjectTesttestClassWithDuplicateFields)
    - [`com.google.gson.functional.ObjectTest.testNestedSerialization`](#ObjectTesttestNestedSerialization)
    - [`com.google.gson.functional.ObjectTest.testNestedDeserialization`](#ObjectTesttestNestedDeserialization)
    - [`com.google.gson.functional.ObjectTest.testNullSerialization`](#ObjectTesttestNullSerialization)
    - [`com.google.gson.functional.ObjectTest.testEmptyStringDeserialization`](#ObjectTesttestEmptyStringDeserialization)
    - [`com.google.gson.functional.ObjectTest.testTruncatedDeserialization`](#ObjectTesttestTruncatedDeserialization)
    - [`com.google.gson.functional.ObjectTest.testNullDeserialization`](#ObjectTesttestNullDeserialization)
    - [`com.google.gson.functional.ObjectTest.testNullFieldsSerialization`](#ObjectTesttestNullFieldsSerialization)
    - [`com.google.gson.functional.ObjectTest.testNullFieldsDeserialization`](#ObjectTesttestNullFieldsDeserialization)
    - [`com.google.gson.functional.ObjectTest.testArrayOfObjectsSerialization`](#ObjectTesttestArrayOfObjectsSerialization)
    - [`com.google.gson.functional.ObjectTest.testArrayOfObjectsDeserialization`](#ObjectTesttestArrayOfObjectsDeserialization)
    - [`com.google.gson.functional.ObjectTest.testArrayOfArraysSerialization`](#ObjectTesttestArrayOfArraysSerialization)
    - [`com.google.gson.functional.ObjectTest.testArrayOfArraysDeserialization`](#ObjectTesttestArrayOfArraysDeserialization)
    - [`com.google.gson.functional.ObjectTest.testArrayOfObjectsAsFields`](#ObjectTesttestArrayOfObjectsAsFields)
    - [`com.google.gson.functional.ObjectTest.testNullArraysDeserialization`](#ObjectTesttestNullArraysDeserialization)
    - [`com.google.gson.functional.ObjectTest.testNullObjectFieldsDeserialization`](#ObjectTesttestNullObjectFieldsDeserialization)
    - [`com.google.gson.functional.ObjectTest.testEmptyCollectionInAnObjectDeserialization`](#ObjectTesttestEmptyCollectionInAnObjectDeserialization)
    - [`com.google.gson.functional.ObjectTest.testPrimitiveArrayInAnObjectDeserialization`](#ObjectTesttestPrimitiveArrayInAnObjectDeserialization)
    - [`com.google.gson.functional.ObjectTest.testNullPrimitiveFieldsDeserialization`](#ObjectTesttestNullPrimitiveFieldsDeserialization)
    - [`com.google.gson.functional.ObjectTest.testEmptyCollectionInAnObjectSerialization`](#ObjectTesttestEmptyCollectionInAnObjectSerialization)
    - [`com.google.gson.functional.ObjectTest.testPrivateNoArgConstructorDeserialization`](#ObjectTesttestPrivateNoArgConstructorDeserialization)
    - [`com.google.gson.functional.ObjectTest.testAnonymousLocalClassesSerialization`](#ObjectTesttestAnonymousLocalClassesSerialization)
    - [`com.google.gson.functional.ObjectTest.testAnonymousLocalClassesCustomSerialization`](#ObjectTesttestAnonymousLocalClassesCustomSerialization)
    - [`com.google.gson.functional.ObjectTest.testAnonymousLocalClassesCustomDeserialization`](#ObjectTesttestAnonymousLocalClassesCustomDeserialization)
    - [`com.google.gson.functional.ObjectTest.testPrimitiveArrayFieldSerialization`](#ObjectTesttestPrimitiveArrayFieldSerialization)
    - [`com.google.gson.functional.ObjectTest.testClassWithObjectFieldSerialization`](#ObjectTesttestClassWithObjectFieldSerialization)
    - [`com.google.gson.functional.ObjectTest.testInnerClassSerialization`](#ObjectTesttestInnerClassSerialization)
    - [`com.google.gson.functional.ObjectTest.testInnerClassDeserialization`](#ObjectTesttestInnerClassDeserialization)
    - [`com.google.gson.functional.ObjectTest.testObjectFieldNamesWithoutQuotesDeserialization`](#ObjectTesttestObjectFieldNamesWithoutQuotesDeserialization)
    - [`com.google.gson.functional.ObjectTest.testStringFieldWithNumberValueDeserialization`](#ObjectTesttestStringFieldWithNumberValueDeserialization)
    - [`com.google.gson.functional.ObjectTest.testStringFieldWithEmptyValueSerialization`](#ObjectTesttestStringFieldWithEmptyValueSerialization)
    - [`com.google.gson.functional.ObjectTest.testStringFieldWithEmptyValueDeserialization`](#ObjectTesttestStringFieldWithEmptyValueDeserialization)
    - [`com.google.gson.functional.ObjectTest.testJsonObjectSerialization`](#ObjectTesttestJsonObjectSerialization)
    - [`com.google.gson.functional.ObjectTest.testSingletonLists`](#ObjectTesttestSingletonLists)
    - [`com.google.gson.functional.ObjectTest.testDateAsMapObjectField`](#ObjectTesttestDateAsMapObjectField)
    - [`com.google.gson.functional.ObjectTest.testStaticFieldSerialization`](#ObjectTesttestStaticFieldSerialization)
    - [`com.google.gson.functional.ObjectTest.testStaticFieldDeserialization`](#ObjectTesttestStaticFieldDeserialization)
    - [`com.google.gson.functional.ObjectTest.testThrowingDefaultConstructor`](#ObjectTesttestThrowingDefaultConstructor)
    - [`com.google.gson.functional.ObjectTest.testDeeplyNested`](#ObjectTesttestDeeplyNested)

**Methods**

---
#### ObjectTest\.setUp<!-- {{#callable:com.google.gson.functional.ObjectTest.setUp}} -->
Sets up the test environment by initializing `Gson` and configuring default `TimeZone` and `Locale`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Initializes the `gson` variable with a new instance of `Gson`.
    - Stores the current default `TimeZone` in `oldTimeZone`.
    - Sets the default `TimeZone` to 'America/Los_Angeles'.
    - Stores the current default `Locale` in `oldLocale`.
    - Sets the default `Locale` to `Locale.US`.
- **Output**:
    - This method does not return any value; it prepares the test environment for subsequent tests.
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.tearDown<!-- {{#callable:com.google.gson.functional.ObjectTest.tearDown}} -->
The `tearDown` method resets the default `TimeZone` and `Locale` to their original values after each test.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with `@After`, indicating it runs after each test method in the class.
    - It sets the default `TimeZone` back to the value stored in `oldTimeZone`.
    - It sets the default `Locale` back to the value stored in `oldLocale`.
- **Output**:
    - The method does not return any value; it performs cleanup operations.
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testJsonInSingleQuotesDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testJsonInSingleQuotesDeserialization}} -->
Tests the deserialization of a JSON string with single quotes into a `BagOfPrimitives` object.
- **Inputs**:
    - `json`: A JSON string formatted with single quotes representing the properties of a `BagOfPrimitives` object.
- **Control Flow**:
    - The method initializes a string `json` containing a JSON representation of a `BagOfPrimitives` object with single quotes.
    - It then uses the `gson.fromJson` method to deserialize the JSON string into a `BagOfPrimitives` object named `target`.
    - Finally, it asserts that the properties of the `target` object match the expected values using assertions.
- **Output**:
    - The method does not return a value; it performs assertions to verify that the deserialized object's properties are correct.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testJsonInMixedQuotesDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testJsonInMixedQuotesDeserialization}} -->
Tests the deserialization of a JSON string with mixed quotes into a `BagOfPrimitives` object.
- **Inputs**:
    - `json`: A JSON string containing mixed quotes for string values and integer values.
- **Control Flow**:
    - The method initializes a JSON string with mixed quotes.
    - It uses the `gson.fromJson` method to deserialize the JSON string into a `BagOfPrimitives` object.
    - Assertions are made to verify that the deserialized object's fields match the expected values.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's fields are correctly populated.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testBagOfPrimitivesSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testBagOfPrimitivesSerialization}} -->
Tests the serialization of a `BagOfPrimitives` object to JSON.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `target`: An instance of `BagOfPrimitives` initialized with specific values (10, 20, false, 'stringValue').
- **Control Flow**:
    - Creates an instance of `BagOfPrimitives` with predefined values.
    - Uses `gson.toJson(target)` to serialize the `target` object to JSON.
    - Asserts that the serialized JSON matches the expected JSON representation obtained from `target.getExpectedJson()`.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON string matches the expected JSON format.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testBagOfPrimitivesDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testBagOfPrimitivesDeserialization}} -->
Tests the deserialization of a `BagOfPrimitives` object from its JSON representation.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `src`: An instance of `BagOfPrimitives` initialized with specific values.
    - `json`: A JSON string representation of the `BagOfPrimitives` instance obtained from `src.getExpectedJson()`.
    - `target`: A new instance of `BagOfPrimitives` created by deserializing the JSON string.
- **Control Flow**:
    - Creates a `BagOfPrimitives` object named `src` with predefined values.
    - Calls `getExpectedJson()` on `src` to obtain its JSON representation.
    - Deserializes the JSON string back into a new `BagOfPrimitives` object named `target` using `gson.fromJson()`.
    - Asserts that the JSON representation of `target` matches the original JSON string.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object matches the original JSON representation.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testBagOfPrimitiveWrappersSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testBagOfPrimitiveWrappersSerialization}} -->
Tests the serialization of a `BagOfPrimitiveWrappers` object to JSON.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `target`: An instance of `BagOfPrimitiveWrappers` initialized with specific primitive values.
- **Control Flow**:
    - Creates a new instance of `BagOfPrimitiveWrappers` with specified values.
    - Uses the `gson` object to convert the `target` instance to its JSON representation.
    - Asserts that the generated JSON matches the expected JSON output from `target.getExpectedJson()`.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `target` matches the expected JSON.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testBagOfPrimitiveWrappersDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testBagOfPrimitiveWrappersDeserialization}} -->
Tests the deserialization of a `BagOfPrimitiveWrappers` object from its JSON representation.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates an instance of `BagOfPrimitiveWrappers` with predefined values.
    - Retrieves the expected JSON string representation of the created object.
    - Deserializes the JSON string back into a `BagOfPrimitiveWrappers` object using Gson.
    - Asserts that the JSON representation of the deserialized object matches the original JSON string.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object matches the expected JSON.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testClassWithTransientFieldsSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testClassWithTransientFieldsSerialization}} -->
Tests the serialization of a class with transient fields.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `target`: An instance of `ClassWithTransientFields<Long>` initialized with a Long value.
- **Control Flow**:
    - Creates an instance of `ClassWithTransientFields<Long>` with a value of 1L.
    - Serializes the `target` object to JSON using the `gson` instance.
    - Asserts that the serialized JSON matches the expected JSON representation of the `target` object.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON matches the expected format.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testClassWithTransientFieldsDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testClassWithTransientFieldsDeserialization}} -->
Tests the deserialization of a JSON string into a `ClassWithTransientFields` object.
- **Inputs**:
    - `json`: A JSON string representing an object with a field `longValue`.
- **Control Flow**:
    - The method initializes a JSON string with a specific structure.
    - It uses the `gson.fromJson` method to deserialize the JSON string into an instance of `ClassWithTransientFields`.
    - Finally, it asserts that the expected JSON string matches the JSON representation of the deserialized object.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's expected JSON matches the input JSON.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testClassWithTransientFieldsDeserializationTransientFieldsPassedInJsonAreIgnored<!-- {{#callable:com.google.gson.functional.ObjectTest.testClassWithTransientFieldsDeserializationTransientFieldsPassedInJsonAreIgnored}} -->
Tests that transient fields in a class are ignored during JSON deserialization.
- **Inputs**:
    - `json`: A JSON string containing both transient and non-transient fields.
- **Control Flow**:
    - The method initializes a JSON string with a transient field and a regular field.
    - It uses `gson.fromJson` to deserialize the JSON string into an instance of `ClassWithTransientFields`.
    - The method then asserts that the value of the transient field is equal to 1, which indicates that the transient field was ignored during deserialization.
- **Output**:
    - The method does not return a value; it asserts that the transient field was ignored.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testClassWithNoFieldsSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testClassWithNoFieldsSerialization}} -->
Tests the serialization of a class with no fields to ensure it produces an empty JSON object.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method calls `gson.toJson()` with a new instance of `ClassWithNoFields`.
    - The result of the serialization is then compared to the expected output, which is an empty JSON object (`{}`).
- **Output**:
    - The method does not return a value; it asserts that the serialized output is equal to the expected empty JSON object.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testClassWithNoFieldsDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testClassWithNoFieldsDeserialization}} -->
Tests the deserialization of a JSON string into a class with no fields.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `json`: A JSON string representing an empty object, which is '{}'
- **Control Flow**:
    - The method initializes a JSON string representing an empty object.
    - It uses the `gson.fromJson` method to deserialize the JSON string into an instance of `ClassWithNoFields`.
    - An expected instance of `ClassWithNoFields` is created for comparison.
    - The method asserts that the deserialized object is equal to the expected object.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object matches the expected instance.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testClassWithDuplicateFields<!-- {{#callable:com.google.gson.functional.ObjectTest.testClassWithDuplicateFields}} -->
Tests the behavior of the Gson library when handling classes with duplicate JSON field names.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Defines an expected error message indicating the presence of duplicate fields in the class hierarchy.
    - Asserts that an `IllegalArgumentException` is thrown when attempting to get a Gson adapter for the `Subclass` class, which has duplicate fields.
    - Verifies that the exception message matches the expected error message.
    - Creates a new `Gson` instance with a deserialization exclusion strategy that skips all fields.
    - Asserts again that an `IllegalArgumentException` is thrown when getting a Gson adapter for the `Subclass` class with the new Gson instance.
    - Checks that the exception message matches the expected error message again.
- **Output**:
    - The method does not return a value but asserts that the expected exception is thrown with the correct message.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.GsonBuilder.addDeserializationExclusionStrategy`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderaddDeserializationExclusionStrategy)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNestedSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNestedSerialization}} -->
Tests the serialization of a `Nested` object containing two `BagOfPrimitives` instances.
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `Nested` with two `BagOfPrimitives` objects as parameters.
    - Calls `gson.toJson(target)` to serialize the `target` object into a JSON string.
    - Asserts that the serialized JSON string is equal to the expected JSON string returned by `target.getExpectedJson()`.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON matches the expected format.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNestedDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNestedDeserialization}} -->
Tests the deserialization of a nested JSON structure into a `Nested` object.
- **Inputs**:
    - `json`: A string representing a JSON object containing two nested objects with primitive values.
- **Control Flow**:
    - The method defines a JSON string that represents a nested structure with two primitives.
    - It uses the `gson.fromJson` method to deserialize the JSON string into an instance of the `Nested` class.
    - Finally, it asserts that the expected JSON string matches the JSON representation of the deserialized `Nested` object.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object matches the original JSON string.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNullSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNullSerialization}} -->
Tests the serialization of a null value to ensure it is represented as 'null' in JSON.
- **Inputs**: None
- **Control Flow**:
    - The method calls `gson.toJson(null)` to convert a null value to its JSON representation.
    - It then asserts that the result is equal to the string 'null'.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of null is 'null'.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testEmptyStringDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testEmptyStringDeserialization}} -->
Tests the deserialization of an empty string to ensure it results in a null object.
- **Inputs**:
    - `gson`: An instance of `Gson` used to perform the deserialization.
- **Control Flow**:
    - The method calls `gson.fromJson` with an empty string and the `Object.class` type.
    - The result of the deserialization is stored in the variable `object`.
    - An assertion is made to check that `object` is null.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object is null.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testTruncatedDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testTruncatedDeserialization}} -->
Tests the behavior of Gson when deserializing a truncated JSON string.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `type`: A `Type` object representing the expected type of the deserialized object, in this case, a `List<String>`.
- **Control Flow**:
    - A `Type` object is created using `TypeToken` to specify the expected type for deserialization.
    - The method `gson.fromJson` is called with a malformed JSON string that is missing a closing bracket.
    - The `assertThrows` method is used to verify that a `JsonParseException` is thrown during the deserialization process.
    - The cause of the exception is checked to ensure it is an instance of `EOFException`, indicating that the end of the file was reached unexpectedly.
- **Output**:
    - The method does not return a value; instead, it asserts that a `JsonParseException` is thrown with a specific cause.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNullDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNullDeserialization}} -->
Tests that deserializing a null string results in a null object.
- **Inputs**:
    - `myNullObject`: A String variable initialized to null, representing the JSON input to be deserialized.
- **Control Flow**:
    - The method initializes a String variable `myNullObject` to null.
    - It then calls `gson.fromJson` with `myNullObject` and `Object.class` to attempt deserialization.
    - Finally, it asserts that the resulting object is null using `assertThat`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object is null.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNullFieldsSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNullFieldsSerialization}} -->
Tests the serialization of a `Nested` object containing a `BagOfPrimitives` and a null field.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `target`: An instance of `Nested` initialized with a `BagOfPrimitives` object and a null value.
- **Control Flow**:
    - Creates a new instance of `Nested` with a `BagOfPrimitives` object and a null value.
    - Serializes the `target` object to JSON using the `gson` instance.
    - Asserts that the serialized JSON matches the expected JSON representation of the `target` object.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `target` matches the expected output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNullFieldsDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNullFieldsDeserialization}} -->
Tests the deserialization of a JSON string into a `Nested` object.
- **Inputs**:
    - `json`: A JSON string representing a `Nested` object with a non-null `primitive1` field.
- **Control Flow**:
    - The method defines a JSON string that represents a `Nested` object with a `primitive1` field containing various primitive values.
    - It uses the `gson.fromJson` method to deserialize the JSON string into a `Nested` object.
    - Finally, it asserts that the expected JSON string is equal to the JSON representation of the deserialized `Nested` object.
- **Output**:
    - The method does not return a value but asserts that the deserialized object matches the original JSON string.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testArrayOfObjectsSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testArrayOfObjectsSerialization}} -->
Tests the serialization of an `ArrayOfObjects` instance to JSON.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `target`: An instance of the `ArrayOfObjects` class that is being serialized.
- **Control Flow**:
    - Creates an instance of `ArrayOfObjects` named `target`.
    - Uses the `gson` object to convert `target` to its JSON representation.
    - Asserts that the generated JSON matches the expected JSON returned by `target.getExpectedJson()`.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `ArrayOfObjects` instance is as expected.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testArrayOfObjectsDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testArrayOfObjectsDeserialization}} -->
Tests the deserialization of an array of objects from JSON.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Calls `getExpectedJson()` on an instance of `ArrayOfObjects` to retrieve the expected JSON string.
    - Uses `gson.fromJson()` to deserialize the JSON string into an instance of `ArrayOfObjects`.
    - Asserts that the JSON representation of the deserialized object matches the original JSON string.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object matches the expected JSON.
- **Functions called**:
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testArrayOfArraysSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testArrayOfArraysSerialization}} -->
Tests the serialization of an `ArrayOfArrays` object to JSON.
- **Inputs**: None
- **Control Flow**:
    - Creates an instance of `ArrayOfArrays`.
    - Serializes the `ArrayOfArrays` instance to JSON using `gson.toJson()`.
    - Asserts that the serialized JSON matches the expected JSON output from `target.getExpectedJson()`.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON string matches the expected format.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testArrayOfArraysDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testArrayOfArraysDeserialization}} -->
Tests the deserialization of an array of arrays using Gson.
- **Modifiers**: `public`, `Test`
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a JSON string representation of an `ArrayOfArrays` object by calling its `getExpectedJson()` method.
    - Deserializes the JSON string into an `ArrayOfArrays` object using the `gson.fromJson()` method.
    - Asserts that the JSON representation of the deserialized `ArrayOfArrays` object matches the original JSON string.
- **Output**:
    - This method does not return a value; it performs assertions to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testArrayOfObjectsAsFields<!-- {{#callable:com.google.gson.functional.ObjectTest.testArrayOfObjectsAsFields}} -->
This method tests the serialization of an array containing various object types into JSON.
- **Inputs**:
    - `classWithObjects`: An instance of `ClassWithObjects`, which is a custom class used for testing.
    - `bagOfPrimitives`: An instance of `BagOfPrimitives`, which contains primitive data types.
    - `stringValue`: A string value used as one of the elements in the array.
- **Control Flow**:
    - Creates instances of `ClassWithObjects` and `BagOfPrimitives`.
    - Serializes these instances to JSON strings using `gson.toJson()`.
    - Creates an instance of `ClassWithArray` with an array containing the string, `ClassWithObjects`, and `BagOfPrimitives`.
    - Serializes the `ClassWithArray` instance to JSON.
    - Asserts that the resulting JSON contains the serialized forms of `classWithObjects`, `bagOfPrimitives`, and the string value.
- **Output**:
    - The method does not return a value but asserts that the JSON output contains the expected serialized representations of the input objects.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNullArraysDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNullArraysDeserialization}} -->
Tests the deserialization of a JSON string containing a null array.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A JSON string is created with an array field set to null.
    - The `gson.fromJson` method is called to deserialize the JSON string into an instance of `ClassWithArray`.
    - An assertion is made to verify that the `array` field of the deserialized object is null.
- **Output**:
    - The method does not return a value; it asserts that the `array` field of the deserialized object is null.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNullObjectFieldsDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNullObjectFieldsDeserialization}} -->
Tests the deserialization of a JSON string with a null object field.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `json`: A JSON string representing an object with a field 'bag' set to null.
- **Control Flow**:
    - The method initializes a JSON string with a null value for the 'bag' field.
    - It then uses the `gson.fromJson` method to deserialize the JSON string into an instance of `ClassWithObjects`.
    - Finally, it asserts that the `bag` field of the deserialized object is null using `assertThat`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's 'bag' field is null.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testEmptyCollectionInAnObjectDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testEmptyCollectionInAnObjectDeserialization}} -->
Tests the deserialization of a JSON string representing an object with an empty collection.
- **Inputs**:
    - `json`: A JSON string representing an object with a field 'children' that is an empty array.
- **Control Flow**:
    - The method begins by defining a JSON string that represents an object with an empty collection.
    - It then uses the `gson.fromJson` method to deserialize the JSON string into an instance of `ClassWithCollectionField`.
    - After deserialization, it asserts that the resulting object is not null.
    - Finally, it checks that the 'children' collection in the deserialized object is empty.
- **Output**:
    - The method does not return a value; instead, it performs assertions to verify that the deserialized object is correctly instantiated and that its 'children' collection is empty.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.JsonObject.isEmpty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectisEmpty)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testPrimitiveArrayInAnObjectDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testPrimitiveArrayInAnObjectDeserialization}} -->
Tests the deserialization of a JSON string into a `PrimitiveArray` object.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing an object with a long array is defined.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `PrimitiveArray` object.
    - An assertion is made to check if the expected JSON string matches the JSON representation of the deserialized `PrimitiveArray` object.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object matches the expected JSON string.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testNullPrimitiveFieldsDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testNullPrimitiveFieldsDeserialization}} -->
Tests the deserialization of a JSON string with a null value for a primitive field.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `json`: A JSON string representing an object with a null value for the 'longValue' field.
- **Control Flow**:
    - The method initializes a JSON string with a null value for the 'longValue' field.
    - It then uses the `gson.fromJson` method to deserialize the JSON string into an instance of `BagOfPrimitives`.
    - Finally, it asserts that the `longValue` field of the deserialized object is equal to the default value defined in `BagOfPrimitives`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's `longValue` is equal to the default value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testEmptyCollectionInAnObjectSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testEmptyCollectionInAnObjectSerialization}} -->
Tests the serialization of an object containing an empty collection.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `target`: An instance of `ClassWithCollectionField` which contains a collection field named `children`.
- **Control Flow**:
    - An instance of `ClassWithCollectionField` is created, which initializes the `children` collection to an empty list.
    - The `gson.toJson(target)` method is called to serialize the `target` object into a JSON string.
    - The resulting JSON string is compared to the expected output using an assertion.
- **Output**:
    - The method asserts that the JSON representation of the `target` object is equal to the string '{"children":[]}', indicating that the empty collection is correctly serialized.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testPrivateNoArgConstructorDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testPrivateNoArgConstructorDeserialization}} -->
Tests the deserialization of a class with a private no-argument constructor.
- **Inputs**:
    - `none`: This method does not take any input arguments.
- **Control Flow**:
    - The method uses the `gson` object to deserialize a JSON string into an instance of `ClassWithPrivateNoArgsConstructor`.
    - It checks if the field `a` of the deserialized object equals 20 using an assertion.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's field `a` is equal to 20.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testAnonymousLocalClassesSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testAnonymousLocalClassesSerialization}} -->
Tests the serialization of anonymous local classes using Gson.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - The method begins by asserting that the JSON representation of an empty anonymous class derived from `ClassWithNoFields` is 'null'.
    - Next, it defines a local class `Local` and asserts that the JSON representation of an instance of this local class is also 'null'.
- **Output**:
    - The method does not return a value; it performs assertions to verify that the JSON output for the anonymous classes is 'null'.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testAnonymousLocalClassesCustomSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testAnonymousLocalClassesCustomSerialization}} -->
Tests custom serialization of anonymous local classes using Gson.
- **Modifiers**: `public`, `Test`
- **Inputs**:
    - `gson`: An instance of `Gson` configured with custom serializers for specific classes.
- **Control Flow**:
    - A `Gson` instance is created with a custom serializer for `ClassWithNoFields` that returns a `JsonPrimitive` with the value 'custom-value'.
    - An anonymous class extending `ClassWithNoFields` is serialized, and the output is asserted to equal '"custom-value"'.
    - A local class `Local` is defined, and another `Gson` instance is created with a custom serializer for `Local` that also returns 'custom-value'.
    - An instance of `Local` is serialized, and the output is asserted to equal '"custom-value"'.
- **Output**:
    - The method outputs assertions that confirm the serialized JSON strings for the anonymous local classes match the expected custom values.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testAnonymousLocalClassesCustomDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testAnonymousLocalClassesCustomDeserialization}} -->
Tests the custom deserialization behavior of anonymous local classes using Gson.
- **Inputs**:
    - `gson`: An instance of `Gson` configured with custom deserializers for specific classes.
- **Control Flow**:
    - Creates a `Gson` instance with a custom deserializer for `ClassWithNoFields` that returns a new instance of the class.
    - Asserts that deserializing an empty JSON object into `ClassWithNoFields` returns a non-null instance.
    - Creates an anonymous class based on `ClassWithNoFields` and asserts that deserializing an empty JSON object into this anonymous class returns null, indicating the custom deserializer is ignored.
    - Defines a local class `Local` and creates another `Gson` instance with a custom deserializer that throws an error when called.
    - Asserts that deserializing an empty JSON object into the local class `Local` also returns null, confirming the custom deserializer is ignored.
- **Output**:
    - The method does not return a value but performs assertions to validate the deserialization behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testPrimitiveArrayFieldSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testPrimitiveArrayFieldSerialization}} -->
Tests the serialization of a `PrimitiveArray` object to JSON.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `target`: An instance of `PrimitiveArray` initialized with a long array containing values 1, 2, and 3.
- **Control Flow**:
    - Creates a new instance of `PrimitiveArray` with a long array.
    - Uses the `gson` object to convert the `target` to its JSON representation.
    - Asserts that the generated JSON matches the expected JSON from `target.getExpectedJson()`.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `PrimitiveArray` matches the expected output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testClassWithObjectFieldSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testClassWithObjectFieldSerialization}} -->
Tests the serialization of a class with an Object field.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `obj`: An instance of `ClassWithObjectField` which contains a member variable.
- **Control Flow**:
    - An instance of `ClassWithObjectField` is created.
    - The `member` field of the object is set to the string 'abc'.
    - The `gson.toJson()` method is called to serialize the object to JSON format.
    - An assertion checks that the resulting JSON string contains the value 'abc'.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON contains the expected string.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testInnerClassSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testInnerClassSerialization}} -->
Tests the serialization of an inner class using Gson.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates an instance of the `Parent` class.
    - Creates an instance of the inner `Child` class using the `Parent` instance.
    - Serializes the `Child` instance to JSON format using `gson.toJson(c)`.
    - Asserts that the resulting JSON string contains the field `value2`.
    - Asserts that the resulting JSON string does not contain the field `value1`.
- **Output**:
    - The method does not return a value; it performs assertions to validate the JSON output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testInnerClassDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testInnerClassDeserialization}} -->
Tests the deserialization of an inner class using Gson.
- **Modifiers**: `public`, `@Test`
- **Inputs**:
    - `json`: A string representation of a JSON object that contains a field 'value2' with an integer value.
- **Control Flow**:
    - Creates an instance of the outer class `Parent`.
    - Initializes a `Gson` instance with a custom `InstanceCreator` for the inner class `Parent.Child`.
    - Deserializes the provided JSON string into an instance of `Parent.Child`.
    - Asserts that the deserialized `value2` field equals 3.
- **Output**:
    - An instance of `Parent.Child` with its `value2` field set to the value from the JSON input.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testObjectFieldNamesWithoutQuotesDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testObjectFieldNamesWithoutQuotesDeserialization}} -->
Tests the deserialization of JSON with field names that do not use quotes.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `json`: A string representing a JSON object with field names and values, where some field names are not enclosed in quotes.
- **Control Flow**:
    - The method initializes a JSON string with field names that are not quoted.
    - It uses the `gson.fromJson` method to deserialize the JSON string into an instance of `BagOfPrimitives`.
    - Assertions are made to verify that the deserialized object's fields match the expected values.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's fields have the expected values.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testStringFieldWithNumberValueDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testStringFieldWithNumberValueDeserialization}} -->
Tests the deserialization of a JSON string into a `BagOfPrimitives` object, specifically handling numeric and boolean values as strings.
- **Inputs**:
    - `json`: A JSON string representing an object with a field `stringValue` that can hold numeric and boolean values.
- **Control Flow**:
    - The method initializes a JSON string with a numeric value (1) and deserializes it into a `BagOfPrimitives` object using `gson.fromJson`.
    - It asserts that the `stringValue` field of the deserialized object is equal to the string representation of the numeric value ("1").
    - The method repeats the process with a different numeric value (1.5E+6) and checks that `stringValue` is equal to "1.5E+6".
    - Finally, it tests with a boolean value (true) and asserts that `stringValue` is equal to "true".
- **Output**:
    - The method does not return a value; instead, it performs assertions to verify that the `stringValue` field in the `BagOfPrimitives` object correctly reflects the string representation of the input JSON values.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testStringFieldWithEmptyValueSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testStringFieldWithEmptyValueSerialization}} -->
Tests the serialization of a class with string fields, ensuring that empty values are correctly represented in JSON.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates an instance of `ClassWithEmptyStringFields` and assigns a non-empty value to field `a`.
    - Serializes the `target` object to JSON using `gson.toJson()`.
    - Asserts that the resulting JSON contains the expected representation of field `a` with its value.
    - Asserts that the resulting JSON contains the expected representation of fields `b` and `c`, which should be empty strings.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the object matches expected values.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testStringFieldWithEmptyValueDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testStringFieldWithEmptyValueDeserialization}} -->
Tests the deserialization of a JSON string with empty values into a class with string fields.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `json`: A JSON string representing an object with fields 'a', 'b', and 'c', where 'b' and 'c' are empty strings.
- **Control Flow**:
    - The method initializes a JSON string with specific values for testing.
    - It uses the `gson.fromJson` method to deserialize the JSON string into an instance of `ClassWithEmptyStringFields`.
    - Assertions are made to verify that the fields of the deserialized object match the expected values.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's fields are correctly populated.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testJsonObjectSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testJsonObjectSerialization}} -->
Tests the serialization of an empty `JsonObject` to JSON format.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with the [`serializeNulls`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls) option enabled.
    - An empty `JsonObject` is instantiated.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of `Gson` is called to serialize the `JsonObject` to a JSON string.
    - An assertion checks that the resulting JSON string is equal to an empty JSON object '{}'.
- **Output**:
    - The method outputs a JSON string representation of the empty `JsonObject`, which is expected to be '{}'. 
- **Functions called**:
    - [`com.google.gson.Gson.serializeNulls`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testSingletonLists<!-- {{#callable:com.google.gson.functional.ObjectTest.testSingletonLists}} -->
Tests the serialization and deserialization of a `Product` object using Gson.
- **Inputs**: None
- **Control Flow**:
    - Creates an instance of `Gson` and a `Product` object.
    - Asserts that the JSON representation of the `Product` object is an empty object with empty attributes and departments.
    - Deserializes the JSON back into a `Product` object and checks that its attributes and departments are empty.
    - Adds a `Department` to the `Product` and asserts the JSON representation reflects this addition.
    - Deserializes the updated JSON and checks that the `departments` list contains one item.
    - Adds an attribute to the `Product` and asserts the JSON representation reflects this addition.
    - Deserializes the final JSON and checks that the `attributes` list contains the added attribute and the `departments` list still contains one item.
- **Output**:
    - The method does not return a value but performs assertions to verify the correctness of JSON serialization and deserialization of the `Product` object.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.JsonObject.isEmpty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectisEmpty)
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testDateAsMapObjectField<!-- {{#callable:com.google.gson.functional.ObjectTest.testDateAsMapObjectField}} -->
Tests the serialization of a `Date` object stored in a map.
- **Modifiers**: `public`, `Test`, `SuppressWarnings`
- **Inputs**:
    - `this`: The instance of the class where the method is defined.
- **Control Flow**:
    - Creates an instance of `HasObjectMap` which contains a map.
    - Adds a `Date` object representing the epoch (January 1, 1970) to the map with the key 'date'.
    - Serializes the `HasObjectMap` instance to JSON using `gson.toJson()`.
    - Asserts that the resulting JSON matches the expected format for the date.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the object matches the expected format.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
    - [`com.google.gson.reflect.TypeToken.matches`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenmatches)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testStaticFieldSerialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testStaticFieldSerialization}} -->
Tests the serialization of static fields using Gson.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - The method begins by asserting that Gson ignores static fields by default, expecting an empty JSON object for a class with a static field.
    - A new `Gson` instance is created with a configuration that includes static fields by excluding fields with modifiers of 0.
    - The method serializes an instance of `ClassWithStaticField` and asserts that the resulting JSON contains the expected static field value.
    - It then serializes an instance of `ClassWithStaticFinalField` and asserts that the resulting JSON also contains the expected static field value.
- **Output**:
    - The method does not return a value but asserts that the serialized JSON matches expected values for static fields.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.GsonBuilder.excludeFieldsWithModifiers`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testStaticFieldDeserialization<!-- {{#callable:com.google.gson.functional.ObjectTest.testStaticFieldDeserialization}} -->
Tests the deserialization behavior of static fields in a class using Gson.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method begins by deserializing a JSON string into an instance of `ClassWithStaticField`, expecting the static field to be ignored.
    - It asserts that the deserialized object is not null and that the static field retains its initial value.
    - A new `Gson` instance is created with a configuration to include static fields.
    - The original value of the static field is saved, and the method attempts to deserialize the same JSON string again, expecting the static field to be updated.
    - It asserts that the deserialized object is not null and that the static field now reflects the new value from the JSON.
    - Finally, it tests deserialization into `ClassWithStaticFinalField`, expecting a `JsonIOException` to be thrown due to the static final field's immutability.
- **Output**:
    - The method does not return a value but asserts various conditions to validate the deserialization behavior of static fields.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.GsonBuilder.excludeFieldsWithModifiers`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testThrowingDefaultConstructor<!-- {{#callable:com.google.gson.functional.ObjectTest.testThrowingDefaultConstructor}} -->
Tests the behavior of Gson when attempting to instantiate a class with a constructor that throws an exception.
- **Modifiers**: `public`, `void`, `@Test`
- **Inputs**:
    - `gson`: An instance of `Gson` used to perform JSON deserialization.
    - `ClassWithThrowingConstructor.class`: The class type that has a constructor which throws an exception.
- **Control Flow**:
    - The method uses `assertThrows` to check if a `RuntimeException` is thrown when attempting to deserialize an empty JSON object into `ClassWithThrowingConstructor`.
    - If the exception is thrown, it captures the exception in variable `e`.
    - The method then asserts that the message of the exception matches the expected failure message indicating the constructor invocation failure.
    - Finally, it checks that the cause of the exception is the same instance as the static `thrownException` defined in `ClassWithThrowingConstructor`.
- **Output**:
    - The method does not return a value; it asserts conditions to validate the behavior of the Gson library when handling exceptions during object construction.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)


---
#### ObjectTest\.testDeeplyNested<!-- {{#callable:com.google.gson.functional.ObjectTest.testDeeplyNested}} -->
Tests the deserialization of deeply nested JSON structures and verifies the handling of nesting limits.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Initializes a variable `defaultLimit` to 255, which represents the maximum allowed nesting level for JSON deserialization.
    - Constructs a valid JSON string `json` that contains a deeply nested structure with `defaultLimit` levels of nesting.
    - Deserializes the `json` string into an instance of `RecursiveClass` and asserts that the deserialized object is not null and its nested field `r` is also not null.
    - Constructs another JSON string `json2` that exceeds the nesting limit by one level.
    - Attempts to deserialize `json2` and expects a `JsonSyntaxException` to be thrown due to exceeding the nesting limit.
    - Asserts that the exception has a cause of type `MalformedJsonException` and checks the exception message to confirm it indicates the nesting limit was reached.
- **Output**:
    - The method does not return a value but asserts conditions to verify the correctness of JSON deserialization and exception handling.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ObjectTest`](#ObjectTest)  (Base Class)



---
### Subclass<!-- {{#class:com.google.gson.functional.ObjectTest.Subclass}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Subclass` is a private static class that extends `Superclass1`, inheriting its properties and methods. It is used within the `ObjectTest` class to demonstrate and test the behavior of classes with duplicate field names in the context of JSON serialization and deserialization using Gson.
- **Extends/Implements**:
    - [`com.google.gson.functional.ObjectTest.Superclass1`](#ObjectTest.Superclass1)


---
### Superclass1<!-- {{#class:com.google.gson.functional.ObjectTest.Superclass1}} -->
- **Modifiers**: `private`, `static`
- **Description**: `Superclass1` is a private static class that extends `Superclass2` and contains a single string field `s`, which is suppressed for unused and hiding field warnings.
- **Fields**:
    - `s`: `String` A string field that is suppressed for unused and hiding field warnings.
- **Extends/Implements**:
    - [`com.google.gson.functional.ObjectTest.Superclass2`](#ObjectTest.Superclass2)


---
### Superclass2<!-- {{#class:com.google.gson.functional.ObjectTest.Superclass2}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Superclass2` class is a simple private static inner class that contains a single string field `s`, which is annotated with `@SuppressWarnings("unused")` to indicate that the field is intentionally unused in the code.
- **Fields**:
    - `s`: `String` A string field that is not used in the code, marked with `@SuppressWarnings("unused")`.


---
### ClassWithCollectionField<!-- {{#class:com.google.gson.functional.ObjectTest.ClassWithCollectionField}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithCollectionField` is a simple class that contains a single field, `children`, which is a collection of strings initialized as an empty `ArrayList`. This class is used to demonstrate serialization and deserialization of objects with collection fields in JSON using Gson.
- **Fields**:
    - `children`: `Collection<String>` A collection of strings initialized as an empty ArrayList.


---
### Local<!-- {{#class:com.google.gson.functional.ObjectTest.testAnonymousLocalClassesCustomDeserialization.Local}} -->
- **Description**: The `Local` class is an empty class defined within the `ObjectTest` class, primarily used for testing purposes in the context of JSON serialization and deserialization using the Gson library. It serves as a placeholder to demonstrate the handling of local classes in serialization and deserialization processes.


---
### ClassWithObjectField<!-- {{#class:com.google.gson.functional.ObjectTest.ClassWithObjectField}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithObjectField` is a simple class that contains a single field of type `Object`, which can hold any type of object. This class is used to demonstrate serialization and deserialization of a class with a generic object field using Gson.
- **Fields**:
    - `member`: `Object` A field of type `Object` that can store any object.


---
### Parent<!-- {{#class:com.google.gson.functional.ObjectTest.Parent}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `Parent` class is a private static class that contains an integer field `value1` and an inner class `Child`. The `Child` class, which is non-static and private, contains its own integer field `value2`. This structure demonstrates a simple parent-child relationship within a class, where the `Parent` class holds a value and the `Child` class holds another value, potentially for testing or demonstration purposes.
- **Fields**:
    - `value1`: `int` An integer field initialized to 1, representing a value in the Parent class.


---
### Child<!-- {{#class:com.google.gson.functional.ObjectTest.Parent.Child}} -->
- **Modifiers**: `private`
- **Description**: The `Child` class is a simple inner class within the `Parent` class, primarily used to demonstrate serialization and deserialization of inner classes in the context of JSON processing with Gson. It contains a single integer field and is marked with a suppression warning to indicate that it could be static, although it is not.
- **Fields**:
    - `value2`: `int` An integer field initialized to 2.


---
### ArrayOfArrays<!-- {{#class:com.google.gson.functional.ObjectTest.ArrayOfArrays}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ArrayOfArrays` class is a private static class that encapsulates a two-dimensional array of `BagOfPrimitives` objects, initialized with specific values based on their indices. It provides a method to generate a JSON representation of the array structure, which is useful for testing serialization and deserialization processes.
- **Fields**:
    - `elements`: `BagOfPrimitives[][]` A two-dimensional array of `BagOfPrimitives` objects, initialized with specific values based on their indices.
- **Methods**:
    - [`com.google.gson.functional.ObjectTest.ArrayOfArrays.ArrayOfArrays`](#ArrayOfArraysArrayOfArrays)
    - [`com.google.gson.functional.ObjectTest.ArrayOfArrays.getExpectedJson`](#ArrayOfArraysgetExpectedJson)

**Methods**

---
#### ArrayOfArrays\.ArrayOfArrays<!-- {{#callable:com.google.gson.functional.ObjectTest.ArrayOfArrays.ArrayOfArrays}} -->
The `ArrayOfArrays` constructor initializes a 2D array of `BagOfPrimitives` objects with specific values based on their indices.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a 2D array `elements` of type `BagOfPrimitives` with dimensions 3x2.
    - Iterate over the rows of the `elements` array using a for-loop with index `i`.
    - For each row, iterate over its columns using a nested for-loop with index `j`.
    - Create a new `BagOfPrimitives` object for each element in the array, using `i + j` for the first parameter, `i * j` for the second parameter, `false` for the third parameter, and a string `i + "_" + j` for the fourth parameter.
    - Assign the newly created `BagOfPrimitives` object to the current position in the array.
- **Output**:
    - A fully initialized 2D array of `BagOfPrimitives` objects stored in the `elements` field.
- **See also**: [`com.google.gson.functional.ObjectTest.ArrayOfArrays`](#ObjectTest.ArrayOfArrays)  (Base Class)


---
#### ArrayOfArrays\.getExpectedJson<!-- {{#callable:com.google.gson.functional.ObjectTest.ArrayOfArrays.getExpectedJson}} -->
The [`getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson) method constructs and returns a JSON string representation of a two-dimensional array of `BagOfPrimitives` objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `StringBuilder` with the starting JSON structure `{"elements":[`.
    - Set a boolean flag `first` to `true` to track the first row in the array.
    - Iterate over each row in the `elements` array of `BagOfPrimitives` objects.
    - For each row, check if it is the first row; if not, append a comma to separate JSON arrays.
    - Set a boolean flag `firstOfRow` to `true` to track the first element in the row.
    - Append the opening bracket `[` for the JSON array of the current row.
    - Iterate over each `BagOfPrimitives` object in the current row.
    - For each element, check if it is the first element in the row; if not, append a comma to separate JSON objects.
    - Append the JSON representation of the current `BagOfPrimitives` object by calling its [`getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson) method.
    - Append the closing bracket `]` for the JSON array of the current row.
    - Append the closing bracket `]` for the `elements` array in the JSON structure.
    - Return the constructed JSON string from the `StringBuilder`.
- **Output**:
    - A JSON string representing the two-dimensional array of `BagOfPrimitives` objects.
- **Functions called**:
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.append`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectionappend)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.ObjectTest.ArrayOfArrays`](#ObjectTest.ArrayOfArrays)  (Base Class)



---
### ClassWithPrivateNoArgsConstructor<!-- {{#class:com.google.gson.functional.ObjectTest.ClassWithPrivateNoArgsConstructor}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithPrivateNoArgsConstructor` is a simple static inner class with a private no-argument constructor that initializes an integer field `a` to 10. This class is used to demonstrate deserialization of objects with private constructors in the context of JSON processing using Gson.
- **Fields**:
    - `a`: `int` An integer field initialized to 10 in the private constructor.
- **Methods**:
    - [`com.google.gson.functional.ObjectTest.ClassWithPrivateNoArgsConstructor.ClassWithPrivateNoArgsConstructor`](#ClassWithPrivateNoArgsConstructorClassWithPrivateNoArgsConstructor)

**Methods**

---
#### ClassWithPrivateNoArgsConstructor\.ClassWithPrivateNoArgsConstructor<!-- {{#callable:com.google.gson.functional.ObjectTest.ClassWithPrivateNoArgsConstructor.ClassWithPrivateNoArgsConstructor}} -->
The private constructor of the `ClassWithPrivateNoArgsConstructor` class initializes the integer field `a` to 10.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is private, meaning it cannot be accessed from outside the class.
    - The integer field `a` is initialized to the value 10.
- **Output**:
    - This constructor does not return any value as it is a constructor.
- **See also**: [`com.google.gson.functional.ObjectTest.ClassWithPrivateNoArgsConstructor`](#ObjectTest.ClassWithPrivateNoArgsConstructor)  (Base Class)



---
### ClassWithEmptyStringFields<!-- {{#class:com.google.gson.functional.ObjectTest.ClassWithEmptyStringFields}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithEmptyStringFields` is a simple class designed to hold three string fields, each initialized to an empty string. This class can be used to test serialization and deserialization processes, particularly focusing on handling empty string values in JSON data.
- **Fields**:
    - `a`: `String` A string field initialized to an empty string.
    - `b`: `String` A string field initialized to an empty string.
    - `c`: `String` A string field initialized to an empty string.


---
### Department<!-- {{#class:com.google.gson.functional.ObjectTest.Department}} -->
- **Modifiers**: `static`, `final`
- **Description**: The `Department` class is a simple data structure that represents a department with a name and a code, both of which are initialized to default values.
- **Fields**:
    - `name`: `String` A public string field representing the name of the department, initialized to "abc".
    - `code`: `String` A public string field representing the code of the department, initialized to "123".


---
### Product<!-- {{#class:com.google.gson.functional.ObjectTest.Product}} -->
- **Modifiers**: `static`, `final`
- **Description**: The `Product` class is a static final class that represents a product with a list of attributes and a list of departments, encapsulating the characteristics and associated departments of a product.
- **Fields**:
    - `attributes`: `List<String>` A list of strings representing the attributes of the product.
    - `departments`: `List<Department>` A list of `Department` objects representing the departments associated with the product.


---
### HasObjectMap<!-- {{#class:com.google.gson.functional.ObjectTest.HasObjectMap}} -->
- **Modifiers**: `static`
- **Description**: The `HasObjectMap` class is a simple static class that contains a single field, a `Map` with `String` keys and `Object` values, initialized as a `HashMap`. This class is designed to store a collection of key-value pairs where the keys are strings and the values can be any object.
- **Fields**:
    - `map`: `Map<String, Object>` A map that holds key-value pairs with String keys and Object values, initialized as a HashMap.


---
### ClassWithStaticField<!-- {{#class:com.google.gson.functional.ObjectTest.ClassWithStaticField}} -->
- **Modifiers**: `static`
- **Description**: The `ClassWithStaticField` class is a simple utility class that contains a single static field `s` initialized to the string "initial". This class is designed to demonstrate the behavior of static fields in serialization and deserialization processes, particularly in the context of the Gson library.
- **Fields**:
    - `s`: `String` A static string field initialized to "initial".


---
### ClassWithStaticFinalField<!-- {{#class:com.google.gson.functional.ObjectTest.ClassWithStaticFinalField}} -->
- **Modifiers**: `static`
- **Description**: The `ClassWithStaticFinalField` is a utility class that contains a single static final field `s`, which is initialized to the string "initial". This class is designed to demonstrate the behavior of static final fields in serialization and deserialization processes, particularly in the context of the Gson library.
- **Fields**:
    - `s`: `String` A static final string field initialized to "initial".


---
### ClassWithThrowingConstructor<!-- {{#class:com.google.gson.functional.ObjectTest.ClassWithThrowingConstructor}} -->
- **Modifiers**: `static`
- **Description**: The `ClassWithThrowingConstructor` is a static class designed to demonstrate a constructor that throws a predefined `RuntimeException` upon instantiation. This class is primarily used for testing purposes to ensure that exception handling mechanisms are correctly implemented when a constructor fails.
- **Fields**:
    - `thrownException`: `RuntimeException` A static final field that holds a `RuntimeException` with a custom message, which is thrown by the class constructor.
- **Methods**:
    - [`com.google.gson.functional.ObjectTest.ClassWithThrowingConstructor.ClassWithThrowingConstructor`](#ClassWithThrowingConstructorClassWithThrowingConstructor)

**Methods**

---
#### ClassWithThrowingConstructor\.ClassWithThrowingConstructor<!-- {{#callable:com.google.gson.functional.ObjectTest.ClassWithThrowingConstructor.ClassWithThrowingConstructor}} -->
The constructor of the `ClassWithThrowingConstructor` class throws a predefined `RuntimeException` when invoked.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor is invoked.
    - Immediately upon invocation, the constructor throws a `RuntimeException` defined as `thrownException`.
- **Output**:
    - The constructor does not return any value as it throws an exception upon invocation.
- **See also**: [`com.google.gson.functional.ObjectTest.ClassWithThrowingConstructor`](#ObjectTest.ClassWithThrowingConstructor)  (Base Class)



---
### RecursiveClass<!-- {{#class:com.google.gson.functional.ObjectTest.RecursiveClass}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `RecursiveClass` is a simple class designed to demonstrate recursive data structures, where an instance of `RecursiveClass` contains a reference to another instance of the same class, allowing for potentially infinite nesting.
- **Fields**:
    - `r`: `RecursiveClass` A reference to another instance of `RecursiveClass`, enabling recursive nesting.


