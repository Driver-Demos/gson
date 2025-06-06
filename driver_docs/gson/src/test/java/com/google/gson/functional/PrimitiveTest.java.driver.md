# Purpose
The provided Java source code file is a comprehensive suite of functional tests for the Gson library, specifically focusing on the serialization and deserialization of primitive and numeric types. The file is part of the `com.google.gson.functional` package and utilizes the JUnit testing framework to validate the behavior of Gson when handling various data types, including integers, bytes, shorts, longs, floats, doubles, BigDecimal, and BigInteger. The tests cover a wide range of scenarios, such as autoboxing, handling of special floating-point values like NaN and Infinity, and the conversion of JSON strings to numeric types. Additionally, the tests ensure that Gson adheres to JSON specifications and handles edge cases, such as lossy conversions and invalid JSON structures, by expecting exceptions where appropriate.

The file defines a series of test methods annotated with `@Test`, each targeting specific functionality of the Gson library. The tests are organized to cover both serialization (converting Java objects to JSON) and deserialization (parsing JSON into Java objects) for each data type. The tests also explore the behavior of Gson when dealing with special cases, such as very large numbers, precision preservation in BigDecimal, and the use of custom serialization policies. The use of assertions, such as `assertThat` and `assertThrows`, ensures that the expected outcomes are met, providing a robust validation framework for Gson's handling of primitive and numeric types. This file serves as a critical component in ensuring the reliability and correctness of the Gson library's core functionalities.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.LongSerializationPolicy`
- `com.google.gson.internal.LazilyParsedNumber`
- `com.google.gson.reflect.TypeToken`
- `java.io.Serializable`
- `java.io.StringReader`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `java.util.Arrays`
- `java.util.List`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### PrimitiveTest<!-- {{#class:com.google.gson.functional.PrimitiveTest}} -->
- **Modifiers**: `public`
- **Description**: The `PrimitiveTest` class is a comprehensive suite of unit tests designed to validate the serialization and deserialization of primitive data types and their wrapper classes using the Gson library. It covers a wide range of scenarios, including handling of integers, floating-point numbers, and special cases like NaN and Infinity, ensuring that the Gson library correctly processes these values according to JSON specifications. The class also tests the behavior of Gson with large numbers, arrays, and special serialization policies, providing a robust validation framework for JSON processing in Java applications.
- **Fields**:
    - `gson`: `Gson` An instance of the Gson class used for JSON serialization and deserialization in the tests.
- **Methods**:
    - [`com.google.gson.functional.PrimitiveTest.setUp`](#PrimitiveTestsetUp)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveIntegerAutoboxedSerialization`](#PrimitiveTesttestPrimitiveIntegerAutoboxedSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveIntegerAutoboxedDeserialization`](#PrimitiveTesttestPrimitiveIntegerAutoboxedDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testByteSerialization`](#PrimitiveTesttestByteSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testByteDeserialization`](#PrimitiveTesttestByteDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testByteDeserializationLossy`](#PrimitiveTesttestByteDeserializationLossy)
    - [`com.google.gson.functional.PrimitiveTest.testShortSerialization`](#PrimitiveTesttestShortSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testShortDeserialization`](#PrimitiveTesttestShortDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testShortDeserializationLossy`](#PrimitiveTesttestShortDeserializationLossy)
    - [`com.google.gson.functional.PrimitiveTest.testIntSerialization`](#PrimitiveTesttestIntSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testLongSerialization`](#PrimitiveTesttestLongSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testFloatSerialization`](#PrimitiveTesttestFloatSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleSerialization`](#PrimitiveTesttestDoubleSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveIntegerAutoboxedInASingleElementArraySerialization`](#PrimitiveTesttestPrimitiveIntegerAutoboxedInASingleElementArraySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testReallyLongValuesSerialization`](#PrimitiveTesttestReallyLongValuesSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testReallyLongValuesDeserialization`](#PrimitiveTesttestReallyLongValuesDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveLongAutoboxedSerialization`](#PrimitiveTesttestPrimitiveLongAutoboxedSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveLongAutoboxedDeserialization`](#PrimitiveTesttestPrimitiveLongAutoboxedDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveLongAutoboxedInASingleElementArraySerialization`](#PrimitiveTesttestPrimitiveLongAutoboxedInASingleElementArraySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveBooleanAutoboxedSerialization`](#PrimitiveTesttestPrimitiveBooleanAutoboxedSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testBooleanDeserialization`](#PrimitiveTesttestBooleanDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveBooleanAutoboxedInASingleElementArraySerialization`](#PrimitiveTesttestPrimitiveBooleanAutoboxedInASingleElementArraySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testNumberSerialization`](#PrimitiveTesttestNumberSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testNumberDeserialization`](#PrimitiveTesttestNumberDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testNumberAsStringDeserialization`](#PrimitiveTesttestNumberAsStringDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveDoubleAutoboxedSerialization`](#PrimitiveTesttestPrimitiveDoubleAutoboxedSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveDoubleAutoboxedDeserialization`](#PrimitiveTesttestPrimitiveDoubleAutoboxedDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveDoubleAutoboxedInASingleElementArraySerialization`](#PrimitiveTesttestPrimitiveDoubleAutoboxedInASingleElementArraySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleAsStringRepresentationDeserialization`](#PrimitiveTesttestDoubleAsStringRepresentationDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleNoFractAsStringRepresentationDeserialization`](#PrimitiveTesttestDoubleNoFractAsStringRepresentationDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleArrayDeserialization`](#PrimitiveTesttestDoubleArrayDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testLargeDoubleDeserialization`](#PrimitiveTesttestLargeDoubleDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalSerialization`](#PrimitiveTesttestBigDecimalSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalDeserialization`](#PrimitiveTesttestBigDecimalDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalInASingleElementArraySerialization`](#PrimitiveTesttestBigDecimalInASingleElementArraySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testSmallValueForBigDecimalSerialization`](#PrimitiveTesttestSmallValueForBigDecimalSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testSmallValueForBigDecimalDeserialization`](#PrimitiveTesttestSmallValueForBigDecimalDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalPreservePrecisionSerialization`](#PrimitiveTesttestBigDecimalPreservePrecisionSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalPreservePrecisionDeserialization`](#PrimitiveTesttestBigDecimalPreservePrecisionDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalAsStringRepresentationDeserialization`](#PrimitiveTesttestBigDecimalAsStringRepresentationDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalNoFractAsStringRepresentationDeserialization`](#PrimitiveTesttestBigDecimalNoFractAsStringRepresentationDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigIntegerSerialization`](#PrimitiveTesttestBigIntegerSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigIntegerDeserialization`](#PrimitiveTesttestBigIntegerDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigIntegerInASingleElementArraySerialization`](#PrimitiveTesttestBigIntegerInASingleElementArraySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testSmallValueForBigIntegerSerialization`](#PrimitiveTesttestSmallValueForBigIntegerSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testSmallValueForBigIntegerDeserialization`](#PrimitiveTesttestSmallValueForBigIntegerDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBadValueForBigIntegerDeserialization`](#PrimitiveTesttestBadValueForBigIntegerDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testLazilyParsedNumberSerialization`](#PrimitiveTesttestLazilyParsedNumberSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testLazilyParsedNumberDeserialization`](#PrimitiveTesttestLazilyParsedNumberDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testMoreSpecificSerialization`](#PrimitiveTesttestMoreSpecificSerialization)
    - [`com.google.gson.functional.PrimitiveTest.extractElementFromArray`](#PrimitiveTestextractElementFromArray)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleNaNSerializationNotSupportedByDefault`](#PrimitiveTesttestDoubleNaNSerializationNotSupportedByDefault)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleNaNSerialization`](#PrimitiveTesttestDoubleNaNSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleNaNDeserialization`](#PrimitiveTesttestDoubleNaNDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testFloatNaNSerializationNotSupportedByDefault`](#PrimitiveTesttestFloatNaNSerializationNotSupportedByDefault)
    - [`com.google.gson.functional.PrimitiveTest.testFloatNaNSerialization`](#PrimitiveTesttestFloatNaNSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testFloatNaNDeserialization`](#PrimitiveTesttestFloatNaNDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalNaNDeserializationNotSupported`](#PrimitiveTesttestBigDecimalNaNDeserializationNotSupported)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleInfinitySerializationNotSupportedByDefault`](#PrimitiveTesttestDoubleInfinitySerializationNotSupportedByDefault)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleInfinitySerialization`](#PrimitiveTesttestDoubleInfinitySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testDoubleInfinityDeserialization`](#PrimitiveTesttestDoubleInfinityDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testFloatInfinitySerializationNotSupportedByDefault`](#PrimitiveTesttestFloatInfinitySerializationNotSupportedByDefault)
    - [`com.google.gson.functional.PrimitiveTest.testFloatInfinitySerialization`](#PrimitiveTesttestFloatInfinitySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testFloatInfinityDeserialization`](#PrimitiveTesttestFloatInfinityDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalInfinityDeserializationNotSupported`](#PrimitiveTesttestBigDecimalInfinityDeserializationNotSupported)
    - [`com.google.gson.functional.PrimitiveTest.testNegativeInfinitySerializationNotSupportedByDefault`](#PrimitiveTesttestNegativeInfinitySerializationNotSupportedByDefault)
    - [`com.google.gson.functional.PrimitiveTest.testNegativeInfinitySerialization`](#PrimitiveTesttestNegativeInfinitySerialization)
    - [`com.google.gson.functional.PrimitiveTest.testNegativeInfinityDeserialization`](#PrimitiveTesttestNegativeInfinityDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testNegativeInfinityFloatSerializationNotSupportedByDefault`](#PrimitiveTesttestNegativeInfinityFloatSerializationNotSupportedByDefault)
    - [`com.google.gson.functional.PrimitiveTest.testNegativeInfinityFloatSerialization`](#PrimitiveTesttestNegativeInfinityFloatSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testNegativeInfinityFloatDeserialization`](#PrimitiveTesttestNegativeInfinityFloatDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testBigDecimalNegativeInfinityDeserializationNotSupported`](#PrimitiveTesttestBigDecimalNegativeInfinityDeserializationNotSupported)
    - [`com.google.gson.functional.PrimitiveTest.testLongAsStringSerialization`](#PrimitiveTesttestLongAsStringSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testLongAsStringDeserialization`](#PrimitiveTesttestLongAsStringDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testQuotedStringSerializationAndDeserialization`](#PrimitiveTesttestQuotedStringSerializationAndDeserialization)
    - [`com.google.gson.functional.PrimitiveTest.testUnquotedStringDeserializationFails`](#PrimitiveTesttestUnquotedStringDeserializationFails)
    - [`com.google.gson.functional.PrimitiveTest.testHtmlCharacterSerialization`](#PrimitiveTesttestHtmlCharacterSerialization)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializePrimitiveWrapperAsObjectField`](#PrimitiveTesttestDeserializePrimitiveWrapperAsObjectField)
    - [`com.google.gson.functional.PrimitiveTest.testPrimitiveClassLiteral`](#PrimitiveTesttestPrimitiveClassLiteral)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsLongPrimitive`](#PrimitiveTesttestDeserializeJsonObjectAsLongPrimitive)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsLongWrapper`](#PrimitiveTesttestDeserializeJsonArrayAsLongWrapper)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsInt`](#PrimitiveTesttestDeserializeJsonArrayAsInt)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsInteger`](#PrimitiveTesttestDeserializeJsonObjectAsInteger)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsShortPrimitive`](#PrimitiveTesttestDeserializeJsonObjectAsShortPrimitive)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsShortWrapper`](#PrimitiveTesttestDeserializeJsonArrayAsShortWrapper)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsDoublePrimitive`](#PrimitiveTesttestDeserializeJsonArrayAsDoublePrimitive)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsDoubleWrapper`](#PrimitiveTesttestDeserializeJsonObjectAsDoubleWrapper)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsFloatPrimitive`](#PrimitiveTesttestDeserializeJsonObjectAsFloatPrimitive)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsFloatWrapper`](#PrimitiveTesttestDeserializeJsonArrayAsFloatWrapper)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBytePrimitive`](#PrimitiveTesttestDeserializeJsonObjectAsBytePrimitive)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsByteWrapper`](#PrimitiveTesttestDeserializeJsonArrayAsByteWrapper)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBooleanPrimitive`](#PrimitiveTesttestDeserializeJsonObjectAsBooleanPrimitive)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsBooleanWrapper`](#PrimitiveTesttestDeserializeJsonArrayAsBooleanWrapper)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsBigDecimal`](#PrimitiveTesttestDeserializeJsonArrayAsBigDecimal)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBigDecimal`](#PrimitiveTesttestDeserializeJsonObjectAsBigDecimal)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsBigInteger`](#PrimitiveTesttestDeserializeJsonArrayAsBigInteger)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBigInteger`](#PrimitiveTesttestDeserializeJsonObjectAsBigInteger)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsNumber`](#PrimitiveTesttestDeserializeJsonArrayAsNumber)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsNumber`](#PrimitiveTesttestDeserializeJsonObjectAsNumber)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializingDecimalPointValueZeroSucceeds`](#PrimitiveTesttestDeserializingDecimalPointValueZeroSucceeds)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializingNonZeroDecimalPointValuesAsIntegerFails`](#PrimitiveTesttestDeserializingNonZeroDecimalPointValuesAsIntegerFails)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializingBigDecimalAsIntegerFails`](#PrimitiveTesttestDeserializingBigDecimalAsIntegerFails)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializingBigIntegerAsInteger`](#PrimitiveTesttestDeserializingBigIntegerAsInteger)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializingBigIntegerAsLong`](#PrimitiveTesttestDeserializingBigIntegerAsLong)
    - [`com.google.gson.functional.PrimitiveTest.testValueVeryCloseToZeroIsZero`](#PrimitiveTesttestValueVeryCloseToZeroIsZero)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializingBigDecimalAsBigIntegerFails`](#PrimitiveTesttestDeserializingBigDecimalAsBigIntegerFails)
    - [`com.google.gson.functional.PrimitiveTest.testDeserializingBigIntegerAsBigDecimal`](#PrimitiveTesttestDeserializingBigIntegerAsBigDecimal)
    - [`com.google.gson.functional.PrimitiveTest.testStringsAsBooleans`](#PrimitiveTesttestStringsAsBooleans)

**Methods**

---
#### PrimitiveTest\.setUp<!-- {{#callable:com.google.gson.functional.PrimitiveTest.setUp}} -->
Initializes a `Gson` instance for use in tests.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with `@Before`, indicating it should run before each test method in the class.
    - A new instance of `Gson` is created and assigned to the class variable `gson`.
- **Output**:
    - This method does not return any value; it sets up the `gson` instance for use in subsequent tests.
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveIntegerAutoboxedSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveIntegerAutoboxedSerialization}} -->
Tests the serialization of a primitive integer to JSON.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - The method uses the `gson` instance to convert the integer `1` to its JSON representation.
    - It then asserts that the resulting JSON string is equal to the string '1'.
- **Output**:
    - The method does not return any value; it asserts that the JSON output is as expected.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveIntegerAutoboxedDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveIntegerAutoboxedDeserialization}} -->
Tests the deserialization of a JSON string into both primitive and boxed `Integer` types.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
    - `expected`: An integer value expected to be the result of the deserialization.
    - `actual`: An integer variable that stores the result of deserialization from JSON.
- **Control Flow**:
    - The method initializes an `expected` integer variable with the value 1.
    - It then deserializes the string '1' into a primitive `int` and checks if it equals `expected` using an assertion.
    - Next, it deserializes the same string '1' into an `Integer` object and again checks if it equals `expected` using an assertion.
- **Output**:
    - The method does not return a value; it asserts that the deserialized values match the expected integer.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testByteSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testByteSerialization}} -->
Tests the serialization of `byte` and `Byte` types using the Gson library.
- **Inputs**:
    - `1`: An integer value to be serialized as a byte.
    - `Byte.MIN_VALUE`: The minimum value of the `Byte` type.
    - `Byte.MAX_VALUE`: The maximum value of the `Byte` type.
    - `128`: An integer that exceeds the maximum value of a byte, testing narrowing conversion.
    - `1.5`: A floating-point number that should be converted to a byte.
- **Control Flow**:
    - The method uses assertions to verify that the output of `gson.toJson()` matches expected string representations for various byte values.
    - It checks both primitive `byte` and wrapper `Byte` types.
    - It tests edge cases such as the minimum and maximum byte values, as well as values that require narrowing conversion.
- **Output**:
    - The method does not return a value but asserts that the JSON representation of the byte values is correct.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testByteDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testByteDeserialization}} -->
Tests the deserialization of byte values from JSON using Gson.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
- **Control Flow**:
    - Deserializes a JSON string representing a single byte value into a `Byte` object and asserts that it equals 1.
    - Deserializes the same JSON string into a primitive `byte` and asserts that it equals 1.
    - Deserializes a JSON array string representing multiple byte values into a `byte[]` and asserts that the resulting array matches the expected byte values.
- **Output**:
    - The method does not return a value; it asserts the correctness of the deserialized values.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testByteDeserializationLossy<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testByteDeserializationLossy}} -->
Tests the deserialization of byte values from JSON strings, ensuring that lossy conversions and out-of-range values throw appropriate exceptions.
- **Inputs**: None
- **Control Flow**:
    - The method begins by asserting that deserializing the string '-129' into a `byte` throws a `JsonSyntaxException` with a specific error message indicating a lossy conversion.
    - Next, it checks that deserializing the string '256' also throws a `JsonSyntaxException` with a similar message for lossy conversion.
    - Finally, it asserts that deserializing the string '2147483648' throws a `JsonSyntaxException` with a message indicating a `NumberFormatException` due to the value being too large.
- **Output**:
    - The method does not return a value; instead, it verifies that specific exceptions are thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testShortSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testShortSerialization}} -->
Tests the serialization of `short` values using Gson.
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify the output of the `gson.toJson()` method for various `short` values.
    - It checks both primitive `short` and `Short` wrapper class serialization.
    - The method tests serialization of minimum and maximum values of `Short`.
    - It verifies widening conversion from `byte` to `short` and narrowing conversion from `int` to `short`.
    - It also checks the serialization of a floating-point number to `short`.
- **Output**:
    - The method does not return a value but asserts that the JSON output matches expected string representations of the serialized `short` values.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testShortDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testShortDeserialization}} -->
Tests the deserialization of `Short` and `short` types from JSON.
- **Inputs**: None
- **Control Flow**:
    - Deserializes a JSON string representing a number into a `Short` object and asserts that it equals 1.
    - Deserializes the same JSON string into a primitive `short` and asserts that it equals 1.
    - Deserializes a JSON array string into an array of `short` values and asserts that the resulting array matches the expected values.
- **Output**:
    - The method does not return a value; it performs assertions to verify the correctness of deserialization.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testShortDeserializationLossy<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testShortDeserializationLossy}} -->
Tests the deserialization of short values from JSON strings, ensuring that lossy conversions and out-of-range values throw appropriate exceptions.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
    - `JsonSyntaxException`: An exception thrown when the JSON syntax is invalid or when a value cannot be converted to the specified type.
- **Control Flow**:
    - The method begins by asserting that deserializing the string '-32769' into a `short` throws a `JsonSyntaxException`.
    - It checks that the exception message indicates a lossy conversion from -32769 to short.
    - Next, it asserts that deserializing the string '65536' into a `short` also throws a `JsonSyntaxException` with a similar message.
    - Finally, it verifies that deserializing '2147483648' throws a `JsonSyntaxException` with a message indicating that an int was expected but a larger value was provided.
- **Output**:
    - The method does not return a value; instead, it verifies that specific exceptions are thrown for invalid deserialization attempts.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testIntSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testIntSerialization}} -->
