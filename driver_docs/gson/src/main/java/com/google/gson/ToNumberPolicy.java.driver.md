# Purpose
The provided Java source code defines an enumeration `ToNumberPolicy` within the `com.google.gson` package, which is part of the Gson library used for converting Java objects to JSON and vice versa. This enumeration implements the `ToNumberStrategy` interface and provides four distinct strategies for deserializing JSON numbers into Java objects. Each strategy is encapsulated as an enum constant: `DOUBLE`, `LAZILY_PARSED_NUMBER`, `LONG_OR_DOUBLE`, and `BIG_DECIMAL`. These strategies dictate how JSON numbers are read and converted into Java's numeric types, addressing different use cases and limitations associated with number parsing in JSON.

The `ToNumberPolicy` enum offers a focused functionality by providing a set of standardized approaches to handle number deserialization, which is a common requirement when dealing with JSON data. The `DOUBLE` strategy reads numbers as `Double` values, while `LAZILY_PARSED_NUMBER` uses a `LazilyParsedNumber` for deferred parsing. The `LONG_OR_DOUBLE` strategy attempts to parse numbers as `Long` if possible, defaulting to `Double` otherwise, and includes error handling for non-finite values. Lastly, the `BIG_DECIMAL` strategy reads numbers as `BigDecimal` for arbitrary precision. This code is integral to the Gson library's flexibility in handling numeric data, allowing developers to choose the most appropriate strategy based on their application's needs.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.gson.internal.LazilyParsedNumber`
- `com.google.gson.internal.NumberLimits`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.IOException`
- `java.math.BigDecimal`


# Classes

---
### ToNumberPolicy<!-- {{#class:com.google.gson.ToNumberPolicy}} -->
- **Modifiers**: `public`
- **Description**: The `ToNumberPolicy` enum defines various strategies for deserializing JSON numbers in the Gson library, allowing numbers to be read as different Java types such as `Double`, `LazilyParsedNumber`, `Long`, `Double`, or `BigDecimal`. Each strategy provides a specific implementation of the `readNumber` method from the `ToNumberStrategy` interface, enabling flexible handling of JSON number representations during deserialization.
- **Methods**:
    - [`com.google.gson.ToNumberPolicy.readNumber`](#ToNumberPolicyreadNumber)
    - [`com.google.gson.ToNumberPolicy.readNumber`](#ToNumberPolicyreadNumber)
    - [`com.google.gson.ToNumberPolicy.readNumber`](#ToNumberPolicyreadNumber)
    - [`com.google.gson.ToNumberPolicy.parseAsDouble`](#ToNumberPolicyparseAsDouble)
    - [`com.google.gson.ToNumberPolicy.readNumber`](#ToNumberPolicyreadNumber)

**Methods**

---
#### ToNumberPolicy\.readNumber<!-- {{#callable:com.google.gson.ToNumberPolicy.readNumber}} -->
The `readNumber` method reads a number from a `JsonReader` and returns it as a `Double`.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the number is read.
- **Control Flow**:
    - The method calls `nextDouble()` on the `JsonReader` instance `in` to read the next number from the JSON input.
- **Output**:
    - Returns a `Double` representing the number read from the JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextDouble`](stream/JsonReader.java.driver.md#JsonReadernextDouble)
- **See also**: [`com.google.gson.ToNumberPolicy`](#ToNumberPolicy)  (Base Class)


---
#### ToNumberPolicy\.readNumber<!-- {{#callable:com.google.gson.ToNumberPolicy.readNumber}} -->
The `readNumber` method reads a JSON number as a lazily parsed number using a string representation.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON number is read.
- **Control Flow**:
    - The method calls `in.nextString()` to read the next JSON value as a string.
    - A new `LazilyParsedNumber` object is created using the string obtained from the `JsonReader`.
- **Output**:
    - Returns a `Number` object that is a lazily parsed number backed by a string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.ToNumberPolicy`](#ToNumberPolicy)  (Base Class)


---
#### ToNumberPolicy\.readNumber<!-- {{#callable:com.google.gson.ToNumberPolicy.readNumber}} -->
The `readNumber` method reads a JSON number from a `JsonReader` and returns it as either a `Long` or `Double`, depending on its format.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON number is read.
- **Control Flow**:
    - Retrieve the next string value from the `JsonReader` using `in.nextString()`.
    - Check if the string contains a decimal point ('.').
    - If it does, call [`parseAsDouble`](#ToNumberPolicyparseAsDouble) to parse the string as a `Double`.
    - If it does not, attempt to parse the string as a `Long` using `Long.parseLong()`.
    - If parsing as `Long` fails with a `NumberFormatException`, call [`parseAsDouble`](#ToNumberPolicyparseAsDouble) to parse the string as a `Double`.
- **Output**:
    - Returns a `Number` object, which is either a `Long` or `Double`, depending on the input string's format.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.ToNumberPolicy.parseAsDouble`](#ToNumberPolicyparseAsDouble)
- **See also**: [`com.google.gson.ToNumberPolicy`](#ToNumberPolicy)  (Base Class)


---
#### ToNumberPolicy\.parseAsDouble<!-- {{#callable:com.google.gson.ToNumberPolicy.parseAsDouble}} -->
The `parseAsDouble` method attempts to parse a given string as a `Double` and handles special cases for non-finite values based on the leniency of the `JsonReader`.
- **Modifiers**: `private`
- **Inputs**:
    - `value`: A string representation of a number to be parsed as a `Double`.
    - `in`: A `JsonReader` instance used to determine the leniency of parsing and to provide context for error messages.
- **Control Flow**:
    - Attempt to convert the input string `value` to a `Double` object.
    - Check if the resulting `Double` is infinite or NaN and if the `JsonReader` is not lenient, throw a `MalformedJsonException`.
    - If the conversion is successful and valid, return the `Double` object.
    - Catch any `NumberFormatException` that occurs during parsing and throw a `JsonParseException` with a detailed error message.
- **Output**:
    - Returns a `Double` object if the parsing is successful and valid; otherwise, it throws an exception.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.isLenient`](stream/JsonReader.java.driver.md#JsonReaderisLenient)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.ToNumberPolicy`](#ToNumberPolicy)  (Base Class)


---
#### ToNumberPolicy\.readNumber<!-- {{#callable:com.google.gson.ToNumberPolicy.readNumber}} -->
The `readNumber` method reads a JSON number as a string and attempts to parse it into a `BigDecimal`, throwing a `JsonParseException` if parsing fails.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON number string is read.
- **Control Flow**:
    - Call `in.nextString()` to read the next JSON value as a string and store it in `value`.
    - Attempt to parse `value` into a `BigDecimal` using `NumberLimits.parseBigDecimal(value)`.
    - If parsing is successful, return the `BigDecimal` result.
    - If a `NumberFormatException` is thrown during parsing, catch the exception and throw a `JsonParseException` with a message including the problematic value and the JSON path.
- **Output**:
    - Returns a `BigDecimal` representing the parsed JSON number.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.internal.NumberLimits.parseBigDecimal`](internal/NumberLimits.java.driver.md#NumberLimitsparseBigDecimal)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.ToNumberPolicy`](#ToNumberPolicy)  (Base Class)



