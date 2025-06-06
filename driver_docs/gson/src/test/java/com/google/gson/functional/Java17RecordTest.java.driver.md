# Purpose
The Java source code file is a comprehensive suite of unit tests designed to validate the functionality of the Gson library, specifically focusing on its handling of Java 17 records. The file is structured using the JUnit4 testing framework and includes a series of test cases that cover various aspects of serialization and deserialization of records. These tests ensure that Gson correctly processes records with custom field names, handles multiple JSON property names, respects field naming strategies, and manages exceptions thrown by constructors and accessor methods. Additionally, the tests verify Gson's behavior with null values, primitive default values, and static fields, as well as its interaction with annotations like `@SerializedName`, `@Expose`, and `@JsonAdapter`.

The file also explores the use of exclusion strategies and reflection access filters, demonstrating how Gson can be configured to include or exclude certain fields or classes during serialization and deserialization. The tests are thorough, covering edge cases such as handling of unknown JSON properties, duplicate properties, and records without components. By providing a detailed examination of these scenarios, the file serves as a critical component in ensuring the robustness and reliability of the Gson library when working with Java records, a feature introduced in Java 14 and standardized in Java 16.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.ExclusionStrategy`
- `com.google.gson.FieldAttributes`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonDeserializationContext`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonIOException`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSerializationContext`
- `com.google.gson.JsonSerializer`
- `com.google.gson.ReflectionAccessFilter.FilterResult`
- `com.google.gson.TypeAdapter`
- `com.google.gson.annotations.Expose`
- `com.google.gson.annotations.JsonAdapter`
- `com.google.gson.annotations.SerializedName`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.Type`
- `org.junit.Test`
- `org.junit.runner.RunWith`
- `org.junit.runners.JUnit4`


# Classes

---
### Java17RecordTest<!-- {{#class:com.google.gson.functional.Java17RecordTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `Java17RecordTest` class is a JUnit test suite designed to test the serialization and deserialization behavior of Java 17 records using the Gson library. It includes various test cases to verify the correct handling of record components, including custom field names, primitive and object default values, static fields, and the use of annotations like `@SerializedName`, `@Expose`, and `@JsonAdapter`. The class also tests Gson's handling of reflection access filters and the behavior of records with throwing constructors or accessors.
- **Fields**:
    - `gson`: `Gson` An instance of the Gson class used for JSON serialization and deserialization.
- **Methods**:
    - [`com.google.gson.functional.Java17RecordTest.testFirstNameIsChosenForSerialization`](#Java17RecordTesttestFirstNameIsChosenForSerialization)
    - [`com.google.gson.functional.Java17RecordTest.testMultipleNamesDeserializedCorrectly`](#Java17RecordTesttestMultipleNamesDeserializedCorrectly)
    - [`com.google.gson.functional.Java17RecordTest.testMultipleNamesInTheSameString`](#Java17RecordTesttestMultipleNamesInTheSameString)
    - [`com.google.gson.functional.Java17RecordTest.testSerializedNameOnAccessor`](#Java17RecordTesttestSerializedNameOnAccessor)
    - [`com.google.gson.functional.Java17RecordTest.testFieldNamingStrategy`](#Java17RecordTesttestFieldNamingStrategy)
    - [`com.google.gson.functional.Java17RecordTest.testUnknownJsonProperty`](#Java17RecordTesttestUnknownJsonProperty)
    - [`com.google.gson.functional.Java17RecordTest.testDuplicateJsonProperties`](#Java17RecordTesttestDuplicateJsonProperties)
    - [`com.google.gson.functional.Java17RecordTest.testConstructorRuns`](#Java17RecordTesttestConstructorRuns)
    - [`com.google.gson.functional.Java17RecordTest.testThrowingConstructor`](#Java17RecordTesttestThrowingConstructor)
    - [`com.google.gson.functional.Java17RecordTest.testAccessorIsCalled`](#Java17RecordTesttestAccessorIsCalled)
    - [`com.google.gson.functional.Java17RecordTest.testThrowingAccessor`](#Java17RecordTesttestThrowingAccessor)
    - [`com.google.gson.functional.Java17RecordTest.testEmptyRecord`](#Java17RecordTesttestEmptyRecord)
    - [`com.google.gson.functional.Java17RecordTest.testRecordNull`](#Java17RecordTesttestRecordNull)
    - [`com.google.gson.functional.Java17RecordTest.testPrimitiveDefaultValues`](#Java17RecordTesttestPrimitiveDefaultValues)
    - [`com.google.gson.functional.Java17RecordTest.testPrimitiveJsonNullValue`](#Java17RecordTesttestPrimitiveJsonNullValue)
    - [`com.google.gson.functional.Java17RecordTest.testPrimitiveAdapterNullValue`](#Java17RecordTesttestPrimitiveAdapterNullValue)
    - [`com.google.gson.functional.Java17RecordTest.testObjectDefaultValue`](#Java17RecordTesttestObjectDefaultValue)
    - [`com.google.gson.functional.Java17RecordTest.testStaticFieldSerialization`](#Java17RecordTesttestStaticFieldSerialization)
    - [`com.google.gson.functional.Java17RecordTest.testStaticFieldDeserialization`](#Java17RecordTesttestStaticFieldDeserialization)
    - [`com.google.gson.functional.Java17RecordTest.testExposeAnnotation`](#Java17RecordTesttestExposeAnnotation)
    - [`com.google.gson.functional.Java17RecordTest.testFieldExclusionStrategy`](#Java17RecordTesttestFieldExclusionStrategy)
    - [`com.google.gson.functional.Java17RecordTest.testJsonAdapterAnnotation`](#Java17RecordTesttestJsonAdapterAnnotation)
    - [`com.google.gson.functional.Java17RecordTest.testClassReflectionFilter`](#Java17RecordTesttestClassReflectionFilter)
    - [`com.google.gson.functional.Java17RecordTest.testReflectionFilterBlockInaccessible`](#Java17RecordTesttestReflectionFilterBlockInaccessible)
    - [`com.google.gson.functional.Java17RecordTest.testRecordBaseClass`](#Java17RecordTesttestRecordBaseClass)

**Methods**

---
#### Java17RecordTest\.testFirstNameIsChosenForSerialization<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testFirstNameIsChosenForSerialization}} -->
The method `testFirstNameIsChosenForSerialization` verifies that the JSON serialization of a `RecordWithCustomNames` object correctly uses the first name for serialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `RecordWithCustomNames` object named `target` is instantiated with values "v1" and "v2".
    - The `gson.toJson(target)` method is called to serialize the `target` object into a JSON string.
    - An assertion is made using `assertThat` to check if the serialized JSON string is equal to `{"name":"v1","name1":"v2"}`.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the JSON serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testMultipleNamesDeserializedCorrectly<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testMultipleNamesDeserializedCorrectly}} -->
The `testMultipleNamesDeserializedCorrectly` method verifies that JSON properties with multiple possible names are correctly deserialized into the appropriate fields of a record using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson.fromJson` method to deserialize JSON strings into instances of `RecordWithCustomNames` class.
    - It asserts that the field `a` of the deserialized object is equal to the value associated with the 'name' property in the JSON.
    - It checks that the field `b` of the deserialized object is correctly set to the value of 'name1', 'name2', or 'name3' properties, depending on which is present in the JSON.
