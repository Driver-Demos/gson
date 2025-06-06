# Purpose
The `ReadersWritersTest` Java file is a collection of functional tests designed to validate the serialization and deserialization capabilities of the Gson library, specifically focusing on the use of `Reader` and `Writer` objects. The tests ensure that the Gson library can correctly handle JSON data when reading from and writing to these stream-based interfaces. The file includes tests for basic serialization and deserialization of objects, handling of null values, and the use of custom appendable objects. It also verifies the library's behavior when encountering type mismatches, ensuring that appropriate exceptions are thrown.

The technical components of this file include the use of the `Gson` and `GsonBuilder` classes for JSON processing, `JsonStreamParser` for parsing JSON streams, and various `Reader` and `Writer` implementations such as `StringReader`, `StringWriter`, `CharArrayReader`, and `CharArrayWriter`. The tests utilize the `BagOfPrimitives` class as a sample data structure for serialization and deserialization operations. The file also demonstrates the use of JUnit testing framework annotations and assertions to validate the expected outcomes of each test case. Overall, this file serves as a comprehensive suite of tests to ensure the robustness and correctness of Gson's handling of JSON data through stream interfaces.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonStreamParser`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.common.TestTypes.BagOfPrimitives`
- `com.google.gson.reflect.TypeToken`
- `java.io.CharArrayReader`
- `java.io.CharArrayWriter`
- `java.io.IOException`
- `java.io.Reader`
- `java.io.StringReader`
- `java.io.StringWriter`
- `java.io.Writer`
- `java.lang.reflect.Type`
- `java.util.Arrays`
- `java.util.Map`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### ReadersWritersTest<!-- {{#class:com.google.gson.functional.ReadersWritersTest}} -->
- **Modifiers**: `public`
- **Description**: The `ReadersWritersTest` class is a suite of functional tests designed to verify the correct serialization and deserialization of objects using the Gson library, specifically focusing on the use of `Reader` and `Writer` interfaces. It includes tests for handling null objects, type mismatches, and custom appendable objects, ensuring that the Gson library behaves as expected in various scenarios. The class uses JUnit for testing and includes setup and multiple test methods to cover different aspects of JSON processing.
- **Fields**:
    - `gson`: `Gson` An instance of the Gson class used for JSON serialization and deserialization in the tests.