Tests the serialization of various integer types using Gson.
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify that the `gson.toJson()` method correctly serializes different integer values.
    - It checks both primitive `int` and `Integer` class types.
    - The method tests serialization of minimum and maximum integer values.
    - It verifies widening conversion from `byte` to `Integer` and narrowing conversion from `long` to `Integer`.
    - It also checks the serialization of a floating-point number to an integer.
- **Output**:
    - The method does not return a value; it asserts that the output of the serialization matches the expected string representation.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testLongSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testLongSerialization}} -->
Tests the serialization of `long` values using Gson.
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify the output of the `gson.toJson()` method for various `long` values.
    - It checks both primitive `long` and wrapper `Long` types.
    - It tests the serialization of minimum and maximum `long` values.
    - It verifies widening conversion from `byte` to `long` and narrowing conversion from `double` to `long`.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `long` values matches the expected string output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testFloatSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testFloatSerialization}} -->
Tests the serialization of various float values using Gson.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify the output of the `gson.toJson` method for different float values.
    - It checks serialization for both primitive `float` and `Float` wrapper types.
    - It tests the serialization of minimum and maximum float values.
    - It verifies widening conversion from `byte` to `float` and checks for lossy conversion from `long` to `float`.
    - It also tests the serialization of `Double.MAX_VALUE` to ensure it returns 'Infinity' when special floating point values are serialized.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON strings match expected values.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleSerialization}} -->
