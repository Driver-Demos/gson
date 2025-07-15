# Purpose
The `JsonPrimitiveTest` class is a comprehensive unit test suite for the `JsonPrimitive` class, part of the Google Gson library. This test class is designed to validate the behavior and functionality of `JsonPrimitive`, which represents a JSON element that can hold a primitive value such as a number, string, or boolean. The tests cover a wide range of scenarios, including the creation of `JsonPrimitive` objects with different data types, the conversion of these objects to various primitive types, and the handling of special cases like null values and unsupported operations. The test methods utilize assertions to ensure that the `JsonPrimitive` class behaves as expected, particularly in terms of type conversion, equality, and immutability.

The test suite is organized into multiple test methods, each focusing on specific aspects of the `JsonPrimitive` class. These include tests for handling null inputs, parsing strings as booleans or numbers, and verifying the equality of `JsonPrimitive` instances across different data types. The tests also check the behavior of `JsonPrimitive` when dealing with special numeric values like NaN and infinity, as well as the correct implementation of the `equals` and `hashCode` methods. Additionally, the suite includes tests for the `toString` method to ensure proper JSON representation of primitive values. Overall, this test class serves as a critical component in ensuring the reliability and correctness of the `JsonPrimitive` class within the Gson library.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `com.google.common.truth.Truth.assertWithMessage`
- `org.junit.Assert.assertThrows`
- `com.google.gson.common.MoreAsserts`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `org.junit.Test`


# Classes