- **Methods**:
    - [`com.google.gson.functional.ReadersWritersTest.setUp`](#ReadersWritersTestsetUp)
    - [`com.google.gson.functional.ReadersWritersTest.testWriterForSerialization`](#ReadersWritersTesttestWriterForSerialization)
    - [`com.google.gson.functional.ReadersWritersTest.testReaderForDeserialization`](#ReadersWritersTesttestReaderForDeserialization)
    - [`com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectSerializationWithWriter`](#ReadersWritersTesttestTopLevelNullObjectSerializationWithWriter)
    - [`com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectDeserializationWithReader`](#ReadersWritersTesttestTopLevelNullObjectDeserializationWithReader)
    - [`com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectSerializationWithWriterAndSerializeNulls`](#ReadersWritersTesttestTopLevelNullObjectSerializationWithWriterAndSerializeNulls)
    - [`com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectDeserializationWithReaderAndSerializeNulls`](#ReadersWritersTesttestTopLevelNullObjectDeserializationWithReaderAndSerializeNulls)
    - [`com.google.gson.functional.ReadersWritersTest.testReadWriteTwoStrings`](#ReadersWritersTesttestReadWriteTwoStrings)
    - [`com.google.gson.functional.ReadersWritersTest.testReadWriteTwoObjects`](#ReadersWritersTesttestReadWriteTwoObjects)
    - [`com.google.gson.functional.ReadersWritersTest.testTypeMismatchThrowsJsonSyntaxExceptionForStrings`](#ReadersWritersTesttestTypeMismatchThrowsJsonSyntaxExceptionForStrings)
    - [`com.google.gson.functional.ReadersWritersTest.testTypeMismatchThrowsJsonSyntaxExceptionForReaders`](#ReadersWritersTesttestTypeMismatchThrowsJsonSyntaxExceptionForReaders)
    - [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable`](#ReadersWritersTesttestToJsonAppendable)

**Methods**

---
#### ReadersWritersTest\.setUp<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.setUp}} -->
The setUp method initializes a Gson object before each test is executed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with @Before, indicating it runs before each test method in the class.
    - A new instance of Gson is created and assigned to the gson field.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testWriterForSerialization<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testWriterForSerialization}} -->
The `testWriterForSerialization` method tests the serialization of a `BagOfPrimitives` object to JSON using a `Writer` and verifies the output against the expected JSON string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` instance is created to capture the JSON output.
    - A `BagOfPrimitives` object is instantiated as the source object for serialization.
    - The `gson.toJson` method is called to serialize the `BagOfPrimitives` object into the `Writer`.
    - The serialized JSON string from the `Writer` is compared to the expected JSON string using an assertion.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testReaderForDeserialization<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testReaderForDeserialization}} -->
The method `testReaderForDeserialization` tests the deserialization of a JSON string into a `BagOfPrimitives` object using a `Reader`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create an instance of `BagOfPrimitives` named `expected`.
    - Create a `StringReader` named `json` initialized with the JSON representation of `expected`.
    - Deserialize the JSON from `json` into a `BagOfPrimitives` object named `actual` using `gson.fromJson`.
    - Assert that `actual` is equal to `expected` using `assertThat`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of deserialization.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testTopLevelNullObjectSerializationWithWriter<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectSerializationWithWriter}} -->
The method tests the serialization of a top-level null object using a StringWriter and verifies that the output is the string "null".
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A StringWriter object is instantiated to capture the serialized output.
    - The Gson instance is used to serialize a null object into the StringWriter.
    - The resulting string from the StringWriter is asserted to be equal to the string "null".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testTopLevelNullObjectDeserializationWithReader<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectDeserializationWithReader}} -->
This method tests the deserialization of a top-level null JSON object using a StringReader and verifies that the result is a null Integer object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A StringReader is initialized with the string "null".
    - The Gson instance is used to deserialize the JSON content from the StringReader into an Integer object.
    - An assertion is made to check that the deserialized Integer object is null.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the deserialization result.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testTopLevelNullObjectSerializationWithWriterAndSerializeNulls<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectSerializationWithWriterAndSerializeNulls}} -->
This method tests the serialization of a top-level null object using a Gson instance configured to serialize nulls, and verifies the output is the string "null".
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using GsonBuilder with the serializeNulls option enabled.
    - A StringWriter is instantiated to capture the JSON output.
    - The Gson instance serializes a null object to the StringWriter.
    - The resulting string from the StringWriter is asserted to be equal to "null".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testTopLevelNullObjectDeserializationWithReaderAndSerializeNulls<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testTopLevelNullObjectDeserializationWithReaderAndSerializeNulls}} -->
This method tests the deserialization of a top-level null JSON object using a StringReader and a Gson instance configured to serialize nulls.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created using GsonBuilder with the serializeNulls option enabled.
    - A StringReader is initialized with the string "null" to simulate a JSON input.
    - The fromJson method of Gson is called with the StringReader and Integer.class to deserialize the JSON input.
    - An assertion is made to check that the deserialized object is null.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the deserialized object is null.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testReadWriteTwoStrings<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testReadWriteTwoStrings}} -->
The `testReadWriteTwoStrings` method tests the serialization and deserialization of two strings using Gson and verifies their correctness.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated for JSON operations.
    - A `CharArrayWriter` is created to write JSON strings to a character array.
    - The strings "one" and "two" are serialized to JSON and written to the `CharArrayWriter`.
    - A `CharArrayReader` is created from the character array of the `CharArrayWriter`.
    - A `JsonStreamParser` is initialized with the `CharArrayReader` to parse JSON tokens.
    - The first JSON token is parsed back to a string and asserted to be equal to "one".
    - The second JSON token is parsed back to a string and asserted to be equal to "two".