Tests the serialization of `double` values using Gson.
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify the output of the `gson.toJson()` method for various `double` values.
    - It checks both primitive `double` and `Double` object types.
    - It tests the serialization of special values like `Double.MIN_VALUE` and `Double.MAX_VALUE`.
    - It verifies widening conversions from `byte` to `double` and checks for lossy conversions from `long` to `double`.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `double` values matches the expected string output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveIntegerAutoboxedInASingleElementArraySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveIntegerAutoboxedInASingleElementArraySerialization}} -->
Tests the serialization of a single-element array of primitive integers.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - An integer array `target` is initialized with a single element -9332.
    - The method `gson.toJson` is called three times to serialize the `target` array into JSON format.
    - The first call checks the JSON output for the primitive int array.
    - The second call checks the JSON output for the int array type.
    - The third call checks the JSON output for the Integer array type.
- **Output**:
    - The method asserts that the JSON representation of the array is equal to '[-9332]' for all three serialization cases.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testReallyLongValuesSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testReallyLongValuesSerialization}} -->
Tests the serialization of a long value to its JSON representation.
- **Inputs**: None
- **Control Flow**:
    - A long variable `value` is initialized with the value 333961828784581L.
    - The method `gson.toJson(value)` is called to convert the long value to its JSON string representation.
    - The result is then compared to the expected string "333961828784581" using an assertion.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the long value is correct.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testReallyLongValuesDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testReallyLongValuesDeserialization}} -->
Tests the deserialization of a long value from a JSON string.
- **Inputs**:
    - `json`: A JSON string representing a long value, in this case, '333961828784581'.
- **Control Flow**:
    - The method begins by defining a JSON string that contains a long value.
    - It then uses the `gson.fromJson` method to convert the JSON string into a `long` type.
    - Finally, it asserts that the deserialized value is equal to the expected long value using `assertThat`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized long value matches the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveLongAutoboxedSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveLongAutoboxedSerialization}} -->
Tests the serialization of primitive long and its wrapper Long using Gson.
- **Inputs**:
    - `1L`: A primitive long value to be serialized.
    - `long.class`: The class type of the primitive long.
    - `Long.class`: The class type of the Long wrapper.
- **Control Flow**:
    - The method calls `gson.toJson` to serialize the primitive long value `1L` as a primitive type and as a wrapper type.
    - It asserts that the serialized output for both cases is equal to the string '1'.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON representation of the long value is correct.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveLongAutoboxedDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveLongAutoboxedDeserialization}} -->
Tests the deserialization of a JSON string into both primitive and wrapper `long` types.
- **Inputs**:
    - `json`: A JSON string representing a numeric value, specifically '1'.
    - `type`: The class type to deserialize into, either `long.class` for primitive or `Long.class` for wrapper.
- **Control Flow**:
    - The method initializes an expected value of `1L`.
    - It calls `gson.fromJson` to deserialize the string '1' into a primitive `long` and asserts that the result equals the expected value.
    - It then calls `gson.fromJson` again to deserialize the same string into a `Long` object and asserts that the result also equals the expected value.
- **Output**:
    - The method does not return a value; it asserts that the deserialized values match the expected long value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveLongAutoboxedInASingleElementArraySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveLongAutoboxedInASingleElementArraySerialization}} -->
Tests the serialization of a single-element array of primitive long values.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A single-element array of long is created with the value -23.
    - The `gson.toJson` method is called three times to serialize the array into JSON format.
    - The first call checks the serialization of the primitive long array.
    - The second call checks the serialization of the long array type.
    - The third call checks the serialization of the boxed Long array type.
- **Output**:
    - The method asserts that the JSON representation of the array is equal to '[-23]' for all three serialization cases.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveBooleanAutoboxedSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveBooleanAutoboxedSerialization}} -->
