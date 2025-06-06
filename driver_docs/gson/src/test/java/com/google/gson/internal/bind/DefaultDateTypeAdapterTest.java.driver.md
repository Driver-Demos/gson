# Purpose
The `DefaultDateTypeAdapterTest` class is a unit test suite designed to validate the functionality of the `DefaultDateTypeAdapter` class within the Google Gson library. This test class focuses on ensuring that date formatting and parsing are handled correctly across different locales and time zones. It includes tests for various date formats, including ISO 8601, and checks the behavior of the adapter when dealing with null values, unexpected tokens, and invalid date patterns. The tests also verify that the adapter consistently uses the default time zone and locale settings, and they ensure that the serialization and deserialization processes produce expected results.

The class is structured to cover a broad range of scenarios related to date handling, making it a comprehensive test suite for the `DefaultDateTypeAdapter`. It uses the JUnit framework for defining test cases and employs assertions from the Google Truth library to validate expected outcomes. The tests are organized to simulate different environmental settings, such as changing the default locale and time zone, to ensure that the adapter's behavior remains consistent and predictable. This test suite is crucial for maintaining the reliability of date serialization and deserialization in applications using the Gson library, particularly in environments with diverse locale and time zone configurations.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.common.truth.Truth.assertThat`
- `com.google.common.truth.Truth.assertWithMessage`
- `org.junit.Assert.assertThrows`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.internal.bind.DefaultDateTypeAdapter.DateType`
- `com.google.gson.reflect.TypeToken`
- `java.io.IOException`
- `java.text.DateFormat`
- `java.text.SimpleDateFormat`
- `java.util.Date`
- `java.util.Locale`
- `java.util.TimeZone`
- `org.junit.Test`


# Classes

---
### DefaultDateTypeAdapterTest<!-- {{#class:com.google.gson.internal.bind.DefaultDateTypeAdapterTest}} -->
- **Modifiers**: `public`
- **Description**: The `DefaultDateTypeAdapterTest` class is a unit test suite designed to validate the functionality of the `DefaultDateTypeAdapter` class in the Gson library. It includes various test methods to ensure that date formatting and parsing are consistent across different locales and time zones, and that the adapter correctly handles ISO 8601 date formats, null values, and unexpected tokens. The tests also verify that the adapter can serialize and deserialize dates using custom date patterns and the default Gson date format.
- **Methods**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testFormattingInEnUs`](#DefaultDateTypeAdapterTesttestFormattingInEnUs)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testFormattingInFr`](#DefaultDateTypeAdapterTesttestFormattingInFr)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormattingAlwaysEmitsUsLocale`](#DefaultDateTypeAdapterTestassertFormattingAlwaysEmitsUsLocale)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testParsingDatesFormattedWithSystemLocale`](#DefaultDateTypeAdapterTesttestParsingDatesFormattedWithSystemLocale)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testParsingDatesFormattedWithUsLocale`](#DefaultDateTypeAdapterTesttestParsingDatesFormattedWithUsLocale)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testFormatUsesDefaultTimezone`](#DefaultDateTypeAdapterTesttestFormatUsesDefaultTimezone)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testDateDeserializationISO8601`](#DefaultDateTypeAdapterTesttestDateDeserializationISO8601)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testDatePattern`](#DefaultDateTypeAdapterTesttestDatePattern)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testInvalidDatePattern`](#DefaultDateTypeAdapterTesttestInvalidDatePattern)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testNullValue`](#DefaultDateTypeAdapterTesttestNullValue)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testUnexpectedToken`](#DefaultDateTypeAdapterTesttestUnexpectedToken)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testGsonDateFormat`](#DefaultDateTypeAdapterTesttestGsonDateFormat)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormatted`](#DefaultDateTypeAdapterTestassertFormatted)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertParsed`](#DefaultDateTypeAdapterTestassertParsed)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.toLiteral`](#DefaultDateTypeAdapterTesttoLiteral)

**Methods**

---
#### DefaultDateTypeAdapterTest\.testFormattingInEnUs<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testFormattingInEnUs}} -->
The `testFormattingInEnUs` method tests that date formatting in the US locale is consistent with expected patterns.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`assertFormattingAlwaysEmitsUsLocale`](#DefaultDateTypeAdapterTestassertFormattingAlwaysEmitsUsLocale) with `Locale.US` as the argument.
    - The [`assertFormattingAlwaysEmitsUsLocale`](#DefaultDateTypeAdapterTestassertFormattingAlwaysEmitsUsLocale) method sets the default time zone to UTC and the default locale to the provided locale (US in this case).
    - It then asserts that various date formats match expected patterns for the US locale.
    - Finally, it restores the original time zone and locale settings.
- **Output**:
    - The method does not return any output; it performs assertions to validate date formatting.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormattingAlwaysEmitsUsLocale`](#DefaultDateTypeAdapterTestassertFormattingAlwaysEmitsUsLocale)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testFormattingInFr<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testFormattingInFr}} -->
The `testFormattingInFr` method tests that date formatting in the French locale still emits a US locale format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`assertFormattingAlwaysEmitsUsLocale`](#DefaultDateTypeAdapterTestassertFormattingAlwaysEmitsUsLocale) with `Locale.FRANCE` as the argument.
    - The [`assertFormattingAlwaysEmitsUsLocale`](#DefaultDateTypeAdapterTestassertFormattingAlwaysEmitsUsLocale) method sets the default time zone to UTC and the default locale to the provided locale (French in this case).
    - It then performs a series of assertions to check that date formatting outputs match expected US locale patterns, regardless of the locale set.
    - Finally, it restores the original time zone and locale settings.
- **Output**:
    - The method does not return any value; it is a test method that asserts conditions.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormattingAlwaysEmitsUsLocale`](#DefaultDateTypeAdapterTestassertFormattingAlwaysEmitsUsLocale)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.assertFormattingAlwaysEmitsUsLocale<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormattingAlwaysEmitsUsLocale}} -->
The method `assertFormattingAlwaysEmitsUsLocale` verifies that date formatting is consistent with the US locale regardless of the system's default locale.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `locale`: The `Locale` object to temporarily set as the default locale for the duration of the test.
- **Control Flow**:
    - Store the current default time zone and locale.
    - Set the default time zone to UTC and the default locale to the provided `locale`.
    - Use [`assertFormatted`](#DefaultDateTypeAdapterTestassertFormatted) to check that various date formats match expected US locale patterns, accommodating minor differences between JDK versions.
    - In a `finally` block, restore the original default time zone and locale.
- **Output**:
    - The method does not return any value; it performs assertions to verify date formatting.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormatted`](#DefaultDateTypeAdapterTestassertFormatted)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapter.DateType.createAdapterFactory`](../../../../../../../main/java/com/google/gson/internal/bind/DefaultDateTypeAdapter.java.driver.md#DateTypecreateAdapterFactory)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testParsingDatesFormattedWithSystemLocale<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testParsingDatesFormattedWithSystemLocale}} -->
The method `testParsingDatesFormattedWithSystemLocale` tests the parsing of dates formatted with the system's locale settings, specifically using the French locale and UTC timezone.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Store the current default timezone and locale.
    - Set the default timezone to UTC and the default locale to France.
    - Create a new Date object representing the epoch time (January 1, 1970, 00:00:00 GMT).
    - Format this date using different date-time styles (MEDIUM, SHORT, LONG, FULL) and assert that the formatted strings can be parsed back to the original date using the appropriate date type adapters.
    - In the finally block, restore the original default timezone and locale.
- **Output**:
    - The method does not return any value; it performs assertions to verify correct date parsing.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertParsed`](#DefaultDateTypeAdapterTestassertParsed)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapter.DateType.createAdapterFactory`](../../../../../../../main/java/com/google/gson/internal/bind/DefaultDateTypeAdapter.java.driver.md#DateTypecreateAdapterFactory)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testParsingDatesFormattedWithUsLocale<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testParsingDatesFormattedWithUsLocale}} -->
The `testParsingDatesFormattedWithUsLocale` method tests the parsing of date strings formatted with the US locale using various date formats.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Store the current default time zone and locale.
    - Set the default time zone to UTC and the default locale to US.
    - Use [`assertParsed`](#DefaultDateTypeAdapterTestassertParsed) to verify that date strings in different formats are correctly parsed to the expected date object.
    - Finally, restore the original default time zone and locale.
- **Output**:
    - The method does not return any value; it performs assertions to validate date parsing.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertParsed`](#DefaultDateTypeAdapterTestassertParsed)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapter.DateType.createAdapterFactory`](../../../../../../../main/java/com/google/gson/internal/bind/DefaultDateTypeAdapter.java.driver.md#DateTypecreateAdapterFactory)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testFormatUsesDefaultTimezone<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testFormatUsesDefaultTimezone}} -->
The method `testFormatUsesDefaultTimezone` tests the date formatting and parsing functionality of the `DefaultDateTypeAdapter` class using the default timezone and locale settings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Store the current default timezone and locale in `defaultTimeZone` and `defaultLocale` variables.
    - Set the default timezone to 'America/Los_Angeles' and the default locale to `Locale.US`.
    - Use [`assertFormatted`](#DefaultDateTypeAdapterTestassertFormatted) to verify that the date is formatted correctly according to the `DefaultDateTypeAdapter.DEFAULT_STYLE_FACTORY`.
    - Use [`assertParsed`](#DefaultDateTypeAdapterTestassertParsed) to verify that the date string is parsed correctly according to the `DefaultDateTypeAdapter.DEFAULT_STYLE_FACTORY`.
    - In the `finally` block, restore the original default timezone and locale settings.
- **Output**:
    - The method does not return any value; it performs assertions to validate date formatting and parsing.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormatted`](#DefaultDateTypeAdapterTestassertFormatted)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertParsed`](#DefaultDateTypeAdapterTestassertParsed)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testDateDeserializationISO8601<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testDateDeserializationISO8601}} -->
The `testDateDeserializationISO8601` method tests the deserialization of ISO 8601 formatted date strings using a default date type adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `TypeAdapterFactory` using `DefaultDateTypeAdapter.DEFAULT_STYLE_FACTORY`.
    - Call [`assertParsed`](#DefaultDateTypeAdapterTestassertParsed) with various ISO 8601 formatted date strings and the initialized `adapterFactory` to verify correct deserialization.
- **Output**:
    - The method does not return any value; it performs assertions to validate date deserialization.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertParsed`](#DefaultDateTypeAdapterTestassertParsed)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testDatePattern<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testDatePattern}} -->
The `testDatePattern` method tests the serialization of a `Date` object to a JSON string using a specific date pattern and verifies the output against the expected formatted date string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a date pattern string `yyyy-MM-dd`.
    - Create a `TypeAdapter<Date>` using the [`dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter) method with a factory created by `DateType.DATE.createAdapterFactory(pattern)`.
    - Instantiate a `DateFormat` object using `SimpleDateFormat` with the defined pattern.
    - Create a `Date` object representing the current date and time.
    - Serialize the `Date` object to a JSON string using the `dateTypeAdapter`.
    - Assert that the serialized JSON string is equal to the expected formatted date string using `assertThat`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the date serialization.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapter.DateType.createAdapterFactory`](../../../../../../../main/java/com/google/gson/internal/bind/DefaultDateTypeAdapter.java.driver.md#DateTypecreateAdapterFactory)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.toLiteral`](#DefaultDateTypeAdapterTesttoLiteral)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testInvalidDatePattern<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testInvalidDatePattern}} -->
The `testInvalidDatePattern` method tests that creating a date adapter with an invalid date pattern throws an `IllegalArgumentException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that an `IllegalArgumentException` is thrown.
    - It attempts to create a date adapter factory using an invalid date pattern string 'I am a bad Date pattern....'.
- **Output**:
    - The method does not return any value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapter.DateType.createAdapterFactory`](../../../../../../../main/java/com/google/gson/internal/bind/DefaultDateTypeAdapter.java.driver.md#DateTypecreateAdapterFactory)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testNullValue<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testNullValue}} -->
The `testNullValue` method tests the serialization and deserialization of null values using a `TypeAdapter` for `Date` objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapter<Date>` is created using the [`dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter) method with `DefaultDateTypeAdapter.DEFAULT_STYLE_FACTORY` as the argument.
    - The method asserts that deserializing the JSON string "null" using the adapter results in a null `Date` object.
    - The method asserts that serializing a null `Date` object using the adapter results in the JSON string "null".
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the correct handling of null values in JSON serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testUnexpectedToken<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testUnexpectedToken}} -->
The `testUnexpectedToken` method tests that an `IllegalStateException` is thrown when a JSON object is incorrectly parsed as a date string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapter<Date>` is created using the [`dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter) method with the `DefaultDateTypeAdapter.DEFAULT_STYLE_FACTORY`.
    - The `assertThrows` method is used to verify that an `IllegalStateException` is thrown when the [`fromJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson) method of the adapter is called with a JSON object (`"{}"`).
    - The exception message is checked to ensure it starts with "Expected a string but was BEGIN_OBJECT".
- **Output**:
    - The method does not return a value but asserts that an `IllegalStateException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.testGsonDateFormat<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.testGsonDateFormat}} -->
The `testGsonDateFormat` method tests the serialization and deserialization of `Date` objects using Gson with a specific date format and timezone handling.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Store the original default timezone.
    - Set the default timezone to UTC.
    - Create a `Gson` instance with a date format of `yyyy-MM-dd HH:mm z`.
    - Create a `Date` object representing the epoch time (0 milliseconds from 1970-01-01T00:00:00Z).
    - Serialize the `Date` object to JSON and assert that it matches the expected UTC format.
    - Deserialize a JSON date string with PST timezone to a `Date` object and assert the time is correct (8 hours ahead of UTC).
    - Serialize the deserialized `Date` object again and assert that it matches the expected UTC format after deserialization.
    - Restore the original default timezone in a `finally` block.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of date serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.dateAdapter<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.dateAdapter}} -->
