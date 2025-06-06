# Purpose
The provided Java source code defines the [`JsonReader`](#JsonReaderJsonReader) class, which is part of the `com.google.gson.stream` package. This class is a core component of the Gson library, designed to read JSON-encoded data as a stream of tokens. The [`JsonReader`](#JsonReaderJsonReader) class provides functionality to parse JSON data in a depth-first manner, handling both literal values (such as strings, numbers, booleans, and nulls) and structural elements (such as the beginning and end of objects and arrays). It supports recursive descent parsing, allowing developers to create custom parsers for specific JSON structures by defining handler methods for different JSON components.

The [`JsonReader`](#JsonReaderJsonReader) class offers a range of configuration options, including strictness levels that dictate how lenient or strict the parser should be with non-standard JSON formats. It supports various methods to navigate and consume JSON tokens, such as `beginArray()`, `endArray()`, `beginObject()`, `endObject()`, `nextName()`, `nextString()`, `nextBoolean()`, and `nextNull()`. Additionally, it provides mechanisms to handle numbers flexibly, allowing numeric values to be read as strings and vice versa, to prevent precision loss. The class also includes methods to skip unwanted JSON values and manage JSON paths, which can be useful for debugging and error reporting. Overall, [`JsonReader`](#JsonReaderJsonReader) is a versatile tool for efficiently parsing JSON data in Java applications.
# Imports and Dependencies

---
- `com.google.gson.stream`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.Strictness`
- `com.google.gson.TypeAdapter`
- `com.google.gson.internal.JsonReaderInternalAccess`
- `com.google.gson.internal.TroubleshootingGuide`
- `com.google.gson.internal.bind.JsonTreeReader`
- `java.io.Closeable`
- `java.io.EOFException`
- `java.io.IOException`
- `java.io.Reader`
- `java.util.Arrays`
- `java.util.Objects`


# Classes

---
### JsonReader<!-- {{#class:com.google.gson.stream.JsonReader}} -->
- **Modifiers**: `public`
- **Description**: The `JsonReader` class is a utility for reading JSON-encoded data as a stream of tokens, allowing for efficient parsing of JSON data in a depth-first order. It supports various configurations for strictness and nesting limits, enabling it to handle both strict and lenient JSON formats. The class provides methods to navigate through JSON structures, such as arrays and objects, and to read different data types like strings, numbers, booleans, and nulls. It also includes functionality to skip unrecognized or unwanted JSON values, making it versatile for different parsing needs.
- **Fields**:
    - `MIN_INCOMPLETE_INTEGER`: `long` A constant representing the minimum incomplete integer value for parsing.
    - `PEEKED_NONE`: `int` A constant indicating that no token has been peeked yet.
    - `PEEKED_BEGIN_OBJECT`: `int` A constant indicating that the next token is the beginning of a JSON object.
    - `PEEKED_END_OBJECT`: `int` A constant indicating that the next token is the end of a JSON object.
    - `PEEKED_BEGIN_ARRAY`: `int` A constant indicating that the next token is the beginning of a JSON array.
    - `PEEKED_END_ARRAY`: `int` A constant indicating that the next token is the end of a JSON array.
    - `PEEKED_TRUE`: `int` A constant indicating that the next token is a JSON true literal.
    - `PEEKED_FALSE`: `int` A constant indicating that the next token is a JSON false literal.
    - `PEEKED_NULL`: `int` A constant indicating that the next token is a JSON null literal.
    - `PEEKED_SINGLE_QUOTED`: `int` A constant indicating that the next token is a single-quoted string.
    - `PEEKED_DOUBLE_QUOTED`: `int` A constant indicating that the next token is a double-quoted string.
    - `PEEKED_UNQUOTED`: `int` A constant indicating that the next token is an unquoted string.
    - `PEEKED_BUFFERED`: `int` A constant indicating that the next token is a buffered string value.
    - `PEEKED_SINGLE_QUOTED_NAME`: `int` A constant indicating that the next token is a single-quoted name.
    - `PEEKED_DOUBLE_QUOTED_NAME`: `int` A constant indicating that the next token is a double-quoted name.
    - `PEEKED_UNQUOTED_NAME`: `int` A constant indicating that the next token is an unquoted name.
    - `PEEKED_LONG`: `int` A constant indicating that the next token is a long integer value.
    - `PEEKED_NUMBER`: `int` A constant indicating that the next token is a number.
    - `PEEKED_EOF`: `int` A constant indicating that the end of the JSON document has been reached.
    - `NUMBER_CHAR_NONE`: `int` A constant representing no character in the number parsing state machine.
    - `NUMBER_CHAR_SIGN`: `int` A constant representing a sign character in the number parsing state machine.
    - `NUMBER_CHAR_DIGIT`: `int` A constant representing a digit character in the number parsing state machine.
    - `NUMBER_CHAR_DECIMAL`: `int` A constant representing a decimal point in the number parsing state machine.
    - `NUMBER_CHAR_FRACTION_DIGIT`: `int` A constant representing a fraction digit in the number parsing state machine.
    - `NUMBER_CHAR_EXP_E`: `int` A constant representing an exponent character in the number parsing state machine.
    - `NUMBER_CHAR_EXP_SIGN`: `int` A constant representing an exponent sign in the number parsing state machine.
    - `NUMBER_CHAR_EXP_DIGIT`: `int` A constant representing an exponent digit in the number parsing state machine.
    - `in`: `Reader` The input reader from which JSON data is read.
    - `strictness`: `Strictness` The strictness level of the JSON reader, determining how strictly it adheres to JSON standards.
    - `DEFAULT_NESTING_LIMIT`: `int` The default limit for JSON nesting depth.
    - `nestingLimit`: `int` The current limit for JSON nesting depth.
    - `BUFFER_SIZE`: `int` The size of the buffer used for reading JSON data.
    - `buffer`: `char[]` A character buffer used for reading and processing JSON data.
    - `pos`: `int` The current position in the buffer.
    - `limit`: `int` The limit of valid data in the buffer.
    - `lineNumber`: `int` The current line number in the JSON input.
    - `lineStart`: `int` The start position of the current line in the buffer.
    - `peeked`: `int` The current peeked token type.
    - `peekedLong`: `long` The long value of a peeked number token.
    - `peekedNumberLength`: `int` The length of the peeked number token.
    - `peekedString`: `String` The string value of a peeked token.
    - `stack`: `int[]` The stack used to track the current state of JSON parsing.
    - `stackSize`: `int` The current size of the stack.
    - `pathNames`: `String[]` An array of path names corresponding to the JSON structure being parsed.
    - `pathIndices`: `int[]` An array of path indices corresponding to the JSON structure being parsed.
- **Methods**:
    - [`com.google.gson.stream.JsonReader.JsonReader`](#JsonReaderJsonReader)
    - [`com.google.gson.stream.JsonReader.setLenient`](#JsonReadersetLenient)
    - [`com.google.gson.stream.JsonReader.isLenient`](#JsonReaderisLenient)
    - [`com.google.gson.stream.JsonReader.setStrictness`](#JsonReadersetStrictness)
    - [`com.google.gson.stream.JsonReader.getStrictness`](#JsonReadergetStrictness)
    - [`com.google.gson.stream.JsonReader.setNestingLimit`](#JsonReadersetNestingLimit)
    - [`com.google.gson.stream.JsonReader.getNestingLimit`](#JsonReadergetNestingLimit)
    - [`com.google.gson.stream.JsonReader.beginArray`](#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.endArray`](#JsonReaderendArray)
    - [`com.google.gson.stream.JsonReader.beginObject`](#JsonReaderbeginObject)
    - [`com.google.gson.stream.JsonReader.endObject`](#JsonReaderendObject)
    - [`com.google.gson.stream.JsonReader.hasNext`](#JsonReaderhasNext)
    - [`com.google.gson.stream.JsonReader.peek`](#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.peekKeyword`](#JsonReaderpeekKeyword)
    - [`com.google.gson.stream.JsonReader.peekNumber`](#JsonReaderpeekNumber)
    - [`com.google.gson.stream.JsonReader.isLiteral`](#JsonReaderisLiteral)
    - [`com.google.gson.stream.JsonReader.nextName`](#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextString`](#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.nextNull`](#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextDouble`](#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonReader.nextLong`](#JsonReadernextLong)
    - [`com.google.gson.stream.JsonReader.nextQuotedValue`](#JsonReadernextQuotedValue)
    - [`com.google.gson.stream.JsonReader.nextUnquotedValue`](#JsonReadernextUnquotedValue)
    - [`com.google.gson.stream.JsonReader.skipQuotedValue`](#JsonReaderskipQuotedValue)
    - [`com.google.gson.stream.JsonReader.skipUnquotedValue`](#JsonReaderskipUnquotedValue)
    - [`com.google.gson.stream.JsonReader.nextInt`](#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.close`](#JsonReaderclose)
    - [`com.google.gson.stream.JsonReader.skipValue`](#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReader.push`](#JsonReaderpush)
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
    - [`com.google.gson.stream.JsonReader.nextNonWhitespace`](#JsonReadernextNonWhitespace)
    - [`com.google.gson.stream.JsonReader.checkLenient`](#JsonReadercheckLenient)
    - [`com.google.gson.stream.JsonReader.skipToEndOfLine`](#JsonReaderskipToEndOfLine)
    - [`com.google.gson.stream.JsonReader.skipTo`](#JsonReaderskipTo)
    - [`com.google.gson.stream.JsonReader.toString`](#JsonReadertoString)
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
    - [`com.google.gson.stream.JsonReader.getPath`](#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.getPath`](#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](#JsonReadergetPreviousPath)
    - [`com.google.gson.stream.JsonReader.readEscapeCharacter`](#JsonReaderreadEscapeCharacter)
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
    - [`com.google.gson.stream.JsonReader.consumeNonExecutePrefix`](#JsonReaderconsumeNonExecutePrefix)
    - [`com.google.gson.stream.JsonReader.promoteNameToValue`](#JsonReaderpromoteNameToValue)
- **Extends/Implements**:
    - `Closeable`

**Methods**

---
#### JsonReader\.JsonReader<!-- {{#callable:com.google.gson.stream.JsonReader.JsonReader}} -->
The `JsonReader` constructor initializes a new instance of the `JsonReader` class with a specified `Reader` input, ensuring the input is not null.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `Reader` object that provides the input stream from which JSON data will be read.
- **Control Flow**:
    - The constructor takes a `Reader` object as an argument.
    - It uses `Objects.requireNonNull` to check that the `Reader` object is not null, throwing a `NullPointerException` with the message "in == null" if it is null.
    - The `Reader` object is then assigned to the instance variable `this.in`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `JsonReader` class.
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.setLenient<!-- {{#callable:com.google.gson.stream.JsonReader.setLenient}} -->
The `setLenient` method sets the strictness level of the `JsonReader` to either `LENIENT` or `LEGACY_STRICT` based on the boolean input.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `lenient`: A boolean value indicating whether the reader should be lenient (`true`) or not (`false`).
- **Control Flow**:
    - The method checks the value of the `lenient` parameter.
    - If `lenient` is `true`, it calls [`setStrictness`](#JsonReadersetStrictness) with `Strictness.LENIENT`.
    - If `lenient` is `false`, it calls [`setStrictness`](#JsonReadersetStrictness) with `Strictness.LEGACY_STRICT`.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.setStrictness`](#JsonReadersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.isLenient<!-- {{#callable:com.google.gson.stream.JsonReader.isLenient}} -->
The `isLenient` method checks if the current `JsonReader` instance is set to lenient mode.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method returns the result of comparing the `strictness` field with `Strictness.LENIENT`.
- **Output**:
    - A boolean value indicating whether the `JsonReader` is in lenient mode.
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.setStrictness<!-- {{#callable:com.google.gson.stream.JsonReader.setStrictness}} -->
The `setStrictness` method sets the strictness level of the `JsonReader` to the specified `Strictness` value.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `strictness`: An instance of the `Strictness` enum that determines the new strictness level for the `JsonReader`.
- **Control Flow**:
    - The method first checks if the `strictness` parameter is not null using `Objects.requireNonNull(strictness)`.
    - If the `strictness` parameter is not null, it assigns the `strictness` parameter to the `this.strictness` field of the `JsonReader` instance.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.getStrictness<!-- {{#callable:com.google.gson.stream.JsonReader.getStrictness}} -->
The `getStrictness` method returns the current strictness level of the `JsonReader`.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the `strictness` field.
- **Output**:
    - The method returns an instance of the `Strictness` enum, representing the current strictness level of the `JsonReader`.
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.setNestingLimit<!-- {{#callable:com.google.gson.stream.JsonReader.setNestingLimit}} -->
The `setNestingLimit` method sets the maximum number of JSON arrays or objects that can be open at the same time, throwing an exception if the limit is negative.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `limit`: An integer representing the new nesting limit for JSON arrays or objects.
- **Control Flow**:
    - Check if the provided limit is less than 0.
    - If the limit is less than 0, throw an IllegalArgumentException with a message indicating the invalid limit.
    - If the limit is valid, set the instance variable `nestingLimit` to the provided limit.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.getNestingLimit<!-- {{#callable:com.google.gson.stream.JsonReader.getNestingLimit}} -->
The `getNestingLimit` method returns the current nesting limit for JSON arrays or objects that can be open simultaneously in the `JsonReader`.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the `nestingLimit` field.
- **Output**:
    - The method returns an integer representing the nesting limit.
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.beginArray<!-- {{#callable:com.google.gson.stream.JsonReader.beginArray}} -->
The `beginArray` method consumes the next token from the JSON stream and verifies that it is the beginning of a new array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check the current state of the `peeked` variable; if it is `PEEKED_NONE`, call `doPeek()` to determine the next token.
    - If the next token is `PEEKED_BEGIN_ARRAY`, push `JsonScope.EMPTY_ARRAY` onto the stack, set the current path index to 0, and reset `peeked` to `PEEKED_NONE`.
    - If the next token is not `PEEKED_BEGIN_ARRAY`, throw an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError) with the message 'BEGIN_ARRAY'.
- **Output**:
    - The method does not return a value but modifies the internal state of the `JsonReader` to reflect the start of a new array in the JSON stream.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.push`](#JsonReaderpush)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.endArray<!-- {{#callable:com.google.gson.stream.JsonReader.endArray}} -->
The `endArray` method checks if the current JSON token is the end of an array and updates the internal state accordingly, or throws an error if it is not.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method starts by checking the value of the `peeked` variable.
    - If `peeked` is `PEEKED_NONE`, it calls `doPeek()` to determine the next token.
    - If the next token is `PEEKED_END_ARRAY`, it decrements `stackSize`, increments the last index in `pathIndices`, and resets `peeked` to `PEEKED_NONE`.
    - If the next token is not `PEEKED_END_ARRAY`, it throws an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError) with the message "END_ARRAY".
- **Output**:
    - The method does not return a value but may throw an `IOException` if an error occurs during token reading.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.beginObject<!-- {{#callable:com.google.gson.stream.JsonReader.beginObject}} -->
The `beginObject` method consumes the next token from the JSON stream and asserts that it is the beginning of a new object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method checks the current state of the `peeked` variable.
    - If `peeked` is `PEEKED_NONE`, it calls `doPeek()` to determine the next token.
    - If the next token is `PEEKED_BEGIN_OBJECT`, it pushes `JsonScope.EMPTY_OBJECT` onto the stack and resets `peeked` to `PEEKED_NONE`.
    - If the next token is not `PEEKED_BEGIN_OBJECT`, it throws an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError) with the message "BEGIN_OBJECT".
- **Output**:
    - The method does not return a value but modifies the internal state of the `JsonReader` to reflect the beginning of a new JSON object.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.push`](#JsonReaderpush)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.endObject<!-- {{#callable:com.google.gson.stream.JsonReader.endObject}} -->
The `endObject` method consumes the next token from the JSON stream and asserts that it is the end of the current object, updating internal state accordingly.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check the current state of the `peeked` variable; if it is `PEEKED_NONE`, call `doPeek()` to determine the next token.
    - If the next token is `PEEKED_END_OBJECT`, decrement the `stackSize`, nullify the last path name for garbage collection, increment the path index, and reset `peeked` to `PEEKED_NONE`.
    - If the next token is not `PEEKED_END_OBJECT`, throw an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError) with the message 'END_OBJECT'.
- **Output**:
    - The method does not return a value but updates the internal state of the `JsonReader` object.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.hasNext<!-- {{#callable:com.google.gson.stream.JsonReader.hasNext}} -->
The `hasNext` method checks if there are more elements to read in the current JSON array or object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method first checks the value of the `peeked` variable.
    - If `peeked` is `PEEKED_NONE`, it calls the [`doPeek`](#JsonReaderdoPeek) method to determine the next token.
    - The method then returns `true` if the next token is not `PEEKED_END_OBJECT`, `PEEKED_END_ARRAY`, or `PEEKED_EOF`, indicating that there are more elements to read.
- **Output**:
    - A boolean value indicating whether there are more elements to read in the current JSON structure.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.peek<!-- {{#callable:com.google.gson.stream.JsonReader.peek}} -->
The `peek` method returns the type of the next JSON token without consuming it.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `peeked` variable is `PEEKED_NONE`; if so, call `doPeek()` to determine the next token type.
    - Use a switch statement on the `peeked` value to determine the type of the next JSON token.
    - Return the corresponding `JsonToken` based on the `peeked` value, such as `BEGIN_OBJECT`, `END_OBJECT`, `BEGIN_ARRAY`, `END_ARRAY`, `NAME`, `BOOLEAN`, `NULL`, `STRING`, `NUMBER`, or `END_DOCUMENT`.
    - If the `peeked` value does not match any known token type, throw an `AssertionError`.
- **Output**:
    - Returns a `JsonToken` representing the type of the next token in the JSON stream.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.doPeek<!-- {{#callable:com.google.gson.stream.JsonReader.doPeek}} -->
The `doPeek` method analyzes the current JSON parsing context and determines the next token type to be processed.
- **Modifiers**: ``
- **Inputs**: None
- **Control Flow**:
    - The method starts by checking the current state of the JSON parsing stack to determine the context (e.g., empty array, non-empty array, empty object, etc.).
    - Depending on the context, it performs different actions such as updating the stack, checking for expected characters (like commas or colons), and handling lenient parsing cases.
    - It uses a switch-case structure to handle different characters encountered in the JSON stream, such as ']', '}', ',', ':', etc., and throws syntax errors for unexpected characters.
    - The method also checks for the end of the document and handles cases where the JSON reader is closed.
    - If none of the specific cases match, it attempts to identify keywords or numbers in the JSON stream and sets the appropriate peeked value.
    - Finally, it returns the determined peeked value, which indicates the type of the next JSON token.
- **Output**:
    - The method returns an integer representing the type of the next JSON token to be processed.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextNonWhitespace`](#JsonReadernextNonWhitespace)
    - [`com.google.gson.stream.JsonReader.checkLenient`](#JsonReadercheckLenient)
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
    - [`com.google.gson.stream.JsonReader.isLiteral`](#JsonReaderisLiteral)
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
    - [`com.google.gson.stream.JsonReader.consumeNonExecutePrefix`](#JsonReaderconsumeNonExecutePrefix)
    - [`com.google.gson.stream.JsonReader.peekKeyword`](#JsonReaderpeekKeyword)
    - [`com.google.gson.stream.JsonReader.peekNumber`](#JsonReaderpeekNumber)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.peekKeyword<!-- {{#callable:com.google.gson.stream.JsonReader.peekKeyword}} -->
The `peekKeyword` method attempts to identify and match a JSON keyword ('true', 'false', or 'null') from the current position in the buffer, considering the strictness mode, and returns a corresponding constant if successful.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method starts by checking the first character at the current buffer position to determine which keyword ('true', 'false', or 'null') it might match.
    - If the character is 't', 'f', or 'n' (case-insensitive), it sets the corresponding keyword, its uppercase version, and the peeking constant.
    - If the character does not match any of these, it returns `PEEKED_NONE`.
    - It checks if uppercase keywords are allowed based on the strictness mode.
    - The method then verifies if the subsequent characters in the buffer match the chosen keyword, considering case sensitivity based on the strictness mode.
    - If the buffer does not contain enough characters, it attempts to fill the buffer and checks again.
    - If the keyword is followed by a literal character, it returns `PEEKED_NONE` to avoid partial matches.
    - If a complete keyword is matched, it updates the position, sets the `peeked` variable to the corresponding constant, and returns it.
- **Output**:
    - Returns an integer constant representing the matched keyword (`PEEKED_TRUE`, `PEEKED_FALSE`, `PEEKED_NULL`) or `PEEKED_NONE` if no keyword is matched.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
    - [`com.google.gson.stream.JsonReader.isLiteral`](#JsonReaderisLiteral)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.peekNumber<!-- {{#callable:com.google.gson.stream.JsonReader.peekNumber}} -->
The `peekNumber` method attempts to parse a number from the current position in the buffer and returns a token indicating the type of number found or if no valid number is found.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Initialize local variables for buffer, position, limit, value, negative flag, fitsInLong flag, last character type, and index.
    - Enter a loop to iterate over characters in the buffer to parse a number.
    - Check if the current position plus index equals the limit, and if so, attempt to fill the buffer with more characters.
    - Switch on the current character to handle different cases: '-', '+', 'e', 'E', '.', and digits, updating the state accordingly.
    - If a non-digit character is encountered that is not part of a literal, break out of the loop.
    - After the loop, determine if a valid number was parsed and set the appropriate peeked token and value.
    - Return the peeked token indicating the type of number found or PEEKED_NONE if no valid number was found.
- **Output**:
    - An integer token indicating the type of number found (PEEKED_LONG, PEEKED_NUMBER) or PEEKED_NONE if no valid number is found.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
    - [`com.google.gson.stream.JsonReader.isLiteral`](#JsonReaderisLiteral)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.isLiteral<!-- {{#callable:com.google.gson.stream.JsonReader.isLiteral}} -->
The `isLiteral` method determines if a given character is considered a literal in the context of JSON parsing.
- **Modifiers**: `private`
- **Inputs**:
    - `c`: A character to be evaluated for its literal status.
- **Control Flow**:
    - The method uses a switch statement to check the character against a set of non-literal characters such as '/', '\', ';', '#', '=', '{', '}', '[', ']', ':', ',', and whitespace characters.
    - If the character matches any of these non-literal characters, the method returns false, indicating it is not a literal.
    - For certain characters ('/', '\', ';', '#', '='), the method calls `checkLenient()` before falling through to return false.
    - If the character does not match any of the specified non-literal characters, the method returns true, indicating it is a literal.
- **Output**:
    - A boolean value indicating whether the character is a literal (true) or not (false).
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.checkLenient`](#JsonReadercheckLenient)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextName<!-- {{#callable:com.google.gson.stream.JsonReader.nextName}} -->
The `nextName` method retrieves the next JSON property name from the input stream, handling different quoting styles, and updates the internal state accordingly.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check the current state of `peeked`; if it is `PEEKED_NONE`, call `doPeek()` to determine the next token type.
    - Based on the value of `peeked`, determine if the next name is unquoted, single-quoted, or double-quoted, and call the appropriate method ([`nextUnquotedValue`](#JsonReadernextUnquotedValue) or [`nextQuotedValue`](#JsonReadernextQuotedValue)) to retrieve the name.
    - If the token is not a valid name type, throw an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError).
    - Reset `peeked` to `PEEKED_NONE` after retrieving the name.
    - Store the retrieved name in the `pathNames` array at the current stack level.
    - Return the retrieved name.
- **Output**:
    - Returns the next JSON property name as a `String`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.nextUnquotedValue`](#JsonReadernextUnquotedValue)
    - [`com.google.gson.stream.JsonReader.nextQuotedValue`](#JsonReadernextQuotedValue)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextString<!-- {{#callable:com.google.gson.stream.JsonReader.nextString}} -->
The `nextString` method retrieves the next JSON token as a string, handling various token types and updating the reader's state accordingly.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `peeked` variable is `PEEKED_NONE`; if so, call `doPeek()` to determine the next token type.
    - Based on the value of `peeked`, determine the type of the next token and retrieve its string representation:
    - - If `PEEKED_UNQUOTED`, call `nextUnquotedValue()` to get the string.
    - - If `PEEKED_SINGLE_QUOTED` or `PEEKED_DOUBLE_QUOTED`, call `nextQuotedValue()` with the appropriate quote character to get the string.
    - - If `PEEKED_BUFFERED`, use the `peekedString` value and set `peekedString` to null.
    - - If `PEEKED_LONG`, convert `peekedLong` to a string using `Long.toString()`.
    - - If `PEEKED_NUMBER`, create a new string from the buffer using `peekedNumberLength` and update `pos`.
    - If none of the above cases match, throw an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError) indicating a string was expected.
    - Reset `peeked` to `PEEKED_NONE` and increment the path index for the current stack level.
    - Return the resulting string.
- **Output**:
    - Returns the string representation of the next JSON token.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.nextUnquotedValue`](#JsonReadernextUnquotedValue)
    - [`com.google.gson.stream.JsonReader.nextQuotedValue`](#JsonReadernextQuotedValue)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextBoolean<!-- {{#callable:com.google.gson.stream.JsonReader.nextBoolean}} -->
The `nextBoolean` method reads the next JSON token from the input stream and returns it as a boolean value, throwing an exception if the token is not a boolean.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check the current state of the `peeked` variable; if it is `PEEKED_NONE`, call `doPeek()` to determine the next token.
    - If the token is `PEEKED_TRUE`, reset `peeked` to `PEEKED_NONE`, increment the path index, and return `true`.
    - If the token is `PEEKED_FALSE`, reset `peeked` to `PEEKED_NONE`, increment the path index, and return `false`.
    - If the token is neither `PEEKED_TRUE` nor `PEEKED_FALSE`, throw an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError) indicating that a boolean was expected.
- **Output**:
    - Returns a boolean value (`true` or `false`) based on the next JSON token.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextNull<!-- {{#callable:com.google.gson.stream.JsonReader.nextNull}} -->
The `nextNull` method consumes the next JSON token, ensuring it is a null, and updates the reader's state accordingly.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check the current state of the `peeked` variable; if it is `PEEKED_NONE`, call `doPeek()` to determine the next token.
    - If the next token is `PEEKED_NULL`, reset `peeked` to `PEEKED_NONE` and increment the path index for the current stack level.
    - If the next token is not `PEEKED_NULL`, throw an [`unexpectedTokenError`](#JsonReaderunexpectedTokenError) indicating that a null was expected.
- **Output**:
    - The method does not return a value but updates the internal state of the `JsonReader` to reflect the consumption of a null token.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextDouble<!-- {{#callable:com.google.gson.stream.JsonReader.nextDouble}} -->
The `nextDouble` method reads the next JSON token as a double value, handling various token types and ensuring strictness rules are followed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check the current peeked token; if none, call `doPeek()` to determine the next token type.
    - If the token is a long, reset the peeked state and return the long value as a double.
    - If the token is a number, extract the number as a string from the buffer and update the position.
    - If the token is a quoted or unquoted string, extract the value using [`nextQuotedValue`](#JsonReadernextQuotedValue) or [`nextUnquotedValue`](#JsonReadernextUnquotedValue).
    - If the token is not buffered, throw an error indicating an unexpected token for a double.
    - Parse the extracted string as a double and check for NaN or infinity if strictness is not lenient, throwing a syntax error if found.
    - Reset the peeked state and increment the path index before returning the parsed double value.
- **Output**:
    - Returns the next JSON token as a double value, or throws an exception if the token cannot be parsed as a double or violates strictness rules.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.nextQuotedValue`](#JsonReadernextQuotedValue)
    - [`com.google.gson.stream.JsonReader.nextUnquotedValue`](#JsonReadernextUnquotedValue)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextLong<!-- {{#callable:com.google.gson.stream.JsonReader.nextLong}} -->
The `nextLong` method reads the next JSON token as a long integer, handling various token types and ensuring precision is maintained.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check the current peeked token; if none, call `doPeek()` to determine the next token type.
    - If the token is a long, reset the peeked state and return the stored long value.
    - If the token is a number, convert the buffered number to a string and update the position.
    - For single, double quoted, or unquoted tokens, retrieve the value as a string and attempt to parse it as a long.
    - If parsing as a long fails, parse the string as a double, cast it to a long, and check for precision loss.
    - If precision is lost during casting, throw a `NumberFormatException`.
    - Reset the peeked state and update the path index before returning the result.
- **Output**:
    - Returns the next JSON token as a long integer, or throws an exception if the token cannot be parsed as a long.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.nextUnquotedValue`](#JsonReadernextUnquotedValue)
    - [`com.google.gson.stream.JsonReader.nextQuotedValue`](#JsonReadernextQuotedValue)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextQuotedValue<!-- {{#callable:com.google.gson.stream.JsonReader.nextQuotedValue}} -->
The `nextQuotedValue` method reads a quoted string from the JSON input, handling escape sequences and ensuring proper termination of the string.
- **Modifiers**: `private`
- **Inputs**:
    - `quote`: A character representing the quote type (either single or double quote) that encloses the string to be read.
- **Control Flow**:
    - Initialize a local buffer and a StringBuilder to construct the result string.
    - Enter a loop to process characters from the buffer until the quoted string is fully read.
    - Within the loop, iterate over the buffer to find the end of the quoted string or handle escape sequences.
    - If a control character is found in strict mode, throw a syntax error.
    - If the closing quote is found, return the constructed string.
    - If an escape character is found, read the escape sequence and append the result to the StringBuilder.
    - If a newline character is found, update the line number and line start position.
    - If the buffer is exhausted without finding the closing quote, attempt to fill the buffer with more data.
    - If the buffer cannot be filled and the string is unterminated, throw a syntax error.
- **Output**:
    - Returns the string value enclosed by the specified quote character, with escape sequences processed.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
    - [`com.google.gson.stream.JsonReader.readEscapeCharacter`](#JsonReaderreadEscapeCharacter)
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextUnquotedValue<!-- {{#callable:com.google.gson.stream.JsonReader.nextUnquotedValue}} -->
The `nextUnquotedValue` method reads and returns the next unquoted string value from the JSON input stream, handling buffer management and leniency checks.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `StringBuilder` to null and an integer `i` to 0.
    - Enter a labeled while loop `findNonLiteralCharacter` to find the next non-literal character.
    - Within the loop, iterate over the buffer starting from the current position `pos` and increment `i` until a non-literal character is found or the buffer limit is reached.
    - Check for specific characters like '/', '\', ';', '#', '=', '{', '}', '[', ']', ':', ',', ' ', '\t', '\f', '\r', '\n' and break the loop if any are found, calling `checkLenient()` for certain characters.
    - If `i` is less than the buffer length, attempt to fill the buffer with more data; if successful, continue the loop, otherwise break.
    - If the value is too long for the buffer, initialize the `StringBuilder` if it is null, append the current buffer content to it, update `pos`, reset `i`, and attempt to fill the buffer again.
    - After exiting the loop, determine the result string: if `builder` is null, create a new string from the buffer; otherwise, append the remaining buffer content to `builder` and convert it to a string.
    - Update `pos` by adding `i` and return the result string.
- **Output**:
    - Returns a `String` representing the next unquoted value from the JSON input stream.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.checkLenient`](#JsonReadercheckLenient)
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.skipQuotedValue<!-- {{#callable:com.google.gson.stream.JsonReader.skipQuotedValue}} -->
The `skipQuotedValue` method skips over a quoted string in the JSON input, handling escape sequences and line breaks, and throws an error if the string is not properly terminated.
- **Modifiers**: `private`
- **Inputs**:
    - `quote`: A `char` representing the quote character (either single or double quote) that marks the beginning and end of the quoted string to be skipped.
- **Control Flow**:
    - Initialize local variables `p` and `l` to `pos` and `limit` respectively to optimize inner-loop field access.
    - Enter a do-while loop that continues as long as `fillBuffer(1)` returns true, indicating more data is available.
    - Within the loop, iterate over the buffer from position `p` to `l`.
    - For each character `c` in the buffer, check if it matches the `quote` character; if so, update `pos` to `p` and return, indicating the end of the quoted string has been found.
    - If `c` is a backslash (`\`), call `readEscapeCharacter()` to handle escape sequences, update `p` and `l` to `pos` and `limit` respectively, and continue the loop.
    - If `c` is a newline character (`\n`), increment `lineNumber` and update `lineStart` to `p`.
    - If the end of the buffer is reached without finding the closing quote, update `pos` to `p` and attempt to fill the buffer with more data.
    - If the loop exits without finding a closing quote, throw a [`syntaxError`](#JsonReadersyntaxError) indicating an unterminated string.
- **Output**:
    - The method does not return a value but updates the `pos` field to the position after the closing quote if the quoted string is successfully skipped.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.readEscapeCharacter`](#JsonReaderreadEscapeCharacter)
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.skipUnquotedValue<!-- {{#callable:com.google.gson.stream.JsonReader.skipUnquotedValue}} -->
The `skipUnquotedValue` method skips over an unquoted JSON value in the input stream until it encounters a delimiter or whitespace.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Initialize a loop that continues as long as `fillBuffer(1)` returns true.
    - Within the loop, initialize an integer `i` to 0 and iterate over the buffer starting from the current position `pos`.
    - For each character in the buffer, check if it is a delimiter or whitespace (e.g., '/', '\', ';', '#', '=', '{', '}', '[', ']', ':', ',', ' ', '\t', '\f', '\r', '\n').
    - If a delimiter or whitespace is found, update `pos` by adding `i` and return from the method.
    - If no delimiter or whitespace is found, increment `i` and continue checking the next character.
    - If the end of the buffer is reached without finding a delimiter or whitespace, update `pos` by adding `i` and attempt to fill the buffer again.
- **Output**:
    - The method does not return any value; it modifies the `pos` field to skip over the unquoted value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.checkLenient`](#JsonReadercheckLenient)
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextInt<!-- {{#callable:com.google.gson.stream.JsonReader.nextInt}} -->
The `nextInt` method reads the next JSON token as an integer, handling various formats and ensuring no precision is lost during conversion.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `peeked` value is `PEEKED_NONE`; if so, call `doPeek()` to determine the next token type.
    - If the token is `PEEKED_LONG`, cast `peekedLong` to an `int` and check for precision loss; if none, return the result.
    - If the token is `PEEKED_NUMBER`, extract the number as a string from the buffer and update the position.
    - If the token is a quoted or unquoted string (`PEEKED_SINGLE_QUOTED`, `PEEKED_DOUBLE_QUOTED`, `PEEKED_UNQUOTED`), parse it as an integer; if parsing fails, attempt to parse it as a double.
    - If the token is not an integer or convertible to one, throw an unexpected token error.
    - If parsed as a double, cast to an `int` and check for precision loss; if none, return the result.
- **Output**:
    - Returns the next JSON token as an integer, or throws an exception if the token cannot be converted to an integer without precision loss.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
    - [`com.google.gson.stream.JsonReader.nextUnquotedValue`](#JsonReadernextUnquotedValue)
    - [`com.google.gson.stream.JsonReader.nextQuotedValue`](#JsonReadernextQuotedValue)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.close<!-- {{#callable:com.google.gson.stream.JsonReader.close}} -->
The `close` method closes the JSON reader by resetting its state and closing the underlying input stream.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Set the `peeked` variable to `PEEKED_NONE` to reset the peeked state.
    - Set the first element of the `stack` array to `JsonScope.CLOSED` to indicate the reader is closed.
    - Set `stackSize` to 1 to reset the stack size.
    - Call the `close` method on the `in` object to close the underlying input stream.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.skipValue<!-- {{#callable:com.google.gson.stream.JsonReader.skipValue}} -->
The `skipValue` method skips over the next JSON value in the stream, including any nested structures, without consuming it.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a counter `count` to 0 to track nested structures.
    - Enter a do-while loop that continues as long as `count` is greater than 0.
    - Check the current `peeked` value; if it is `PEEKED_NONE`, call `doPeek()` to determine the next token.
    - Use a switch statement to handle different token types:
    - For `PEEKED_BEGIN_ARRAY` and `PEEKED_BEGIN_OBJECT`, push the corresponding empty scope onto the stack and increment `count`.
    - For `PEEKED_END_ARRAY` and `PEEKED_END_OBJECT`, decrement the stack size and `count`; for `PEEKED_END_OBJECT`, also clear the last path name if `count` is 0.
    - For `PEEKED_UNQUOTED`, `PEEKED_SINGLE_QUOTED`, and `PEEKED_DOUBLE_QUOTED`, call `skipUnquotedValue()` or `skipQuotedValue()` to skip the value.
    - For `PEEKED_UNQUOTED_NAME`, `PEEKED_SINGLE_QUOTED_NAME`, and `PEEKED_DOUBLE_QUOTED_NAME`, skip the name and set the path name to "<skipped>" if `count` is 0.
    - For `PEEKED_NUMBER`, increment the position by `peekedNumberLength`.
    - For `PEEKED_EOF`, exit the method as there is nothing more to skip.
    - Reset `peeked` to `PEEKED_NONE` after handling each token.
    - After exiting the loop, increment the path index for the current stack size.
- **Output**:
    - The method does not return any value; it modifies the internal state of the `JsonReader` to skip the current JSON value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.push`](#JsonReaderpush)
    - [`com.google.gson.stream.JsonReader.skipUnquotedValue`](#JsonReaderskipUnquotedValue)
    - [`com.google.gson.stream.JsonReader.skipQuotedValue`](#JsonReaderskipQuotedValue)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.push<!-- {{#callable:com.google.gson.stream.JsonReader.push}} -->
The `push` method adds a new element to the stack while ensuring the stack does not exceed a predefined nesting limit and dynamically resizing the stack if necessary.
- **Modifiers**: `private`
- **Inputs**:
    - `newTop`: An integer representing the new element to be added to the stack.
- **Control Flow**:
    - Check if the current stack size minus one is greater than or equal to the nesting limit; if so, throw a `MalformedJsonException`.
    - If the stack size equals the length of the stack array, double the size of the stack, `pathIndices`, and `pathNames` arrays using `Arrays.copyOf`.
    - Add the `newTop` element to the stack and increment the stack size.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.fillBuffer<!-- {{#callable:com.google.gson.stream.JsonReader.fillBuffer}} -->
The `fillBuffer` method attempts to fill the internal buffer with at least a specified minimum number of characters from the input stream, handling byte order marks if present.
- **Modifiers**: `private`
- **Inputs**:
    - `minimum`: The minimum number of characters that need to be available in the buffer after the method execution.
- **Control Flow**:
    - The method starts by adjusting the `lineStart` and `limit` variables based on the current `pos` position in the buffer.
    - If there are remaining characters in the buffer (`limit != pos`), it shifts the existing characters to the start of the buffer.
    - The `pos` is reset to 0, and the method enters a loop to read characters from the input stream into the buffer.
    - In each iteration, it reads characters into the buffer starting from the current `limit` position up to the buffer's capacity.
    - If this is the first read and a byte order mark (BOM) is detected at the start of the buffer, it adjusts the `pos`, `lineStart`, and `minimum` to account for the BOM.
    - The loop continues until the buffer contains at least the specified `minimum` number of characters or the end of the stream is reached.
    - If the buffer is filled with at least `minimum` characters, the method returns `true`; otherwise, it returns `false`.
- **Output**:
    - A boolean value indicating whether the buffer was successfully filled with at least the specified minimum number of characters.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.read`](../internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderread)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.nextNonWhitespace<!-- {{#callable:com.google.gson.stream.JsonReader.nextNonWhitespace}} -->
The `nextNonWhitespace` method reads the next non-whitespace character from the input buffer, handling comments and EOF conditions.
- **Modifiers**: `private`
- **Inputs**:
    - `throwOnEof`: A boolean indicating whether to throw an EOFException if the end of the input is reached.
- **Control Flow**:
    - Initialize local variables `p` and `l` to represent the current position and limit of the buffer.
    - Enter a loop to process characters from the buffer.
    - If the current position `p` equals the limit `l`, attempt to fill the buffer and update `p` and `l`.
    - Read the character at the current position `p` and increment `p`.
    - If the character is a newline, increment the line number and update the line start position.
    - If the character is a space, carriage return, or tab, continue to the next iteration of the loop.
    - If the character is a forward slash, check for comments and handle them appropriately, updating `p` and `l` as needed.
    - If the character is a hash, skip to the end of the line, updating `p` and `l`.
    - If none of the above conditions are met, set the position `pos` to `p` and return the character.
    - If the end of the input is reached and `throwOnEof` is true, throw an EOFException.
    - If the end of the input is reached and `throwOnEof` is false, return -1.
- **Output**:
    - Returns the next non-whitespace character as an integer, or -1 if the end of the input is reached and `throwOnEof` is false.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
    - [`com.google.gson.stream.JsonReader.checkLenient`](#JsonReadercheckLenient)
    - [`com.google.gson.stream.JsonReader.skipTo`](#JsonReaderskipTo)
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
    - [`com.google.gson.stream.JsonReader.skipToEndOfLine`](#JsonReaderskipToEndOfLine)
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.checkLenient<!-- {{#callable:com.google.gson.stream.JsonReader.checkLenient}} -->
The `checkLenient` method verifies if the JSON reader is set to lenient mode and throws an exception if it is not.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Check if the `strictness` field is not equal to `Strictness.LENIENT`.
    - If the condition is true, throw a `MalformedJsonException` with a message indicating that lenient mode should be enabled.
- **Output**:
    - The method does not return any value but may throw a `MalformedJsonException` if the JSON reader is not in lenient mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.skipToEndOfLine<!-- {{#callable:com.google.gson.stream.JsonReader.skipToEndOfLine}} -->
The `skipToEndOfLine` method advances the reading position to the end of the current line in the buffer, updating line-related metadata as necessary.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method enters a while loop that continues as long as the current position `pos` is less than `limit` or the buffer can be filled with at least one character using `fillBuffer(1)`.
    - Within the loop, it reads the current character from the buffer and increments the position `pos`.
    - If the character is a newline character '\n', it increments the `lineNumber`, updates `lineStart` to the current position, and breaks out of the loop.
    - If the character is a carriage return '\r', it breaks out of the loop without updating the line number or line start.
- **Output**:
    - The method does not return any value, but it updates the `pos`, `lineNumber`, and `lineStart` fields of the class.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.skipTo<!-- {{#callable:com.google.gson.stream.JsonReader.skipTo}} -->
The `skipTo` method searches for a specified string within a buffer, updating line numbers and positions as it progresses, and returns true if the string is found.
- **Modifiers**: `private`
- **Inputs**:
    - `toFind`: A string to search for in the buffer; it must not contain a newline character.
- **Control Flow**:
    - Calculate the length of the string `toFind`.
    - Enter a loop that continues as long as the current position plus the length of `toFind` is less than or equal to the buffer limit, or until the buffer is filled with enough characters.
    - Within the loop, check if the current character in the buffer is a newline; if so, increment the line number and update the line start position, then continue to the next iteration.
    - For each character in `toFind`, check if it matches the corresponding character in the buffer; if any character does not match, continue to the outer loop to check the next position in the buffer.
    - If all characters match, return true, indicating that the string `toFind` was found in the buffer.
    - If the loop completes without finding the string, return false.
- **Output**:
    - Returns a boolean value: true if the string `toFind` is found in the buffer, false otherwise.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.toString<!-- {{#callable:com.google.gson.stream.JsonReader.toString}} -->
The `toString` method returns a string representation of the class name followed by its location string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getClass().getSimpleName()` to retrieve the simple name of the class.
    - It then calls `locationString()` to get the location string of the object.
    - The method concatenates the class name and location string and returns the result.
- **Output**:
    - A string that combines the class's simple name and its location string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.locationString<!-- {{#callable:com.google.gson.stream.JsonReader.locationString}} -->
The `locationString` method returns a string describing the current line, column, and JSON path of the reader.
- **Modifiers**: ``
- **Inputs**: None
- **Control Flow**:
    - Calculate the line number by adding 1 to `lineNumber`.
    - Calculate the column number by subtracting `lineStart` from `pos` and adding 1.
    - Concatenate the line, column, and path information into a formatted string.
- **Output**:
    - A string indicating the current line, column, and path in the JSON being read.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.getPath`](#JsonReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.getPath<!-- {{#callable:com.google.gson.stream.JsonReader.getPath}} -->
The `getPath` method constructs a JSONPath string representing the current or previous location in a JSON document based on the stack of JSON scopes.
- **Modifiers**: `private`
- **Inputs**:
    - `usePreviousPath`: A boolean flag indicating whether to use the previous path index for the last array element.
- **Control Flow**:
    - Initialize a StringBuilder with the root symbol '$'.
    - Iterate over the stack of JSON scopes up to the current stack size.
    - For each scope, determine the type of JSON structure (array, object, document) and append the appropriate path notation to the StringBuilder.
    - For arrays, append the current or previous index in square brackets, depending on the `usePreviousPath` flag.
    - For objects, append a dot followed by the property name if available.
    - Ignore document and closed scopes.
    - Throw an AssertionError if an unknown scope value is encountered.
- **Output**:
    - A string representing the JSONPath to the current or previous location in the JSON document.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.getPath<!-- {{#callable:com.google.gson.stream.JsonReader.getPath}} -->
The [`getPath`](#JsonReadergetPath) method returns the JSONPath to the current location in the JSON document.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls another method `getPath(boolean usePreviousPath)` with the argument `false`.
- **Output**:
    - A `String` representing the JSONPath to the current location in the JSON document.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.getPath`](#JsonReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.getPreviousPath<!-- {{#callable:com.google.gson.stream.JsonReader.getPreviousPath}} -->
The `getPreviousPath` method returns the JSON path to the previous or current location in the JSON document.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`getPath`](#JsonReadergetPath) method with the argument `true` to indicate that it should return the path to the previous location.
    - The [`getPath`](#JsonReadergetPath) method constructs a JSONPath string by iterating over the `stack` array, which represents the current state of the JSON reader.
    - For each element in the stack, it appends the appropriate path segment to the result string, adjusting the index for arrays if `usePreviousPath` is true.
    - The constructed path string is returned.
- **Output**:
    - A `String` representing the JSON path to the previous or current location in the JSON document.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.getPath`](#JsonReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.readEscapeCharacter<!-- {{#callable:com.google.gson.stream.JsonReader.readEscapeCharacter}} -->
The `readEscapeCharacter` method reads and returns the character represented by an escape sequence in a JSON string, handling various escape cases and throwing errors for malformed sequences.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Check if the current position `pos` is at the limit and attempt to fill the buffer; throw an error if unsuccessful.
    - Read the next character from the buffer and switch on its value to determine the escape sequence.
    - For a Unicode escape ('u'), ensure there are at least 4 more characters in the buffer, parse the next 4 characters as a hexadecimal number, and return the corresponding character.
    - For specific escape characters ('t', 'b', 'n', 'r', 'f'), return their corresponding control characters ('\t', '\b', '\n', '\r', '\f').
    - For a newline character, increment the line number and update the line start position, unless in strict mode, where an error is thrown.
    - For single quote ('\''), throw an error in strict mode; otherwise, fall through to return the character.
    - For double quote ('"'), backslash ('\\'), and forward slash ('/'), return the character itself.
    - Throw an error for any other character, indicating an invalid escape sequence.
- **Output**:
    - Returns the character represented by the escape sequence.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
    - [`com.google.gson.stream.JsonReader.syntaxError`](#JsonReadersyntaxError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.syntaxError<!-- {{#callable:com.google.gson.stream.JsonReader.syntaxError}} -->
The `syntaxError` method throws a `MalformedJsonException` with a detailed error message including the current location and a troubleshooting URL.
- **Modifiers**: `private`
- **Inputs**:
    - `message`: A `String` representing the error message to be included in the exception.
- **Control Flow**:
    - The method constructs a new `MalformedJsonException` by concatenating the provided `message`, the current location string obtained from `locationString()`, and a troubleshooting URL generated by `TroubleshootingGuide.createUrl("malformed-json")`.
    - The method then throws the constructed `MalformedJsonException`.
- **Output**:
    - The method does not return any value as it always throws an exception.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../internal/TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.unexpectedTokenError<!-- {{#callable:com.google.gson.stream.JsonReader.unexpectedTokenError}} -->
The `unexpectedTokenError` method generates an `IllegalStateException` with a detailed error message when an unexpected JSON token is encountered.
- **Modifiers**: `private`
- **Inputs**:
    - `expected`: A `String` representing the expected JSON token.
- **Control Flow**:
    - The method calls `peek()` to get the current JSON token.
    - It checks if the peeked token is `JsonToken.NULL` to determine the appropriate troubleshooting ID.
    - It constructs an error message using the expected token, the actual token from `peek()`, the current location from `locationString()`, and a troubleshooting URL from `TroubleshootingGuide.createUrl()`.
    - It returns a new `IllegalStateException` with the constructed error message.
- **Output**:
    - An `IllegalStateException` with a message detailing the expected and actual JSON tokens, the location of the error, and a troubleshooting URL.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.locationString`](#JsonReaderlocationString)
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../internal/TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.consumeNonExecutePrefix<!-- {{#callable:com.google.gson.stream.JsonReader.consumeNonExecutePrefix}} -->
The `consumeNonExecutePrefix` method checks for and consumes a specific non-executable prefix in a JSON stream to prevent security vulnerabilities.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method begins by skipping any leading whitespace using `nextNonWhitespace(true)` and then decrements the position `pos` by one.
    - It checks if there are at least 5 characters available in the buffer; if not, it attempts to fill the buffer with `fillBuffer(5)`.
    - If the buffer does not contain the required 5 characters, the method returns early.
    - The method then checks if the next five characters in the buffer match the sequence ")]}\'\n".
    - If the sequence matches, it increments the position `pos` by 5 to consume the prefix.
- **Output**:
    - The method does not return any value; it modifies the internal state of the `JsonReader` by potentially advancing the position `pos`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextNonWhitespace`](#JsonReadernextNonWhitespace)
    - [`com.google.gson.stream.JsonReader.fillBuffer`](#JsonReaderfillBuffer)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)


---
#### JsonReader\.promoteNameToValue<!-- {{#callable:com.google.gson.stream.JsonReader.promoteNameToValue}} -->
The [`promoteNameToValue`](../internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpromoteNameToValue) method promotes a JSON name token to a value token in a `JsonReader`.
- **Modifiers**: `public`
- **Inputs**:
    - `reader`: An instance of `JsonReader` from which the name token is to be promoted to a value token.
- **Control Flow**:
    - Check if the `reader` is an instance of `JsonTreeReader`; if so, call its [`promoteNameToValue`](../internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpromoteNameToValue) method and return.
    - Retrieve the current peeked token from the `reader`.
    - If the peeked token is `PEEKED_NONE`, call `doPeek()` to determine the next token.
    - If the peeked token is `PEEKED_DOUBLE_QUOTED_NAME`, set the peeked token to `PEEKED_DOUBLE_QUOTED`.
    - If the peeked token is `PEEKED_SINGLE_QUOTED_NAME`, set the peeked token to `PEEKED_SINGLE_QUOTED`.
    - If the peeked token is `PEEKED_UNQUOTED_NAME`, set the peeked token to `PEEKED_UNQUOTED`.
    - If none of the above conditions are met, throw an unexpected token error indicating that a name was expected.
- **Output**:
    - The method does not return a value but modifies the state of the `reader` by changing the peeked token from a name to a value.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.promoteNameToValue`](../internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpromoteNameToValue)
    - [`com.google.gson.stream.JsonReader.doPeek`](#JsonReaderdoPeek)
    - [`com.google.gson.stream.JsonReader.unexpectedTokenError`](#JsonReaderunexpectedTokenError)
- **See also**: [`com.google.gson.stream.JsonReader`](#JsonReader)  (Base Class)