Tests the serialization of primitive boolean values to JSON.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThat` to verify the output of the `gson.toJson` method for the boolean value `true`.
    - It checks that the JSON representation of `true` is equal to the string "true".
    - Similarly, it verifies that the JSON representation of the boolean value `false` is equal to the string "false".
- **Output**:
    - The method does not return a value; it asserts that the JSON output matches the expected string representations of the boolean values.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBooleanDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBooleanDeserialization}} -->
Tests the deserialization of boolean values from JSON strings.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Deserializes the string 'false' into a boolean and asserts that the value is false.
    - Deserializes the string 'true' into a boolean and asserts that the value is true.
- **Output**:
    - The method does not return a value; it asserts the correctness of the deserialized boolean values.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveBooleanAutoboxedInASingleElementArraySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveBooleanAutoboxedInASingleElementArraySerialization}} -->
Tests the serialization of a single-element boolean array using Gson.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A boolean array `target` is initialized with a single element `false`.
    - The method asserts that the JSON representation of `target` is equal to the string '[false]'.
    - The method asserts that the JSON representation of `target` when explicitly typed as `boolean[].class` is also equal to '[false]'.
    - The method asserts that the JSON representation of `target` when typed as `Boolean[].class` is equal to '[false]'.
- **Output**:
    - The method does not return a value; it performs assertions to verify the correctness of the JSON serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNumberSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNumberSerialization}} -->
Tests the serialization of a `Number` object to JSON using Gson.
- **Inputs**: None
- **Control Flow**:
    - Creates a `Number` object `expected` initialized to 1L.
    - Serializes `expected` to JSON using `gson.toJson(expected)` and stores the result in `json`.
    - Asserts that the serialized JSON string `json` is equal to the string representation of `expected`.
    - Serializes `expected` again, explicitly specifying `Number.class`, and stores the result in `json`.
    - Asserts that the serialized JSON string `json` is still equal to the string representation of `expected`.
- **Output**:
    - The method does not return a value; it performs assertions to verify that the JSON serialization of the `Number` object matches its expected string representation.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNumberDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNumberDeserialization}} -->
Tests the deserialization of various numeric formats into `Number` objects using Gson.
- **Inputs**:
    - `json`: A string representation of a number in JSON format.
- **Control Flow**:
    - The method begins by initializing a string `json` with the value '1' and expects it to be deserialized into an `Integer`.
    - It then uses `gson.fromJson` to convert the `json` string into a `Number` object and asserts that the integer value of the actual result matches the expected value.
    - Next, it updates `json` to the string representation of `Long.MAX_VALUE`, deserializes it, and asserts that the long value of the actual result matches the expected value.
    - Finally, it sets `json` to '1.0', deserializes it, and asserts that the long value of the actual result equals 1.
- **Output**:
    - The method does not return a value but asserts that the deserialized `Number` objects match the expected values for various numeric formats.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.internal.LazilyParsedNumber.intValue`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberintValue)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNumberAsStringDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNumberAsStringDeserialization}} -->
Tests the deserialization of a JSON string representing a number into a `Number` object.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
    - `"18"`: A JSON string representation of the number 18.
- **Control Flow**:
    - The method calls `gson.fromJson` to convert the JSON string into a `Number` object.
    - It then asserts that the integer value of the deserialized `Number` is equal to 18.
- **Output**:
    - The method does not return a value; it asserts that the deserialized number is equal to 18.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.internal.LazilyParsedNumber.intValue`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberintValue)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveDoubleAutoboxedSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveDoubleAutoboxedSerialization}} -->
Tests the serialization of primitive double values using Gson.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThat` to verify the output of `gson.toJson` for two specific double values.
    - It checks that the JSON representation of -122.08234335D is equal to the string "-122.08234335".
    - It checks that the JSON representation of 122.08112002D is equal to the string "122.08112002".
- **Output**:
    - The method does not return a value; it asserts that the JSON output matches the expected string representations of the double values.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveDoubleAutoboxedDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveDoubleAutoboxedDeserialization}} -->
Tests the deserialization of primitive and autoboxed double values from JSON.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Deserializes a JSON string representing a negative double value into a primitive `double` type.
    - Asserts that the deserialized value equals the expected negative double value.
    - Deserializes a JSON string representing a positive double value into a `Double` object type.
    - Asserts that the deserialized value equals the expected positive double value.
- **Output**:
    - The method does not return a value; it asserts the correctness of the deserialized double values.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveDoubleAutoboxedInASingleElementArraySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveDoubleAutoboxedInASingleElementArraySerialization}} -->
Tests the serialization of a single-element array of primitive doubles.
- **Inputs**:
    - `target`: A single-element array of primitive doubles containing the value -122.08.
- **Control Flow**:
    - The method first serializes the `target` array using `gson.toJson()` and checks if the output matches the expected JSON string representation of the array.
    - It then serializes the `target` array explicitly as a `double[]` and checks if the output matches the expected JSON string.
    - Finally, it serializes the `target` array as a `Double[]` (the wrapper type) and verifies that the output is still correct.
- **Output**:
    - The method does not return a value but asserts that the serialized JSON strings match the expected output for each serialization case.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleAsStringRepresentationDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleAsStringRepresentationDeserialization}} -->
Tests the deserialization of a double value represented as a string.
- **Inputs**:
    - `doubleValue`: A string representation of a double value in scientific notation.
- **Control Flow**:
    - The method initializes a string `doubleValue` with the value '1.0043E+5'.
    - It then converts this string to a `Double` object using `Double.valueOf(doubleValue)` and stores it in `expected`.
    - Next, it deserializes the string `doubleValue` into a `Double` object using `gson.fromJson(doubleValue, Double.class)` and stores the result in `actual`.
    - An assertion checks if `actual` is equal to `expected`.
    - The method then deserializes `doubleValue` into a primitive `double` using `gson.fromJson(doubleValue, double.class)` and stores the result in `actual1`.
    - Another assertion checks if `actual1` is equal to `expected`.
- **Output**:
    - The method does not return a value but asserts that the deserialized values match the expected double value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleNoFractAsStringRepresentationDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleNoFractAsStringRepresentationDeserialization}} -->
Tests the deserialization of a double value represented as a string without a fractional part.
- **Inputs**:
    - `doubleValue`: A string representation of a double value in scientific notation, e.g., '1E+5'.
- **Control Flow**:
    - The method initializes a string variable `doubleValue` with the value '1E+5'.
    - It then converts this string to a `Double` object using `Double.valueOf(doubleValue)` and stores it in `expected`.
    - The method uses `gson.fromJson(doubleValue, Double.class)` to deserialize the string into a `Double` object and stores it in `actual`.
    - An assertion checks if `actual` is equal to `expected`.
    - The method also deserializes the string into a primitive `double` using `gson.fromJson(doubleValue, double.class)` and stores it in `actual1`.
    - Another assertion checks if `actual1` is equal to `expected`.
- **Output**:
    - The method does not return a value but asserts that the deserialized values match the expected double value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleArrayDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleArrayDeserialization}} -->
Tests the deserialization of a JSON array of doubles into a Java double array.
- **Inputs**:
    - `json`: A string representing a JSON array of double values.
- **Control Flow**:
    - The method initializes a JSON string containing six double values.
    - It uses the `gson.fromJson` method to deserialize the JSON string into a double array.
    - Assertions are made to verify the length of the resulting array and the values at each index.
- **Output**:
    - The method does not return a value; it asserts that the deserialized double array has the expected length and values.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testLargeDoubleDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testLargeDoubleDeserialization}} -->
Tests the deserialization of a large double value from a JSON string.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `doubleValue`: A string representation of a large double value in scientific notation.
- **Control Flow**:
    - The method initializes a string `doubleValue` with a large double value in scientific notation.
    - It then converts this string to a `Double` object using `gson.fromJson` and stores it in `actual`.
    - The expected value is also computed by converting the string to a `Double` using `Double.valueOf`.
    - The method asserts that the deserialized `actual` value is equal to the `expected` value.
    - Next, it deserializes the same string into a primitive `double` and stores it in `actual1`.
    - Finally, it asserts that `actual1` is also equal to the `expected` value.
- **Output**:
    - The method does not return a value; it performs assertions to verify that the deserialized values match the expected double value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalSerialization}} -->
Tests the serialization and deserialization of a `BigDecimal` object using Gson.
- **Inputs**: None
- **Control Flow**:
    - A `BigDecimal` object is created with the value '-122.0e-21'.
    - The `BigDecimal` object is serialized to a JSON string using `gson.toJson()`.
    - The JSON string is then deserialized back into a `BigDecimal` object.
    - An assertion is made to check if the deserialized `BigDecimal` is equal to the original `BigDecimal`.
- **Output**:
    - The method does not return a value but asserts that the original and deserialized `BigDecimal` objects are equal.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalDeserialization}} -->
Tests the deserialization of a JSON string into a `BigDecimal` object.
- **Inputs**:
    - `json`: A JSON string representation of a `BigDecimal`, specifically '-122.0e-21'.