- **Output**:
    - The method does not return any value; it uses assertions to validate the deserialization behavior.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testMultipleNamesInTheSameString<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testMultipleNamesInTheSameString}} -->
The method `testMultipleNamesInTheSameString` tests the deserialization behavior of a JSON string with multiple fields having similar names, ensuring that the last field value takes precedence.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson.fromJson` method to deserialize a JSON string containing multiple fields with similar names ('name', 'name1', 'name2', 'name3') into an instance of `RecordWithCustomNames`.
    - The deserialized object's field `b` is checked to ensure it equals 'v3', which is the value of the last field ('name3') in the JSON string.
- **Output**:
    - The method does not return any value; it asserts that the deserialized value of field `b` is 'v3'.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testSerializedNameOnAccessor<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testSerializedNameOnAccessor}} -->
The method `testSerializedNameOnAccessor` tests that using the `@SerializedName` annotation on a record accessor method results in a `JsonIOException` being thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` is defined with a single integer component `i` and an accessor method `i()` that is annotated with `@SerializedName("a")`.
    - The method `gson.getAdapter(LocalRecord.class)` is called, which is expected to throw a `JsonIOException`.
    - The exception is caught and its message is asserted to be equal to a specific string indicating that `@SerializedName` on the method is not supported.
- **Output**:
    - The method does not return any value; it asserts that a `JsonIOException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.FieldAttributes.getName`](../../../../../../main/java/com/google/gson/FieldAttributes.java.driver.md#FieldAttributesgetName)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testFieldNamingStrategy<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testFieldNamingStrategy}} -->
The `testFieldNamingStrategy` method tests the custom field naming strategy in Gson serialization and deserialization for a local record.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` with an integer field `i` is defined.
    - A `Gson` instance is created with a custom field naming strategy that appends '-custom' to field names.
    - The method asserts that serializing a `LocalRecord` instance with value `1` results in a JSON string with the field name 'i-custom'.
    - The method asserts that deserializing a JSON string with the field name 'i-custom' and value `2` results in a `LocalRecord` instance with value `2`.
- **Output**:
    - The method does not return any value; it uses assertions to verify the expected behavior of the custom field naming strategy.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setFieldNamingStrategy`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetFieldNamingStrategy)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.FieldAttributes.getName`](../../../../../../main/java/com/google/gson/FieldAttributes.java.driver.md#FieldAttributesgetName)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testUnknownJsonProperty<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testUnknownJsonProperty}} -->
The `testUnknownJsonProperty` method tests that unknown JSON properties are ignored during deserialization using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` with a single integer field `i` is defined.
    - The method uses Gson to deserialize a JSON string containing known and unknown properties into an instance of `LocalRecord`.
    - The JSON string `{"i":1,"x":2}` is deserialized, where `i` is a known property and `x` is an unknown property.
    - An assertion checks that the deserialized object is equal to a new `LocalRecord` instance with the value `1`, confirming that the unknown property `x` is ignored.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of Gson when encountering unknown JSON properties.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testDuplicateJsonProperties<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testDuplicateJsonProperties}} -->
