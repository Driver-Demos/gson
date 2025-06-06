# Purpose
The `SqlTypesGsonTest` Java class is a unit test suite designed to validate the serialization and deserialization of SQL date and time types using the Gson library. This code provides a focused functionality, specifically testing how `java.sql.Date`, `java.sql.Time`, and `java.sql.Timestamp` objects are converted to and from JSON strings. The class uses JUnit for structuring the tests, with setup and teardown methods to ensure consistent test environments by setting the default time zone and locale. The tests cover both default and custom date formats, ensuring that the Gson library correctly handles these SQL types under various conditions.

The class is organized into several test methods, each targeting specific aspects of SQL type handling. It includes tests for null serialization and deserialization, default serialization and deserialization of SQL dates, times, and timestamps, and custom serialization formats. The use of `GsonBuilder` to specify date formats highlights the flexibility of Gson in handling different date representations. The tests also address known issues, as referenced by the comments linking to specific issues in the Gson project. This class does not define public APIs or external interfaces but serves as an internal validation tool to ensure the robustness of SQL type handling within the Gson library.
# Imports and Dependencies

---
- `com.google.gson.internal.sql`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.functional.DefaultTypeAdaptersTest`
- `java.sql.Time`
- `java.sql.Timestamp`
- `java.util.Locale`
- `java.util.TimeZone`
- `org.junit.After`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### SqlTypesGsonTest<!-- {{#class:com.google.gson.internal.sql.SqlTypesGsonTest}} -->
- **Modifiers**: `public`
- **Description**: The `SqlTypesGsonTest` class is a JUnit test suite designed to verify the serialization and deserialization of SQL date and time types using the Gson library. It includes tests for handling `java.sql.Date`, `Time`, and `Timestamp` objects, ensuring that null values are correctly processed and that the default and custom date formats are properly serialized and deserialized. The class also manages the system's default time zone and locale settings to ensure consistent test results.
- **Fields**:
    - `gson`: `Gson` An instance of the Gson library used for serialization and deserialization in the tests.
    - `oldTimeZone`: `TimeZone` Stores the original default time zone to restore after tests are completed.
    - `oldLocale`: `Locale` Stores the original default locale to restore after tests are completed.
- **Methods**:
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.setUp`](#SqlTypesGsonTestsetUp)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.tearDown`](#SqlTypesGsonTesttearDown)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlDateSerialization`](#SqlTypesGsonTesttestDefaultSqlDateSerialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlDateDeserialization`](#SqlTypesGsonTesttestDefaultSqlDateDeserialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testSqlDateSerialization`](#SqlTypesGsonTesttestSqlDateSerialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimeSerialization`](#SqlTypesGsonTesttestDefaultSqlTimeSerialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimeDeserialization`](#SqlTypesGsonTesttestDefaultSqlTimeDeserialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimestampSerialization`](#SqlTypesGsonTesttestDefaultSqlTimestampSerialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimestampDeserialization`](#SqlTypesGsonTesttestDefaultSqlTimestampDeserialization)
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testTimestampSerialization`](#SqlTypesGsonTesttestTimestampSerialization)

**Methods**

---
#### SqlTypesGsonTest\.setUp<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.setUp}} -->
The setUp method initializes the test environment by setting the default time zone and locale, and creating a new Gson instance.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Store the current default time zone in the oldTimeZone variable.
    - Set the default time zone to 'America/Los_Angeles'.
    - Store the current default locale in the oldLocale variable.
    - Set the default locale to Locale.US.
    - Initialize the gson variable with a new Gson instance.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.tearDown<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.tearDown}} -->
The `tearDown` method restores the default time zone and locale settings to their original values after a test is executed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with `@After`, indicating it runs after each test method in the class.
    - It sets the default time zone to the value stored in `oldTimeZone`.
    - It sets the default locale to the value stored in `oldLocale`.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testNullSerializationAndDeserialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testNullSerializationAndDeserialization}} -->
The method [`testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization) tests the serialization and deserialization of null values for SQL date/time classes using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization) with `java.sql.Date.class` as an argument.
    - It then calls [`testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization) with `Time.class` as an argument.
    - Finally, it calls [`testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization) with `Timestamp.class` as an argument.
- **Output**:
    - The method does not return any value; it is a test method that verifies the behavior of null serialization and deserialization for specific classes.
- **Functions called**:
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testNullSerializationAndDeserialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testNullSerializationAndDeserialization}} -->
The method [`testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization) tests the serialization and deserialization of null values for a given class type using Gson.
- **Modifiers**: `private`
- **Inputs**:
    - `c`: The class type for which null serialization and deserialization is to be tested.
- **Control Flow**:
    - The method calls `DefaultTypeAdaptersTest.testNullSerializationAndDeserialization` with the `gson` instance and the provided class type `c`.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.sql.SqlTypesGsonTest.testNullSerializationAndDeserialization`](#SqlTypesGsonTesttestNullSerializationAndDeserialization)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testDefaultSqlDateSerialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlDateSerialization}} -->
The method `testDefaultSqlDateSerialization` tests the serialization of a `java.sql.Date` object to a JSON string using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `java.sql.Date` object with a specific timestamp (1259875082000L).
    - Serialize the `java.sql.Date` object to a JSON string using the `gson.toJson` method.
    - Assert that the resulting JSON string is equal to the expected string `"Dec 3, 2009"`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testDefaultSqlDateDeserialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlDateDeserialization}} -->