- **Output**:
    - The method does not return any value but asserts that the deserialized strings match the expected values.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.JsonStreamParser.next`](../../../../../../main/java/com/google/gson/JsonStreamParser.java.driver.md#JsonStreamParsernext)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testReadWriteTwoObjects<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testReadWriteTwoObjects}} -->
The `testReadWriteTwoObjects` method tests the serialization and deserialization of two `BagOfPrimitives` objects using Gson and verifies their integrity.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `Gson` object for JSON operations.
    - Create a `CharArrayWriter` to write JSON data to a character array.
    - Create two `BagOfPrimitives` objects, `expectedOne` and `expectedTwo`, with different values.
    - Serialize `expectedOne` to JSON and write it to the `CharArrayWriter`.
    - Serialize `expectedTwo` to JSON and write it to the `CharArrayWriter`.
    - Create a `CharArrayReader` from the character array of the `CharArrayWriter`.
    - Instantiate a `JsonStreamParser` with the `CharArrayReader` to parse JSON data.
    - Deserialize the first JSON object from the parser into a `BagOfPrimitives` object, `actualOne`.
    - Assert that the `stringValue` of `actualOne` is equal to "one".
    - Deserialize the second JSON object from the parser into a `BagOfPrimitives` object, `actualTwo`.
    - Assert that the `stringValue` of `actualTwo` is equal to "two".
    - Assert that there are no more JSON objects to parse, ensuring `parser.hasNext()` is false.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.JsonStreamParser.next`](../../../../../../main/java/com/google/gson/JsonStreamParser.java.driver.md#JsonStreamParsernext)
    - [`com.google.gson.JsonStreamParser.hasNext`](../../../../../../main/java/com/google/gson/JsonStreamParser.java.driver.md#JsonStreamParserhasNext)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testTypeMismatchThrowsJsonSyntaxExceptionForStrings<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testTypeMismatchThrowsJsonSyntaxExceptionForStrings}} -->
This method tests that a JsonSyntaxException is thrown when attempting to deserialize a boolean JSON value into a Map<String, String> type using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a Type object representing a Map<String, String> using TypeToken.
    - Use assertThrows to verify that a JsonSyntaxException is thrown when attempting to deserialize the string "true" into the defined type using Gson's fromJson method.
    - Check that the exception's message starts with "Expected BEGIN_OBJECT but was BOOLEAN" to confirm the type mismatch error.
- **Output**:
    - The method does not return any value; it asserts that a JsonSyntaxException is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testTypeMismatchThrowsJsonSyntaxExceptionForReaders<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testTypeMismatchThrowsJsonSyntaxExceptionForReaders}} -->
This method tests that a JsonSyntaxException is thrown when attempting to deserialize a boolean value into a Map<String, String> using a StringReader.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a Type object representing a Map<String, String> using TypeToken.
    - Use assertThrows to verify that a JsonSyntaxException is thrown when gson.fromJson is called with a StringReader containing the string 'true' and the defined Type.
    - Check that the exception's message starts with 'Expected BEGIN_OBJECT but was BOOLEAN'.
- **Output**:
    - The method does not return any value; it asserts that a JsonSyntaxException is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)


