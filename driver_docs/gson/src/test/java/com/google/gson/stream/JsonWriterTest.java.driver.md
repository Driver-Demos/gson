# Purpose
The provided Java source code file is a comprehensive test suite for the `JsonWriter` class, which is part of the Google Gson library. This test class, `JsonWriterTest`, is designed to validate the functionality and robustness of the `JsonWriter` class by executing a series of unit tests. These tests cover a wide range of scenarios, including writing different data types (such as booleans, numbers, strings, and nulls) to JSON, handling various JSON structures (like arrays and objects), and ensuring proper behavior under different strictness settings (strict, lenient, and legacy strict). The tests also verify the handling of edge cases, such as malformed numbers, non-finite numbers, and deep nesting of JSON structures.

The test suite is structured to ensure that the `JsonWriter` class adheres to expected behaviors, such as throwing appropriate exceptions for invalid operations (e.g., writing a name without an object context or attempting to write multiple top-level values in strict mode). It also checks the correct formatting of JSON output, including pretty-printing with custom indentation and line separators. By using assertions from the `Truth` library and JUnit's `assertThrows` method, the tests provide a robust mechanism for verifying the correctness and reliability of the `JsonWriter` implementation. This file is crucial for maintaining the integrity of the `JsonWriter` class by ensuring that any changes to the codebase do not introduce regressions or unexpected behaviors.
# Imports and Dependencies

