# Purpose
The `ToNumberPolicyTest` Java class is a unit test suite designed to validate the behavior of different number parsing strategies provided by the `ToNumberPolicy` in the Google Gson library. This class is part of the `com.google.gson` package and utilizes the JUnit testing framework to ensure that various number parsing strategies, such as `DOUBLE`, `LAZILY_PARSED_NUMBER`, `LONG_OR_DOUBLE`, and `BIG_DECIMAL`, function correctly when reading JSON numbers. The tests cover a range of scenarios, including parsing valid numbers, handling malformed JSON, and dealing with special cases like `NaN` and `Infinity`. The class also checks for appropriate exceptions when invalid inputs are encountered, ensuring that the strategies adhere to expected behavior and error handling.

The test methods within this class focus on verifying the correct conversion of JSON number strings into Java number types, such as `double`, `LazilyParsedNumber`, `long`, and `BigDecimal`, depending on the strategy used. The tests also ensure that the strategies throw the correct exceptions, such as `MalformedJsonException`, `JsonParseException`, and `IllegalStateException`, when encountering invalid JSON or unexpected null values. Additionally, the class includes helper methods to create `JsonReader` instances from strings, with an option to set the reader to lenient mode, allowing for more flexible parsing of malformed JSON. This test suite is crucial for maintaining the robustness and reliability of the Gson library's number parsing capabilities.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.internal.LazilyParsedNumber`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.IOException`
- `java.io.StringReader`
- `java.math.BigDecimal`
- `org.junit.Test`


# Classes