The `testDuplicateJsonProperties` method tests the behavior of Gson when deserializing JSON with duplicate properties, ensuring that the last occurrence of a property is used.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` with two Integer fields `a` and `b` is defined within the method.
    - A JSON string `json` is created with duplicate properties for `a` and `b`.
    - The method uses Gson to deserialize the JSON string into an instance of `LocalRecord`.
    - An assertion checks that the deserialized `LocalRecord` has the value of the last occurrence of each property, i.e., `a` is 2 and `b` is null.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the behavior of Gson.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testConstructorRuns<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testConstructorRuns}} -->
The `testConstructorRuns` method tests the behavior of a local record's constructor when deserializing JSON data using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` is defined with a single field [`s`](#Java17RecordTesttestAccessorIsCalled.s) and a constructor that prepends 'custom-' to the field [`s`](#Java17RecordTesttestAccessorIsCalled.s).
    - The method deserializes a JSON string `{"s": null}` into an instance of `LocalRecord` using Gson.
    - An assertion checks that the deserialized object is equal to a new `LocalRecord` instance with `null` as its field value.
    - Another assertion checks that the `s()` method of the deserialized object returns 'custom-null'.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the constructor.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.Java17RecordTest.testAccessorIsCalled.s`](#Java17RecordTesttestAccessorIsCalled.s)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testThrowingConstructor<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testThrowingConstructor}} -->
The `testThrowingConstructor` method tests the behavior of Gson when deserializing a JSON string into a record whose constructor throws a runtime exception.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` is defined with a single component `String s` and a constructor that throws a static `RuntimeException` named `thrownException`.
    - The method uses `assertThrows` to verify that deserializing a JSON string into `LocalRecord` using Gson results in a `RuntimeException`.
    - The exception message is checked to ensure it matches the expected message indicating a failure to invoke the constructor with the given arguments.
    - The cause of the exception is verified to be the same instance as `LocalRecord.thrownException`.
- **Output**:
    - The method does not return a value; it asserts that a `RuntimeException` is thrown and verifies the exception's message and cause.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.FieldAttributes.getName`](../../../../../../main/java/com/google/gson/FieldAttributes.java.driver.md#FieldAttributesgetName)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testAccessorIsCalled<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testAccessorIsCalled}} -->
The `testAccessorIsCalled` method tests that a custom accessor method in a local record is correctly called during JSON serialization using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` is defined with a single component `s` and an overridden accessor method `s()` that returns a fixed string 'accessor-value'.
    - The method uses Gson to serialize an instance of `LocalRecord` with a `null` value for `s`.
    - An assertion checks that the JSON output is equal to '{"s":"accessor-value"}', verifying that the overridden accessor method is called during serialization.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the accessor method during serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testThrowingAccessor<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testThrowingAccessor}} -->
The `testThrowingAccessor` method tests the behavior of a record accessor method that throws an exception during JSON serialization using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` is defined with a single component `s` and an accessor method `s()` that throws a static `RuntimeException` named `thrownException`.
    - The method uses `assertThrows` to verify that calling `gson.toJson` on a new instance of `LocalRecord` with a string argument throws a `JsonIOException`.
    - The test asserts that the exception message matches the expected message indicating the accessor method threw an exception.
    - The test also asserts that the cause of the exception is the same instance as `LocalRecord.thrownException`.
- **Output**:
    - The method does not return any value; it performs assertions to validate expected exceptions and their messages.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.FieldAttributes.getName`](../../../../../../main/java/com/google/gson/FieldAttributes.java.driver.md#FieldAttributesgetName)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testEmptyRecord<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testEmptyRecord}} -->
The `testEmptyRecord` method tests the serialization and deserialization of an empty record using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Defines a local record class `EmptyRecord` with no components.
    - Serializes an instance of `EmptyRecord` to JSON using `gson.toJson` and asserts that the result is an empty JSON object `{}`.
    - Deserializes an empty JSON object `{}` back into an `EmptyRecord` instance using `gson.fromJson` and asserts that it equals a new `EmptyRecord` instance.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of Gson with empty records.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testRecordNull<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testRecordNull}} -->
The `testRecordNull` method tests the serialization and deserialization of a null record value using Gson's TypeAdapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` with an integer field `i` is defined within the method.
    - A `TypeAdapter` for `LocalRecord` is obtained using `gson.getAdapter(LocalRecord.class)`.
    - The method asserts that serializing a null `LocalRecord` using the adapter results in the JSON string "null".
    - The method asserts that deserializing the JSON string "null" using the adapter results in a null `LocalRecord` object.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of Gson's TypeAdapter with null values.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testPrimitiveDefaultValues<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testPrimitiveDefaultValues}} -->
The `testPrimitiveDefaultValues` method verifies that deserialization of a JSON string into a `RecordWithPrimitives` object correctly assigns default values to primitive fields not specified in the JSON.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `RecordWithPrimitives` object named `expected` is created with default values for all primitive fields except `aString`, which is set to 's'.
    - The `gson.fromJson` method is called to deserialize the JSON string "{'aString': 's'}" into a `RecordWithPrimitives` object.
    - The `assertThat` method is used to check if the deserialized object is equal to the `expected` object.
- **Output**:
    - The method does not return any value; it asserts that the deserialized object matches the expected object.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testPrimitiveJsonNullValue<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testPrimitiveJsonNullValue}} -->