---
- `com.google.gson.stream`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.FormattingStyle`
- `com.google.gson.Strictness`
- `com.google.gson.internal.LazilyParsedNumber`
- `java.io.IOException`
- `java.io.StringWriter`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `org.junit.Test`


# Classes

---
### JsonWriterTest<!-- {{#class:com.google.gson.stream.JsonWriterTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonWriterTest` class is a comprehensive suite of unit tests designed to validate the functionality and behavior of the `JsonWriter` class from the Gson library. It covers a wide range of scenarios including strictness settings, handling of various data types, nesting of JSON structures, and error conditions such as invalid states and malformed inputs. The tests ensure that `JsonWriter` correctly handles JSON formatting, including pretty printing, and that it throws appropriate exceptions for invalid operations, such as writing names without values or attempting to write multiple top-level values in strict mode.
- **Methods**:
    - [`com.google.gson.stream.JsonWriterTest.testDefaultStrictness`](#JsonWriterTesttestDefaultStrictness)
    - [`com.google.gson.stream.JsonWriterTest.testSetLenientTrue`](#JsonWriterTesttestSetLenientTrue)
    - [`com.google.gson.stream.JsonWriterTest.testSetLenientFalse`](#JsonWriterTesttestSetLenientFalse)
    - [`com.google.gson.stream.JsonWriterTest.testSetStrictness`](#JsonWriterTesttestSetStrictness)
    - [`com.google.gson.stream.JsonWriterTest.testSetStrictnessNull`](#JsonWriterTesttestSetStrictnessNull)
    - [`com.google.gson.stream.JsonWriterTest.testTopLevelValueTypes`](#JsonWriterTesttestTopLevelValueTypes)
    - [`com.google.gson.stream.JsonWriterTest.testNameAsTopLevelValue`](#JsonWriterTesttestNameAsTopLevelValue)
    - [`com.google.gson.stream.JsonWriterTest.testNameInArray`](#JsonWriterTesttestNameInArray)
    - [`com.google.gson.stream.JsonWriterTest.testTwoNames`](#JsonWriterTesttestTwoNames)
    - [`com.google.gson.stream.JsonWriterTest.testNameWithoutValue`](#JsonWriterTesttestNameWithoutValue)
    - [`com.google.gson.stream.JsonWriterTest.testValueWithoutName`](#JsonWriterTesttestValueWithoutName)
    - [`com.google.gson.stream.JsonWriterTest.testMultipleTopLevelValues`](#JsonWriterTesttestMultipleTopLevelValues)
    - [`com.google.gson.stream.JsonWriterTest.testMultipleTopLevelValuesStrict`](#JsonWriterTesttestMultipleTopLevelValuesStrict)
    - [`com.google.gson.stream.JsonWriterTest.testMultipleTopLevelValuesLenient`](#JsonWriterTesttestMultipleTopLevelValuesLenient)
    - [`com.google.gson.stream.JsonWriterTest.testBadNestingObject`](#JsonWriterTesttestBadNestingObject)
    - [`com.google.gson.stream.JsonWriterTest.testBadNestingArray`](#JsonWriterTesttestBadNestingArray)
    - [`com.google.gson.stream.JsonWriterTest.testNullName`](#JsonWriterTesttestNullName)
    - [`com.google.gson.stream.JsonWriterTest.testNullStringValue`](#JsonWriterTesttestNullStringValue)
    - [`com.google.gson.stream.JsonWriterTest.testJsonValue`](#JsonWriterTesttestJsonValue)
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteFloatsExceptions`](#JsonWriterTestassertNonFiniteFloatsExceptions)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteFloats`](#JsonWriterTesttestNonFiniteFloats)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteFloatsWhenStrict`](#JsonWriterTesttestNonFiniteFloatsWhenStrict)
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteDoublesExceptions`](#JsonWriterTestassertNonFiniteDoublesExceptions)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteDoubles`](#JsonWriterTesttestNonFiniteDoubles)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteDoublesWhenStrict`](#JsonWriterTesttestNonFiniteDoublesWhenStrict)
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteNumbersExceptions`](#JsonWriterTestassertNonFiniteNumbersExceptions)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteNumbers`](#JsonWriterTesttestNonFiniteNumbers)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteNumbersWhenStrict`](#JsonWriterTesttestNonFiniteNumbersWhenStrict)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteFloatsWhenLenient`](#JsonWriterTesttestNonFiniteFloatsWhenLenient)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteDoublesWhenLenient`](#JsonWriterTesttestNonFiniteDoublesWhenLenient)
    - [`com.google.gson.stream.JsonWriterTest.testNonFiniteNumbersWhenLenient`](#JsonWriterTesttestNonFiniteNumbersWhenLenient)
    - [`com.google.gson.stream.JsonWriterTest.testFloats`](#JsonWriterTesttestFloats)
    - [`com.google.gson.stream.JsonWriterTest.testDoubles`](#JsonWriterTesttestDoubles)
    - [`com.google.gson.stream.JsonWriterTest.testLongs`](#JsonWriterTesttestLongs)
    - [`com.google.gson.stream.JsonWriterTest.testNumbers`](#JsonWriterTesttestNumbers)
    - [`com.google.gson.stream.JsonWriterTest.testNumbersCustomClass`](#JsonWriterTesttestNumbersCustomClass)
    - [`com.google.gson.stream.JsonWriterTest.testMalformedNumbers`](#JsonWriterTesttestMalformedNumbers)
    - [`com.google.gson.stream.JsonWriterTest.testBooleans`](#JsonWriterTesttestBooleans)
    - [`com.google.gson.stream.JsonWriterTest.testBoxedBooleans`](#JsonWriterTesttestBoxedBooleans)
    - [`com.google.gson.stream.JsonWriterTest.testNulls`](#JsonWriterTesttestNulls)
    - [`com.google.gson.stream.JsonWriterTest.testStrings`](#JsonWriterTesttestStrings)
    - [`com.google.gson.stream.JsonWriterTest.testUnicodeLineBreaksEscaped`](#JsonWriterTesttestUnicodeLineBreaksEscaped)
    - [`com.google.gson.stream.JsonWriterTest.testEmptyArray`](#JsonWriterTesttestEmptyArray)
    - [`com.google.gson.stream.JsonWriterTest.testEmptyObject`](#JsonWriterTesttestEmptyObject)
    - [`com.google.gson.stream.JsonWriterTest.testObjectsInArrays`](#JsonWriterTesttestObjectsInArrays)
    - [`com.google.gson.stream.JsonWriterTest.testArraysInObjects`](#JsonWriterTesttestArraysInObjects)
    - [`com.google.gson.stream.JsonWriterTest.testDeepNestingArrays`](#JsonWriterTesttestDeepNestingArrays)
    - [`com.google.gson.stream.JsonWriterTest.testDeepNestingObjects`](#JsonWriterTesttestDeepNestingObjects)
    - [`com.google.gson.stream.JsonWriterTest.testRepeatedName`](#JsonWriterTesttestRepeatedName)
    - [`com.google.gson.stream.JsonWriterTest.testPrettyPrintObject`](#JsonWriterTesttestPrettyPrintObject)
    - [`com.google.gson.stream.JsonWriterTest.testPrettyPrintArray`](#JsonWriterTesttestPrettyPrintArray)
    - [`com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnStructure`](#JsonWriterTesttestClosedWriterThrowsOnStructure)
    - [`com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnName`](#JsonWriterTesttestClosedWriterThrowsOnName)
    - [`com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnValue`](#JsonWriterTesttestClosedWriterThrowsOnValue)
    - [`com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnFlush`](#JsonWriterTesttestClosedWriterThrowsOnFlush)
    - [`com.google.gson.stream.JsonWriterTest.testWriterCloseIsIdempotent`](#JsonWriterTesttestWriterCloseIsIdempotent)
    - [`com.google.gson.stream.JsonWriterTest.testSetGetFormattingStyle`](#JsonWriterTesttestSetGetFormattingStyle)
    - [`com.google.gson.stream.JsonWriterTest.testIndentOverwritesFormattingStyle`](#JsonWriterTesttestIndentOverwritesFormattingStyle)

**Methods**

---
#### JsonWriterTest\.testDefaultStrictness<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testDefaultStrictness}} -->
Tests the default strictness of the `JsonWriter` class.
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `JsonWriter` with a `StringWriter`.
    - Asserts that the default strictness of the `JsonWriter` is `Strictness.LEGACY_STRICT`.
    - Writes a boolean value `false` to the `JsonWriter`.
    - Closes the `JsonWriter`.
- **Output**:
    - The method does not return a value; it performs assertions to verify the behavior of the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testSetLenientTrue<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testSetLenientTrue}} -->
Tests the behavior of the `JsonWriter` when set to lenient mode.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `JsonWriter` with a `StringWriter`.
    - Sets the `JsonWriter` to lenient mode by calling `setLenient(true)`.
    - Asserts that the strictness of the `JsonWriter` is now `Strictness.LENIENT`.
    - Writes a boolean value `false` to the `JsonWriter`.
    - Closes the `JsonWriter`.
- **Output**:
    - The method does not return a value but verifies that the `JsonWriter` operates correctly in lenient mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setLenient`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetLenient)
    - [`com.google.gson.stream.JsonWriter.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testSetLenientFalse<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testSetLenientFalse}} -->
Tests the behavior of the `JsonWriter` when set to non-lenient mode.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` initialized with a `StringWriter`.
- **Control Flow**:
    - Creates a new instance of `JsonWriter` with a `StringWriter`.
    - Sets the `lenient` mode of the `JsonWriter` to false.
    - Asserts that the strictness of the `JsonWriter` is `Strictness.LEGACY_STRICT`.
    - Writes a boolean value (false) to the `JsonWriter`.
    - Closes the `JsonWriter`.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setLenient`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetLenient)
    - [`com.google.gson.stream.JsonWriter.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testSetStrictness<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testSetStrictness}} -->
Tests the [`setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness) method of the `JsonWriter` class to ensure it correctly sets the strictness level.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` initialized with a `StringWriter`.
    - `Strictness.STRICT`: An enum value representing the strictness level to be set for the `JsonWriter`.
- **Control Flow**:
    - Creates a new instance of `JsonWriter` with a `StringWriter`.
    - Sets the strictness of the `JsonWriter` to `Strictness.STRICT`.
    - Asserts that the strictness level of the `JsonWriter` is now `Strictness.STRICT`.
    - Writes a boolean value `false` to the `JsonWriter`.
    - Closes the `JsonWriter`.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the [`setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness) method.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testSetStrictnessNull<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testSetStrictnessNull}} -->
Tests that setting the strictness of a `JsonWriter` to null throws a `NullPointerException`.
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` that is being tested.
    - `null`: The value being passed to [`setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness), which is expected to be null.
- **Control Flow**:
    - A new instance of `JsonWriter` is created using a `StringWriter`.
    - The method [`setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness) is called with a null argument, which is expected to throw a `NullPointerException`.
    - The [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method is called with a boolean value (false) to ensure the writer can still function after the exception.
    - The [`close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose) method is called to close the `JsonWriter`.
- **Output**:
    - The method does not return a value; instead, it verifies that a `NullPointerException` is thrown when attempting to set strictness to null.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testTopLevelValueTypes<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testTopLevelValueTypes}} -->
Tests the serialization of various top-level value types using `JsonWriter`.
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` and a `JsonWriter` for each value type to be tested.
    - Writes a boolean value `true` and asserts the output is 'true'.
    - Writes a null value and asserts the output is 'null'.
    - Writes an integer value `123` and asserts the output is '123'.
    - Writes a double value `123.4` and asserts the output is '123.4'.
    - Writes a string value 'a' and asserts the output is '"a"'.
- **Output**:
    - The method does not return a value but asserts that the serialized output matches the expected JSON representation for each value type.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNameAsTopLevelValue<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNameAsTopLevelValue}} -->
Tests the behavior of `JsonWriter` when attempting to write a name at the top level without a preceding object.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `StringWriter` and a `JsonWriter` instance to write JSON data.
    - Attempts to write a name 'hello' without starting an object, expecting an `IllegalStateException` with a specific message.
    - Writes a value (12) to the `JsonWriter` and then closes it.
    - Attempts to write a name 'hello' again after closing the `JsonWriter`, expecting another `IllegalStateException` with a different message.
- **Output**:
    - The method does not return a value; it asserts that specific exceptions are thrown with expected messages during its execution.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNameInArray<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNameInArray}} -->
Tests the behavior of `JsonWriter` when attempting to write a name within an array.
- **Inputs**:
    - `stringWriter`: A `StringWriter` instance used to capture the output of the `JsonWriter`.
    - `jsonWriter`: A `JsonWriter` instance that writes JSON data to the `StringWriter`.
    - `e`: An `IllegalStateException` that is expected to be thrown when invalid operations are performed on the `JsonWriter`.
- **Control Flow**:
    - The method begins by creating a `StringWriter` and a `JsonWriter` that writes to this `StringWriter`.
    - It starts a JSON array using `jsonWriter.beginArray()`.
    - The method then attempts to write a name 'hello' using `jsonWriter.name('hello')`, which throws an `IllegalStateException` because names can only be written within an object.
    - The exception is caught and its message is asserted to ensure it matches the expected error message.
    - Next, a value (12) is written to the array using `jsonWriter.value(12)`.
    - Another attempt to write the name 'hello' is made, which again throws an `IllegalStateException` for the same reason as before.
    - The exception is caught and its message is asserted again.
    - Finally, the array is closed with `jsonWriter.endArray()` and the `StringWriter` is closed.
    - The output of the `StringWriter` is asserted to ensure it matches the expected JSON representation of the array containing the value 12.
- **Output**:
    - The output is a string representation of a JSON array containing the value 12, which is expected to be '[12]'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testTwoNames<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testTwoNames}} -->
Tests the behavior of `JsonWriter` when attempting to write two names consecutively without a value in between.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON object using `jsonWriter.beginObject()`.
    - Writes the first name 'a' using `jsonWriter.name('a')`.
    - Attempts to write the name 'a' again, expecting an `IllegalStateException` to be thrown.
    - Asserts that the exception message is 'Already wrote a name, expecting a value.'
- **Output**:
    - The method does not return a value but asserts that an `IllegalStateException` is thrown with the expected message.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNameWithoutValue<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNameWithoutValue}} -->
Tests that an `IllegalStateException` is thrown when attempting to end a JSON object without providing a value for the last name.
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is created to capture the output of the `JsonWriter`.
    - A `JsonWriter` instance is initialized with the `StringWriter`.
    - The method begins a JSON object using `jsonWriter.beginObject()`.
    - A name 'a' is added to the JSON object using `jsonWriter.name('a')`.
    - An attempt is made to end the JSON object with `jsonWriter.endObject()`, which is expected to throw an `IllegalStateException` because no value has been provided for the name 'a'.
    - The exception is caught and its message is asserted to ensure it matches the expected error message.
- **Output**:
    - An `IllegalStateException` is thrown with the message 'Dangling name: a'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testValueWithoutName<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testValueWithoutName}} -->
Tests that an `IllegalStateException` is thrown when attempting to write a value without a preceding name in a JSON object.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON object using `jsonWriter.beginObject()`.
    - Attempts to write a boolean value using `jsonWriter.value(true)` without a preceding name, which is expected to throw an `IllegalStateException`.
    - Asserts that the exception message is 'Nesting problem.'
- **Output**:
    - The method does not produce a return value; instead, it verifies that an exception is thrown with the expected message.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testMultipleTopLevelValues<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testMultipleTopLevelValues}} -->
Tests that attempting to begin a new array after ending the previous one throws an IllegalStateException.
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins and immediately ends a JSON array to set the state of the `JsonWriter`.
    - Attempts to begin another array, which should throw an `IllegalStateException` due to the JSON specification allowing only one top-level value.
    - Asserts that the exception message matches the expected error message.
- **Output**:
    - Throws an `IllegalStateException` with the message 'JSON must have only one top-level value.' when trying to begin a new array after one has already been closed.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testMultipleTopLevelValuesStrict<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testMultipleTopLevelValuesStrict}} -->
Tests that an `IllegalStateException` is thrown when attempting to begin a new array after already writing a top-level array in strict mode.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture JSON output.
    - Initializes a `JsonWriter` with strictness set to `Strictness.STRICT`.
    - Begins and immediately ends a JSON array, which is valid.
    - Attempts to begin another array, which should throw an `IllegalStateException` due to strictness rules.
- **Output**:
    - An `IllegalStateException` is thrown with the message 'JSON must have only one top-level value.' when trying to begin a new array after the first.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testMultipleTopLevelValuesLenient<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testMultipleTopLevelValuesLenient}} -->
Tests the behavior of `JsonWriter` when multiple top-level JSON arrays are written in a lenient mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter` and sets its strictness to `LENIENT`.
    - Begins and ends the first JSON array.
    - Begins and ends a second JSON array.
    - Closes the `JsonWriter`.
    - Asserts that the output matches the expected string representation of two empty arrays.
- **Output**:
    - The method outputs a string representation of two empty JSON arrays, which is represented as "[][]".
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testBadNestingObject<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testBadNestingObject}} -->
Tests that an `IllegalStateException` is thrown when attempting to end an array after beginning an object.
- **Inputs**:
    - `stringWriter`: A `StringWriter` instance used to capture the output of the `JsonWriter`.
    - `jsonWriter`: A `JsonWriter` instance that writes JSON data.
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the JSON output.
    - A `JsonWriter` is created using the `StringWriter`.
    - The method begins a JSON array using `jsonWriter.beginArray()`.
    - The method begins a JSON object using `jsonWriter.beginObject()`.
    - An attempt is made to end the array using `jsonWriter.endArray()`, which is expected to throw an `IllegalStateException` due to improper nesting.
    - The exception is caught and its message is asserted to be 'Nesting problem.'
- **Output**:
    - An `IllegalStateException` is thrown with the message 'Nesting problem.' indicating that the JSON structure is improperly nested.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testBadNestingArray<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testBadNestingArray}} -->
Tests that an `IllegalStateException` is thrown when attempting to end an object while nested within arrays.
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is created to capture the output of the `JsonWriter`.
    - A `JsonWriter` instance is initialized with the `StringWriter`.
    - The method begins two nested arrays using `beginArray()`.
    - An attempt is made to call `endObject()`, which is expected to fail due to the incorrect nesting of arrays.
    - The exception is caught and verified to ensure it has the correct message indicating a nesting problem.
- **Output**:
    - The method does not produce a valid JSON output due to the exception; instead, it verifies that an `IllegalStateException` is thrown with the message 'Nesting problem.'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNullName<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNullName}} -->
Tests that a `NullPointerException` is thrown when attempting to set a name to `null` in a `JsonWriter`.
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` that is used to write JSON data.
- **Control Flow**:
    - A `StringWriter` is created to capture the output of the `JsonWriter`.
    - A `JsonWriter` instance is initialized with the `StringWriter`.
    - The [`beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject) method is called on the `JsonWriter` to start a new JSON object.
    - The `assertThrows` method is used to check that calling `name(null)` on the `JsonWriter` throws a `NullPointerException`.
- **Output**:
    - The method does not produce a direct output; instead, it verifies that a `NullPointerException` is thrown when a null name is provided.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNullStringValue<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNullStringValue}} -->
Tests the behavior of `JsonWriter` when writing a null string value.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**:
    - `stringWriter`: A `StringWriter` instance used to capture the JSON output.
    - `jsonWriter`: A `JsonWriter` instance that writes JSON data to the `StringWriter`.
- **Control Flow**:
    - Creates a new `StringWriter` to hold the JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON object using `jsonWriter.beginObject()`.
    - Writes a name 'a' to the JSON object using `jsonWriter.name('a')`.
    - Writes a null value associated with the name 'a' using `jsonWriter.value((String) null)`.
    - Ends the JSON object using `jsonWriter.endObject()`.
    - Asserts that the output of `stringWriter` matches the expected JSON string '{"a":null}'.
- **Output**:
    - The method outputs a JSON string representation of an object with a single key 'a' mapped to a null value, which is expected to be '{"a":null}'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testJsonValue<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testJsonValue}} -->
Tests the `JsonWriter` class by writing a JSON object with nested values.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `StringWriter` to capture the JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON object.
    - Writes a name-value pair where the name is 'a' and the value is a JSON string representing another object.
    - Writes another name-value pair where the name is 'c' and the value is an integer 1.
    - Ends the JSON object.
    - Asserts that the output matches the expected JSON string.
- **Output**:
    - The method outputs a JSON string that represents an object with two properties: 'a' containing a nested object and 'c' containing an integer.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.jsonValue`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterjsonValue)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.assertNonFiniteFloatsExceptions<!-- {{#callable:com.google.gson.stream.JsonWriterTest.assertNonFiniteFloatsExceptions}} -->
Asserts that `JsonWriter` throws exceptions for non-finite float values.
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` used to write JSON data.
- **Control Flow**:
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Attempts to write `Float.NaN` to the `jsonWriter` and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message is 'Numeric values must be finite, but was NaN'.
    - Attempts to write `Float.NEGATIVE_INFINITY` to the `jsonWriter` and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message is 'Numeric values must be finite, but was -Infinity'.
    - Attempts to write `Float.POSITIVE_INFINITY` to the `jsonWriter` and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message is 'Numeric values must be finite, but was Infinity'.
- **Output**:
    - No output is returned; the method validates that exceptions are thrown for invalid float values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteFloats<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteFloats}} -->
Tests the behavior of the `JsonWriter` when handling non-finite float values.
- **Modifiers**: `public`, `void`, `@Test`
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` used to write JSON data.
- **Control Flow**:
    - Creates a new `StringWriter` to capture the output of the `JsonWriter`.
    - Calls the [`assertNonFiniteFloatsExceptions`](#JsonWriterTestassertNonFiniteFloatsExceptions) method, passing the `jsonWriter` instance to it.
- **Output**:
    - The method does not return a value; it asserts that exceptions are thrown for non-finite float values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteFloatsExceptions`](#JsonWriterTestassertNonFiniteFloatsExceptions)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteFloatsWhenStrict<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteFloatsWhenStrict}} -->
Tests that non-finite float values throw exceptions when strictness is set to STRICT.
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` that is configured to write JSON data.
- **Control Flow**:
    - Creates a new `StringWriter` to capture the output of the `JsonWriter`.
    - Sets the strictness of the `JsonWriter` to `Strictness.STRICT`.
    - Calls the [`assertNonFiniteFloatsExceptions`](#JsonWriterTestassertNonFiniteFloatsExceptions) method, which checks that writing non-finite float values (NaN, -Infinity, Infinity) results in `IllegalArgumentException` being thrown.
- **Output**:
    - No output is returned; instead, the method verifies that exceptions are thrown for non-finite float values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteFloatsExceptions`](#JsonWriterTestassertNonFiniteFloatsExceptions)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.assertNonFiniteDoublesExceptions<!-- {{#callable:com.google.gson.stream.JsonWriterTest.assertNonFiniteDoublesExceptions}} -->
Asserts that `JsonWriter` throws exceptions for non-finite double values.
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` used to write JSON data.
- **Control Flow**:
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Attempts to write `Double.NaN` to the `jsonWriter` and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message is 'Numeric values must be finite, but was NaN'.
    - Attempts to write `Double.NEGATIVE_INFINITY` to the `jsonWriter` and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message is 'Numeric values must be finite, but was -Infinity'.
    - Attempts to write `Double.POSITIVE_INFINITY` to the `jsonWriter` and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message is 'Numeric values must be finite, but was Infinity'.
- **Output**:
    - No output is returned; the method validates that exceptions are thrown for invalid double values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteDoubles<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteDoubles}} -->
Tests that the `JsonWriter` throws exceptions for non-finite double values.
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` instance with the `StringWriter`.
    - Calls the [`assertNonFiniteDoublesExceptions`](#JsonWriterTestassertNonFiniteDoublesExceptions) method, which checks for exceptions when non-finite double values are written.
- **Output**:
    - No output is returned; instead, the method verifies that exceptions are thrown for invalid double values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteDoublesExceptions`](#JsonWriterTestassertNonFiniteDoublesExceptions)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteDoublesWhenStrict<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteDoublesWhenStrict}} -->
Tests that non-finite double values throw exceptions when strictness is set to STRICT.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Sets the strictness of the `JsonWriter` to `Strictness.STRICT`.
    - Calls the [`assertNonFiniteDoublesExceptions`](#JsonWriterTestassertNonFiniteDoublesExceptions) method, which checks for exceptions when non-finite double values are written.
- **Output**:
    - No output is returned; instead, the method verifies that exceptions are thrown for non-finite double values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteDoublesExceptions`](#JsonWriterTestassertNonFiniteDoublesExceptions)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.assertNonFiniteNumbersExceptions<!-- {{#callable:com.google.gson.stream.JsonWriterTest.assertNonFiniteNumbersExceptions}} -->
Asserts that non-finite numeric values throw exceptions when written to a `JsonWriter`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` used to write JSON data.
- **Control Flow**:
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Attempts to write `Double.NaN` to the `jsonWriter` and asserts that it throws an `IllegalArgumentException` with the expected message.
    - Attempts to write `Double.NEGATIVE_INFINITY` to the `jsonWriter` and asserts that it throws an `IllegalArgumentException` with the expected message.
    - Attempts to write `Double.POSITIVE_INFINITY` to the `jsonWriter` and asserts that it throws an `IllegalArgumentException` with the expected message.
    - Attempts to write a `LazilyParsedNumber` initialized with 'Infinity' to the `jsonWriter` and asserts that it throws an `IllegalArgumentException` with the expected message.
- **Output**:
    - No output is returned; instead, the method verifies that specific exceptions are thrown for non-finite numeric values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteNumbers<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteNumbers}} -->
Tests the behavior of the `JsonWriter` when handling non-finite numbers.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**:
    - `jsonWriter`: An instance of `JsonWriter` used to write JSON data.
- **Control Flow**:
    - Creates a new `StringWriter` to capture the output of the `JsonWriter`.
    - Calls the [`assertNonFiniteNumbersExceptions`](#JsonWriterTestassertNonFiniteNumbersExceptions) method, passing the `jsonWriter` instance to it.
- **Output**:
    - No direct output; the method verifies that exceptions are thrown for non-finite numbers.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteNumbersExceptions`](#JsonWriterTestassertNonFiniteNumbersExceptions)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteNumbersWhenStrict<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteNumbersWhenStrict}} -->
Tests that non-finite numbers throw exceptions when strictness is set to STRICT.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Sets the strictness of the `JsonWriter` to `Strictness.STRICT`.
    - Calls the [`assertNonFiniteNumbersExceptions`](#JsonWriterTestassertNonFiniteNumbersExceptions) method with the `JsonWriter` to validate that non-finite numbers throw exceptions.
- **Output**:
    - No output is returned; the method validates exceptions thrown for non-finite numbers.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriterTest.assertNonFiniteNumbersExceptions`](#JsonWriterTestassertNonFiniteNumbersExceptions)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteFloatsWhenLenient<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteFloatsWhenLenient}} -->
Tests the behavior of `JsonWriter` when writing non-finite float values in lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter` and sets its strictness to `LENIENT`.
    - Begins a JSON array using `beginArray()` method.
    - Writes three non-finite float values: `Float.NaN`, `Float.NEGATIVE_INFINITY`, and `Float.POSITIVE_INFINITY` using the `value()` method.
    - Ends the JSON array using `endArray()` method.
    - Asserts that the output string matches the expected JSON representation of the non-finite float values.
- **Output**:
    - The method outputs a JSON array string representation of the non-finite float values, which is expected to be '[NaN,-Infinity,Infinity]'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteDoublesWhenLenient<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteDoublesWhenLenient}} -->
Tests the behavior of `JsonWriter` when writing non-finite double values in lenient mode.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter` and sets its strictness to `LENIENT`.
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Writes three non-finite double values: `Double.NaN`, `Double.NEGATIVE_INFINITY`, and `Double.POSITIVE_INFINITY`.
    - Ends the JSON array using `jsonWriter.endArray()`.
    - Asserts that the output string matches the expected JSON representation of the non-finite values.
- **Output**:
    - The method outputs a JSON array string representation of the non-finite double values, which is expected to be "[NaN,-Infinity,Infinity]".
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNonFiniteNumbersWhenLenient<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNonFiniteNumbersWhenLenient}} -->
Tests the behavior of `JsonWriter` when handling non-finite numbers in a lenient mode.
- **Modifiers**: `public`, `void`, `throws`
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter` and sets its strictness to `LENIENT`.
    - Begins a JSON array using `beginArray()` method.
    - Writes various non-finite numbers (NaN, negative infinity, positive infinity, and a lazily parsed infinity) to the JSON array.
    - Ends the JSON array using `endArray()` method.
    - Asserts that the output matches the expected JSON string representation of the non-finite numbers.
- **Output**:
    - The method outputs a JSON array string representation of non-finite numbers: '[NaN,-Infinity,Infinity,Infinity]'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testFloats<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testFloats}} -->
Tests the serialization of various float values into JSON format.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Writes multiple float values to the JSON array using `jsonWriter.value()`, including special float values like `-0.0f`, `Float.MAX_VALUE`, and `Math.PI`.
    - Ends the JSON array with `jsonWriter.endArray()`.
    - Closes the `JsonWriter` to finalize the output.
    - Asserts that the output string matches the expected JSON format using `assertThat()`.
- **Output**:
    - A JSON string representation of the float values written to the `StringWriter`, which is expected to match a predefined string.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testDoubles<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testDoubles}} -->
Tests the serialization of various double values into JSON format.
- **Modifiers**: `public`, `void`, `@Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Writes several double values to the JSON array using `jsonWriter.value(doubleValue)`.
    - Ends the JSON array with `jsonWriter.endArray()`.
    - Closes the `JsonWriter` to finalize the output.
    - Asserts that the output string matches the expected JSON representation of the double values.
- **Output**:
    - A string representation of a JSON array containing the specified double values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testLongs<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testLongs}} -->
Tests the `JsonWriter` class by writing a JSON array of long values.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Writes several long values including 0, 1, -1, `Long.MIN_VALUE`, and `Long.MAX_VALUE` to the JSON array.
    - Ends the JSON array with `jsonWriter.endArray()`.
    - Closes the `JsonWriter` to finalize the output.
    - Asserts that the output string matches the expected JSON representation of the long values.
- **Output**:
    - The method outputs a JSON string representation of an array containing the long values: [0, 1, -1, -9223372036854775808, 9223372036854775807].
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNumbers<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNumbers}} -->
Tests the serialization of various numeric types into JSON format.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `StringWriter` to capture the JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Writes several numeric values including `BigInteger` and `BigDecimal` to the JSON array.
    - Ends the JSON array with `jsonWriter.endArray()`.
    - Closes the `JsonWriter` to finalize the output.
    - Asserts that the output matches the expected JSON string.
- **Output**:
    - The method outputs a JSON array string containing the serialized numeric values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNumbersCustomClass<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNumbersCustomClass}} -->
Tests the serialization of various valid number strings using the `LazilyParsedNumber` class.
- **Inputs**:
    - `validNumbers`: An array of strings representing valid number formats that will be tested for serialization.
- **Control Flow**:
    - Iterates over each string in the `validNumbers` array.
    - For each valid number, creates a new `StringWriter` and `JsonWriter` instance.
    - Writes the number as a JSON value using `jsonWriter.value()`.
    - Closes the `jsonWriter` to finalize the output.
    - Asserts that the output from `stringWriter` matches the original valid number string.
- **Output**:
    - The method does not return a value but asserts that the serialized output matches the expected valid number string.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testMalformedNumbers<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testMalformedNumbers}} -->
Tests that various malformed number strings throw an IllegalArgumentException when parsed.
- **Inputs**:
    - `malformedNumbers`: An array of strings representing malformed number formats that are expected to fail when parsed.
- **Control Flow**:
    - Iterates over each string in the `malformedNumbers` array.
    - For each malformed number, a new `JsonWriter` instance is created.
    - The method attempts to write the malformed number using `jsonWriter.value()` wrapped in an assertion that expects an `IllegalArgumentException` to be thrown.
    - The exception's message is then checked to ensure it matches the expected error message for that malformed number.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown for each malformed number.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testBooleans<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testBooleans}} -->
Tests the `JsonWriter` class by writing a JSON array containing boolean values.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Writes the boolean value `true` to the JSON array.
    - Writes the boolean value `false` to the JSON array.
    - Ends the JSON array using `jsonWriter.endArray()`.
    - Asserts that the output of the `StringWriter` matches the expected JSON string '[true,false]'.
- **Output**:
    - The method outputs a JSON string representation of an array containing the boolean values true and false.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testBoxedBooleans<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testBoxedBooleans}} -->
Tests the serialization of boxed Boolean values to JSON.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array.
    - Writes a boxed `Boolean` value of `true`.
    - Writes a boxed `Boolean` value of `false`.
    - Writes a boxed `Boolean` value of `null`.
    - Ends the JSON array.
    - Asserts that the output matches the expected JSON string '[true,false,null]'.
- **Output**:
    - A JSON string representation of an array containing the values true, false, and null.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testNulls<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testNulls}} -->
Tests the `JsonWriter` class to ensure it correctly writes a JSON array containing a null value.
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the output of the `JsonWriter`.
    - A `JsonWriter` is created using the `StringWriter`.
    - The [`beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray) method is called to start a new JSON array.
    - The [`nullValue`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue) method is called to write a null value into the array.
    - The [`endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray) method is called to close the JSON array.
    - The output of the `StringWriter` is compared to the expected JSON string '[null]' using an assertion.
- **Output**:
    - The method outputs a string representation of a JSON array containing a single null value, which is '[null]'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testStrings<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testStrings}} -->
Tests the `JsonWriter` class by writing various string values to a JSON array.
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array using `jsonWriter.beginArray()`.
    - Writes multiple string values to the JSON array using `jsonWriter.value()`, including escaped characters and special characters.
    - Ends the JSON array using `jsonWriter.endArray()`.
    - Asserts that the output of the `StringWriter` matches the expected JSON string.
- **Output**:
    - The output is a JSON array containing various string values, including escaped characters.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testUnicodeLineBreaksEscaped<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testUnicodeLineBreaksEscaped}} -->
Tests the escaping of Unicode line breaks in JSON output.
- **Modifiers**: `public`, `void`, `throws`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the JSON output.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON array.
    - Writes a string containing Unicode line break characters (`` and `	`) to the JSON array.
    - Ends the JSON array.
    - Asserts that the output matches the expected escaped format.
- **Output**:
    - A string representation of a JSON array containing the escaped Unicode line breaks.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testEmptyArray<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testEmptyArray}} -->
Tests the behavior of the `JsonWriter` when writing an empty JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` instance to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins writing a JSON array using `jsonWriter.beginArray()`.
    - Ends the JSON array with `jsonWriter.endArray()`.
    - Converts the output from `StringWriter` to a string and asserts that it equals '[]'.
- **Output**:
    - The method outputs a string representation of an empty JSON array, which is '[]'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testEmptyObject<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testEmptyObject}} -->
Tests the creation of an empty JSON object.
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the output of the JSON writer.
    - A `JsonWriter` is created using the `StringWriter`.
    - The `beginObject()` method is called to start a new JSON object.
    - The `endObject()` method is called to close the JSON object.
    - The output from the `StringWriter` is compared to the expected JSON representation of an empty object.
- **Output**:
    - The method asserts that the output string is equal to the JSON representation of an empty object, which is '{}'. 
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testObjectsInArrays<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testObjectsInArrays}} -->
Tests the creation of a JSON array containing two objects with specified key-value pairs.
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the JSON output.
    - A `JsonWriter` is created using the `StringWriter`.
    - The JSON array is started with `beginArray()`.
    - The first JSON object is created with `beginObject()`, followed by adding key-value pairs using `name()` and `value()` methods, and then closed with `endObject()`.
    - The second JSON object is created similarly to the first, with its own key-value pairs.
    - The JSON array is closed with `endArray()`.
    - Finally, the output of the `StringWriter` is asserted to match the expected JSON string.
- **Output**:
    - A string representation of a JSON array containing two objects: [{"a":5,"b":false},{"c":6,"d":true}].
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testArraysInObjects<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testArraysInObjects}} -->
Tests the creation of JSON objects containing arrays using `JsonWriter`.
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter`.
    - Begins a JSON object with `beginObject()`.
    - Writes the first name 'a' and begins an array, adding values 5 and false, then ends the array.
    - Writes the second name 'b' and begins another array, adding values 6 and true, then ends the array.
    - Ends the JSON object.
    - Asserts that the output matches the expected JSON string.
- **Output**:
    - A string representation of a JSON object containing two arrays: {"a":[5,false],"b":[6,true]}.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testDeepNestingArrays<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testDeepNestingArrays}} -->
Tests the ability to create deeply nested JSON arrays.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the output of the `JsonWriter`.
    - A `JsonWriter` is created using the `StringWriter`.
    - A loop runs 20 times, calling `beginArray()` on the `JsonWriter` each time to create nested arrays.
    - Another loop runs 20 times, calling `endArray()` on the `JsonWriter` each time to close the nested arrays.
    - Finally, the output of the `StringWriter` is asserted to match the expected deeply nested JSON array structure.
- **Output**:
    - A string representation of a deeply nested JSON array with 20 levels of nesting, resulting in the string '[[[[[[[[[[[[[[[[[[[[]]]]]]]]]]]]]]]]]]]]'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testDeepNestingObjects<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testDeepNestingObjects}} -->
Tests the `JsonWriter` class by creating a deeply nested JSON object.
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is created to capture the output of the `JsonWriter`.
    - A `JsonWriter` instance is initialized with the `StringWriter`.
    - The method begins a JSON object using `jsonWriter.beginObject()`.
    - A loop iterates 20 times, each time writing a name 'a' and beginning a new object.
    - Another loop iterates 20 times, each time ending the most recently opened object.
    - The JSON object is closed with `jsonWriter.endObject()`.
    - The output from the `StringWriter` is compared to the expected deeply nested JSON string using an assertion.
- **Output**:
    - The output is a string representation of a deeply nested JSON object with 20 levels of nesting, all named 'a'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testRepeatedName<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testRepeatedName}} -->
Tests the behavior of `JsonWriter` when writing duplicate names in a JSON object.
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is created to capture the output of the `JsonWriter`.
    - A `JsonWriter` instance is initialized with the `StringWriter`.
    - The method begins a JSON object using `jsonWriter.beginObject()`.
    - The name 'a' is written with a value of `true` using `jsonWriter.name('a').value(true)`.
    - The name 'a' is written again with a value of `false` using `jsonWriter.name('a').value(false)`.
    - The JSON object is closed with `jsonWriter.endObject()`.
    - The output is asserted to check if it matches the expected JSON string with duplicate names.
- **Output**:
    - The output is a string representation of a JSON object that contains duplicate keys, specifically '{"a":true,"a":false}'.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testPrettyPrintObject<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testPrettyPrintObject}} -->
Tests the pretty printing of a JSON object using `JsonWriter`.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter` and sets the indentation to three spaces.
    - Begins a JSON object and writes several key-value pairs, including boolean values, a null value, an array, and a nested object.
    - Ends the JSON object.
    - Defines an expected JSON string that represents the formatted output.
    - Asserts that the output from the `StringWriter` matches the expected JSON string.
- **Output**:
    - The method outputs a formatted JSON string that represents the structure defined in the method, which includes various data types and nested objects.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setIndent`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetIndent)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testPrettyPrintArray<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testPrettyPrintArray}} -->
Tests the pretty printing of a JSON array using `JsonWriter`.
- **Inputs**: None
- **Control Flow**:
    - Creates a `StringWriter` to capture the output of the `JsonWriter`.
    - Initializes a `JsonWriter` with the `StringWriter` and sets the indentation to three spaces.
    - Begins a JSON array and writes various values including booleans, a number, a null value, an object, and another array.
    - Ends the inner array and the outer array.
    - Defines the expected JSON string format for comparison.
    - Asserts that the output from the `StringWriter` matches the expected JSON string.
- **Output**:
    - The method outputs a formatted JSON string representation of the written values.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setIndent`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetIndent)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testClosedWriterThrowsOnStructure<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnStructure}} -->
Tests that a closed `JsonWriter` throws an `IllegalStateException` when attempting to write JSON structures.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - A `StringWriter` is created to capture the output of the `JsonWriter`.
    - A `JsonWriter` instance is initialized with the `StringWriter`.
    - The writer begins and ends an array, then closes the writer.
    - An expected message is defined for the exception that should be thrown.
    - The method asserts that calling [`beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray), [`endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray), [`beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject), and [`endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject) on the closed writer throws an `IllegalStateException` with the expected message.
- **Output**:
    - The method does not return a value; it asserts that specific exceptions are thrown when methods are called on a closed `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testClosedWriterThrowsOnName<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnName}} -->
Tests that an `IllegalStateException` is thrown when attempting to write a name after the `JsonWriter` has been closed.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the output of the `JsonWriter`.
    - A `JsonWriter` is created using the `StringWriter`.
    - The [`beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray) method is called to start a JSON array.
    - The [`endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray) method is called to close the JSON array.
    - The [`close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose) method is called on the `JsonWriter` to close it.
    - An attempt is made to call the [`name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername) method on the closed `JsonWriter`, which is expected to throw an `IllegalStateException`.
    - The exception is caught and its message is asserted to be 'JsonWriter is closed.'
- **Output**:
    - The method does not return a value but asserts that an `IllegalStateException` is thrown with the message 'JsonWriter is closed.' when trying to write a name after the writer has been closed.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testClosedWriterThrowsOnValue<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnValue}} -->
Tests that an `IllegalStateException` is thrown when attempting to write a value after the `JsonWriter` has been closed.
- **Inputs**:
    - `stringWriter`: A `StringWriter` instance used to capture the output of the `JsonWriter`.
    - `writer`: A `JsonWriter` instance that writes JSON data to the `StringWriter`.
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the output.
    - A `JsonWriter` is created using the `StringWriter`.
    - The writer begins and ends a JSON array, then closes the writer.
    - An attempt is made to write a value to the closed writer, which should throw an `IllegalStateException`.
    - The exception is caught and its message is asserted to be 'JsonWriter is closed.'
- **Output**:
    - An `IllegalStateException` is thrown with the message 'JsonWriter is closed.' when trying to write a value after the writer has been closed.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testClosedWriterThrowsOnFlush<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testClosedWriterThrowsOnFlush}} -->
Tests that calling [`flush`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterflush) on a closed `JsonWriter` throws an `IllegalStateException`.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the output of the `JsonWriter`.
    - A `JsonWriter` is created using the `StringWriter`.
    - The [`beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray) method is called to start a JSON array.
    - The [`endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray) method is called to close the JSON array.
    - The [`close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose) method is called on the `JsonWriter` to close it.
    - An assertion is made to check that calling [`flush`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterflush) on the closed `JsonWriter` throws an `IllegalStateException`.
    - The exception's message is verified to be 'JsonWriter is closed.'.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.stream.JsonWriter.flush`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterflush)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testWriterCloseIsIdempotent<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testWriterCloseIsIdempotent}} -->
Tests that closing a `JsonWriter` multiple times does not change the output.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**:
    - `stringWriter`: A `StringWriter` instance used to capture the output of the `JsonWriter`.
    - `writer`: A `JsonWriter` instance that writes JSON data to the `StringWriter`.
- **Control Flow**:
    - A new `StringWriter` is created to capture the output.
    - A new `JsonWriter` is instantiated with the `StringWriter`.
    - The writer begins and ends a JSON array, which results in an empty array being written to the `StringWriter`.
    - The writer is closed, and the output is asserted to be '[]'.
    - The writer is closed again, and the output is asserted again to be '[]', confirming idempotency.
- **Output**:
    - The output is a string representation of an empty JSON array, '[]', which remains unchanged after multiple close calls.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testSetGetFormattingStyle<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testSetGetFormattingStyle}} -->
Tests the setting and getting of formatting styles in a `JsonWriter`.
- **Inputs**:
    - `lineSeparator`: A string representing the line separator to be used in the formatted output.
    - `stringWriter`: A `StringWriter` instance used to capture the output of the `JsonWriter`.
    - `jsonWriter`: An instance of `JsonWriter` that is being tested for formatting style.
- **Control Flow**:
    - The method begins by defining a line separator string.
    - A `StringWriter` and a `JsonWriter` are instantiated.
    - The default formatting style of the `JsonWriter` is asserted to be `FormattingStyle.COMPACT`.
    - The formatting style of the `JsonWriter` is set to a pretty format with specified indentation and newline.
    - An array is started in the `JsonWriter`, and various values (boolean, string, number, null) are written to it.
    - The expected formatted string is constructed based on the specified formatting style.
    - The output of the `StringWriter` is compared to the expected string to verify correctness.
    - Finally, the newline character of the current formatting style is asserted to match the defined line separator.
- **Output**:
    - The method does not return a value but asserts that the output of the `JsonWriter` matches the expected formatted JSON string.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.getFormattingStyle`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritergetFormattingStyle)
    - [`com.google.gson.stream.JsonWriter.setFormattingStyle`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetFormattingStyle)
    - [`com.google.gson.FormattingStyle.withIndent`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithIndent)
    - [`com.google.gson.FormattingStyle.withNewline`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithNewline)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
    - [`com.google.gson.FormattingStyle.getNewline`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylegetNewline)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)


---
#### JsonWriterTest\.testIndentOverwritesFormattingStyle<!-- {{#callable:com.google.gson.stream.JsonWriterTest.testIndentOverwritesFormattingStyle}} -->
Tests that the indentation setting overwrites the formatting style in a `JsonWriter`.
- **Inputs**:
    - `stringWriter`: A `StringWriter` instance used to capture the output of the `JsonWriter`.
    - `jsonWriter`: A `JsonWriter` instance that writes JSON data to the `StringWriter`.
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the JSON output.
    - A `JsonWriter` is created using the `StringWriter`.
    - The formatting style of the `JsonWriter` is set to `FormattingStyle.COMPACT`.
    - The indentation is set to two spaces, which should overwrite the compact formatting style.
    - The method begins a JSON object and writes a name followed by an array containing two integer values.
    - The JSON object is closed, and the expected output is defined.
    - Finally, the actual output from the `StringWriter` is compared to the expected output using an assertion.
- **Output**:
    - The method outputs a formatted JSON string that includes an object with a key "a" and an array of integers [1, 2], properly indented.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setFormattingStyle`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetFormattingStyle)
    - [`com.google.gson.stream.JsonWriter.setIndent`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetIndent)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumbertoString)
- **See also**: [`com.google.gson.stream.JsonWriterTest`](#JsonWriterTest)  (Base Class)



