# Purpose
The `NumberLimitsTest` class is a comprehensive test suite designed to evaluate the behavior of the Gson library when handling large numerical values in JSON. This file is part of the `com.google.gson.functional` package and focuses on testing the limits and constraints of various components within the Gson library, such as `JsonReader`, `JsonPrimitive`, `ToNumberPolicy`, `LazilyParsedNumber`, and type adapters for `BigDecimal` and `BigInteger`. The tests are structured to verify how these components parse, interpret, and handle extremely large numbers, both in terms of magnitude and string length, ensuring that the library behaves as expected when encountering such edge cases.

The test cases are methodically organized to cover different scenarios, including parsing large numbers as strings, handling scientific notation, and testing the library's response to numbers that exceed typical limits. The tests utilize assertions to confirm expected outcomes, such as successful parsing or the throwing of exceptions like `MalformedJsonException`, `NumberFormatException`, and `JsonSyntaxException` when limits are breached. By doing so, the `NumberLimitsTest` class serves as a critical validation tool for developers to ensure the robustness and reliability of the Gson library in processing large numerical data, thereby maintaining data integrity and preventing potential errors in applications that rely on JSON parsing.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.Gson`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.ToNumberPolicy`
- `com.google.gson.ToNumberStrategy`
- `com.google.gson.TypeAdapter`
- `com.google.gson.internal.LazilyParsedNumber`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.IOException`
- `java.io.ObjectOutputStream`
- `java.io.OutputStream`
- `java.io.StringReader`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `org.junit.Test`


# Classes

---
### NumberLimitsTest<!-- {{#class:com.google.gson.functional.NumberLimitsTest}} -->
- **Modifiers**: `public`
- **Description**: The `NumberLimitsTest` class is a test suite designed to evaluate the behavior of the Gson library's `JsonReader` and related classes when handling large numbers. It includes tests for parsing large numbers using `JsonReader`, `JsonPrimitive`, and various number policies and strategies, such as `ToNumberPolicy` and `LazilyParsedNumber`. The class also tests the behavior of Gson's `TypeAdapter` for `BigDecimal` and `BigInteger` types, ensuring that exceptions are thrown for numbers that exceed certain limits or scales. The tests verify that the library correctly handles large numbers, throws appropriate exceptions for unsupported scales, and adheres to expected behavior when parsing numbers as strings or other types.
- **Fields**:
    - `MAX_LENGTH`: `int` A constant representing the maximum length for number strings, set to 10,000.
- **Methods**:
    - [`com.google.gson.functional.NumberLimitsTest.jsonReader`](#NumberLimitsTestjsonReader)
    - [`com.google.gson.functional.NumberLimitsTest.testJsonReader`](#NumberLimitsTesttestJsonReader)
    - [`com.google.gson.functional.NumberLimitsTest.testJsonPrimitive`](#NumberLimitsTesttestJsonPrimitive)
    - [`com.google.gson.functional.NumberLimitsTest.testToNumberPolicy`](#NumberLimitsTesttestToNumberPolicy)
    - [`com.google.gson.functional.NumberLimitsTest.testLazilyParsedNumber`](#NumberLimitsTesttestLazilyParsedNumber)
    - [`com.google.gson.functional.NumberLimitsTest.testBigDecimalAdapter`](#NumberLimitsTesttestBigDecimalAdapter)
    - [`com.google.gson.functional.NumberLimitsTest.testBigIntegerAdapter`](#NumberLimitsTesttestBigIntegerAdapter)

**Methods**

---
#### NumberLimitsTest\.jsonReader<!-- {{#callable:com.google.gson.functional.NumberLimitsTest.jsonReader}} -->
The `jsonReader` method creates a `JsonReader` object from a given JSON string.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `json`: A `String` representing the JSON data to be read.
- **Control Flow**:
    - The method takes a JSON string as input.
    - It creates a `StringReader` object using the input JSON string.
    - A `JsonReader` object is instantiated using the `StringReader` object.
    - The `JsonReader` object is returned.
- **Output**:
    - A `JsonReader` object initialized with the provided JSON string.
- **See also**: [`com.google.gson.functional.NumberLimitsTest`](#NumberLimitsTest)  (Base Class)


---
#### NumberLimitsTest\.testJsonReader<!-- {{#callable:com.google.gson.functional.NumberLimitsTest.testJsonReader}} -->
The `testJsonReader` method tests the behavior of `JsonReader` when handling large numbers and malformed JSON inputs.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonReader` instance with a string of 1000 repeated '1's and assert that it is recognized as a `JsonToken.NUMBER` and can be read as a string.
    - Create a `JsonReader` instance with a string exceeding `MAX_LENGTH` and assert that it throws a `MalformedJsonException` when peeking, with a specific error message.
    - Create `JsonReader` instances with various large exponential numbers ('1e9999', '1e+9999', '1e10000', '1e00001') and assert that they are recognized as `JsonToken.NUMBER` and can be read as strings.