The `testPrimitiveJsonNullValue` method tests the behavior of Gson when deserializing a JSON string with a null value for a primitive type field, expecting a `JsonParseException` to be thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string `s` is defined with a null value for the 'aByte' field, which is a primitive type in the `RecordWithPrimitives` class.
    - The method uses `assertThrows` to check that deserializing this JSON string with Gson throws a `JsonParseException`.
    - The exception `e` is captured and its message is asserted to be equal to a specific error message indicating that null is not allowed for the primitive type field 'aByte'.
- **Output**:
    - The method does not return any value; it asserts that a `JsonParseException` is thrown with a specific error message.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testPrimitiveAdapterNullValue<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testPrimitiveAdapterNullValue}} -->
The `testPrimitiveAdapterNullValue` method tests the behavior of Gson when a custom adapter returns null for a primitive type during deserialization, expecting a `JsonParseException` to be thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder`, with a custom `TypeAdapter` registered for the `byte` primitive type.
    - The custom `TypeAdapter` overrides the `read` method to always return `null` and the `write` method to throw an `AssertionError`.
    - A JSON string `s` is defined with a non-null value for a byte field.
    - The method uses `assertThrows` to verify that deserializing the JSON string `s` into `RecordWithPrimitives` class throws a `JsonParseException`.
    - The exception message is asserted to confirm it indicates that `null` is not allowed for the primitive `aByte` field.
- **Output**:
    - The method does not return a value; it asserts that a `JsonParseException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testObjectDefaultValue<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testObjectDefaultValue}} -->
