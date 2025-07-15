# Purpose
The [`NumberLimits`](#NumberLimitsNumberLimits) class in the `com.google.gson.internal` package is designed to enforce constraints on the size and scale of numbers parsed from JSON data. This class provides a focused functionality by ensuring that numbers do not exceed certain limits, which could otherwise lead to performance issues or potential vulnerabilities when handling extremely large numbers. The class is not intended for broad use but rather serves a specific purpose within the context of JSON parsing, likely as part of the Gson library's internal mechanisms to handle numeric data safely.

The class defines two public static methods, [`parseBigDecimal`](#NumberLimitsparseBigDecimal) and [`parseBigInteger`](#NumberLimitsparseBigInteger), which are responsible for parsing strings into `BigDecimal` and `BigInteger` objects, respectively. Before parsing, both methods utilize a private helper method, [`checkNumberStringLength`](#NumberLimitscheckNumberStringLength), to ensure that the string representation of the number does not exceed a predefined maximum length of 10,000 characters. Additionally, [`parseBigDecimal`](#NumberLimitsparseBigDecimal) checks the scale of the resulting `BigDecimal` to ensure it is within acceptable bounds. These methods throw a `NumberFormatException` if the input string violates any of these constraints, thereby providing a safeguard against processing excessively large numbers. The class does not define any public APIs or external interfaces beyond these methods, and it is constructed to be non-instantiable, as indicated by its private constructor.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `java.math.BigDecimal`
- `java.math.BigInteger`


# Classes

---
### NumberLimits<!-- {{#class:com.google.gson.internal.NumberLimits}} -->
- **Modifiers**: `public`
- **Description**: The `NumberLimits` class is designed to enforce constraints on the size and scale of numbers parsed from JSON strings, preventing performance issues associated with extremely large numbers. It provides static methods to parse strings into `BigDecimal` and `BigInteger` objects, while ensuring that the string length does not exceed a predefined maximum and that the scale of `BigDecimal` values is within acceptable limits.
- **Fields**:
    - `MAX_NUMBER_STRING_LENGTH`: `int` A constant defining the maximum allowed length for a number string, set to 10,000.
- **Methods**:
    - [`com.google.gson.internal.NumberLimits.NumberLimits`](#NumberLimitsNumberLimits)
    - [`com.google.gson.internal.NumberLimits.checkNumberStringLength`](#NumberLimitscheckNumberStringLength)
    - [`com.google.gson.internal.NumberLimits.parseBigDecimal`](#NumberLimitsparseBigDecimal)
    - [`com.google.gson.internal.NumberLimits.parseBigInteger`](#NumberLimitsparseBigInteger)

**Methods**

---
#### NumberLimits\.NumberLimits<!-- {{#callable:com.google.gson.internal.NumberLimits.NumberLimits}} -->
The `NumberLimits` constructor is a private method that prevents instantiation of the `NumberLimits` class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as private, which means it cannot be accessed from outside the class.
    - This effectively prevents any instantiation of the `NumberLimits` class, ensuring it is used only for its static methods.
- **Output**:
    - There is no output as this is a constructor method with no body.
- **See also**: [`com.google.gson.internal.NumberLimits`](#NumberLimits)  (Base Class)


---
#### NumberLimits\.checkNumberStringLength<!-- {{#callable:com.google.gson.internal.NumberLimits.checkNumberStringLength}} -->
The method checks if the length of a given string exceeds a predefined maximum limit and throws an exception if it does.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `s`: A string representing a number whose length is to be checked.
- **Control Flow**:
    - The method checks if the length of the input string 's' is greater than the constant MAX_NUMBER_STRING_LENGTH.
    - If the condition is true, it throws a NumberFormatException with a message indicating the number string is too large, including a substring of the first 30 characters of 's'.
- **Output**:
    - The method does not return a value; it either completes without issue or throws a NumberFormatException if the string is too long.
- **Functions called**:
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.length`](Streams.java.driver.md#CurrentWritelength)
- **See also**: [`com.google.gson.internal.NumberLimits`](#NumberLimits)  (Base Class)


---
#### NumberLimits\.parseBigDecimal<!-- {{#callable:com.google.gson.internal.NumberLimits.parseBigDecimal}} -->
The `parseBigDecimal` method converts a string representation of a number into a `BigDecimal` object while enforcing limits on the string length and the scale of the number to prevent performance issues.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `s`: A string representing the number to be converted into a BigDecimal.
- **Control Flow**:
    - The method first calls `checkNumberStringLength(s)` to ensure the input string does not exceed a predefined maximum length, throwing a `NumberFormatException` if it does.
    - A `BigDecimal` object is created from the input string `s`.
    - The method checks if the absolute value of the `BigDecimal`'s scale, cast to a long, is greater than or equal to 10,000.
    - If the scale check fails, a `NumberFormatException` is thrown with a message indicating the unsupported scale.
    - If all checks pass, the method returns the created `BigDecimal` object.
- **Output**:
    - The method returns a `BigDecimal` object representing the number parsed from the input string.
- **Functions called**:
    - [`com.google.gson.internal.NumberLimits.checkNumberStringLength`](#NumberLimitscheckNumberStringLength)
- **See also**: [`com.google.gson.internal.NumberLimits`](#NumberLimits)  (Base Class)


---
#### NumberLimits\.parseBigInteger<!-- {{#callable:com.google.gson.internal.NumberLimits.parseBigInteger}} -->
The `parseBigInteger` method converts a string representation of a number into a `BigInteger` object after ensuring the string is not excessively long.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `s`: A string representing the number to be converted into a BigInteger.
- **Control Flow**:
    - The method first calls `checkNumberStringLength(s)` to ensure the input string `s` does not exceed a predefined maximum length.
    - If the string length is acceptable, the method proceeds to create and return a new `BigInteger` object using the input string `s`.
- **Output**:
    - A `BigInteger` object representing the numeric value of the input string `s`.
- **Functions called**:
    - [`com.google.gson.internal.NumberLimits.checkNumberStringLength`](#NumberLimitscheckNumberStringLength)
- **See also**: [`com.google.gson.internal.NumberLimits`](#NumberLimits)  (Base Class)