- **Control Flow**:
    - Creates a `BigDecimal` object `target` initialized with the value '-122.0e-21'.
    - Deserializes the JSON string `json` into a `BigDecimal` using the `gson.fromJson` method.
    - Asserts that the deserialized `BigDecimal` is equal to the `target` using `assertThat`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigDecimal` matches the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalInASingleElementArraySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalInASingleElementArraySerialization}} -->
Tests the serialization and deserialization of a `BigDecimal` in a single-element array.
- **Modifiers**: `public`, `Test`
- **Inputs**:
    - `target`: An array of `BigDecimal` containing a single element, specifically `new BigDecimal("-122.08e-21")`.
- **Control Flow**:
    - The method first serializes the `target` array to JSON format using `gson.toJson()`.
    - It then extracts the single element from the resulting JSON string using the `extractElementFromArray()` method.
    - The extracted string is converted back to a `BigDecimal` and compared to the original element in the `target` array using an assertion.
    - The method repeats the serialization process, explicitly specifying the type `BigDecimal[].class`, and performs the same extraction and assertion.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigDecimal` matches the original value.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.PrimitiveTest.extractElementFromArray`](#PrimitiveTestextractElementFromArray)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testSmallValueForBigDecimalSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testSmallValueForBigDecimalSerialization}} -->
Tests the serialization of a small `BigDecimal` value.
- **Inputs**:
    - `target`: A `BigDecimal` object initialized with the value '1.55'.
- **Control Flow**:
    - Creates a `BigDecimal` instance with the value '1.55'.
    - Serializes the `BigDecimal` instance to JSON using `gson.toJson()`.
    - Asserts that the serialized JSON string is equal to the string representation of the `BigDecimal`.
- **Output**:
    - The method does not return a value; it asserts that the serialized output matches the expected string representation of the `BigDecimal`.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testSmallValueForBigDecimalDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testSmallValueForBigDecimalDeserialization}} -->
Tests the deserialization of a small `BigDecimal` value from a JSON string.
- **Inputs**: None
- **Control Flow**:
    - Creates an expected `BigDecimal` object with the value '1.55'.
    - Deserializes the JSON string '1.55' into a `BigDecimal` object using `gson.fromJson`.
    - Asserts that the deserialized `BigDecimal` is equal to the expected value using `assertThat`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized value matches the expected `BigDecimal`.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalPreservePrecisionSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalPreservePrecisionSerialization}} -->
Tests the serialization of a `BigDecimal` to ensure that precision is preserved.
- **Inputs**:
    - `expectedValue`: A string representation of the expected value after serialization, set to '1.000'.
    - `obj`: A `BigDecimal` object created from the expected value.
    - `actualValue`: The JSON string representation of the `BigDecimal` object obtained through serialization.
- **Control Flow**:
    - A `BigDecimal` object is created from the string '1.000'.
    - The `BigDecimal` object is serialized to JSON using `gson.toJson()`.
    - The serialized JSON string is compared to the expected string '1.000' using an assertion.
- **Output**:
    - The method does not return a value but asserts that the serialized output matches the expected string representation.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalPreservePrecisionDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalPreservePrecisionDeserialization}} -->
Tests the deserialization of a `BigDecimal` from a JSON string while preserving its precision.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `json`: A JSON string representation of a `BigDecimal`, specifically '1.000'.
- **Control Flow**:
    - A `BigDecimal` object is created from the input JSON string to establish the expected value.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `BigDecimal` object.
    - An assertion is made to check if the deserialized `BigDecimal` matches the expected value.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigDecimal` is equal to the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalAsStringRepresentationDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalAsStringRepresentationDeserialization}} -->
Tests the deserialization of a `BigDecimal` from its string representation.
- **Inputs**:
    - `doubleValue`: A string representation of a `BigDecimal`, in this case '0.05E+5'.
- **Control Flow**:
    - A `BigDecimal` object is created using the string representation provided in `doubleValue`.
    - The `gson.fromJson` method is called to deserialize the string into a `BigDecimal` object.
    - An assertion is made to check if the deserialized `BigDecimal` matches the expected value.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigDecimal` is equal to the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalNoFractAsStringRepresentationDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalNoFractAsStringRepresentationDeserialization}} -->
Tests the deserialization of a `BigDecimal` from a string representation without a fractional part.
- **Inputs**:
    - `doubleValue`: A string representation of a `BigDecimal` in scientific notation, specifically without a fractional part.
- **Control Flow**:
    - A `BigDecimal` object is created from the string representation `doubleValue`.
    - The `gson.fromJson` method is called to deserialize the same string into a `BigDecimal` object.
    - An assertion is made to check if the deserialized `BigDecimal` matches the expected value.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigDecimal` is equal to the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigIntegerSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigIntegerSerialization}} -->
Tests the serialization of a `BigInteger` object to its JSON representation.
- **Inputs**:
    - `target`: A `BigInteger` instance initialized with a large integer value.
- **Control Flow**:
    - Creates a `BigInteger` object with a specific large value.
    - Serializes the `BigInteger` object to JSON using the `gson` instance.
    - Asserts that the serialized JSON string is equal to the string representation of the `BigInteger`.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `BigInteger` matches its string representation.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigIntegerDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigIntegerDeserialization}} -->
Tests the deserialization of a `BigInteger` from a JSON string.
- **Inputs**:
    - `json`: A string representation of a large integer in JSON format.
- **Control Flow**:
    - A `BigInteger` object is created from the input JSON string.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `BigInteger`.
    - An assertion is made to check if the deserialized `BigInteger` is equal to the original `BigInteger`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigInteger` matches the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigIntegerInASingleElementArraySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigIntegerInASingleElementArraySerialization}} -->
Tests the serialization and deserialization of a `BigInteger` in a single-element array.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a single-element array of `BigInteger` containing a large number.
    - Serializes the array to JSON using `gson.toJson()` and extracts the element from the resulting JSON string.
    - Asserts that the deserialized `BigInteger` from the JSON matches the original value.
    - Repeats the serialization and extraction process using the specific type `BigInteger[].class`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized value matches the original `BigInteger`.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.PrimitiveTest.extractElementFromArray`](#PrimitiveTestextractElementFromArray)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testSmallValueForBigIntegerSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testSmallValueForBigIntegerSerialization}} -->
Tests the serialization of a small `BigInteger` value.
- **Inputs**: None
- **Control Flow**:
    - A `BigInteger` object is created with the value '15'.
    - The `gson.toJson()` method is called to serialize the `BigInteger` to a JSON string.
    - An assertion is made to check if the serialized JSON string equals the string representation of the `BigInteger`.
- **Output**:
    - The method does not return a value; it asserts that the serialized output matches the expected string representation of the `BigInteger`.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testSmallValueForBigIntegerDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testSmallValueForBigIntegerDeserialization}} -->