---
### JsonPrimitiveTest<!-- {{#class:com.google.gson.JsonPrimitiveTest}} -->
- **Modifiers**: `public`
- **Description**: The `JsonPrimitiveTest` class is a comprehensive unit test suite for the `JsonPrimitive` class, which is part of the Google Gson library. It tests various functionalities of `JsonPrimitive`, including its ability to handle different data types such as Boolean, Number, String, and Character. The class ensures that `JsonPrimitive` correctly throws exceptions for null inputs, accurately parses strings as booleans and numbers, and maintains equality and hash code consistency across different numeric types. It also verifies the immutability of `JsonPrimitive` instances and checks the transitive property of equality for `BigDecimal` values.
- **Methods**:
    - [`com.google.gson.JsonPrimitiveTest.testNulls`](#JsonPrimitiveTesttestNulls)
    - [`com.google.gson.JsonPrimitiveTest.testBoolean`](#JsonPrimitiveTesttestBoolean)
    - [`com.google.gson.JsonPrimitiveTest.testParsingStringAsBoolean`](#JsonPrimitiveTesttestParsingStringAsBoolean)
    - [`com.google.gson.JsonPrimitiveTest.testParsingStringAsNumber`](#JsonPrimitiveTesttestParsingStringAsNumber)
    - [`com.google.gson.JsonPrimitiveTest.testAsNumber_Boolean`](#JsonPrimitiveTesttestAsNumber_Boolean)
    - [`com.google.gson.JsonPrimitiveTest.testStringsAndChar`](#JsonPrimitiveTesttestStringsAndChar)
    - [`com.google.gson.JsonPrimitiveTest.testExponential`](#JsonPrimitiveTesttestExponential)
    - [`com.google.gson.JsonPrimitiveTest.testByteEqualsShort`](#JsonPrimitiveTesttestByteEqualsShort)
    - [`com.google.gson.JsonPrimitiveTest.testByteEqualsInteger`](#JsonPrimitiveTesttestByteEqualsInteger)
    - [`com.google.gson.JsonPrimitiveTest.testByteEqualsLong`](#JsonPrimitiveTesttestByteEqualsLong)
    - [`com.google.gson.JsonPrimitiveTest.testByteEqualsBigInteger`](#JsonPrimitiveTesttestByteEqualsBigInteger)
    - [`com.google.gson.JsonPrimitiveTest.testShortEqualsInteger`](#JsonPrimitiveTesttestShortEqualsInteger)
    - [`com.google.gson.JsonPrimitiveTest.testShortEqualsLong`](#JsonPrimitiveTesttestShortEqualsLong)
    - [`com.google.gson.JsonPrimitiveTest.testShortEqualsBigInteger`](#JsonPrimitiveTesttestShortEqualsBigInteger)
    - [`com.google.gson.JsonPrimitiveTest.testIntegerEqualsLong`](#JsonPrimitiveTesttestIntegerEqualsLong)
    - [`com.google.gson.JsonPrimitiveTest.testIntegerEqualsBigInteger`](#JsonPrimitiveTesttestIntegerEqualsBigInteger)
    - [`com.google.gson.JsonPrimitiveTest.testLongEqualsBigInteger`](#JsonPrimitiveTesttestLongEqualsBigInteger)
    - [`com.google.gson.JsonPrimitiveTest.testFloatEqualsDouble`](#JsonPrimitiveTesttestFloatEqualsDouble)
    - [`com.google.gson.JsonPrimitiveTest.testFloatEqualsBigDecimal`](#JsonPrimitiveTesttestFloatEqualsBigDecimal)
    - [`com.google.gson.JsonPrimitiveTest.testDoubleEqualsBigDecimal`](#JsonPrimitiveTesttestDoubleEqualsBigDecimal)
    - [`com.google.gson.JsonPrimitiveTest.testToString`](#JsonPrimitiveTesttestToString)
    - [`com.google.gson.JsonPrimitiveTest.testEquals`](#JsonPrimitiveTesttestEquals)
    - [`com.google.gson.JsonPrimitiveTest.testEqualsAcrossTypes`](#JsonPrimitiveTesttestEqualsAcrossTypes)
    - [`com.google.gson.JsonPrimitiveTest.testEqualsIntegerAndBigInteger`](#JsonPrimitiveTesttestEqualsIntegerAndBigInteger)
    - [`com.google.gson.JsonPrimitiveTest.testEqualsDoesNotEquateStringAndNonStringTypes`](#JsonPrimitiveTesttestEqualsDoesNotEquateStringAndNonStringTypes)
    - [`com.google.gson.JsonPrimitiveTest.testDeepCopy`](#JsonPrimitiveTesttestDeepCopy)
    - [`com.google.gson.JsonPrimitiveTest.testBigDecimalEquals`](#JsonPrimitiveTesttestBigDecimalEquals)
    - [`com.google.gson.JsonPrimitiveTest.testBigDecimalEqualsZero`](#JsonPrimitiveTesttestBigDecimalEqualsZero)
    - [`com.google.gson.JsonPrimitiveTest.testBigDecimalEqualsTransitive`](#JsonPrimitiveTesttestBigDecimalEqualsTransitive)
    - [`com.google.gson.JsonPrimitiveTest.testEqualsDoubleNaNAndBigDecimal`](#JsonPrimitiveTesttestEqualsDoubleNaNAndBigDecimal)

**Methods**

---
#### JsonPrimitiveTest\.testNulls<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testNulls}} -->
The `testNulls` method verifies that creating a `JsonPrimitive` with a null value for different data types throws a `NullPointerException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check that a `NullPointerException` is thrown when a `JsonPrimitive` is instantiated with a null `Boolean`.
    - It repeats the `assertThrows` check for a null `Number`.
    - It repeats the `assertThrows` check for a null `String`.
    - It repeats the `assertThrows` check for a null `Character`.
- **Output**:
    - The method does not return any value; it is a test method that asserts exceptions are thrown.
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testBoolean<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testBoolean}} -->
The `testBoolean` method tests the behavior of the `JsonPrimitive` class when handling boolean values and various inputs that can be interpreted as booleans.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonPrimitive` object is created with a `Boolean.TRUE` value, and assertions are made to check that it is recognized as a boolean and returns true when [`getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean) is called.
    - A `JsonPrimitive` object is created with an integer value `1`, and an assertion checks that [`getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean) returns false.
    - A `JsonPrimitive` object is created with a string value "1", and an assertion checks that [`getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean) returns false.
    - A `JsonPrimitive` object is created with a string value "true", and an assertion checks that [`getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean) returns true.
    - A `JsonPrimitive` object is created with a string value "TrUe", and an assertion checks that [`getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean) returns true.
    - A `JsonPrimitive` object is created with a string value "1.3", and an assertion checks that [`getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean) returns false.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of `JsonPrimitive` with boolean-related inputs.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitiveisBoolean)
    - [`com.google.gson.JsonPrimitive.getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testParsingStringAsBoolean<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testParsingStringAsBoolean}} -->
The `testParsingStringAsBoolean` method tests the behavior of the `JsonPrimitive` class when parsing a string representation of a boolean value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonPrimitive` object is created with the string value "true".
    - The method asserts that `json.isBoolean()` returns `false`, indicating that the `JsonPrimitive` does not recognize the string "true" as a boolean type.
    - The method asserts that `json.getAsBoolean()` returns `true`, demonstrating that the `JsonPrimitive` can interpret the string "true" as a boolean value when explicitly requested.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonPrimitive` class.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitiveisBoolean)
    - [`com.google.gson.JsonPrimitive.getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testParsingStringAsNumber<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testParsingStringAsNumber}} -->
The `testParsingStringAsNumber` method tests the conversion of a string representation of a number into various numeric types using the `JsonPrimitive` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonPrimitive` object is created with the string "1".
    - The method asserts that `json.isNumber()` returns `false`, indicating that the string is not recognized as a number by default.
    - The method then asserts that calling `getAsDouble()`, `getAsFloat()`, `getAsInt()`, `getAsLong()`, `getAsShort()`, `getAsByte()`, `getAsBigInteger()`, and `getAsBigDecimal()` on the `JsonPrimitive` object returns the expected numeric values equivalent to 1 in their respective types.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonPrimitive` class when parsing a string as a number.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsDouble`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsDouble)
    - [`com.google.gson.JsonPrimitive.getAsFloat`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsFloat)
    - [`com.google.gson.JsonPrimitive.getAsInt`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt)
    - [`com.google.gson.JsonPrimitive.getAsLong`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsLong)
    - [`com.google.gson.JsonPrimitive.getAsShort`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsShort)
    - [`com.google.gson.JsonPrimitive.getAsByte`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsByte)
    - [`com.google.gson.JsonPrimitive.getAsBigInteger`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBigInteger)
    - [`com.google.gson.JsonPrimitive.getAsBigDecimal`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBigDecimal)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testAsNumber\_Boolean<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testAsNumber_Boolean}} -->
The `testAsNumber_Boolean` method tests that attempting to retrieve a number from a `JsonPrimitive` initialized with a boolean value throws an `UnsupportedOperationException` with a specific error message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonPrimitive` object is created with a boolean value `true`.
    - The method `getAsNumber()` is called on this `JsonPrimitive` object within an `assertThrows` block to check if it throws an `UnsupportedOperationException`.
    - The exception is captured in a variable `e`.
    - An assertion is made to verify that the exception message is 'Primitive is neither a number nor a string'.
- **Output**:
    - The method does not return any value as it is a test method; it verifies behavior by asserting expected exceptions and messages.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.getAsNumber`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsNumber)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testStringsAndChar<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testStringsAndChar}} -->
The `testStringsAndChar` method tests the behavior of the `JsonPrimitive` class when handling string and character values, including edge cases like empty strings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonPrimitive` object is created with the string "abc" and assertions are made to check if it is recognized as a string, if its first character is 'a', and if its string representation is "abc".
    - A `JsonPrimitive` object is created with the character 'z' and similar assertions are made to check its string status, character value, and string representation.
    - A `JsonPrimitive` object is created with a boolean value `true`, and an assertion checks if its string representation is "true".
    - A `JsonPrimitive` object is created with an empty string, and an assertion checks if its string representation is an empty string.
    - An `UnsupportedOperationException` is expected to be thrown when attempting to get a character from the empty string `JsonPrimitive`, and the exception message is verified to be "String value is empty".
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the correctness of `JsonPrimitive` operations with strings and characters through assertions.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isString`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitiveisString)
    - [`com.google.gson.JsonPrimitive.getAsCharacter`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsCharacter)
    - [`com.google.gson.JsonPrimitive.getAsString`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testExponential<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testExponential}} -->
The `testExponential` method tests the behavior of the `JsonPrimitive` class when handling a string representation of an exponential number.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonPrimitive` object is created with the string "1E+7".
    - The method asserts that calling `getAsBigDecimal()` on the `JsonPrimitive` object returns a `BigDecimal` equal to `new BigDecimal("1E+7")`.
    - The method asserts that calling `getAsDouble()` on the `JsonPrimitive` object returns a `double` equal to `1E+7`.
    - The method asserts that calling `getAsInt()` on the `JsonPrimitive` object throws a `NumberFormatException`, as integers cannot handle exponential formats.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonPrimitive` class.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.getAsBigDecimal`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBigDecimal)
    - [`com.google.gson.JsonPrimitive.getAsDouble`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsDouble)
    - [`com.google.gson.JsonPrimitive.getAsInt`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testByteEqualsShort<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testByteEqualsShort}} -->
The `testByteEqualsShort` method verifies that a `JsonPrimitive` created with a byte value is equal to another `JsonPrimitive` created with a short value, and that their hash codes are also equal.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` with a byte value of 10.
    - Create another `JsonPrimitive` object `p2` with a short value of 10.
    - Assert that `p1` is equal to `p2` using `assertThat(p1).isEqualTo(p2)`.
    - Assert that the hash code of `p1` is equal to the hash code of `p2` using `assertThat(p1.hashCode()).isEqualTo(p2.hashCode())`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality of two `JsonPrimitive` objects and their hash codes.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testByteEqualsInteger<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testByteEqualsInteger}} -->
The `testByteEqualsInteger` method tests the equality and hash code consistency between a `JsonPrimitive` created with a byte value and another created with an integer value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` with a byte value of 10.
    - Create another `JsonPrimitive` object `p2` with an integer value of 10.
    - Use `assertThat` to verify that `p1` is equal to `p2`.
    - Use `assertThat` to verify that the hash code of `p1` is equal to the hash code of `p2`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testByteEqualsLong<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testByteEqualsLong}} -->
The `testByteEqualsLong` method verifies that a `JsonPrimitive` created with a byte value is equal to a `JsonPrimitive` created with a long value, and that their hash codes are also equal.
- **Modifiers**: `public`, `@Test`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` with a byte value of 10.
    - Create a `JsonPrimitive` object `p2` with a long value of 10.
    - Assert that `p1` is equal to `p2` using `assertThat`.
    - Assert that the hash code of `p1` is equal to the hash code of `p2` using `assertThat`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality of two `JsonPrimitive` objects and their hash codes.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testByteEqualsBigInteger<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testByteEqualsBigInteger}} -->
The `testByteEqualsBigInteger` method tests the equality and hash code consistency between a `JsonPrimitive` created from a byte and another created from a `BigInteger` with the same numeric value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` initialized with a byte value of 10.
    - Create another `JsonPrimitive` object `p2` initialized with a `BigInteger` value of 10.
    - Use `assertThat` to verify that `p1` is equal to `p2`.
    - Use `assertThat` to verify that the hash code of `p1` is equal to the hash code of `p2`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testShortEqualsInteger<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testShortEqualsInteger}} -->
The `testShortEqualsInteger` method tests the equality and hash code consistency between a `JsonPrimitive` created with a `short` value and another created with an `int` value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` initialized with a `short` value of 10.
    - Create another `JsonPrimitive` object `p2` initialized with an `int` value of 10.
    - Assert that `p1` is equal to `p2` using the `assertThat` method from the `Truth` library.
    - Assert that the hash codes of `p1` and `p2` are equal using the `assertThat` method.
- **Output**:
    - The method does not return any value; it performs assertions to verify the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testShortEqualsLong<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testShortEqualsLong}} -->
The `testShortEqualsLong` method tests the equality and hash code consistency between a `JsonPrimitive` created with a short value and another created with a long value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` with a short value of 10.
    - Create another `JsonPrimitive` object `p2` with a long value of 10.
    - Assert that `p1` is equal to `p2` using the `isEqualTo` method from the `Truth` library.
    - Assert that the hash codes of `p1` and `p2` are equal using the `isEqualTo` method from the `Truth` library.
- **Output**:
    - The method does not return any value as it is a test method; it asserts the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testShortEqualsBigInteger<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testShortEqualsBigInteger}} -->
The method `testShortEqualsBigInteger` tests the equality and hash code consistency between a `JsonPrimitive` created from a `short` and another created from a `BigInteger` with the same numeric value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` initialized with a `short` value of 10.
    - Create another `JsonPrimitive` object `p2` initialized with a `BigInteger` value of 10.
    - Assert that `p1` is equal to `p2` using the `assertThat` method from the `Truth` library.
    - Assert that the hash codes of `p1` and `p2` are equal using the `assertThat` method.
- **Output**:
    - The method does not return any value; it performs assertions to verify the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testIntegerEqualsLong<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testIntegerEqualsLong}} -->
The `testIntegerEqualsLong` method verifies that a `JsonPrimitive` created with an integer value is equal to a `JsonPrimitive` created with a long value, and that their hash codes are also equal.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` with an integer value of 10.
    - Create a `JsonPrimitive` object `p2` with a long value of 10L.
    - Use `assertThat` to check that `p1` is equal to `p2`.
    - Use `assertThat` to check that the hash code of `p1` is equal to the hash code of `p2`.
- **Output**:
    - The method does not return any value; it performs assertions to validate equality and hash code consistency between two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testIntegerEqualsBigInteger<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testIntegerEqualsBigInteger}} -->
The method `testIntegerEqualsBigInteger` tests the equality and hash code consistency between a `JsonPrimitive` created with an `Integer` and another created with a `BigInteger` of the same value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` initialized with an `Integer` value of 10.
    - Create another `JsonPrimitive` object `p2` initialized with a `BigInteger` value of 10.
    - Use `assertThat` to verify that `p1` is equal to `p2`.
    - Use `assertThat` to verify that the hash codes of `p1` and `p2` are equal.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.hashCode`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivehashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testLongEqualsBigInteger<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testLongEqualsBigInteger}} -->
The `testLongEqualsBigInteger` method tests the equality and hash code consistency between a `JsonPrimitive` created from a `long` and another created from a `BigInteger` with the same numeric value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` initialized with a `long` value of 10.
    - Create another `JsonPrimitive` object `p2` initialized with a `BigInteger` value of 10.
    - Use `assertThat` to verify that `p1` is equal to `p2`.
    - Use `assertThat` to verify that the hash code of `p1` is equal to the hash code of `p2`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.hashCode`](GsonTest.java.driver.md#DummyFactoryhashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testFloatEqualsDouble<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testFloatEqualsDouble}} -->
The `testFloatEqualsDouble` method tests the equality of two `JsonPrimitive` objects created with a float and a double value, ensuring they are considered equal and have the same hash code.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` with a float value of 10.25F.
    - Create another `JsonPrimitive` object `p2` with a double value of 10.25D.
    - Use `assertThat` to verify that `p1` is equal to `p2`.
    - Use `assertThat` to verify that the hash code of `p1` is equal to the hash code of `p2`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code of the two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.hashCode`](GsonTest.java.driver.md#DummyFactoryhashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testFloatEqualsBigDecimal<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testFloatEqualsBigDecimal}} -->
The method `testFloatEqualsBigDecimal` tests the equality and hash code consistency between a `JsonPrimitive` created from a `float` and another created from a `BigDecimal` with the same value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` initialized with a `float` value of 10.25F.
    - Create another `JsonPrimitive` object `p2` initialized with a `BigDecimal` value of 10.25.
    - Use `assertThat` to verify that `p1` is equal to `p2`.
    - Use `assertThat` to verify that the hash code of `p1` is equal to the hash code of `p2`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code consistency of two `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.hashCode`](GsonTest.java.driver.md#DummyFactoryhashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testDoubleEqualsBigDecimal<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testDoubleEqualsBigDecimal}} -->
The method `testDoubleEqualsBigDecimal` tests the equality and hash code consistency between a `JsonPrimitive` created from a `double` and another created from a `BigDecimal` with the same value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `p1` initialized with a `double` value of 10.25.
    - Create another `JsonPrimitive` object `p2` initialized with a `BigDecimal` value of 10.25.
    - Use `assertThat` to verify that `p1` is equal to `p2`.
    - Use `assertThat` to verify that the hash code of `p1` is equal to the hash code of `p2`.
- **Output**:
    - The method does not return any value; it performs assertions to verify equality and hash code consistency.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.hashCode`](GsonTest.java.driver.md#DummyFactoryhashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testToString<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testToString}} -->
The `testToString` method tests the [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) functionality of the `JsonPrimitive` class for various data types and values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object with a string containing escaped newlines and assert its [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) output matches the expected escaped format.
    - Create a `JsonPrimitive` object with an empty string and assert its [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) output is an empty quoted string.
    - Create a `JsonPrimitive` object with a `BigDecimal` value and assert its [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) output matches the expected decimal format, including preservation of trailing zeros.
    - Create `JsonPrimitive` objects with `Float.NaN` and `Double.NEGATIVE_INFINITY` and assert their [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) outputs match the expected string representations of 'NaN' and '-Infinity'.
    - Create `JsonPrimitive` objects with a character and a null character, asserting their [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) outputs match the expected quoted character and Unicode escape sequence respectively.
    - Create a `JsonPrimitive` object with a boolean value and assert its [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) output matches the expected boolean string representation.
- **Output**:
    - The method does not return any value; it performs assertions to validate the [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) method of `JsonPrimitive`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testEquals<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testEquals}} -->
The `testEquals` method verifies the equality and hash code consistency of `JsonPrimitive` objects with various data types and values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses `MoreAsserts.assertEqualsAndHashCode` to check that `JsonPrimitive` objects with identical values (e.g., strings, booleans, numbers, and special float/double values like NaN and infinity) are equal and have the same hash code.
    - It then uses `assertThat` to verify that `JsonPrimitive` objects with different values are not equal.
- **Output**:
    - The method does not return any value; it is a test method that asserts conditions to validate the behavior of `JsonPrimitive` equality and hash code methods.
- **Functions called**:
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testEqualsAcrossTypes<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testEqualsAcrossTypes}} -->
The `testEqualsAcrossTypes` method tests the equality and hash code consistency of `JsonPrimitive` objects created from different data types.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses `MoreAsserts.assertEqualsAndHashCode` to verify that `JsonPrimitive` objects created from different types are considered equal and have the same hash code.
    - It compares a `JsonPrimitive` created from a `String` with one created from a `char`.
    - It compares a `JsonPrimitive` created from a `BigInteger` with one created from an `int`.
    - It compares a `JsonPrimitive` created from an `int` with one created from a `long`.
    - It compares a `JsonPrimitive` created from a `BigDecimal` with one created from an `int`.
    - It compares a `JsonPrimitive` created from `Float.NaN` with one created from `Double.NaN`.
- **Output**:
    - The method does not return any value; it asserts the equality and hash code consistency of the `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testEqualsIntegerAndBigInteger<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testEqualsIntegerAndBigInteger}} -->
The method `testEqualsIntegerAndBigInteger` tests the equality comparison between a `JsonPrimitive` initialized with a `long` value and another `JsonPrimitive` initialized with a `BigInteger` value, asserting that they are not equal.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `a` initialized with a `long` value of 5.
    - Create a `JsonPrimitive` object `b` initialized with a `BigInteger` value of 18446744073709551621.
    - Use `assertWithMessage` to assert that `a.equals(b)` is false, with a custom message format indicating the two objects being compared.
- **Output**:
    - The method does not return any value; it performs an assertion to verify that the two `JsonPrimitive` objects are not equal.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testEqualsDoesNotEquateStringAndNonStringTypes<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testEqualsDoesNotEquateStringAndNonStringTypes}} -->
The method `testEqualsDoesNotEquateStringAndNonStringTypes` verifies that `JsonPrimitive` objects created from strings are not considered equal to those created from non-string types, even if their content appears similar.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to check the equality of `JsonPrimitive` objects created from strings and non-string types.
    - It asserts that a `JsonPrimitive` created from the string "true" is not equal to one created from the boolean `true`.
    - It asserts that a `JsonPrimitive` created from the string "0" is not equal to one created from the integer `0`.
    - It asserts that a `JsonPrimitive` created from the string "NaN" is not equal to one created from the float `Float.NaN`.
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of the [`equals`](GsonTest.java.driver.md#DummyFactoryequals) method in `JsonPrimitive`.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testDeepCopy<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testDeepCopy}} -->
The `testDeepCopy` method verifies that the [`deepCopy`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementdeepCopy) method of a `JsonPrimitive` object returns the same instance, confirming the immutability of primitive JSON values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `a` initialized with the string value "a".
    - Use the `assertThat` method to check if `a` is the same instance as `a.deepCopy()`, which should be true since primitives are immutable.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the [`deepCopy`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementdeepCopy) method.
- **Functions called**:
    - [`com.google.gson.JsonElement.deepCopy`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementdeepCopy)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testBigDecimalEquals<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testBigDecimalEquals}} -->
The `testBigDecimalEquals` method tests the equality of `JsonPrimitive` objects created from different `BigDecimal` values to ensure they are not considered equal when they represent different numeric values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `small` initialized with the value `1.0`.
    - Create a `JsonPrimitive` object `large` initialized with the value `2.0`.
    - Assert that `small` is not equal to `large` using `assertThat(small.equals(large)).isFalse()`.
    - Create a `BigDecimal` object `doubleMax` initialized with the maximum value of a `Double`.
    - Create a `JsonPrimitive` object `smallDecimal` initialized with `doubleMax` plus `100.0`.
    - Create a `JsonPrimitive` object `largeDecimal` initialized with `doubleMax` plus `200.0`.
    - Assert that `smallDecimal` is not equal to `largeDecimal` using `assertThat(smallDecimal.equals(largeDecimal)).isFalse()`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the equality behavior of `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testBigDecimalEqualsZero<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testBigDecimalEqualsZero}} -->
The method `testBigDecimalEqualsZero` tests the equality of `JsonPrimitive` objects created with `BigDecimal` and `Double` representations of zero.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object with `BigDecimal` value '0.0' and another with '0.00', and assert that they are equal.
    - Create a `JsonPrimitive` object with `BigDecimal` value '0.00' and another with `Double` value '0.00', and assert that they are equal.
- **Output**:
    - The method does not return any value; it performs assertions to verify the equality of `JsonPrimitive` objects.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testBigDecimalEqualsTransitive<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testBigDecimalEqualsTransitive}} -->
The method `testBigDecimalEqualsTransitive` verifies the transitive property of the [`equals`](GsonTest.java.driver.md#DummyFactoryequals) method for `JsonPrimitive` objects created with `BigDecimal` and `double` values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object `x` initialized with a `BigDecimal` value of "0".
    - Create a `JsonPrimitive` object `y` initialized with a `double` value of 0.0.
    - Create a `JsonPrimitive` object `z` initialized with a `BigDecimal` value of "0.00".
    - Assert that `x.equals(y)` returns `true`.
    - Assert that `y.equals(z)` returns `true`.
    - Assert that `x.equals(z)` returns `true`, demonstrating the transitive property.
- **Output**:
    - The method does not return any value; it uses assertions to verify the transitive property of equality.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)


---
#### JsonPrimitiveTest\.testEqualsDoubleNaNAndBigDecimal<!-- {{#callable:com.google.gson.JsonPrimitiveTest.testEqualsDoubleNaNAndBigDecimal}} -->
The method `testEqualsDoubleNaNAndBigDecimal` tests the equality comparison between a `JsonPrimitive` containing `Double.NaN` and another containing a `BigDecimal` value of `1.0`, asserting that they are not equal.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonPrimitive` object with `Double.NaN`.
    - Create another `JsonPrimitive` object with a `BigDecimal` value of `1.0`.
    - Use the [`equals`](GsonTest.java.driver.md#DummyFactoryequals) method to compare the two `JsonPrimitive` objects.
    - Assert that the result of the comparison is `false` using `assertThat` from the `Truth` library.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior of the [`equals`](GsonTest.java.driver.md#DummyFactoryequals) method.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonPrimitiveTest`](#JsonPrimitiveTest)  (Base Class)