---
#### ReadersWritersTest\.testToJsonAppendable<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testToJsonAppendable}} -->
The `testToJsonAppendable` method tests the functionality of serializing a list to JSON using a custom `Appendable` implementation and verifies the correct behavior of the [`toString`](MapTest.java.driver.md#PointtoString) method calls.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A custom class `CustomAppendable` is defined, implementing the `Appendable` interface with methods to append characters and character sequences to a `StringBuilder`.
    - An instance of `CustomAppendable` is created.
    - The `gson.toJson` method is called to serialize a list containing a string, an integer, and a boolean into JSON format, using the `CustomAppendable` instance.
    - Assertions are made to ensure that the [`toString`](MapTest.java.driver.md#PointtoString) method of `CharSequence` is called at least twice, verifying that the `CurrentWrite.cachedString` is properly overwritten when the character array changes.
    - Another assertion checks that the resulting JSON string in the `StringBuilder` matches the expected JSON representation of the list.
- **Output**:
    - The method does not return any value but performs assertions to verify the correct behavior of the JSON serialization process using a custom `Appendable`.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.ReadersWritersTest`](#ReadersWritersTest)  (Base Class)



---
### CustomAppendable<!-- {{#class:com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable}} -->
- **Description**: The `CustomAppendable` class is an implementation of the `Appendable` interface, designed to accumulate character sequences using an internal `StringBuilder`. It provides methods to append single characters, character sequences, and sub-sequences, while also keeping track of how many times the `toString()` method is called on the character sequences. This class is particularly useful for scenarios where an `Appendable` is needed that is not necessarily a `Writer`, such as when using `Gson` to serialize objects to a custom appendable output.
- **Fields**:
    - `stringBuilder`: `StringBuilder` A `StringBuilder` used to accumulate appended characters and sequences.
    - `toStringCallCount`: `int` An integer counter that tracks the number of times `toString()` is called on character sequences.
- **Methods**:
    - [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable.append`](#ReadersWritersTesttestToJsonAppendable.CustomAppendable.append)
    - [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable.append`](#ReadersWritersTesttestToJsonAppendable.CustomAppendable.append)
    - [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable.append`](#ReadersWritersTesttestToJsonAppendable.CustomAppendable.append)
- **Extends/Implements**:
    - `Appendable`

**Methods**

---
#### CustomAppendable\.append<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable.append}} -->
The `append` method appends a single character to a `StringBuilder` and returns the current instance of the `Appendable`.
- **Modifiers**: `public`, `@Override`
- **Inputs**:
    - `c`: A character to be appended to the `StringBuilder`.
- **Control Flow**:
    - The method appends the character `c` to the `stringBuilder` using its `append` method.
    - The method returns the current instance of the `Appendable` (i.e., `this`).
- **Output**:
    - The method returns the current instance of the `Appendable`, allowing for method chaining.
- **See also**: [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable`](#ReadersWritersTest.testToJsonAppendable.CustomAppendable)  (Base Class)


---
#### CustomAppendable\.append<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable.append}} -->
The `append` method appends a given `CharSequence` to the current `Appendable` object, handling null values by converting them to the string "null".
- **Modifiers**: `public`, `@Override`
- **Inputs**:
    - `csq`: A `CharSequence` to be appended to the current `Appendable` object; if null, it is converted to the string "null".
- **Control Flow**:
    - Check if the input `CharSequence` (csq) is null.
    - If `csq` is null, assign it the string value "null".
    - Call the overloaded `append` method with `csq`, starting index 0, and ending index as the length of `csq`.
    - Return the current instance of the `Appendable` object.
- **Output**:
    - Returns the current instance of the `Appendable` object after appending the `CharSequence`.
- **See also**: [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable`](#ReadersWritersTest.testToJsonAppendable.CustomAppendable)  (Base Class)


---
#### CustomAppendable\.append<!-- {{#callable:com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable.append}} -->
The `append` method appends a subsequence of a given `CharSequence` to the `stringBuilder` and returns the current instance of `CustomAppendable`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `csq`: The `CharSequence` to be appended; if null, it defaults to the string "null".
    - `start`: The starting index of the subsequence to be appended.
    - `end`: The ending index of the subsequence to be appended.
- **Control Flow**:
    - Check if the input `CharSequence` (`csq`) is null and if so, assign it the string "null".
    - Convert the `CharSequence` to a `String` using `toString()` and increment the `toStringCallCount`.
    - Append the specified subsequence (from `start` to `end`) of the `String` to the `stringBuilder`.
    - Return the current instance of `CustomAppendable`.
- **Output**:
    - Returns the current instance of `CustomAppendable` after appending the specified subsequence.
- **See also**: [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable`](#ReadersWritersTest.testToJsonAppendable.CustomAppendable)  (Base Class)