Tests the deserialization of a small integer value into a `BigInteger`.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `BigInteger` instance `expected` with the value of 15.
    - Deserializes the string '15' into a `BigInteger` instance `actual` using the `gson.fromJson` method.
    - Asserts that the deserialized value `actual` is equal to the expected value `expected`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigInteger` matches the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBadValueForBigIntegerDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBadValueForBigIntegerDeserialization}} -->
Tests that deserializing a decimal value into a `BigInteger` throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a decimal string.
    - The `gson.fromJson` method is called with the string '15.099' and the `BigInteger.class` type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testLazilyParsedNumberSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testLazilyParsedNumberSerialization}} -->
Tests the serialization of a `LazilyParsedNumber` object to JSON.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Creates an instance of `LazilyParsedNumber` initialized with the string '1.5'.
    - Uses the `gson` object to convert the `LazilyParsedNumber` instance to its JSON representation.
    - Asserts that the resulting JSON string is equal to '1.5'.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `LazilyParsedNumber` is correct.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testLazilyParsedNumberDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testLazilyParsedNumberDeserialization}} -->
Tests the deserialization of a `LazilyParsedNumber` from a JSON string.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates an instance of `LazilyParsedNumber` with the string '1.5' as the expected value.
    - Deserializes the JSON string '1.5' into a `LazilyParsedNumber` object using the `gson.fromJson` method.
    - Asserts that the deserialized object is equal to the expected `LazilyParsedNumber` instance.
- **Output**:
    - This method does not return a value; it asserts that the actual deserialized object matches the expected object.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testMoreSpecificSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testMoreSpecificSerialization}} -->
Tests the serialization of a string to JSON using a more specific type.
- **Inputs**:
    - `gson`: An instance of `Gson` used for converting Java objects to JSON.
    - `expected`: A string that represents the expected value to be serialized.
    - `serializableString`: A `Serializable` object that holds the same value as `expected`.
    - `expectedJson`: The JSON representation of the `expected` string.
    - `actualJson`: The JSON representation of the `serializableString` serialized as a `Serializable`.
- **Control Flow**:
    - Creates a new instance of `Gson`.
    - Serializes the `expected` string to JSON and stores it in `expectedJson`.
    - Creates a `Serializable` object from `expected`.
    - Serializes the `serializableString` as a `Serializable` to JSON and stores it in `actualJson`.
    - Asserts that `actualJson` is not equal to `expectedJson`.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of a `Serializable` string is different from the JSON representation of a regular string.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.extractElementFromArray<!-- {{#callable:com.google.gson.functional.PrimitiveTest.extractElementFromArray}} -->
Extracts the content of a JSON array from a string representation.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `json`: A string representation of a JSON array.
- **Control Flow**:
    - Finds the index of the first occurrence of '[' in the input string.
    - Finds the index of the last occurrence of ']' in the input string.
    - Extracts the substring between these two indices, effectively returning the content of the array.
- **Output**:
    - A string containing the elements of the JSON array, excluding the brackets.
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleNaNSerializationNotSupportedByDefault<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleNaNSerializationNotSupportedByDefault}} -->
Tests that serializing `Double.NaN` throws an `IllegalArgumentException`.
- **Inputs**: None
- **Control Flow**:
    - Defines an expected error message indicating that `NaN` is not a valid double value according to JSON specifications.
    - Attempts to serialize `Double.NaN` as a primitive `double` and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message matches the expected error message.
    - Attempts to serialize `Double.NaN` as a `Double` object and expects an `IllegalArgumentException` to be thrown.
    - Asserts that the exception message matches the expected error message.
- **Output**:
    - The method does not return a value; it asserts that exceptions are thrown with the correct messages.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleNaNSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleNaNSerialization}} -->
Tests the serialization of `Double.NaN` to JSON using Gson.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with special floating point values serialization enabled.
    - The method asserts that serializing `Double.NaN` as a primitive `double` results in the string 'NaN'.
    - The method asserts that serializing `Double.NaN` as a `Double` object also results in the string 'NaN'.
- **Output**:
    - The method does not return a value; it performs assertions to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleNaNDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleNaNDeserialization}} -->
Tests the deserialization of the string "NaN" into both primitive and wrapper `double` types.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
    - `double.class`: The class type for primitive double.
    - `Double.class`: The class type for the wrapper Double.
- **Control Flow**:
    - The method calls `gson.fromJson` with the string "NaN" and the primitive type `double.class`, and asserts that the result is NaN using `assertThat`.
    - The method then calls `gson.fromJson` again with the string "NaN" and the wrapper type `Double.class`, and asserts that the result is also NaN.
- **Output**:
    - The method does not return a value; it asserts that the deserialized values are NaN for both primitive and wrapper types.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testFloatNaNSerializationNotSupportedByDefault<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testFloatNaNSerializationNotSupportedByDefault}} -->
Tests that serializing `Float.NaN` throws an `IllegalArgumentException`.
- **Inputs**: None
- **Control Flow**:
    - Defines an expected error message indicating that `NaN` is not a valid value for JSON serialization.
    - Uses `assertThrows` to check that calling `gson.toJson` with `Float.NaN` and `float.class` throws an `IllegalArgumentException`.
    - Asserts that the exception message matches the expected error message.
    - Repeats the above step for `Float.NaN` and `Float.class`.
- **Output**:
    - The method does not return a value; it asserts that exceptions are thrown with the correct messages.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testFloatNaNSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testFloatNaNSerialization}} -->
Tests the serialization of `Float.NaN` to JSON using Gson.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `Gson` instance with special floating point values serialization enabled.
    - Serializes `Float.NaN` as a primitive float and checks if the output is 'NaN'.
    - Serializes `Float.NaN` as a `Float` object and checks if the output is 'NaN'.
- **Output**:
    - The method does not return a value; it asserts that the serialized output is 'NaN' for both float and Float types.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testFloatNaNDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testFloatNaNDeserialization}} -->
Tests the deserialization of the string "NaN" into both primitive and wrapper float types.
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson` instance to deserialize the string "NaN" into a primitive `float` type and checks if the result is NaN using `isNaN()`.
    - It then performs the same deserialization for the wrapper class `Float` and checks if the result is also NaN.
- **Output**:
    - The method does not return a value; it asserts that both deserialized values are NaN.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalNaNDeserializationNotSupported<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalNaNDeserializationNotSupported}} -->
Tests that Gson does not allow deserialization of NaN into a `BigDecimal`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize the string 'NaN' into a `BigDecimal`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleInfinitySerializationNotSupportedByDefault<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleInfinitySerializationNotSupportedByDefault}} -->
Tests that serializing `Double.POSITIVE_INFINITY` throws an `IllegalArgumentException`.
- **Inputs**: None
- **Control Flow**:
    - The method begins by defining an expected error message that describes the issue with serializing infinity values.
    - It then uses `assertThrows` to check if an `IllegalArgumentException` is thrown when attempting to serialize `Double.POSITIVE_INFINITY` as a primitive `double`.
    - The exception's message is verified against the expected message.
    - The same process is repeated for serializing `Double.POSITIVE_INFINITY` as a `Double` object.
- **Output**:
    - The method does not return a value; it asserts that the expected exception is thrown with the correct message.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleInfinitySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleInfinitySerialization}} -->
Tests the serialization of positive infinity for `double` and `Double` types using Gson.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with special floating point values serialization enabled.
    - The method asserts that serializing `Double.POSITIVE_INFINITY` as a primitive `double` results in the string 'Infinity'.
    - The method asserts that serializing `Double.POSITIVE_INFINITY` as a `Double` object also results in the string 'Infinity'.
- **Output**:
    - The method does not return a value; it performs assertions to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDoubleInfinityDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDoubleInfinityDeserialization}} -->
Tests the deserialization of the string "Infinity" into both primitive and wrapper `double` types.
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson` instance to convert the string "Infinity" into a primitive `double` type and checks if the result is positive infinity.
    - It then performs the same conversion for the wrapper class `Double` and checks if the result is also positive infinity.
- **Output**:
    - The method does not return a value; it asserts that the deserialized values are positive infinity.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testFloatInfinitySerializationNotSupportedByDefault<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testFloatInfinitySerializationNotSupportedByDefault}} -->
Tests that serializing `Float.POSITIVE_INFINITY` throws an `IllegalArgumentException`.
- **Inputs**: None
- **Control Flow**:
    - The method begins by defining an expected error message for the serialization of positive infinity.
    - It then attempts to serialize `Float.POSITIVE_INFINITY` using `gson.toJson` for both primitive and wrapper types.
    - For each serialization attempt, it asserts that an `IllegalArgumentException` is thrown and that the exception message matches the expected message.
- **Output**:
    - The method does not return a value; it verifies that exceptions are thrown as expected.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testFloatInfinitySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testFloatInfinitySerialization}} -->
Tests the serialization of positive infinity for `float` values using Gson.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with special floating point values serialization enabled.
    - The method asserts that serializing `Float.POSITIVE_INFINITY` as a primitive `float` results in the string 'Infinity'.
    - The method asserts that serializing `Float.POSITIVE_INFINITY` as a `Float` object also results in the string 'Infinity'.
- **Output**:
    - The method does not return a value; it performs assertions to verify the expected JSON output.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testFloatInfinityDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testFloatInfinityDeserialization}} -->
Tests the deserialization of the string "Infinity" into both primitive and wrapper `float` types.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
    - `"Infinity"`: A JSON string representing positive infinity.
    - `float.class`: The class type for primitive float.
    - `Float.class`: The class type for the Float wrapper.
- **Control Flow**:
    - The method calls `gson.fromJson` to convert the string "Infinity" into a primitive `float` and checks if the result is positive infinity using `isPositiveInfinity()`.
    - It then calls `gson.fromJson` again to convert the same string into a `Float` object and checks if the result is also positive infinity.
- **Output**:
    - The method does not return a value; it asserts that both deserialized values are positive infinity.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalInfinityDeserializationNotSupported<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalInfinityDeserializationNotSupported}} -->
Tests that Gson does not allow deserialization of positive infinity into a `BigDecimal`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize the string 'Infinity' into a `BigDecimal`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNegativeInfinitySerializationNotSupportedByDefault<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNegativeInfinitySerializationNotSupportedByDefault}} -->
Tests that serializing `Double.NEGATIVE_INFINITY` throws an `IllegalArgumentException`.
- **Inputs**: None
- **Control Flow**:
    - Defines an expected error message for the exception.
    - Uses `assertThrows` to check if serializing `Double.NEGATIVE_INFINITY` to JSON throws an `IllegalArgumentException` for both primitive and wrapper types.
    - Verifies that the exception message matches the expected error message.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown with the correct message.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNegativeInfinitySerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNegativeInfinitySerialization}} -->
Tests the serialization of negative infinity using Gson.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with special floating point values serialization enabled.
    - The method asserts that serializing `Double.NEGATIVE_INFINITY` as a primitive `double` results in the string "-Infinity".
    - The method asserts that serializing `Double.NEGATIVE_INFINITY` as a `Double` object also results in the string "-Infinity".
- **Output**:
    - The method does not return a value; it performs assertions to verify the expected output of the serialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNegativeInfinityDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNegativeInfinityDeserialization}} -->
Tests the deserialization of negative infinity values from JSON.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson` instance to deserialize the string '-Infinity' into a primitive `double` type and asserts that the result is negative infinity.
    - It then performs the same deserialization for the `Double` wrapper class and asserts that the result is also negative infinity.