The `dateAdapter` method creates and returns a `TypeAdapter` for `Date` objects using a provided `TypeAdapterFactory`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `adapterFactory`: A `TypeAdapterFactory` used to create a `TypeAdapter` for `Date` objects.
- **Control Flow**:
    - Invoke the [`create`](../../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactorycreate) method on the `adapterFactory` with a new `Gson` instance and a `TypeToken` for `Date` to obtain a `TypeAdapter<Date>`.
    - Use `assertThat` to ensure the created `TypeAdapter<Date>` is not null.
    - Return the `TypeAdapter<Date>` instance.
- **Output**:
    - A `TypeAdapter<Date>` instance created using the provided `TypeAdapterFactory`.
- **Functions called**:
    - [`com.google.gson.TypeAdapterFactory.create`](../../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactorycreate)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.assertFormatted<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertFormatted}} -->
The `assertFormatted` method verifies that a JSON representation of a `Date` object matches a specified formatted pattern using a given `TypeAdapterFactory`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `formattedPattern`: A string representing the expected formatted pattern of the date in JSON.
    - `adapterFactory`: A `TypeAdapterFactory` used to create a `TypeAdapter` for `Date` objects.
- **Control Flow**:
    - Create a `TypeAdapter<Date>` using the provided `adapterFactory`.
    - Convert a `Date` object initialized to epoch time (0) to its JSON representation using the `TypeAdapter`.
    - Assert that the JSON representation matches the expected `formattedPattern` by converting the pattern to a literal string and using the `assertThat` method.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the JSON format.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.reflect.TypeToken.matches`](../../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenmatches)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.toLiteral`](#DefaultDateTypeAdapterTesttoLiteral)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.assertParsed<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.assertParsed}} -->
The `assertParsed` method verifies that a given date string can be correctly parsed into a `Date` object representing the epoch time (January 1, 1970, 00:00:00 GMT) using a specified `TypeAdapterFactory`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `date`: A string representing the date to be parsed.
    - `adapterFactory`: A `TypeAdapterFactory` used to create a `TypeAdapter` for parsing the date string.
- **Control Flow**:
    - Create a `TypeAdapter<Date>` using the provided `adapterFactory`.
    - Parse the input `date` string into a `Date` object using the `TypeAdapter` and assert that it equals a `Date` object representing the epoch time.
    - Parse the ISO 8601 date string "1970-01-01T00:00:00Z" into a `Date` object using the `TypeAdapter` and assert that it equals a `Date` object representing the epoch time.
- **Output**:
    - The method does not return any value; it throws an assertion error if the parsed date does not match the expected epoch time.
- **Functions called**:
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.dateAdapter`](#DefaultDateTypeAdapterTestdateAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest.toLiteral`](#DefaultDateTypeAdapterTesttoLiteral)
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)


---
#### DefaultDateTypeAdapterTest\.toLiteral<!-- {{#callable:com.google.gson.internal.bind.DefaultDateTypeAdapterTest.toLiteral}} -->
The `toLiteral` method wraps a given string with double quotes to convert it into a string literal.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `s`: The input string that needs to be converted into a string literal.
- **Control Flow**:
    - Concatenate a double quote character '"' to the beginning of the input string `s`.
    - Concatenate another double quote character '"' to the end of the input string `s`.
- **Output**:
    - A new string that is the input string `s` wrapped in double quotes.
- **See also**: [`com.google.gson.internal.bind.DefaultDateTypeAdapterTest`](#DefaultDateTypeAdapterTest)  (Base Class)



