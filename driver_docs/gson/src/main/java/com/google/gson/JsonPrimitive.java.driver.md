# Purpose
The [`JsonPrimitive`](#JsonPrimitiveJsonPrimitive) class in the provided Java source code is part of the Google Gson library, which is used for converting Java objects to JSON and vice versa. This class specifically represents a JSON primitive value, which can be a String, a Java primitive, or a Java primitive wrapper type. The class extends `JsonElement`, indicating that it is a specialized form of a JSON element within the Gson library. The primary purpose of [`JsonPrimitive`](#JsonPrimitiveJsonPrimitive) is to encapsulate these basic data types and provide methods to interact with them in a JSON context. It includes constructors for creating instances with boolean, number, string, and character values, and provides methods to retrieve these values in various forms, such as `getAsBoolean()`, `getAsNumber()`, `getAsString()`, and others.

The class also includes methods to check the type of the contained value, such as `isBoolean()`, `isNumber()`, and `isString()`. It overrides methods from its superclass to provide specific implementations for handling primitive values, such as `deepCopy()`, `hashCode()`, and `equals()`. The `equals()` method is particularly noteworthy as it ensures that two [`JsonPrimitive`](#JsonPrimitiveJsonPrimitive) objects are considered equal if they contain equivalent values, even if those values are of different numeric types. The class also handles special cases, such as comparing `BigDecimal` values by ignoring their scale and treating `NaN` values as equal. Overall, [`JsonPrimitive`](#JsonPrimitiveJsonPrimitive) provides a focused functionality within the Gson library, serving as a fundamental building block for representing and manipulating JSON primitive data types.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.gson.internal.LazilyParsedNumber`
- `com.google.gson.internal.NumberLimits`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `java.util.Objects`


# Classes

---
### JsonPrimitive<!-- {{#class:com.google.gson.JsonPrimitive}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonPrimitive` class is a part of the Gson library and represents a JSON primitive value, which can be a String, a Java primitive, or a Java primitive wrapper type. It extends the `JsonElement` class and provides methods to create and manipulate JSON primitive values, including booleans, numbers, and strings. The class ensures immutability of the primitive values and provides various methods to retrieve the value in different data types, such as boolean, number, string, and character. It also includes methods to check the type of the primitive value and to compare equality with other `JsonPrimitive` instances.
- **Fields**:
    - `value`: `Object` A private final Object that holds the primitive value, which can be a Boolean, Number, or String.
- **Methods**:
    - [`com.google.gson.JsonPrimitive.JsonPrimitive`](#JsonPrimitiveJsonPrimitive)
    - [`com.google.gson.JsonPrimitive.JsonPrimitive`](#JsonPrimitiveJsonPrimitive)
    - [`com.google.gson.JsonPrimitive.JsonPrimitive`](#JsonPrimitiveJsonPrimitive)
    - [`com.google.gson.JsonPrimitive.JsonPrimitive`](#JsonPrimitiveJsonPrimitive)
    - [`com.google.gson.JsonPrimitive.deepCopy`](#JsonPrimitivedeepCopy)
    - [`com.google.gson.JsonPrimitive.isBoolean`](#JsonPrimitiveisBoolean)
    - [`com.google.gson.JsonPrimitive.getAsBoolean`](#JsonPrimitivegetAsBoolean)
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.JsonPrimitive.isString`](#JsonPrimitiveisString)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
    - [`com.google.gson.JsonPrimitive.getAsDouble`](#JsonPrimitivegetAsDouble)
    - [`com.google.gson.JsonPrimitive.getAsBigDecimal`](#JsonPrimitivegetAsBigDecimal)
    - [`com.google.gson.JsonPrimitive.getAsBigInteger`](#JsonPrimitivegetAsBigInteger)
    - [`com.google.gson.JsonPrimitive.getAsFloat`](#JsonPrimitivegetAsFloat)
    - [`com.google.gson.JsonPrimitive.getAsLong`](#JsonPrimitivegetAsLong)
    - [`com.google.gson.JsonPrimitive.getAsShort`](#JsonPrimitivegetAsShort)
    - [`com.google.gson.JsonPrimitive.getAsInt`](#JsonPrimitivegetAsInt)
    - [`com.google.gson.JsonPrimitive.getAsByte`](#JsonPrimitivegetAsByte)
    - [`com.google.gson.JsonPrimitive.getAsCharacter`](#JsonPrimitivegetAsCharacter)
    - [`com.google.gson.JsonPrimitive.hashCode`](#JsonPrimitivehashCode)
    - [`com.google.gson.JsonPrimitive.equals`](#JsonPrimitiveequals)
    - [`com.google.gson.JsonPrimitive.isIntegral`](#JsonPrimitiveisIntegral)
- **Extends/Implements**:
    - [`com.google.gson.JsonElement`](JsonElement.java.driver.md#JsonElement)

**Methods**

---
#### JsonPrimitive\.JsonPrimitive<!-- {{#callable:com.google.gson.JsonPrimitive.JsonPrimitive}} -->
The `JsonPrimitive` constructor initializes a JSON primitive with a non-null Boolean value.
- **Modifiers**: `public`
- **Inputs**:
    - `bool`: A Boolean value to initialize the JSON primitive with.
- **Control Flow**:
    - The constructor takes a Boolean parameter named `bool`.
    - It uses `Objects.requireNonNull(bool)` to ensure that the Boolean value is not null before assigning it to the `value` field.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of the `JsonPrimitive` class.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.JsonPrimitive<!-- {{#callable:com.google.gson.JsonPrimitive.JsonPrimitive}} -->
The `JsonPrimitive` constructor initializes a JSON primitive object with a non-null `Number` value.
- **Modifiers**: `public`
- **Inputs**:
    - `number`: The `Number` object to be used as the value for the JSON primitive.
- **Control Flow**:
    - The constructor is called with a `Number` object as an argument.
    - The `Objects.requireNonNull` method is used to ensure that the `number` argument is not null, throwing a `NullPointerException` if it is.
    - The `value` field of the `JsonPrimitive` object is assigned the non-null `number` argument.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of the `JsonPrimitive` class.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.JsonPrimitive<!-- {{#callable:com.google.gson.JsonPrimitive.JsonPrimitive}} -->
The `JsonPrimitive` constructor initializes a new instance with a non-null string value.
- **Modifiers**: `public`
- **Inputs**:
    - `string`: The string value to create the primitive with, which must not be null.
- **Control Flow**:
    - The method uses `Objects.requireNonNull` to ensure that the input string is not null.
    - The non-null string is assigned to the `value` field of the `JsonPrimitive` instance.
- **Output**:
    - The method does not return a value as it is a constructor.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.JsonPrimitive<!-- {{#callable:com.google.gson.JsonPrimitive.JsonPrimitive}} -->
The `JsonPrimitive` constructor initializes a JSON primitive with a character, converting it to a string representation.
- **Modifiers**: `public`
- **Inputs**:
    - `c`: The character to be converted into a JSON primitive.
- **Control Flow**:
    - The method takes a `Character` input `c`.
    - It uses `Objects.requireNonNull(c)` to ensure the character is not null, throwing a `NullPointerException` if it is.
    - The character is then converted to a string using `toString()` method, as JSON represents characters as single-character strings.
    - The resulting string is assigned to the `value` field of the `JsonPrimitive` instance.
- **Output**:
    - The method does not return a value; it initializes the `value` field of the `JsonPrimitive` instance with a string representation of the character.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.deepCopy<!-- {{#callable:com.google.gson.JsonPrimitive.deepCopy}} -->
The `deepCopy` method returns the current instance of `JsonPrimitive` as it is immutable.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns `this`, indicating that no new object is created and the current instance is returned.
- **Output**:
    - The method returns the current instance of `JsonPrimitive`.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.isBoolean<!-- {{#callable:com.google.gson.JsonPrimitive.isBoolean}} -->
The `isBoolean` method checks if the `value` field of the `JsonPrimitive` instance is of type `Boolean`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `instanceof` operator to check if the `value` field is an instance of `Boolean`.
    - It returns `true` if `value` is a `Boolean`, otherwise it returns `false`.
- **Output**:
    - A boolean value indicating whether the `value` field is a `Boolean`.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsBoolean<!-- {{#callable:com.google.gson.JsonPrimitive.getAsBoolean}} -->
The `getAsBoolean` method returns the boolean representation of the `JsonPrimitive` value, either directly if it's a boolean or by parsing its string representation.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Check if the `value` is an instance of `Boolean` using the `isBoolean()` method.
    - If true, cast and return the `value` as a `Boolean`.
    - If false, convert the `value` to a `String` using `getAsString()` and parse it using `Boolean.parseBoolean()`, returning the result.
- **Output**:
    - A boolean value representing the `JsonPrimitive`'s value.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isBoolean`](#JsonPrimitiveisBoolean)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.isNumber<!-- {{#callable:com.google.gson.JsonPrimitive.isNumber}} -->
The `isNumber` method checks if the `value` field of the `JsonPrimitive` instance is an instance of the `Number` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `instanceof` operator to determine if the `value` field is an instance of `Number`.
    - It returns `true` if `value` is a `Number`, otherwise it returns `false`.
- **Output**:
    - A boolean value indicating whether the `value` field is a `Number`.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsNumber<!-- {{#callable:com.google.gson.JsonPrimitive.getAsNumber}} -->
The `getAsNumber` method returns the value of the `JsonPrimitive` as a `Number`, either directly if it's already a `Number` or by parsing it if it's a `String`, and throws an exception if neither.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `value` is an instance of `Number`.
    - If true, cast and return the `value` as a `Number`.
    - If the `value` is an instance of `String`, create and return a `LazilyParsedNumber` from the `String`.
    - If neither, throw an `UnsupportedOperationException` indicating the primitive is neither a number nor a string.
- **Output**:
    - Returns a `Number` representation of the `JsonPrimitive`'s value or throws an exception if the value is neither a number nor a string.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.isString<!-- {{#callable:com.google.gson.JsonPrimitive.isString}} -->
The `isString` method checks if the `value` field of the `JsonPrimitive` instance is of type `String`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `instanceof` operator to determine if the `value` field is an instance of `String`.
    - It returns `true` if `value` is a `String`, otherwise it returns `false`.
- **Output**:
    - A boolean value indicating whether the `value` field is a `String`.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsString<!-- {{#callable:com.google.gson.JsonPrimitive.getAsString}} -->
The `getAsString` method returns the string representation of the value stored in the `JsonPrimitive` object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `value` is an instance of `String`; if true, return it as a `String`.
    - If `value` is not a `String`, check if it is a `Number` using `isNumber()`; if true, convert it to a `String` using `getAsNumber().toString()` and return it.
    - If `value` is not a `Number`, check if it is a `Boolean` using `isBoolean()`; if true, convert it to a `String` using `((Boolean) value).toString()` and return it.
    - If none of the above conditions are met, throw an `AssertionError` indicating an unexpected value type.
- **Output**:
    - The method returns a `String` representation of the `value` stored in the `JsonPrimitive` object.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
    - [`com.google.gson.JsonPrimitive.isBoolean`](#JsonPrimitiveisBoolean)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsDouble<!-- {{#callable:com.google.gson.JsonPrimitive.getAsDouble}} -->
The `getAsDouble` method returns the value of the `JsonPrimitive` as a double, either by directly converting a number or parsing a string representation.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Check if the `JsonPrimitive` is a number using `isNumber()`.
    - If it is a number, return the double value of the number using `getAsNumber().doubleValue()`.
    - If it is not a number, parse the string representation of the value to a double using `Double.parseDouble(getAsString())`.
- **Output**:
    - Returns the value of the `JsonPrimitive` as a `double`.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.doubleValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberdoubleValue)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsBigDecimal<!-- {{#callable:com.google.gson.JsonPrimitive.getAsBigDecimal}} -->
The `getAsBigDecimal` method returns the value of the `JsonPrimitive` as a `BigDecimal`, either directly if it is already a `BigDecimal`, or by parsing its string representation.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Check if the `value` is an instance of `BigDecimal`.
    - If true, cast and return the `value` as `BigDecimal`.
    - If false, call `getAsString()` to get the string representation of the `value`.
    - Parse the string representation to a `BigDecimal` using `NumberLimits.parseBigDecimal` and return it.
- **Output**:
    - Returns a `BigDecimal` representation of the `JsonPrimitive` value.
- **Functions called**:
    - [`com.google.gson.internal.NumberLimits.parseBigDecimal`](internal/NumberLimits.java.driver.md#NumberLimitsparseBigDecimal)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsBigInteger<!-- {{#callable:com.google.gson.JsonPrimitive.getAsBigInteger}} -->
The `getAsBigInteger` method returns the value of the `JsonPrimitive` as a `BigInteger`, converting it if necessary.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `value` is an instance of `BigInteger`; if true, cast and return it.
    - If the `value` is integral, convert it to a `BigInteger` using its long value and return it.
    - Otherwise, parse the `value` as a `BigInteger` from its string representation using `NumberLimits.parseBigInteger`.
- **Output**:
    - A `BigInteger` representation of the `JsonPrimitive`'s value.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isIntegral`](#JsonPrimitiveisIntegral)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
    - [`com.google.gson.internal.NumberLimits.parseBigInteger`](internal/NumberLimits.java.driver.md#NumberLimitsparseBigInteger)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsFloat<!-- {{#callable:com.google.gson.JsonPrimitive.getAsFloat}} -->
The `getAsFloat` method returns the value of the `JsonPrimitive` as a float, either by directly converting a number or parsing a string.
- **Modifiers**: `public`, `float`
- **Inputs**: None
- **Control Flow**:
    - Check if the `JsonPrimitive` contains a number using `isNumber()`.
    - If it is a number, return the float value of the number using `getAsNumber().floatValue()`.
    - If it is not a number, parse the string representation of the value to a float using `Float.parseFloat(getAsString())`.
- **Output**:
    - A float representation of the `JsonPrimitive` value.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.floatValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberfloatValue)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsLong<!-- {{#callable:com.google.gson.JsonPrimitive.getAsLong}} -->
The `getAsLong` method returns the value of the `JsonPrimitive` as a long, either by directly converting a number or parsing a string.
- **Modifiers**: `public`, `long`
- **Inputs**: None
- **Control Flow**:
    - Check if the `JsonPrimitive` is a number using `isNumber()`.
    - If it is a number, return the long value of the number using `getAsNumber().longValue()`.
    - If it is not a number, parse the string representation of the value to a long using `Long.parseLong(getAsString())`.
- **Output**:
    - The method returns the value of the `JsonPrimitive` as a primitive long.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsShort<!-- {{#callable:com.google.gson.JsonPrimitive.getAsShort}} -->
The `getAsShort` method returns the value of the `JsonPrimitive` as a `short` by either converting it directly if it's a number or parsing it from a string.
- **Modifiers**: `public`, `short`
- **Inputs**: None
- **Control Flow**:
    - Check if the `JsonPrimitive` is a number using `isNumber()`.
    - If it is a number, call `getAsNumber().shortValue()` to convert the number to a `short`.
    - If it is not a number, call `getAsString()` to get the string representation and parse it to a `short` using `Short.parseShort()`.
- **Output**:
    - The method returns the `JsonPrimitive` value as a `short`.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsInt<!-- {{#callable:com.google.gson.JsonPrimitive.getAsInt}} -->
The `getAsInt` method returns the value of the `JsonPrimitive` as an integer, either by directly converting a number or parsing a string.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Check if the `JsonPrimitive` contains a number using `isNumber()`.
    - If it is a number, return the integer value of the number using `getAsNumber().intValue()`.
    - If it is not a number, parse the string representation of the value to an integer using `Integer.parseInt(getAsString())`.
- **Output**:
    - The method returns an integer representation of the `JsonPrimitive` value.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.intValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberintValue)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsByte<!-- {{#callable:com.google.gson.JsonPrimitive.getAsByte}} -->
The `getAsByte` method returns the value of the `JsonPrimitive` as a byte, either by converting a number directly or parsing a string representation.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Check if the `JsonPrimitive` is a number using `isNumber()`.
    - If it is a number, return the byte value of the number using `getAsNumber().byteValue()`.
    - If it is not a number, parse the string representation of the value to a byte using `Byte.parseByte(getAsString())`.
- **Output**:
    - The method returns a byte representation of the `JsonPrimitive` value.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isNumber`](#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.getAsCharacter<!-- {{#callable:com.google.gson.JsonPrimitive.getAsCharacter}} -->
The `getAsCharacter` method returns the first character of the string representation of the JSON primitive value, throwing an exception if the string is empty.
- **Modifiers**: `public`, `deprecated`, `override`
- **Inputs**: None
- **Control Flow**:
    - Call the [`getAsString`](#JsonPrimitivegetAsString) method to obtain the string representation of the JSON primitive value.
    - Check if the obtained string is empty.
    - If the string is empty, throw an `UnsupportedOperationException` with the message 'String value is empty'.
    - If the string is not empty, return the first character of the string using `charAt(0)`.
- **Output**:
    - The method returns the first character of the string representation of the JSON primitive value as a `char`.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.getAsString`](#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.hashCode<!-- {{#callable:com.google.gson.JsonPrimitive.hashCode}} -->
The `hashCode` method computes a hash code for the `JsonPrimitive` object based on its value, using different strategies for null, integral, and non-integral numbers.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `value` is `null`; if so, return a constant hash code of 31.
    - If the `value` is an integral number, compute the hash code using a bitwise operation on its long representation.
    - If the `value` is a non-integral number, compute the hash code using a bitwise operation on the long bits of its double representation.
    - If the `value` is neither null nor a number, return the hash code of the `value` itself.
- **Output**:
    - An integer representing the hash code of the `JsonPrimitive` object.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isIntegral`](#JsonPrimitiveisIntegral)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](#JsonPrimitivegetAsNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
    - [`com.google.gson.internal.LazilyParsedNumber.doubleValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberdoubleValue)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.equals<!-- {{#callable:com.google.gson.JsonPrimitive.equals}} -->
The `equals` method determines if the current `JsonPrimitive` object is equal to another object by comparing their values and types.
- **Modifiers**: `public`
- **Inputs**:
    - `obj`: The object to compare with the current `JsonPrimitive` instance.
- **Control Flow**:
    - Check if the current object is the same as the input object using reference equality; if true, return true.
    - Check if the input object is null or not of the same class as the current object; if true, return false.
    - Cast the input object to `JsonPrimitive` and compare the `value` fields of both objects.
    - If the `value` is null, return true if the other object's `value` is also null.
    - If both objects have integral values, compare them as `BigInteger` if either is a `BigInteger`, otherwise compare their long values.
    - If both objects have `Number` values, compare them as `BigDecimal` if both are `BigDecimal`, otherwise compare their double values, considering NaN values as equal and ignoring the sign of zero.
    - If none of the above conditions are met, use the `equals` method of the `value` field to determine equality.
- **Output**:
    - A boolean value indicating whether the current `JsonPrimitive` is equal to the input object.
- **Functions called**:
    - [`com.google.gson.JsonPrimitive.isIntegral`](#JsonPrimitiveisIntegral)
    - [`com.google.gson.JsonPrimitive.getAsBigInteger`](#JsonPrimitivegetAsBigInteger)
    - [`com.google.gson.JsonElement.getAsNumber`](JsonElement.java.driver.md#JsonElementgetAsNumber)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](internal/LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
    - [`com.google.gson.JsonElement.getAsBigDecimal`](JsonElement.java.driver.md#JsonElementgetAsBigDecimal)
    - [`com.google.gson.JsonElement.getAsDouble`](JsonElement.java.driver.md#JsonElementgetAsDouble)
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)


---
#### JsonPrimitive\.isIntegral<!-- {{#callable:com.google.gson.JsonPrimitive.isIntegral}} -->
The `isIntegral` method checks if a `JsonPrimitive` contains a value of an integral type such as `BigInteger`, `Long`, `Integer`, `Short`, or `Byte`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `primitive`: A `JsonPrimitive` object whose value is to be checked for being an integral type.
- **Control Flow**:
    - Check if the `value` of the `JsonPrimitive` is an instance of `Number`.
    - If it is a `Number`, cast it to `Number` and check if it is an instance of `BigInteger`, `Long`, `Integer`, `Short`, or `Byte`.
    - Return `true` if the number is an instance of any of these integral types, otherwise return `false`.
    - If the `value` is not a `Number`, return `false`.
- **Output**:
    - A boolean value indicating whether the `JsonPrimitive` contains an integral type.
- **See also**: [`com.google.gson.JsonPrimitive`](#JsonPrimitive)  (Base Class)



