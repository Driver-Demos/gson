# Purpose
The [`LazilyParsedNumber`](#LazilyParsedNumberLazilyParsedNumber) class is a specialized utility within the Google Gson library, designed to handle number values that are stored as strings and converted to specific numeric types only when needed. This class extends the `Number` class, providing implementations for methods such as `intValue()`, `longValue()`, `floatValue()`, and `doubleValue()`. The primary purpose of this class is to defer the parsing of a numeric string into a specific number type until it is explicitly required, optimizing performance by avoiding unnecessary conversions. This lazy parsing approach is particularly useful in scenarios where the exact numeric type is not known upfront or when dealing with large datasets where performance is a concern.

The class encapsulates a single string value and provides methods to convert this string into various numeric types, handling potential `NumberFormatException` errors by attempting alternative parsing strategies, such as converting to a `BigDecimal` when necessary. Additionally, the class includes serialization logic to ensure that if an instance is serialized, it is done so as a `BigDecimal`, thus maintaining compatibility with systems that do not use Gson. The class also overrides `equals()` and `hashCode()` methods to ensure proper comparison and hashing based on the encapsulated string value. Overall, [`LazilyParsedNumber`](#LazilyParsedNumberLazilyParsedNumber) provides a focused functionality within the Gson library, enhancing its ability to handle JSON number parsing efficiently.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `java.io.IOException`
- `java.io.InvalidObjectException`
- `java.io.ObjectInputStream`
- `java.io.ObjectStreamException`
- `java.math.BigDecimal`


# Classes

---
### LazilyParsedNumber<!-- {{#class:com.google.gson.internal.LazilyParsedNumber}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `LazilyParsedNumber` class is a specialized implementation of the `Number` class that stores a number as a string and converts it to a specific numeric type only when needed. This lazy conversion approach is useful for handling numbers that may be represented in various formats, such as integers, longs, floats, or doubles, without immediately committing to a specific type. The class provides methods to convert the stored string to different numeric types, including `int`, `long`, `float`, and `double`, and handles potential `NumberFormatException` by attempting alternative conversions or using `BigDecimal` as a fallback. Additionally, it includes serialization logic to ensure compatibility and prevent direct deserialization, opting instead to serialize as a `BigDecimal`. The class is immutable and overrides standard methods like `equals`, `hashCode`, and `toString` to ensure consistent behavior.
- **Fields**:
    - `value`: `String` A final string that holds the numeric value to be lazily parsed.
- **Methods**:
    - [`com.google.gson.internal.LazilyParsedNumber.LazilyParsedNumber`](#LazilyParsedNumberLazilyParsedNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.asBigDecimal`](#LazilyParsedNumberasBigDecimal)
    - [`com.google.gson.internal.LazilyParsedNumber.intValue`](#LazilyParsedNumberintValue)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](#LazilyParsedNumberlongValue)
    - [`com.google.gson.internal.LazilyParsedNumber.floatValue`](#LazilyParsedNumberfloatValue)
    - [`com.google.gson.internal.LazilyParsedNumber.doubleValue`](#LazilyParsedNumberdoubleValue)
    - [`com.google.gson.internal.LazilyParsedNumber.toString`](#LazilyParsedNumbertoString)
    - [`com.google.gson.internal.LazilyParsedNumber.writeReplace`](#LazilyParsedNumberwriteReplace)
    - [`com.google.gson.internal.LazilyParsedNumber.readObject`](#LazilyParsedNumberreadObject)
    - [`com.google.gson.internal.LazilyParsedNumber.hashCode`](#LazilyParsedNumberhashCode)
    - [`com.google.gson.internal.LazilyParsedNumber.equals`](#LazilyParsedNumberequals)
- **Extends/Implements**:
    - `Number`

**Methods**

---
#### LazilyParsedNumber\.LazilyParsedNumber<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.LazilyParsedNumber}} -->
The constructor `LazilyParsedNumber` initializes a new instance of the class with a given string value representing a number.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A non-null string representing a number to be lazily parsed.
- **Control Flow**:
    - Assigns the input string `value` to the instance variable `this.value`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `LazilyParsedNumber` class.
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.asBigDecimal<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.asBigDecimal}} -->
The `asBigDecimal` method converts the stored string value to a `BigDecimal` using the `NumberLimits.parseBigDecimal` method.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling `NumberLimits.parseBigDecimal` with the `value` field as an argument.
- **Output**:
    - The method returns a `BigDecimal` representation of the `value` field.
- **Functions called**:
    - [`com.google.gson.internal.NumberLimits.parseBigDecimal`](NumberLimits.java.driver.md#NumberLimitsparseBigDecimal)
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.intValue<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.intValue}} -->
The `intValue` method attempts to convert the stored string value to an integer, using a series of parsing attempts with different number types.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Attempt to parse the string `value` as an `int` using `Integer.parseInt(value)`.
    - If a `NumberFormatException` is caught, attempt to parse the string `value` as a `long` and cast it to an `int`.
    - If another `NumberFormatException` is caught, convert the string `value` to a `BigDecimal` and return its integer value using `asBigDecimal().intValue()`.
- **Output**:
    - Returns the integer representation of the stored string value, or the closest possible integer if the value is too large.
- **Functions called**:
    - [`com.google.gson.internal.LazilyParsedNumber.asBigDecimal`](#LazilyParsedNumberasBigDecimal)
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.longValue<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.longValue}} -->
The `longValue` method attempts to parse the stored string value as a long, and if it fails, it converts the value to a BigDecimal and returns its long representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Attempt to parse the `value` string as a long using `Long.parseLong(value)`.
    - If parsing succeeds, return the parsed long value.
    - If a `NumberFormatException` is thrown during parsing, catch the exception.
    - Convert the `value` string to a `BigDecimal` using the `asBigDecimal()` method.
    - Return the long representation of the `BigDecimal` using `longValue()`.
- **Output**:
    - The method returns a `long` value, which is the long representation of the stored string value.
- **Functions called**:
    - [`com.google.gson.internal.LazilyParsedNumber.asBigDecimal`](#LazilyParsedNumberasBigDecimal)
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.floatValue<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.floatValue}} -->
The `floatValue` method converts the stored string representation of a number into a float.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method uses `Float.parseFloat` to convert the string `value` to a float.
- **Output**:
    - The method returns a float representation of the string `value`.
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.doubleValue<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.doubleValue}} -->
The `doubleValue` method converts the stored string representation of a number into a double precision floating point number.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method calls `Double.parseDouble` with the `value` string to convert it into a double.
- **Output**:
    - The method returns a `double` value parsed from the string `value`.
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.toString<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.toString}} -->
The `toString` method returns the string representation of the `LazilyParsedNumber` object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `value` field of the `LazilyParsedNumber` class.
- **Output**:
    - The method returns a `String` that represents the `value` field of the object.
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.writeReplace<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.writeReplace}} -->
The `writeReplace` method returns a `BigDecimal` representation of the `LazilyParsedNumber` instance for serialization purposes.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`asBigDecimal`](#LazilyParsedNumberasBigDecimal) method on the current instance.
    - The [`asBigDecimal`](#LazilyParsedNumberasBigDecimal) method converts the `value` string to a `BigDecimal`.
    - The `BigDecimal` object is returned as the result of the `writeReplace` method.
- **Output**:
    - The method returns an `Object`, specifically a `BigDecimal`, which is used as a replacement during serialization.
- **Functions called**:
    - [`com.google.gson.internal.LazilyParsedNumber.asBigDecimal`](#LazilyParsedNumberasBigDecimal)
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.readObject<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.readObject}} -->
The `readObject` method prevents the deserialization of the `LazilyParsedNumber` class by throwing an `InvalidObjectException`.
- **Modifiers**: `private`
- **Inputs**:
    - `in`: An `ObjectInputStream` from which the object is to be deserialized.
- **Control Flow**:
    - The method immediately throws an `InvalidObjectException` with the message 'Deserialization is unsupported', preventing any deserialization process.
- **Output**:
    - The method does not return any value as it always throws an exception.
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.hashCode<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.hashCode}} -->
The `hashCode` method returns the hash code of the `value` string in the `LazilyParsedNumber` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly calls the `hashCode` method on the `value` string and returns the result.
- **Output**:
    - An integer representing the hash code of the `value` string.
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)


---
#### LazilyParsedNumber\.equals<!-- {{#callable:com.google.gson.internal.LazilyParsedNumber.equals}} -->
The `equals` method checks if the current `LazilyParsedNumber` object is equal to another object by comparing their string values.
- **Modifiers**: `public`
- **Inputs**:
    - `obj`: The object to compare with the current `LazilyParsedNumber` instance.
- **Control Flow**:
    - Check if the current object (`this`) is the same as the input object (`obj`) using reference equality; if true, return `true`.
    - Check if the input object (`obj`) is an instance of `LazilyParsedNumber`; if true, cast it to `LazilyParsedNumber`.
    - Compare the `value` string of the current object with the `value` string of the casted `LazilyParsedNumber` object; return the result of this comparison.
    - If the input object is not an instance of `LazilyParsedNumber`, return `false`.
- **Output**:
    - Returns `true` if the input object is the same instance or a `LazilyParsedNumber` with an equal `value` string; otherwise, returns `false`.
- **See also**: [`com.google.gson.internal.LazilyParsedNumber`](#LazilyParsedNumber)  (Base Class)