- **Output**:
    - The method does not return a value; it asserts that the deserialized values are negative infinity.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNegativeInfinityFloatSerializationNotSupportedByDefault<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNegativeInfinityFloatSerializationNotSupportedByDefault}} -->
Tests that serializing `Float.NEGATIVE_INFINITY` throws an `IllegalArgumentException`.
- **Inputs**: None
- **Control Flow**:
    - The method begins by defining an expected error message for the serialization of negative infinity.
    - It then attempts to serialize `Float.NEGATIVE_INFINITY` using `gson.toJson` for both primitive and wrapper types.
    - For each serialization attempt, it asserts that an `IllegalArgumentException` is thrown.
    - Finally, it checks that the exception message matches the expected error message.
- **Output**:
    - The method does not return a value; it verifies that exceptions are thrown with the correct messages.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNegativeInfinityFloatSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNegativeInfinityFloatSerialization}} -->
Tests the serialization of negative infinity for float values using Gson.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with special floating point values serialization enabled.
    - The method asserts that serializing `Float.NEGATIVE_INFINITY` as a primitive float results in the string '-Infinity'.
    - The method asserts that serializing `Float.NEGATIVE_INFINITY` as a `Float` object also results in the string '-Infinity'.
- **Output**:
    - The method does not return a value; it performs assertions to verify the correctness of the serialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testNegativeInfinityFloatDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testNegativeInfinityFloatDeserialization}} -->
Tests the deserialization of negative infinity values for both primitive and wrapper float types.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson.fromJson` method to convert the string '-Infinity' into a primitive `float` type.
    - It asserts that the result is negative infinity using the `isNegativeInfinity()` assertion.
    - The method then repeats the deserialization for the wrapper class `Float` and asserts the same condition.
- **Output**:
    - The method does not return a value; it asserts that the deserialized values are negative infinity.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testBigDecimalNegativeInfinityDeserializationNotSupported<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testBigDecimalNegativeInfinityDeserializationNotSupported}} -->
Tests that Gson does not allow deserialization of negative infinity into a `BigDecimal`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize the string '-Infinity' into a `BigDecimal`.
    - The lambda expression passed to `assertThrows` contains the call to `gson.fromJson` which is expected to fail.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testLongAsStringSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testLongAsStringSerialization}} -->
Tests the serialization of `Long` values as strings using Gson.
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created with a specific serialization policy that converts `Long` values to their string representation.
    - The method serializes the `Long` value `15L` and checks if the result is the string representation of `15` (i.e., "15").
    - The method then serializes an integer value `2` and verifies that it remains a number (i.e., `2`).
- **Output**:
    - The method does not return a value; it asserts that the serialized output matches expected string representations.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setLongSerializationPolicy`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetLongSerializationPolicy)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testLongAsStringDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testLongAsStringDeserialization}} -->
Tests the deserialization of long values from JSON strings.
- **Inputs**: None
- **Control Flow**:
    - The method first deserializes a JSON string representing the number 15 into a `long` and asserts that the value is equal to 15.
    - Then, it creates a new `Gson` instance with a specific serialization policy that treats long values as strings.
    - Next, it deserializes another JSON string representing the number 25 into a `long` and asserts that the value is equal to 25.
- **Output**:
    - The method does not return a value but asserts that the deserialized long values match the expected results.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.GsonBuilder.setLongSerializationPolicy`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetLongSerializationPolicy)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testQuotedStringSerializationAndDeserialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testQuotedStringSerializationAndDeserialization}} -->
Tests the serialization and deserialization of a quoted string using Gson.
- **Inputs**: None
- **Control Flow**:
    - A string `value` is initialized with the text 'String Blah Blah Blah...1, 2, 3'.
    - The string is serialized to JSON format using `gson.toJson(value)` and stored in `serializedForm`.
    - An assertion checks if `serializedForm` equals the expected JSON representation of the string, which includes surrounding quotes.
    - The serialized JSON string is then deserialized back into a string using `gson.fromJson(serializedForm, String.class)`.
    - Another assertion checks if the deserialized string `actual` matches the original `value`.
- **Output**:
    - The method does not return a value but asserts that the serialization and deserialization processes are correct.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testUnquotedStringDeserializationFails<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testUnquotedStringDeserializationFails}} -->
Tests that deserialization of unquoted strings fails.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - The method first asserts that deserializing an unquoted string 'UnquotedSingleWord' returns the same string.
    - Then, it defines a string 'value' containing 'String Blah Blah Blah...1, 2, 3'.
    - It asserts that deserializing this string as a JSON string throws a `JsonSyntaxException`.
- **Output**:
    - The method does not return a value; it verifies the expected behavior of the Gson library during deserialization.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testHtmlCharacterSerialization<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testHtmlCharacterSerialization}} -->
Tests the serialization of HTML characters using Gson.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A string `target` containing HTML content is defined.
    - The `gson.toJson` method is called to serialize `target`, and the result is checked to ensure it is not equal to the escaped version of `target`.
    - A new `Gson` instance is created with HTML escaping disabled.
    - The `gson.toJson` method is called again to serialize `target`, and the result is checked to ensure it equals the escaped version of `target`.
- **Output**:
    - The method does not return a value; it asserts conditions to verify the behavior of the Gson serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.GsonBuilder.disableHtmlEscaping`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderdisableHtmlEscaping)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializePrimitiveWrapperAsObjectField<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializePrimitiveWrapperAsObjectField}} -->
Tests the deserialization of a JSON string into a Java object with an Integer field.
- **Inputs**:
    - `json`: A JSON string representing an object with an integer field, formatted as '{i:10}'.
- **Control Flow**:
    - The method initializes a JSON string that represents an object with an integer field.
    - It uses the `gson.fromJson` method to deserialize the JSON string into an instance of `ClassWithIntegerField`.
    - The method then asserts that the integer field `i` of the deserialized object equals 10.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's integer field matches the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testPrimitiveClassLiteral<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testPrimitiveClassLiteral}} -->
Tests the deserialization of a JSON string into a primitive integer.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
    - `String`: A JSON string representation of the integer to be deserialized.
    - `StringReader`: A `StringReader` that provides the JSON string for deserialization.
    - `JsonPrimitive`: A `JsonPrimitive` object that represents the integer to be deserialized.
- **Control Flow**:
    - The method calls `gson.fromJson` with a string representation of '1' and checks if the result equals 1.
    - It then calls `gson.fromJson` with a `StringReader` containing '1' and checks if the result equals 1.
    - Finally, it calls `gson.fromJson` with a `JsonPrimitive` containing 1 and checks if the result equals 1.
- **Output**:
    - The method does not return a value; it asserts that the deserialized integer equals 1 for all three cases.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsLongPrimitive<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsLongPrimitive}} -->
Tests that deserializing a JSON object into a `long` primitive throws a `JsonSyntaxException`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown.
    - It attempts to deserialize a JSON string representing an object with a key-value pair into a `long` primitive.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsLongWrapper<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsLongWrapper}} -->
Tests that deserializing a JSON array into a `Long` wrapper throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check if a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array string into a `Long` class.
    - The JSON string being tested is '[1,2,3]', which is not compatible with the `Long` wrapper type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsInt<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsInt}} -->
This method tests that deserializing a JSON array into a primitive `int` type throws a `JsonSyntaxException`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array into an `int`.
    - The `gson.fromJson` method is called with a JSON string representing an array and the `int.class` type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsInteger<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsInteger}} -->
Tests that deserializing an empty JSON object into an `Integer` throws a `JsonSyntaxException`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown.
    - It attempts to deserialize an empty JSON object (`{}`) into an `Integer` using the `gson.fromJson` method.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsShortPrimitive<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsShortPrimitive}} -->
Tests that deserializing a JSON object into a `short` primitive type throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check if a `JsonSyntaxException` is thrown when attempting to deserialize a JSON string into a `short` primitive.
    - The JSON string being tested is "{'abc':1}", which is not a valid representation for a `short`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsShortWrapper<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsShortWrapper}} -->
Tests that deserializing a JSON array of strings into a `Short` wrapper results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array of strings into a `Short` class.
    - The lambda expression passed to `assertThrows` contains the call to `gson.fromJson` with the invalid JSON input.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsDoublePrimitive<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsDoublePrimitive}} -->
