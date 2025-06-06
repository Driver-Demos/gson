# Purpose
The [`MalformedJsonException`](#MalformedJsonExceptionMalformedJsonException) class is a custom exception in the `com.google.gson.stream` package, designed to handle errors encountered when parsing malformed JSON data. It extends `IOException`, indicating that it is related to input/output operations, specifically those involving JSON parsing. This class provides narrow functionality, as it is specifically tailored to signal syntax errors in JSON data that cannot be ignored unless the `Strictness#LENIENT` mode is set in a `JsonReader`. The class offers three constructors, allowing for flexibility in exception handling by accepting a message, a throwable cause, or both, thus providing detailed context about the parsing error.
# Imports and Dependencies

---
- `com.google.gson.stream`
- `com.google.gson.Strictness`
- `java.io.IOException`


# Classes

---
### MalformedJsonException<!-- {{#class:com.google.gson.stream.MalformedJsonException}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `MalformedJsonException` class is a specialized exception that extends `IOException` and is thrown when a JSON reader encounters malformed JSON data. It provides constructors to create an exception instance with a message, a cause, or both, and is part of the `com.google.gson.stream` package. This exception is particularly useful in scenarios where JSON syntax errors need to be reported, and it can be used in conjunction with the `JsonReader` class to handle such errors, with the option to ignore certain syntax errors by setting the reader's strictness to `LENIENT`.
- **Fields**:
    - `serialVersionUID`: `long` A unique identifier for serialization, ensuring class consistency during deserialization.
- **Methods**:
    - [`com.google.gson.stream.MalformedJsonException.MalformedJsonException`](#MalformedJsonExceptionMalformedJsonException)
    - [`com.google.gson.stream.MalformedJsonException.MalformedJsonException`](#MalformedJsonExceptionMalformedJsonException)
    - [`com.google.gson.stream.MalformedJsonException.MalformedJsonException`](#MalformedJsonExceptionMalformedJsonException)
- **Extends/Implements**:
    - `IOException`

**Methods**

---
#### MalformedJsonException\.MalformedJsonException<!-- {{#callable:com.google.gson.stream.MalformedJsonException.MalformedJsonException}} -->
The `MalformedJsonException` constructor initializes a new instance of the exception with a specified error message.
- **Modifiers**: `public`
- **Inputs**:
    - `msg`: A string containing the error message that describes the malformed JSON issue.
- **Control Flow**:
    - The constructor takes a single string argument `msg`.
    - It calls the superclass `IOException` constructor with the provided `msg` to initialize the exception with the specified error message.
- **Output**:
    - An instance of `MalformedJsonException` initialized with the provided error message.
- **See also**: [`com.google.gson.stream.MalformedJsonException`](#MalformedJsonException)  (Base Class)


---
#### MalformedJsonException\.MalformedJsonException<!-- {{#callable:com.google.gson.stream.MalformedJsonException.MalformedJsonException}} -->
The MalformedJsonException constructor initializes a new instance of the exception with a specified error message and a cause.
- **Modifiers**: `public`
- **Inputs**:
    - `msg`: A string representing the error message associated with the exception.
    - `throwable`: A Throwable object representing the cause of the exception.
- **Control Flow**:
    - The constructor calls the superclass (IOException) constructor with the provided message and throwable as arguments.
- **Output**:
    - A new instance of MalformedJsonException is created with the specified message and cause.
- **See also**: [`com.google.gson.stream.MalformedJsonException`](#MalformedJsonException)  (Base Class)


---
#### MalformedJsonException\.MalformedJsonException<!-- {{#callable:com.google.gson.stream.MalformedJsonException.MalformedJsonException}} -->
The MalformedJsonException constructor initializes a new instance of the exception with a specified cause.
- **Modifiers**: `public`
- **Inputs**:
    - `throwable`: A Throwable object that represents the cause of the exception.
- **Control Flow**:
    - The constructor calls the superclass (IOException) constructor with the provided Throwable object.
- **Output**:
    - A new instance of MalformedJsonException initialized with the specified cause.
- **See also**: [`com.google.gson.stream.MalformedJsonException`](#MalformedJsonException)  (Base Class)