- **Output**:
    - The method does not return any value but asserts the behavior of `JsonReader` with large numbers and malformed JSON.
- **Functions called**:
    - [`com.google.gson.functional.NumberLimitsTest.jsonReader`](#NumberLimitsTestjsonReader)
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.NumberLimitsTest`](#NumberLimitsTest)  (Base Class)


---
#### NumberLimitsTest\.testJsonPrimitive<!-- {{#callable:com.google.gson.functional.NumberLimitsTest.testJsonPrimitive}} -->
The `testJsonPrimitive` method tests the behavior of `JsonPrimitive` when converting large numeric strings to `BigDecimal` and `BigInteger`, and verifies that appropriate exceptions are thrown for numbers exceeding certain limits.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method first asserts that a `JsonPrimitive` created with a string of repeated '1's of length `MAX_LENGTH` can be correctly converted to a `BigDecimal` and a `BigInteger` of the same value.
    - It then asserts that `JsonPrimitive` objects created with strings '1e9999' and '1e-9999' can be converted to `BigDecimal` objects of the same value.
    - The method checks that creating a `JsonPrimitive` with a string of repeated '1's of length `MAX_LENGTH + 1` and converting it to a `BigDecimal` throws a `NumberFormatException` with a specific message.
    - It verifies that creating a `JsonPrimitive` with '1e10000' or '1e-10000' and converting it to a `BigDecimal` throws a `NumberFormatException` with a message indicating unsupported scale.
    - Finally, it asserts that converting a `JsonPrimitive` with a string of repeated '1's of length `MAX_LENGTH + 1` to a `BigInteger` throws a `NumberFormatException` with a specific message.
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of `JsonPrimitive` and throws exceptions if the assertions fail.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.getAsBigDecimal`](../../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBigDecimal)
    - [`com.google.gson.JsonPrimitive.getAsBigInteger`](../../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBigInteger)