Tests that deserializing a JSON array into a `double` primitive results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array string into a `double` primitive.
    - The `gson.fromJson` method is called with the JSON string '[1,2]' and the target type `double.class`.
- **Output**:
    - The method does not return a value; instead, it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsDoubleWrapper<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsDoubleWrapper}} -->
Tests that deserializing a JSON object into a `Double` wrapper throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON string into a `Double` wrapper.
    - The JSON string being tested is "{'abc':1}", which is not a valid representation for a `Double`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsFloatPrimitive<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsFloatPrimitive}} -->
Tests that deserializing a JSON object with a non-float key results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON string.
    - The JSON string being tested is "{'abc':1}", which contains a key that is not compatible with the expected float primitive type.
- **Output**:
    - The method does not return a value; instead, it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsFloatWrapper<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsFloatWrapper}} -->
Tests that deserializing a JSON array into a `Float` wrapper throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array string into a `Float` class.
    - The `gson.fromJson` method is called with a JSON array string and the `Float.class` type, which is expected to fail.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsBytePrimitive<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBytePrimitive}} -->
Tests that deserializing a JSON object into a `byte` primitive throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON object with a non-numeric field into a `byte` primitive.
    - The lambda expression passed to `assertThrows` calls `gson.fromJson` with a JSON string containing an object and the target type `byte.class`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsByteWrapper<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsByteWrapper}} -->
Tests that deserializing a JSON array into a `Byte` wrapper throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array string into a `Byte` class.
    - The lambda expression passed to `assertThrows` calls `gson.fromJson` with a JSON array string and the `Byte.class` type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsBooleanPrimitive<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBooleanPrimitive}} -->
Tests that deserializing a JSON object with a non-boolean value into a boolean primitive throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON string that represents an object with a non-boolean value into a boolean primitive.
    - The JSON string being tested is "{'abc':1}", which contains a key-value pair where the value is an integer (1) instead of a boolean.
- **Output**:
    - The method does not return a value; instead, it asserts that an exception is thrown, indicating that the deserialization failed as expected.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsBooleanWrapper<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsBooleanWrapper}} -->
Tests that deserializing a JSON array into a `Boolean` wrapper results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array into a `Boolean` class.
    - The `gson.fromJson` method is called with a JSON string representing an array and the `Boolean.class` type.
- **Output**:
    - The method does not return a value; instead, it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsBigDecimal<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsBigDecimal}} -->
Tests that deserializing a JSON array into a `BigDecimal` throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array string into a `BigDecimal`.
    - The `gson.fromJson` method is called with a JSON array string and the `BigDecimal.class` type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsBigDecimal<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBigDecimal}} -->
Tests that deserializing a JSON object into a `BigDecimal` throws a `JsonSyntaxException`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown.
    - It attempts to deserialize a JSON string representing an object with a key-value pair into a `BigDecimal`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsBigInteger<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsBigInteger}} -->
Tests that deserializing a JSON array into a `BigInteger` throws a `JsonSyntaxException`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check if a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array string into a `BigInteger`.
    - The `gson.fromJson` method is called with a JSON array string and the `BigInteger.class` type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsBigInteger<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsBigInteger}} -->
Tests that deserializing a JSON object into a `BigInteger` throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON string into a `BigInteger`.
    - The JSON string being tested is "{'c':2}", which is not a valid representation for a `BigInteger`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonArrayAsNumber<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonArrayAsNumber}} -->
Tests that deserializing a JSON array into a `Number` type throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON array string into a `Number` class.
    - The `gson.fromJson` method is called with the JSON array string and the `Number.class` type.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializeJsonObjectAsNumber<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializeJsonObjectAsNumber}} -->
Tests that deserializing a JSON object as a `Number` type throws a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a JSON object with a key-value pair into a `Number` type.
    - The JSON string being tested is "{'c':2}", which is not a valid representation for a `Number`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializingDecimalPointValueZeroSucceeds<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializingDecimalPointValueZeroSucceeds}} -->
Tests that deserializing a decimal point value of '1.0' into an `Integer` succeeds.
- **Inputs**: None
- **Control Flow**:
    - The method uses the `assertThat` assertion to verify the result of deserializing the JSON string '1.0' into an `Integer`.
    - It calls `gson.fromJson` with the string '1.0' and the `Integer.class` type to perform the deserialization.
- **Output**:
    - The method does not return a value; it asserts that the deserialized value equals 1.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializingNonZeroDecimalPointValuesAsIntegerFails<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializingNonZeroDecimalPointValuesAsIntegerFails}} -->
Tests that deserializing non-zero decimal point values as integers results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown for each of the specified types when attempting to deserialize the string '1.02'.
    - It checks the deserialization for `Byte.class`, `Short.class`, `Integer.class`, and `Long.class`.
- **Output**:
    - The method does not return a value; it asserts that exceptions are thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializingBigDecimalAsIntegerFails<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializingBigDecimalAsIntegerFails}} -->
Tests that deserializing a `BigDecimal` value as an `Integer` results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a `BigDecimal` string representation into an `Integer`.
    - The exception is expected to have a specific message indicating the type mismatch.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown with the expected message.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializingBigIntegerAsInteger<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializingBigIntegerAsInteger}} -->
Tests that deserializing a `BigInteger` as an `Integer` results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - A `String` representing a large number is defined.
    - The method `gson.fromJson` is called to attempt deserialization of the `String` into an `Integer`.
    - The call to `gson.fromJson` is wrapped in an `assertThrows` to check for a `JsonSyntaxException`.
    - The exception is then validated to ensure it has the expected message indicating the failure reason.
- **Output**:
    - The method does not return a value; instead, it asserts that a `JsonSyntaxException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializingBigIntegerAsLong<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializingBigIntegerAsLong}} -->
Tests the deserialization of a `BigInteger` as a `Long` and verifies that a `JsonSyntaxException` is thrown.
- **Inputs**:
    - `number`: A string representation of a large number that exceeds the range of a `Long`.
- **Control Flow**:
    - The method initializes a string `number` with a very large value.
    - It then uses `assertThrows` to check if deserializing this string into a `Long` using `gson.fromJson` throws a `JsonSyntaxException`.
    - Finally, it asserts that the exception's message matches the expected error message indicating the failure.
- **Output**:
    - The method does not return a value; instead, it verifies that a `JsonSyntaxException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testValueVeryCloseToZeroIsZero<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testValueVeryCloseToZeroIsZero}} -->
Tests the deserialization of very small floating-point values to their respective primitive types.
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify the output of the `gson.fromJson` method for various primitive types.
    - It checks the deserialization of a very small negative number '-122.08e-2132' to `byte`, `short`, `int`, and `long`, expecting all to be 0.
    - It checks the deserialization of the same small negative number to `float` and `double`, expecting -0.0.
    - It checks the deserialization of a small positive number '122.08e-2132' to `float` and `double`, expecting both to be 0.0.
- **Output**:
    - The method does not return a value but asserts that the deserialized values match the expected results.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializingBigDecimalAsBigIntegerFails<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializingBigDecimalAsBigIntegerFails}} -->
Tests that deserializing a `BigDecimal` value as a `BigInteger` results in a `JsonSyntaxException`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that a `JsonSyntaxException` is thrown when attempting to deserialize a `BigDecimal` string into a `BigInteger`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testDeserializingBigIntegerAsBigDecimal<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testDeserializingBigIntegerAsBigDecimal}} -->
Tests the deserialization of a `BigInteger` value as a `BigDecimal`.
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson.fromJson` method to convert a JSON string representation of a large integer into a `BigDecimal` object.
    - It then asserts that the plain string representation of the resulting `BigDecimal` matches the original string input.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `BigDecimal` matches the expected value.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)


---
#### PrimitiveTest\.testStringsAsBooleans<!-- {{#callable:com.google.gson.functional.PrimitiveTest.testStringsAsBooleans}} -->
This method tests the deserialization of various string representations of boolean values into a list of Boolean.
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing an array of boolean-like strings is defined.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `List<Boolean>`.
    - The deserialized list is then compared to an expected list of Boolean values using an assertion.
- **Output**:
    - The method does not return a value; it asserts that the deserialized list matches the expected list of Boolean values.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.PrimitiveTest`](#PrimitiveTest)  (Base Class)



---
### ClassWithIntegerField<!-- {{#class:com.google.gson.functional.PrimitiveTest.ClassWithIntegerField}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithIntegerField` is a simple private static class that contains a single field of type `Integer`. This class is likely used for testing or demonstration purposes within the context of the surrounding code, particularly in relation to JSON serialization and deserialization using Gson.
- **Fields**:
    - `i`: `Integer` An Integer field that can hold a nullable integer value.