The `testObjectDefaultValue` method tests the deserialization of a JSON object into a Java record, ensuring that missing object components default to `null`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` with a `String` and an `int` component is defined within the method.
    - The method uses Gson to deserialize a JSON string `{"i":1}` into an instance of `LocalRecord`.
    - An assertion checks that the deserialized object is equal to a new `LocalRecord` instance with `null` for the `String` component and `1` for the `int` component.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the behavior of Gson deserialization.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testStaticFieldSerialization<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testStaticFieldSerialization}} -->
The `testStaticFieldSerialization` method tests the serialization behavior of static fields in a record using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method first asserts that by default, Gson ignores static fields by serializing a `RecordWithStaticField` instance and checking that the result is an empty JSON object `{}`.
    - A new `Gson` instance is created using `GsonBuilder`, configured to include static fields by calling `excludeFieldsWithModifiers(0)`.
    - The method serializes a `RecordWithStaticField` instance using the newly configured `Gson` instance and asserts that the resulting JSON string includes the static field, checking that it equals `{"s":"initial"}`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior of static field serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.GsonBuilder.excludeFieldsWithModifiers`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testStaticFieldDeserialization<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testStaticFieldDeserialization}} -->
The `testStaticFieldDeserialization` method tests the behavior of Gson when deserializing a JSON object into a record with a static field, ensuring that static fields are ignored during deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by deserializing a JSON string into a `RecordWithStaticField` object using a default `Gson` instance, which should ignore static fields, and asserts that the static field `s` remains unchanged with its initial value.
    - A new `Gson` instance is created with a `GsonBuilder` that includes static fields by setting `excludeFieldsWithModifiers(0)`.
    - The current value of the static field `s` is stored in `oldValue` for later restoration.
    - The method attempts to deserialize the JSON string again using the new `Gson` instance, asserts that the resulting object is not null, and checks that the static field `s` still retains its initial value, demonstrating that static fields are ignored during deserialization.
    - Finally, the static field `s` is restored to its original value using the `finally` block to ensure the static field is reset even if an exception occurs.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of static field deserialization.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.GsonBuilder.excludeFieldsWithModifiers`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testExposeAnnotation<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testExposeAnnotation}} -->
The `testExposeAnnotation` method tests the serialization behavior of a record with fields annotated with `@Expose` using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `RecordWithExpose` is defined with two fields, `a` and `b`, where `a` is annotated with `@Expose`.
    - A `Gson` instance is created using `GsonBuilder` with the configuration to exclude fields without the `@Expose` annotation.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the `Gson` instance is called to serialize an instance of `RecordWithExpose` with values `1` and `2`.
    - An assertion is made to check that the resulting JSON string is equal to `{"a":1}`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.excludeFieldsWithoutExposeAnnotation`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithoutExposeAnnotation)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testFieldExclusionStrategy<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testFieldExclusionStrategy}} -->