- **See also**: [`com.google.gson.functional.NumberLimitsTest`](#NumberLimitsTest)  (Base Class)


---
#### NumberLimitsTest\.testToNumberPolicy<!-- {{#callable:com.google.gson.functional.NumberLimitsTest.testToNumberPolicy}} -->
The `testToNumberPolicy` method tests the behavior of the `ToNumberStrategy` when reading large numbers from JSON strings, ensuring correct parsing and exception handling for numbers exceeding certain limits.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `ToNumberStrategy` with `ToNumberPolicy.BIG_DECIMAL` to handle number parsing.
    - Use `assertThat` to verify that a JSON string representing a large number within the limit is correctly parsed to a `BigDecimal`.
    - Use `assertThat` to verify that a JSON string representing a large exponential number is correctly parsed to a `BigDecimal`.
    - Use `assertThrows` to test that parsing a JSON string representing a number exceeding the maximum length throws a `JsonParseException`.
    - Verify the exception message and cause for the above test to ensure it matches expected error messages.
    - Use `assertThrows` to test that parsing a JSON string representing an exponential number with an unsupported scale throws a `JsonParseException`.
    - Verify the exception message and cause for the above test to ensure it matches expected error messages.
- **Output**:
    - The method does not return any value as it is a test method; it asserts conditions and throws exceptions if the conditions are not met.
- **Functions called**:
    - [`com.google.gson.functional.ToNumberPolicyFunctionalTest.testCustomStrategiesCannotAffectConcreteDeclaredNumbers.readNumber`](ToNumberPolicyFunctionalTest.java.driver.md#testCustomStrategiesCannotAffectConcreteDeclaredNumbersreadNumber)
    - [`com.google.gson.functional.NumberLimitsTest.jsonReader`](#NumberLimitsTestjsonReader)
- **See also**: [`com.google.gson.functional.NumberLimitsTest`](#NumberLimitsTest)  (Base Class)


---
#### NumberLimitsTest\.testLazilyParsedNumber<!-- {{#callable:com.google.gson.functional.NumberLimitsTest.testLazilyParsedNumber}} -->
The `testLazilyParsedNumber` method tests the behavior of the `LazilyParsedNumber` class when handling large numbers and numbers with unsupported scales, ensuring it throws appropriate exceptions.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method asserts that a `LazilyParsedNumber` created with a string of repeated '1's up to `MAX_LENGTH` has the same integer value as a `BigDecimal` created with the same string.
    - It asserts that a `LazilyParsedNumber` created with the string '1e9999' has the same integer value as a `BigDecimal` created with the same string.
    - It checks that creating a `LazilyParsedNumber` with a string of repeated '1's exceeding `MAX_LENGTH` throws a `NumberFormatException` with a specific message.
    - It checks that creating a `LazilyParsedNumber` with the string '1e10000' throws a `NumberFormatException` with a specific message when calling `intValue()` and `longValue()`.
    - It verifies that serializing a `LazilyParsedNumber` with the string '1e10000' using `ObjectOutputStream` throws a `NumberFormatException` with a specific message.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of `LazilyParsedNumber`.
- **Functions called**:
    - [`com.google.gson.internal.LazilyParsedNumber.intValue`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberintValue)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](../../../../../../main/java/com/google/gson/internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
- **See also**: [`com.google.gson.functional.NumberLimitsTest`](#NumberLimitsTest)  (Base Class)


---
#### NumberLimitsTest\.testBigDecimalAdapter<!-- {{#callable:com.google.gson.functional.NumberLimitsTest.testBigDecimalAdapter}} -->
The `testBigDecimalAdapter` method tests the behavior of a Gson `TypeAdapter` for `BigDecimal` when parsing large numbers and numbers with unsupported scales from JSON strings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapter` for `BigDecimal` is obtained using `Gson.getAdapter(BigDecimal.class)`.
    - The method asserts that parsing a JSON string with a repeated '1' of `MAX_LENGTH` results in a `BigDecimal` of the same value.
    - It asserts that parsing a JSON string '1e9999' results in a `BigDecimal` of the same value.
    - It checks that parsing a JSON string with a repeated '1' of `MAX_LENGTH + 1` throws a `JsonSyntaxException` with a specific error message indicating the number string is too large.
    - It checks that parsing a JSON string '1e10000' throws a `JsonSyntaxException` with a specific error message indicating the number has an unsupported scale.
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of the `TypeAdapter` for `BigDecimal`.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.NumberLimitsTest`](#NumberLimitsTest)  (Base Class)


---
#### NumberLimitsTest\.testBigIntegerAdapter<!-- {{#callable:com.google.gson.functional.NumberLimitsTest.testBigIntegerAdapter}} -->
The `testBigIntegerAdapter` method tests the behavior of a Gson `TypeAdapter` for `BigInteger` when parsing large JSON number strings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapter` for `BigInteger` is obtained from a `Gson` instance.
    - The method asserts that parsing a JSON string of maximum allowed length (`MAX_LENGTH`) results in a `BigInteger` of the same value.
    - It then attempts to parse a JSON string that exceeds the maximum length by one character, expecting a `JsonSyntaxException` to be thrown.
    - The exception is verified to have a specific error message indicating failure to parse the oversized number as a `BigInteger`.
    - The cause of the exception is also checked to ensure it indicates the number string is too large.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `TypeAdapter` for `BigInteger`.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.NumberLimitsTest`](#NumberLimitsTest)  (Base Class)



