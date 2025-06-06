# Purpose
The `UtcDateTypeAdapter` class is a specialized implementation of the `TypeAdapter` class from the Gson library, designed to handle the serialization and deserialization of `Date` objects in UTC format. This class provides a narrow functionality focused on converting `Date` objects to and from JSON strings that adhere to the ISO-8601 standard, specifically formatted in UTC time zone. The class overrides the [`write`](#UtcDateTypeAdapterwrite) and [`read`](#UtcDateTypeAdapterread) methods to respectively serialize a `Date` object into a JSON string and deserialize a JSON string back into a `Date` object. The serialization process involves formatting the date into a string representation that includes year, month, day, time, and optional milliseconds, while the deserialization process involves parsing a string to extract these components and construct a `Date` object.

The class includes several private helper methods to facilitate the parsing and formatting processes, such as [`format`](#UtcDateTypeAdapterformat), [`padInt`](#UtcDateTypeAdapterpadInt), [`parse`](#UtcDateTypeAdapterparse), [`checkOffset`](#UtcDateTypeAdaptercheckOffset), and [`parseInt`](#UtcDateTypeAdapterparseInt). These methods handle the intricacies of date manipulation, such as zero-padding integers, checking character offsets, and parsing integers from strings. The `UtcDateTypeAdapter` class does not define public APIs or external interfaces beyond the overridden methods from `TypeAdapter`, and it is specifically tailored for use within the Gson framework to ensure consistent handling of date-time data in JSON, particularly in environments like Android where certain Java date-time features may not be fully supported.
# Imports and Dependencies

---
- `com.google.gson.typeadapters`
- `com.google.gson.JsonParseException`
- `com.google.gson.TypeAdapter`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.text.ParseException`
- `java.text.ParsePosition`
- `java.util.Calendar`
- `java.util.Date`
- `java.util.GregorianCalendar`
- `java.util.Locale`
- `java.util.TimeZone`


# Classes

---
### UtcDateTypeAdapter<!-- {{#class:com.google.gson.typeadapters.UtcDateTypeAdapter}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `UtcDateTypeAdapter` class is a custom Gson `TypeAdapter` for serializing and deserializing `Date` objects to and from JSON, specifically handling dates in the UTC time zone. It overrides the `write` and `read` methods to format dates into a specific ISO-8601 string format and parse them back into `Date` objects, respectively. The class includes utility methods for formatting and parsing dates, ensuring compatibility with environments like Android that may not support certain date formats natively.
- **Fields**:
    - `UTC_TIME_ZONE`: `TimeZone` A static final field representing the UTC time zone used for date formatting and parsing.
    - `GMT_ID`: `String` A static final string representing the GMT time zone identifier used in date parsing.
- **Methods**:
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.write`](#UtcDateTypeAdapterwrite)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.read`](#UtcDateTypeAdapterread)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.format`](#UtcDateTypeAdapterformat)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.padInt`](#UtcDateTypeAdapterpadInt)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.parse`](#UtcDateTypeAdapterparse)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.checkOffset`](#UtcDateTypeAdaptercheckOffset)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.parseInt`](#UtcDateTypeAdapterparseInt)

**Methods**

---
#### UtcDateTypeAdapter\.write<!-- {{#callable:com.google.gson.typeadapters.UtcDateTypeAdapter.write}} -->
The `write` method serializes a `Date` object into a JSON format using a `JsonWriter`.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write the JSON output.
    - `date`: A `Date` object that is to be serialized into JSON.
- **Control Flow**:
    - Check if the `date` is null.
    - If `date` is null, write a JSON null value using `out.nullValue()`.
    - If `date` is not null, format the `date` into a string using the [`format`](#UtcDateTypeAdapterformat) method with UTC time zone.
    - Write the formatted date string to the JSON output using `out.value(value)`.
- **Output**:
    - The method does not return a value but writes to the `JsonWriter` output stream.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.format`](#UtcDateTypeAdapterformat)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.typeadapters.UtcDateTypeAdapter`](#UtcDateTypeAdapter)  (Base Class)


---
#### UtcDateTypeAdapter\.read<!-- {{#callable:com.google.gson.typeadapters.UtcDateTypeAdapter.read}} -->
The `read` method reads a JSON token from a `JsonReader` and parses it into a `Date` object, handling null values and parsing exceptions.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON token is read.
- **Control Flow**:
    - The method first checks if the next token in the `JsonReader` is `JsonToken.NULL`.
    - If the token is `JsonToken.NULL`, it consumes the null token using `in.nextNull()` and returns `null`.
    - If the token is not `JsonToken.NULL`, it reads the next string from the `JsonReader` using `in.nextString()`.
    - The method then attempts to parse the string into a `Date` object using the [`parse`](#UtcDateTypeAdapterparse) method with a `ParsePosition` starting at 0.
    - If a `ParseException` is thrown during parsing, it is caught and rethrown as a `JsonParseException`.
- **Output**:
    - The method returns a `Date` object parsed from the JSON token, or `null` if the token was `JsonToken.NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../../../gson/src/main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.parse`](#UtcDateTypeAdapterparse)
- **See also**: [`com.google.gson.typeadapters.UtcDateTypeAdapter`](#UtcDateTypeAdapter)  (Base Class)


---
#### UtcDateTypeAdapter\.format<!-- {{#callable:com.google.gson.typeadapters.UtcDateTypeAdapter.format}} -->
The `format` method formats a given `Date` object into a string representation following the pattern `yyyy-MM-ddThh:mm:ss[.sss][Z|[+-]hh:mm]`, optionally including milliseconds and using a specified time zone.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `date`: The `Date` object to be formatted.
    - `millis`: A boolean indicating whether to include milliseconds in the formatted output.
    - `tz`: The `TimeZone` to use for formatting the date.
- **Control Flow**:
    - A `Calendar` object is initialized with the specified time zone and the date is set to it.
    - The initial capacity of the `StringBuilder` is estimated based on the format pattern and whether milliseconds are included.
    - The year, month, day, hour, minute, and second are extracted from the `Calendar` and appended to the `StringBuilder` in the specified format.
    - If `millis` is true, milliseconds are also appended to the `StringBuilder`.
    - The time zone offset is calculated and formatted as either 'Z' for UTC or as a `+hh:mm` or `-hh:mm` offset, and appended to the `StringBuilder`.
    - The formatted date string is returned.
- **Output**:
    - A string representing the formatted date according to the specified pattern and time zone.
- **Functions called**:
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.padInt`](#UtcDateTypeAdapterpadInt)
- **See also**: [`com.google.gson.typeadapters.UtcDateTypeAdapter`](#UtcDateTypeAdapter)  (Base Class)


---
#### UtcDateTypeAdapter\.padInt<!-- {{#callable:com.google.gson.typeadapters.UtcDateTypeAdapter.padInt}} -->
The `padInt` method zero-pads an integer value to a specified length and appends it to a given `StringBuilder` buffer.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `buffer`: A `StringBuilder` object to which the padded integer will be appended.
    - `value`: The integer value that needs to be zero-padded.
    - `length`: The total length of the resulting string after padding.
- **Control Flow**:
    - Convert the integer `value` to a string representation `strValue`.
    - Calculate the number of zeros needed by subtracting the length of `strValue` from `length`.
    - Append the calculated number of '0' characters to the `buffer`.
    - Append the string representation of the integer `value` to the `buffer`.
- **Output**:
    - The method does not return a value; it modifies the `buffer` by appending the zero-padded integer.
- **See also**: [`com.google.gson.typeadapters.UtcDateTypeAdapter`](#UtcDateTypeAdapter)  (Base Class)


---
#### UtcDateTypeAdapter\.parse<!-- {{#callable:com.google.gson.typeadapters.UtcDateTypeAdapter.parse}} -->
The `parse` method parses an ISO-8601 formatted date string into a `Date` object, updating the `ParsePosition` to reflect the parsing progress.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `date`: A string representing the date in ISO-8601 format to be parsed.
    - `pos`: A `ParsePosition` object indicating the starting position for parsing and updated to the position after parsing.
- **Control Flow**:
    - Initialize a variable `fail` to capture exceptions.
    - Retrieve the current index from `pos` and store it in `offset`.
    - Parse the year from the `date` string and update `offset`.
    - Check for a '-' character and adjust `offset` if present.
    - Parse the month from the `date` string and update `offset`.
    - Check for a '-' character and adjust `offset` if present.
    - Parse the day from the `date` string and update `offset`.
    - Initialize default time values for hour, minutes, seconds, and milliseconds.
    - Check for a 'T' character to determine if time information is present and parse hours, minutes, seconds, and milliseconds accordingly, updating `offset` as needed.
    - Determine the timezone from the `date` string, updating `offset` and constructing a `timezoneId`.
    - Validate the timezone and create a `TimeZone` object.
    - Create a `Calendar` object with the parsed date and time values, using the determined timezone.
    - Set the `ParsePosition` index to the current `offset`.
    - Return the `Date` object from the `Calendar`.
    - Catch `IndexOutOfBoundsException` and `IllegalArgumentException`, storing them in `fail`.
    - Throw a `ParseException` if parsing fails, including the error message and position.
- **Output**:
    - Returns a `Date` object representing the parsed date and time, or throws a `ParseException` if parsing fails.
- **Functions called**:
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.parseInt`](#UtcDateTypeAdapterparseInt)
    - [`com.google.gson.typeadapters.UtcDateTypeAdapter.checkOffset`](#UtcDateTypeAdaptercheckOffset)
- **See also**: [`com.google.gson.typeadapters.UtcDateTypeAdapter`](#UtcDateTypeAdapter)  (Base Class)


---
#### UtcDateTypeAdapter\.checkOffset<!-- {{#callable:com.google.gson.typeadapters.UtcDateTypeAdapter.checkOffset}} -->
The `checkOffset` method verifies if a specified character exists at a given position in a string.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `value`: The string in which to check for the expected character.
    - `offset`: The position in the string to check for the expected character.
    - `expected`: The character that is expected to be found at the specified offset.
- **Control Flow**:
    - Check if the offset is less than the length of the string `value`.
    - If true, check if the character at the specified `offset` in `value` is equal to the `expected` character.
    - Return true if both conditions are met, otherwise return false.
- **Output**:
    - A boolean value indicating whether the expected character is found at the specified offset in the string.
- **See also**: [`com.google.gson.typeadapters.UtcDateTypeAdapter`](#UtcDateTypeAdapter)  (Base Class)


---
#### UtcDateTypeAdapter\.parseInt<!-- {{#callable:com.google.gson.typeadapters.UtcDateTypeAdapter.parseInt}} -->
The `parseInt` method parses a substring of a given string into an integer, ensuring the substring represents a valid non-negative integer.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `value`: The string containing the integer to be parsed.
    - `beginIndex`: The starting index of the substring to be parsed.
    - `endIndex`: The ending index of the substring to be parsed.
- **Control Flow**:
    - Check if the indices are valid; if not, throw a NumberFormatException.
    - Initialize the parsing index `i` to `beginIndex` and `result` to 0.
    - If `i` is less than `endIndex`, parse the first character as a digit; if invalid, throw a NumberFormatException.
    - Negate the parsed digit and assign it to `result`.
    - Iterate over the remaining characters in the substring, parsing each as a digit.
    - For each digit, multiply `result` by 10 and subtract the digit from `result`.
    - If any character is not a valid digit, throw a NumberFormatException.
    - Return the negated `result` to convert it back to a positive integer.
- **Output**:
    - The method returns the integer value parsed from the specified substring of the input string.
- **See also**: [`com.google.gson.typeadapters.UtcDateTypeAdapter`](#UtcDateTypeAdapter)  (Base Class)