The `testFieldExclusionStrategy` method tests the functionality of excluding specific fields and classes from JSON serialization using a custom `ExclusionStrategy` in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` with fields `a`, `b`, and `c` is defined.
    - A `Gson` object is created using `GsonBuilder` with a custom `ExclusionStrategy`.
    - The `ExclusionStrategy` is defined to skip fields named 'a' and classes of type `double`.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of `Gson` is used to serialize an instance of `LocalRecord` with values (1, 2, 3.0).
    - An assertion checks that the resulting JSON string is equal to '{"b":2}', confirming that field 'a' and the class type `double` are excluded from serialization.
- **Output**:
    - The method does not return a value but asserts that the JSON serialization excludes the specified field and class type.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setExclusionStrategies`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetExclusionStrategies)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.FieldAttributes.getName`](../../../../../../main/java/com/google/gson/FieldAttributes.java.driver.md#FieldAttributesgetName)
    - [`com.google.gson.functional.MapTest.Point.equals`](MapTest.java.driver.md#Pointequals)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testJsonAdapterAnnotation<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testJsonAdapterAnnotation}} -->
The `testJsonAdapterAnnotation` method tests the serialization and deserialization of a record using a custom JSON adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Defines a record `Adapter` that implements `JsonSerializer` and `JsonDeserializer` for `String` type, providing custom serialization and deserialization logic.
    - Defines a `LocalRecord` with a `String` field annotated with `@JsonAdapter(Adapter.class)`, indicating that the `Adapter` should be used for this field.
    - Serializes a `LocalRecord` instance with the value "a" and asserts that the output JSON is `{"s":"serializer-a"}`.
    - Deserializes a JSON string `{"s":"a"}` into a `LocalRecord` and asserts that the resulting object is equivalent to a `LocalRecord` with the value "deserializer-a".
- **Output**:
    - The method does not return a value; it performs assertions to verify the behavior of the JSON adapter.
- **Functions called**:
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testClassReflectionFilter<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testClassReflectionFilter}} -->
The `testClassReflectionFilter` method tests the behavior of Gson's reflection access filter by allowing serialization of a specific record class and blocking another, verifying the expected JSON output and exception handling.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define two record classes, `Allowed` and `Blocked`, each with a single integer field.
    - Create a `Gson` instance using `GsonBuilder`, adding a reflection access filter that allows reflection for the `Allowed` class and blocks all others.
    - Serialize an instance of `Allowed` to JSON and assert that the output is as expected.
    - Attempt to serialize an instance of `Blocked`, expecting a `JsonIOException` to be thrown.
    - Assert that the exception message matches the expected message indicating that reflection is not permitted for the `Blocked` class.
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected behavior of the Gson reflection access filter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.addReflectionAccessFilter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderaddReflectionAccessFilter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.FieldAttributes.getName`](../../../../../../main/java/com/google/gson/FieldAttributes.java.driver.md#FieldAttributesgetName)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testReflectionFilterBlockInaccessible<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testReflectionFilterBlockInaccessible}} -->
The method `testReflectionFilterBlockInaccessible` tests the behavior of Gson when a reflection access filter is set to block inaccessible constructors during serialization and deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with a reflection access filter that blocks inaccessible constructors.
    - An attempt is made to serialize a `PrivateRecord` object, which is expected to throw a `JsonIOException` due to the inaccessible constructor, and the exception message is verified.
    - An attempt is made to deserialize a JSON string into a `PrivateRecord` object, which is also expected to throw a `JsonIOException`, and the exception message is verified.
    - A `PublicRecord` object is serialized and deserialized successfully, verifying that the reflection access filter does not block accessible constructors.
- **Output**:
    - The method does not return any value but asserts the expected exceptions and messages during the test execution.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.addReflectionAccessFilter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderaddReflectionAccessFilter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)


---
#### Java17RecordTest\.testRecordBaseClass<!-- {{#callable:com.google.gson.functional.Java17RecordTest.testRecordBaseClass}} -->
The `testRecordBaseClass` method tests the behavior of Gson when serializing and deserializing a local record using `java.lang.Record` as the type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecord` with an integer component is defined within the method.
    - The method asserts that serializing a `LocalRecord` instance to JSON using `Record.class` as the type results in an empty JSON object (`{}`).
    - The method then attempts to deserialize an empty JSON object (`{}`) into a `Record.class`, expecting a `JsonIOException` to be thrown.
    - The exception is caught and asserted to have a specific message indicating that abstract classes cannot be instantiated and suggesting solutions.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the expected behavior of Gson when handling records with `java.lang.Record` as the type.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.Java17RecordTest`](#Java17RecordTest)  (Base Class)