---
### ToNumberPolicyTest<!-- {{#class:com.google.gson.ToNumberPolicyTest}} -->
- **Modifiers**: `public`
- **Description**: The `ToNumberPolicyTest` class is a test suite designed to validate the behavior of different number parsing strategies provided by the `ToNumberPolicy` in the Gson library. It includes tests for various strategies such as DOUBLE, LAZILY_PARSED_NUMBER, LONG_OR_DOUBLE, and BIG_DECIMAL, ensuring that each strategy correctly parses JSON numbers and handles edge cases like malformed JSON, NaN, and infinities. The class uses JUnit for testing and includes helper methods to create `JsonReader` instances for parsing JSON strings.
- **Methods**:
    - [`com.google.gson.ToNumberPolicyTest.testDouble`](#ToNumberPolicyTesttestDouble)
    - [`com.google.gson.ToNumberPolicyTest.testLazilyParsedNumber`](#ToNumberPolicyTesttestLazilyParsedNumber)
    - [`com.google.gson.ToNumberPolicyTest.testLongOrDouble`](#ToNumberPolicyTesttestLongOrDouble)
    - [`com.google.gson.ToNumberPolicyTest.testBigDecimal`](#ToNumberPolicyTesttestBigDecimal)
    - [`com.google.gson.ToNumberPolicyTest.testNullsAreNeverExpected`](#ToNumberPolicyTesttestNullsAreNeverExpected)
    - [`com.google.gson.ToNumberPolicyTest.fromString`](#ToNumberPolicyTestfromString)
    - [`com.google.gson.ToNumberPolicyTest.fromStringLenient`](#ToNumberPolicyTestfromStringLenient)

**Methods**

---
#### ToNumberPolicyTest\.testDouble<!-- {{#callable:com.google.gson.ToNumberPolicyTest.testDouble}} -->
The `testDouble` method tests the `ToNumberPolicy.DOUBLE` strategy for reading numbers from JSON strings and handling malformed JSON inputs.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `ToNumberStrategy` with `ToNumberPolicy.DOUBLE`.
    - Assert that reading the number from the JSON string "10.1" results in the double value 10.1.
    - Assert that reading the number from the JSON string "3.141592653589793238462643383279" results in the double value 3.141592653589793D.
    - Assert that reading the number from the JSON string "1e400" throws a `MalformedJsonException` with a specific error message about JSON forbidding NaN and infinities.
    - Assert that reading the number from the JSON string "\"not-a-number\"" throws a `NumberFormatException`.
- **Output**:
    - The method does not return any value as it is a test method; it asserts expected outcomes for various inputs.
- **Functions called**:
    - [`com.google.gson.ToNumberStrategy.readNumber`](../../../../../main/java/com/google/gson/ToNumberStrategy.java.driver.md#ToNumberStrategyreadNumber)
    - [`com.google.gson.ToNumberPolicyTest.fromString`](#ToNumberPolicyTestfromString)
- **See also**: [`com.google.gson.ToNumberPolicyTest`](#ToNumberPolicyTest)  (Base Class)


---
#### ToNumberPolicyTest\.testLazilyParsedNumber<!-- {{#callable:com.google.gson.ToNumberPolicyTest.testLazilyParsedNumber}} -->
The `testLazilyParsedNumber` method tests the `LAZILY_PARSED_NUMBER` strategy of the `ToNumberPolicy` by asserting that numbers read from JSON strings are correctly parsed into `LazilyParsedNumber` objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method sets the `strategy` variable to `ToNumberPolicy.LAZILY_PARSED_NUMBER`.
    - It asserts that the number read from the JSON string "10.1" using the strategy is equal to a new `LazilyParsedNumber` initialized with "10.1".
    - It asserts that the number read from the JSON string "3.141592653589793238462643383279" using the strategy is equal to a new `LazilyParsedNumber` initialized with "3.141592653589793238462643383279".
    - It asserts that the number read from the JSON string "1e400" using the strategy is equal to a new `LazilyParsedNumber` initialized with "1e400".
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `LAZILY_PARSED_NUMBER` strategy.
- **Functions called**:
    - [`com.google.gson.ToNumberStrategy.readNumber`](../../../../../main/java/com/google/gson/ToNumberStrategy.java.driver.md#ToNumberStrategyreadNumber)
    - [`com.google.gson.ToNumberPolicyTest.fromString`](#ToNumberPolicyTestfromString)
- **See also**: [`com.google.gson.ToNumberPolicyTest`](#ToNumberPolicyTest)  (Base Class)


---
#### ToNumberPolicyTest\.testLongOrDouble<!-- {{#callable:com.google.gson.ToNumberPolicyTest.testLongOrDouble}} -->
The `testLongOrDouble` method tests the `ToNumberPolicy.LONG_OR_DOUBLE` strategy for reading numbers from JSON strings, handling both valid and invalid inputs.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `ToNumberStrategy` with `ToNumberPolicy.LONG_OR_DOUBLE`.
    - Assert that reading the number '10' from a JSON string returns a `Long` value of 10L.
    - Assert that reading the number '10.1' from a JSON string returns a `Double` value of 10.1.
    - Assert that reading a long decimal number returns a `Double` value of 3.141592653589793D.
    - Assert that reading a very large number '1e400' throws a `MalformedJsonException` with a specific message about JSON forbidding NaN and infinities.
    - Assert that reading a non-numeric string throws a `JsonParseException` with a specific message about parsing failure.
    - Assert that reading 'NaN', 'Infinity', and '-Infinity' in lenient mode returns `Double.NaN`, `Double.POSITIVE_INFINITY`, and `Double.NEGATIVE_INFINITY` respectively.
    - Assert that reading 'NaN', 'Infinity', and '-Infinity' in strict mode throws a `MalformedJsonException` with a message suggesting to use lenient mode.
- **Output**:
    - The method does not return a value; it performs assertions to validate the behavior of the `ToNumberPolicy.LONG_OR_DOUBLE` strategy.
- **Functions called**:
    - [`com.google.gson.ToNumberStrategy.readNumber`](../../../../../main/java/com/google/gson/ToNumberStrategy.java.driver.md#ToNumberStrategyreadNumber)
    - [`com.google.gson.ToNumberPolicyTest.fromString`](#ToNumberPolicyTestfromString)
    - [`com.google.gson.ToNumberPolicyTest.fromStringLenient`](#ToNumberPolicyTestfromStringLenient)
- **See also**: [`com.google.gson.ToNumberPolicyTest`](#ToNumberPolicyTest)  (Base Class)


---
#### ToNumberPolicyTest\.testBigDecimal<!-- {{#callable:com.google.gson.ToNumberPolicyTest.testBigDecimal}} -->
The `testBigDecimal` method tests the `ToNumberPolicy.BIG_DECIMAL` strategy for reading numbers from JSON strings and handling invalid inputs.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `ToNumberStrategy` with `ToNumberPolicy.BIG_DECIMAL`.
    - Use `assertThat` to verify that `strategy.readNumber` correctly parses JSON strings representing numbers into `BigDecimal` objects.
    - Test with various numeric strings including '10.1', '3.141592653589793238462643383279', and '1e400'.
    - Use `assertThrows` to verify that a `JsonParseException` is thrown when attempting to parse a non-numeric string '"not-a-number"'.
    - Check that the exception message matches the expected error message.
- **Output**:
    - The method does not return a value; it performs assertions to validate the behavior of the `ToNumberPolicy.BIG_DECIMAL` strategy.
- **Functions called**:
    - [`com.google.gson.ToNumberStrategy.readNumber`](../../../../../main/java/com/google/gson/ToNumberStrategy.java.driver.md#ToNumberStrategyreadNumber)
    - [`com.google.gson.ToNumberPolicyTest.fromString`](#ToNumberPolicyTestfromString)
- **See also**: [`com.google.gson.ToNumberPolicyTest`](#ToNumberPolicyTest)  (Base Class)


---
#### ToNumberPolicyTest\.testNullsAreNeverExpected<!-- {{#callable:com.google.gson.ToNumberPolicyTest.testNullsAreNeverExpected}} -->
The `testNullsAreNeverExpected` method verifies that reading a 'null' value with different `ToNumberPolicy` strategies throws an `IllegalStateException` with the expected error message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by using `assertThrows` to check that an `IllegalStateException` is thrown when `ToNumberPolicy.DOUBLE.readNumber` is called with a JSON string 'null'.
    - It then asserts that the exception message matches the expected message indicating a double was expected but a null was found.
    - The process is repeated for `ToNumberPolicy.LAZILY_PARSED_NUMBER`, `ToNumberPolicy.LONG_OR_DOUBLE`, and `ToNumberPolicy.BIG_DECIMAL`, each time checking that an `IllegalStateException` is thrown and the message indicates a string was expected but a null was found.
- **Output**:
    - The method does not return any value; it is a test method that asserts exceptions are thrown with specific messages.
- **Functions called**:
    - [`com.google.gson.ToNumberStrategy.readNumber`](../../../../../main/java/com/google/gson/ToNumberStrategy.java.driver.md#ToNumberStrategyreadNumber)
    - [`com.google.gson.ToNumberPolicyTest.fromString`](#ToNumberPolicyTestfromString)
- **See also**: [`com.google.gson.ToNumberPolicyTest`](#ToNumberPolicyTest)  (Base Class)


---
#### ToNumberPolicyTest\.fromString<!-- {{#callable:com.google.gson.ToNumberPolicyTest.fromString}} -->
The `fromString` method creates a `JsonReader` from a given JSON string.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `json`: A `String` representing the JSON data to be read.
- **Control Flow**:
    - The method takes a JSON string as input.
    - It creates a `StringReader` using the input JSON string.
    - A `JsonReader` is instantiated using the `StringReader`.
    - The `JsonReader` is returned as the output.
- **Output**:
    - A `JsonReader` object initialized with the provided JSON string.
- **See also**: [`com.google.gson.ToNumberPolicyTest`](#ToNumberPolicyTest)  (Base Class)


---
#### ToNumberPolicyTest\.fromStringLenient<!-- {{#callable:com.google.gson.ToNumberPolicyTest.fromStringLenient}} -->
The `fromStringLenient` method creates a `JsonReader` from a JSON string and sets its strictness to lenient mode.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `json`: A JSON string to be parsed into a `JsonReader`.
- **Control Flow**:
    - Call the [`fromString`](#ToNumberPolicyTestfromString) method with the input JSON string to create a `JsonReader` object.
    - Set the strictness of the `JsonReader` to `Strictness.LENIENT` to allow for more permissive parsing.
    - Return the modified `JsonReader` object.
- **Output**:
    - A `JsonReader` object configured to parse JSON in lenient mode.
- **Functions called**:
    - [`com.google.gson.ToNumberPolicyTest.fromString`](#ToNumberPolicyTestfromString)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
- **See also**: [`com.google.gson.ToNumberPolicyTest`](#ToNumberPolicyTest)  (Base Class)



