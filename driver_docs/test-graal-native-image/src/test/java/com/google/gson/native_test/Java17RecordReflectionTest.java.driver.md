# Purpose
The Java source code file is a comprehensive test suite designed to validate the functionality of Java 17 records in conjunction with the Gson library, which is used for JSON serialization and deserialization. The file contains a series of JUnit tests that explore various scenarios involving records, such as public and private records, local records, and records with custom serialization and deserialization logic. Each test method is focused on a specific aspect of record handling, ensuring that Gson correctly processes records with different configurations, including those with custom constructors, accessors, and field names specified via annotations like `@SerializedName`.

The file also demonstrates the use of custom `TypeAdapter` implementations to modify the default serialization and deserialization behavior of records. This is achieved through both class-level and field-level adapters, as well as adapters registered with a `GsonBuilder`. The tests ensure that these custom adapters correctly transform the JSON input and output according to the specified logic. Overall, the file serves as a detailed exploration of how Java records can be integrated with Gson, providing a robust set of examples for handling various customization scenarios in JSON processing.
# Imports and Dependencies

---
- `com.google.gson.native_test`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.TypeAdapter`
- `com.google.gson.annotations.JsonAdapter`
- `com.google.gson.annotations.SerializedName`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `org.junit.jupiter.api.Test`


# Classes

---
### Java17RecordReflectionTest<!-- {{#class:com.google.gson.native_test.Java17RecordReflectionTest}} -->
- **Description**: The `Java17RecordReflectionTest` class is a test suite designed to validate the serialization and deserialization of Java records using the Gson library. It includes various test cases that demonstrate the use of public, private, and local records, as well as records with custom constructors, accessors, and adapters. The class showcases how Gson can handle records with custom field names, custom serialization logic, and registered type adapters, ensuring that the records are correctly serialized to and deserialized from JSON.
- **Methods**:
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testPublicRecord`](#Java17RecordReflectionTesttestPublicRecord)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testPrivateRecord`](#Java17RecordReflectionTesttestPrivateRecord)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testLocalRecord`](#Java17RecordReflectionTesttestLocalRecord)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testLocalRecordSerialization`](#Java17RecordReflectionTesttestLocalRecordSerialization)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testSerializedName`](#Java17RecordReflectionTesttestSerializedName)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testCustomConstructor`](#Java17RecordReflectionTesttestCustomConstructor)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.i`](#Java17RecordReflectionTesti)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testCustomAccessor`](#Java17RecordReflectionTesttestCustomAccessor)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testCustomClassAdapter`](#Java17RecordReflectionTesttestCustomClassAdapter)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testCustomFieldAdapter`](#Java17RecordReflectionTesttestCustomFieldAdapter)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.testCustomAdapter`](#Java17RecordReflectionTesttestCustomAdapter)

**Methods**

---
#### Java17RecordReflectionTest\.testPublicRecord<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testPublicRecord}} -->
The `testPublicRecord` method tests the deserialization of a JSON string into a `PublicRecord` object using Gson and verifies the value of its field.
- **Modifiers**: ``
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - The [`fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of the `Gson` object is called with a JSON string `{"i":1}` and the `PublicRecord.class` to deserialize the JSON into a `PublicRecord` object.
    - An assertion is made using `assertThat` to verify that the field `i` of the `PublicRecord` object is equal to 1.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testPrivateRecord<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testPrivateRecord}} -->
The `testPrivateRecord` method tests the deserialization of a JSON string into a private record using Gson and verifies the value of the record's field.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - A new instance of Gson is created.
    - The JSON string '{"i":1}' is deserialized into an instance of the `PrivateRecord` class using Gson's [`fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method.
    - An assertion is made to check that the field `i` of the deserialized `PrivateRecord` instance is equal to 1.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testLocalRecord<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testLocalRecord}} -->
The `testLocalRecord` method tests the deserialization of a local record using Gson.
- **Modifiers**: `void`
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecordDeserialization` with an integer field `i` is defined within the method.
    - A `Gson` object is instantiated to handle JSON operations.
    - The [`fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of `Gson` is used to deserialize a JSON string `{"i":1}` into an instance of `LocalRecordDeserialization`.
    - An assertion is made using `assertThat` to verify that the field `i` of the deserialized record is equal to 1.
- **Output**:
    - The method does not return any value but asserts that the deserialization process correctly sets the field `i` to 1.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testLocalRecordSerialization<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testLocalRecordSerialization}} -->