The method `testDefaultSqlDateDeserialization` tests the deserialization of a JSON string representing a date into a `java.sql.Date` object using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a date, `'Dec 3, 2009'`, is defined.
    - The JSON string is deserialized into a `java.sql.Date` object using the `gson.fromJson` method.
    - The deserialized date is then compared to the expected date (December 3, 2009) using the `DefaultTypeAdaptersTest.assertEqualsDate` method.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsDate`](../../functional/DefaultTypeAdaptersTest.java.driver.md#DefaultTypeAdaptersTestassertEqualsDate)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testSqlDateSerialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testSqlDateSerialization}} -->
The `testSqlDateSerialization` method tests the serialization and deserialization of `java.sql.Date` objects using Gson with a specific date format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Store the current default time zone and locale.
    - Set the default time zone to UTC and the default locale to US.
    - Create a `java.sql.Date` object initialized to the epoch time (0L).
    - Create a `Gson` instance with a date format of 'yyyy-MM-dd'.
    - Serialize the `java.sql.Date` object to JSON using the `Gson` instance and assert that the result is '"1970-01-01"'.
    - Deserialize the JSON string '"1970-01-01"' back to a `java.sql.Date` object and assert that its time value is 0.
    - In the `finally` block, restore the original default time zone and locale.
- **Output**:
    - The method does not return any value but performs assertions to verify correct serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testDefaultSqlTimeSerialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimeSerialization}} -->
The method `testDefaultSqlTimeSerialization` tests the serialization of a `java.sql.Time` object to a JSON string using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Time` object is instantiated with a specific timestamp (1259875082000L).
    - The `gson.toJson` method is called to serialize the `Time` object into a JSON string.
    - An assertion is made to check if the serialized JSON string is equal to the expected time format `"01:18:02 PM"`.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the serialization result.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testDefaultSqlTimeDeserialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimeDeserialization}} -->
The method `testDefaultSqlTimeDeserialization` tests the deserialization of a JSON string representing a time into a `java.sql.Time` object using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a time, `'1:18:02 PM'`, is defined.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `Time` object.
    - The `DefaultTypeAdaptersTest.assertEqualsTime` method is used to assert that the deserialized `Time` object has the expected hour, minute, and second values (13, 18, 2).
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsTime`](../../functional/DefaultTypeAdaptersTest.java.driver.md#DefaultTypeAdaptersTestassertEqualsTime)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testDefaultSqlTimestampSerialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimestampSerialization}} -->
The method tests the serialization of a SQL Timestamp object to a JSON string using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Timestamp object is created with a specific time value (1259875082000L).
    - The Timestamp object is serialized to a JSON string using the Gson instance.
    - An assertion checks if the serialized JSON string matches the expected date-time format, allowing for variations in the JDK version.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the serialization format.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testDefaultSqlTimestampDeserialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testDefaultSqlTimestampDeserialization}} -->
The method `testDefaultSqlTimestampDeserialization` tests the deserialization of a SQL `Timestamp` from a JSON string using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a date and time is defined as `'Dec 3, 2009 1:18:02 PM'`.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `Timestamp` object.
    - The [`assertEqualsDate`](../../functional/DefaultTypeAdaptersTest.java.driver.md#DefaultTypeAdaptersTestassertEqualsDate) method from `DefaultTypeAdaptersTest` is used to verify that the deserialized `Timestamp` has the expected year, month, and day values (2009, 11, 3).
    - The [`assertEqualsTime`](../../functional/DefaultTypeAdaptersTest.java.driver.md#DefaultTypeAdaptersTestassertEqualsTime) method from `DefaultTypeAdaptersTest` is used to verify that the deserialized `Timestamp` has the expected hour, minute, and second values (13, 18, 2).
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsDate`](../../functional/DefaultTypeAdaptersTest.java.driver.md#DefaultTypeAdaptersTestassertEqualsDate)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsTime`](../../functional/DefaultTypeAdaptersTest.java.driver.md#DefaultTypeAdaptersTestassertEqualsTime)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)


---
#### SqlTypesGsonTest\.testTimestampSerialization<!-- {{#callable:com.google.gson.internal.sql.SqlTypesGsonTest.testTimestampSerialization}} -->
The `testTimestampSerialization` method tests the serialization and deserialization of a `Timestamp` object to and from JSON using a specific date format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method starts by saving the current default `TimeZone` and `Locale` settings.
    - It then sets the default `TimeZone` to UTC and the default `Locale` to US.
    - A `Timestamp` object is created with the epoch time (0L).
    - A `Gson` object is instantiated with a date format of `yyyy-MM-dd`.
    - The `Timestamp` object is serialized to a JSON string using the `Gson` object.
    - An assertion checks that the serialized JSON string is equal to `"1970-01-01"`.
    - The JSON string `"1970-01-01"` is deserialized back into a `Timestamp` object.
    - An assertion checks that the deserialized `Timestamp` object's time is equal to 0.
    - Finally, the method restores the original `TimeZone` and `Locale` settings in a `finally` block.
- **Output**:
    - The method does not return any value but asserts the correctness of the serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.internal.sql.SqlTypesGsonTest`](#SqlTypesGsonTest)  (Base Class)