The `testLocalRecordSerialization` method tests the serialization of a local record using Gson to ensure it produces the expected JSON output.
- **Modifiers**: ``
- **Inputs**: None
- **Control Flow**:
    - A local record `LocalRecordSerialization` with a single integer field `i` is defined within the method.
    - An instance of `Gson` is created to handle JSON serialization.
    - A new instance of `LocalRecordSerialization` is created with the integer value `1`.
    - The [`toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of `Gson` is used to serialize the `LocalRecordSerialization` instance to a JSON string.
    - An assertion is made using `assertThat` to verify that the serialized JSON string is equal to the expected string `{"i":1}`.
- **Output**:
    - The method does not return any value, but it performs an assertion to verify the correctness of the JSON serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testSerializedName<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testSerializedName}} -->
The `testSerializedName` method tests the serialization and deserialization of a record with a custom field name using Gson.
- **Modifiers**: `void`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated.
    - The JSON string `{"custom-name":1}` is deserialized into a `RecordWithSerializedName` object using Gson.
    - An assertion checks that the field `i` of the deserialized object equals 1.
    - A `RecordWithSerializedName` object is created with the value 2 for field `i`.
    - The object is serialized back to JSON using Gson.
    - An assertion checks that the serialized JSON string equals `{"custom-name":2}`.
- **Output**:
    - The method does not return any value but performs assertions to verify correct serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testCustomConstructor<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testCustomConstructor}} -->
The `testCustomConstructor` method tests the deserialization of a JSON string into a `RecordWithCustomConstructor` object using Gson, verifying that the custom constructor logic is applied.
- **Modifiers**: `@Test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - The [`fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of the `Gson` object is called to deserialize the JSON string `{"i":1}` into an instance of `RecordWithCustomConstructor`.
    - The custom constructor of `RecordWithCustomConstructor` adds 5 to the deserialized value of `i`, resulting in `i` being 6.
    - An assertion is made using `assertThat` to verify that the value of `i` in the deserialized object is equal to 6.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the behavior of the custom constructor during deserialization.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.i<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.i}} -->
The method `i` overrides the default accessor to return the value of the field `i` incremented by 5.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the field `i` plus 5.
- **Output**:
    - The method returns an integer value, which is the field `i` incremented by 5.
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testCustomAccessor<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testCustomAccessor}} -->
The `testCustomAccessor` method tests the serialization of a `RecordWithCustomAccessor` object using Gson, verifying that the custom accessor method is correctly applied during serialization.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON serialization.
    - A `RecordWithCustomAccessor` object is created with an initial value of 2 for its field `i`.
    - The [`toJson`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the `Gson` object is called to serialize the `RecordWithCustomAccessor` object.
    - The custom accessor method `i()` in `RecordWithCustomAccessor` adds 5 to the field `i` during serialization, resulting in a serialized JSON string with the value 7 for `i`.
    - An assertion is made to check that the serialized JSON string is equal to `{"i":7}`.
- **Output**:
    - The method does not return any value, but it asserts that the serialized JSON string of the `RecordWithCustomAccessor` object is `{"i":7}`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testCustomClassAdapter<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testCustomClassAdapter}} -->
The `testCustomClassAdapter` method tests the serialization and deserialization of a `RecordWithCustomClassAdapter` using a custom `TypeAdapter` in Gson.
- **Modifiers**: `void`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created.
    - The [`fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of `Gson` is used to deserialize the integer `1` into a `RecordWithCustomClassAdapter` object, which uses a custom adapter to add 5 to the input value, resulting in an object with `i` equal to 6.
    - An assertion checks that the deserialized object's `i` field is equal to 6.
    - The [`toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of `Gson` is used to serialize a `RecordWithCustomClassAdapter` object initialized with `i` equal to 1, which uses a custom adapter to add 6 to the `i` value, resulting in the JSON string `"7"`.
    - An assertion checks that the serialized JSON string is equal to `"7"`.
- **Output**:
    - The method does not return any value but performs assertions to verify the correctness of serialization and deserialization using a custom adapter.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testCustomFieldAdapter<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testCustomFieldAdapter}} -->
The `testCustomFieldAdapter` method tests the serialization and deserialization of a record with a custom field adapter using Gson.
- **Modifiers**: `@Test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created.
    - The [`fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson) method of `Gson` is used to deserialize a JSON string `{"i":1}` into an instance of `RecordWithCustomFieldAdapter`.
    - The deserialized field `i` of the record is asserted to be equal to 6, verifying the custom adapter's read logic.
    - The [`toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of `Gson` is used to serialize a new `RecordWithCustomFieldAdapter` instance with `i` initialized to 1.
    - The serialized JSON string is asserted to be `{"i":7}`, verifying the custom adapter's write logic.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the custom field adapter.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)


---
#### Java17RecordReflectionTest\.testCustomAdapter<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.testCustomAdapter}} -->
The `testCustomAdapter` method tests the serialization and deserialization of a `RecordWithRegisteredAdapter` using a custom `TypeAdapter` registered with Gson.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder`, and a custom `TypeAdapter` for `RecordWithRegisteredAdapter` is registered.
    - The `read` method of the `TypeAdapter` is overridden to deserialize a JSON integer by adding 5 to it and returning a new `RecordWithRegisteredAdapter` instance.
    - The `write` method of the `TypeAdapter` is overridden to serialize a `RecordWithRegisteredAdapter` instance by adding 6 to its integer field and writing it as a JSON value.
    - A `RecordWithRegisteredAdapter` instance is deserialized from the JSON string "1", and it is asserted that its integer field equals 6.
    - A `RecordWithRegisteredAdapter` instance is serialized to JSON, and it is asserted that the resulting JSON string equals "7".
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest`](#Java17RecordReflectionTest)  (Base Class)



---
### CustomAdapter<!-- {{#class:com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `CustomAdapter` class is a private static inner class that extends `TypeAdapter<Integer>` to provide custom serialization and deserialization logic for integer values, specifically adding 5 to the integer during deserialization and adding 6 during serialization.
- **Methods**:
    - [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.read`](#CustomAdapterread)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.write`](#CustomAdapterwrite)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.read`](#CustomAdapterread)
    - [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.write`](#CustomAdapterwrite)

**Methods**

---
#### CustomAdapter\.read<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.read}} -->
The `read` method reads an integer from a `JsonReader`, adds 5 to it, and returns a new `RecordWithCustomClassAdapter` instance with the resulting value.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which an integer is read.
- **Control Flow**:
    - Call `in.nextInt()` to read the next integer from the `JsonReader`.
    - Add 5 to the integer obtained from the `JsonReader`.
    - Create a new `RecordWithCustomClassAdapter` instance using the modified integer value.
    - Return the newly created `RecordWithCustomClassAdapter` instance.
- **Output**:
    - A `RecordWithCustomClassAdapter` instance initialized with the integer read from the `JsonReader` plus 5.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter`](#Java17RecordReflectionTest.CustomAdapter)  (Base Class)


---
#### CustomAdapter\.write<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.write}} -->
The `write` method serializes a `RecordWithCustomClassAdapter` object by writing its integer field value incremented by 6 to a `JsonWriter`.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - [`value`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `RecordWithCustomClassAdapter` object whose integer field is to be serialized.
- **Control Flow**:
    - The method takes a `JsonWriter` and a `RecordWithCustomClassAdapter` object as parameters.
    - It writes the integer field `i` of the `RecordWithCustomClassAdapter` object, incremented by 6, to the `JsonWriter`.
- **Output**:
    - The method does not return any value; it writes to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter`](#Java17RecordReflectionTest.CustomAdapter)  (Base Class)


---
#### CustomAdapter\.read<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.read}} -->
The `read` method reads an integer from a `JsonReader` and returns it incremented by 5.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which the next integer is read.
- **Control Flow**:
    - Invoke the [`nextInt`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt) method on the `JsonReader` object `in` to read the next integer from the JSON input.
    - Add 5 to the integer obtained from the `JsonReader`.
    - Return the resulting integer.
- **Output**:
    - An `Integer` that is the result of adding 5 to the integer read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter`](#Java17RecordReflectionTest.CustomAdapter)  (Base Class)


---
#### CustomAdapter\.write<!-- {{#callable:com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter.write}} -->
The `write` method writes an integer value incremented by 6 to a JSON writer.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - [`value`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): An `Integer` value that is to be written to the JSON writer after being incremented by 6.
- **Control Flow**:
    - The method takes an integer value, adds 6 to it, and writes the result to the provided `JsonWriter` object.
- **Output**:
    - The method does not return any value; it writes the modified integer to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.native_test.Java17RecordReflectionTest.CustomAdapter`](#Java17RecordReflectionTest.CustomAdapter)  (Base Class)



