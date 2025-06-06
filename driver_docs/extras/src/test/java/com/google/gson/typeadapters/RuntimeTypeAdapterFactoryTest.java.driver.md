# Purpose
The `RuntimeTypeAdapterFactoryTest` Java file is a comprehensive test suite designed to validate the functionality of the `RuntimeTypeAdapterFactory` class within the context of the Gson library. This test class is part of the `com.google.gson.typeadapters` package and utilizes JUnit for testing. The primary focus of the tests is to ensure that the `RuntimeTypeAdapterFactory` can correctly serialize and deserialize objects of different subtypes of a base class, [`BillingInstrument`](#BillingInstrumentBillingInstrument), which includes [`CreditCard`](#CreditCardCreditCard) and [`BankTransfer`](#BankTransferBankTransfer) as its subtypes. The tests cover various scenarios, such as registering subtypes, handling null values, and managing serialization and deserialization errors when subtypes are not registered or when there are naming collisions.

The file defines several test methods that check the behavior of the `RuntimeTypeAdapterFactory` in different situations, such as recognizing subtypes, handling null inputs, and ensuring unique type and label registrations. It also tests the serialization and deserialization processes, including error handling for missing type fields and unregistered subtypes. The test cases use assertions to verify expected outcomes, ensuring that the `RuntimeTypeAdapterFactory` behaves as intended. Additionally, the file includes inner static classes representing the [`BillingInstrument`](#BillingInstrumentBillingInstrument) and its subtypes, which are used in the test cases to simulate real-world usage scenarios. This test suite is crucial for maintaining the reliability and correctness of the `RuntimeTypeAdapterFactory` functionality within the Gson library.
# Imports and Dependencies

---
- `com.google.gson.typeadapters`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonParseException`
- `com.google.gson.TypeAdapterFactory`
- `org.junit.Test`


# Classes

---
### RuntimeTypeAdapterFactoryTest<!-- {{#class:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `RuntimeTypeAdapterFactoryTest` class is a comprehensive test suite designed to validate the functionality of the `RuntimeTypeAdapterFactory` in the Gson library, which facilitates polymorphic serialization and deserialization of objects. It includes various test cases to ensure correct behavior when registering subtypes, handling null values, managing duplicate types and labels, and dealing with missing type fields during serialization and deserialization. The tests cover scenarios such as recognizing subtypes, handling base types, and ensuring that exceptions are thrown for invalid operations, thereby ensuring robustness and correctness of the type adapter factory's implementation.
- **Methods**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testRuntimeTypeAdapter`](#RuntimeTypeAdapterFactoryTesttestRuntimeTypeAdapter)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testRuntimeTypeAdapterRecognizeSubtypes`](#RuntimeTypeAdapterFactoryTesttestRuntimeTypeAdapterRecognizeSubtypes)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testRuntimeTypeIsBaseType`](#RuntimeTypeAdapterFactoryTesttestRuntimeTypeIsBaseType)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullBaseType`](#RuntimeTypeAdapterFactoryTesttestNullBaseType)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullTypeFieldName`](#RuntimeTypeAdapterFactoryTesttestNullTypeFieldName)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullSubtype`](#RuntimeTypeAdapterFactoryTesttestNullSubtype)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullLabel`](#RuntimeTypeAdapterFactoryTesttestNullLabel)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDuplicateSubtype`](#RuntimeTypeAdapterFactoryTesttestDuplicateSubtype)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDuplicateLabel`](#RuntimeTypeAdapterFactoryTesttestDuplicateLabel)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDeserializeMissingTypeField`](#RuntimeTypeAdapterFactoryTesttestDeserializeMissingTypeField)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDeserializeMissingSubtype`](#RuntimeTypeAdapterFactoryTesttestDeserializeMissingSubtype)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testSerializeMissingSubtype`](#RuntimeTypeAdapterFactoryTesttestSerializeMissingSubtype)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testSerializeCollidingTypeFieldName`](#RuntimeTypeAdapterFactoryTesttestSerializeCollidingTypeFieldName)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testSerializeWrappedNullValue`](#RuntimeTypeAdapterFactoryTesttestSerializeWrappedNullValue)

**Methods**

---
#### RuntimeTypeAdapterFactoryTest\.testRuntimeTypeAdapter<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testRuntimeTypeAdapter}} -->
The `testRuntimeTypeAdapter` method tests the serialization and deserialization of a `CreditCard` object using a `RuntimeTypeAdapterFactory` with Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `RuntimeTypeAdapterFactory` for `BillingInstrument` is created and a subtype `CreditCard` is registered.
    - A `Gson` instance is created with the registered type adapter factory.
    - A `CreditCard` object is instantiated with owner name 'Jesse' and CVV 234.
    - The `CreditCard` object is serialized to JSON using the `Gson` instance and checked against the expected JSON string.
    - A JSON string representing a `CreditCard` is deserialized back into a `BillingInstrument` object using the `Gson` instance.
    - Assertions are made to verify that the deserialized object's `ownerName` is 'Jesse' and that it is an instance of `CreditCard`.
- **Output**:
    - The method does not return any value but performs assertions to verify correct serialization and deserialization behavior.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testRuntimeTypeAdapterRecognizeSubtypes<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testRuntimeTypeAdapterRecognizeSubtypes}} -->
The method tests the ability of a RuntimeTypeAdapterFactory to recognize and handle subtypes during JSON serialization and deserialization without explicit type specification.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A RuntimeTypeAdapterFactory for BillingInstrument is created with recognizeSubtypes() and registers CreditCard as a subtype.
    - A Gson instance is created with the RuntimeTypeAdapterFactory registered.
    - A CreditCard object is instantiated and serialized to JSON using Gson, expecting the output to include the type information.
    - The JSON string is deserialized back into a BillingInstrument object, which is then checked to ensure it retains the correct ownerName and is an instance of CreditCard.
- **Output**:
    - The method does not return a value but asserts that the serialized JSON matches the expected format and that the deserialized object is of the correct type and has the correct properties.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.recognizeSubtypes`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryrecognizeSubtypes)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testRuntimeTypeIsBaseType<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testRuntimeTypeIsBaseType}} -->
The method tests serialization and deserialization of a base type using Gson with a RuntimeTypeAdapterFactory.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A RuntimeTypeAdapterFactory is created for the BillingInstrument class and registers BillingInstrument as a subtype.
    - A Gson instance is created with the RuntimeTypeAdapterFactory registered.
    - A BillingInstrument object is instantiated with the owner name 'Jesse'.
    - The object is serialized to JSON and asserted to match the expected JSON string.
    - The JSON string is deserialized back into a BillingInstrument object.
    - The deserialized object's owner name is asserted to be 'Jesse'.
- **Output**:
    - The method does not return any value; it performs assertions to validate the serialization and deserialization process.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testNullBaseType<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullBaseType}} -->
The `testNullBaseType` method verifies that a `NullPointerException` is thrown when attempting to create a `RuntimeTypeAdapterFactory` with a null base type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `assertThrows` function to check that a `NullPointerException` is thrown.
    - It attempts to create a `RuntimeTypeAdapterFactory` by calling `RuntimeTypeAdapterFactory.of(null)`, which is expected to fail and throw the exception.
- **Output**:
    - The method does not return any value; it is a test method that asserts the occurrence of an exception.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testNullTypeFieldName<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullTypeFieldName}} -->
The `testNullTypeFieldName` method verifies that a `NullPointerException` is thrown when a `null` type field name is passed to the `RuntimeTypeAdapterFactory.of` method.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check that a `NullPointerException` is thrown.
    - It calls `RuntimeTypeAdapterFactory.of` with `BillingInstrument.class` and `null` as arguments.
    - The lambda expression `() -> RuntimeTypeAdapterFactory.of(BillingInstrument.class, null)` is executed to trigger the exception.
- **Output**:
    - The method does not return any value; it is a test method that asserts the occurrence of an exception.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testNullSubtype<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullSubtype}} -->
The `testNullSubtype` method tests that registering a null subtype with a `RuntimeTypeAdapterFactory` throws a `NullPointerException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `RuntimeTypeAdapterFactory` instance for the `BillingInstrument` class.
    - Use `assertThrows` to verify that calling [`registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype) with a null argument on the `RuntimeTypeAdapterFactory` instance throws a `NullPointerException`.
- **Output**:
    - The method does not return any value; it verifies that a `NullPointerException` is thrown when a null subtype is registered.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testNullLabel<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testNullLabel}} -->
The `testNullLabel` method tests that registering a subtype with a null label in a `RuntimeTypeAdapterFactory` throws a `NullPointerException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `RuntimeTypeAdapterFactory` for the `BillingInstrument` class.
    - Use `assertThrows` to verify that registering a `CreditCard` subtype with a null label throws a `NullPointerException`.
- **Output**:
    - The method does not return any value; it asserts that a `NullPointerException` is thrown.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testDuplicateSubtype<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDuplicateSubtype}} -->
The `testDuplicateSubtype` method tests that registering a duplicate subtype with a different label in a `RuntimeTypeAdapterFactory` throws an `IllegalArgumentException` with a specific message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `RuntimeTypeAdapterFactory` for the `BillingInstrument` class.
    - Register the `CreditCard` class as a subtype with the label 'CC'.
    - Attempt to register the `CreditCard` class again with a different label 'Visa', expecting an `IllegalArgumentException` to be thrown.
    - Verify that the exception message is 'types and labels must be unique'.
- **Output**:
    - The method does not return a value but asserts that an `IllegalArgumentException` is thrown with a specific message when a duplicate subtype is registered.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testDuplicateLabel<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDuplicateLabel}} -->
The `testDuplicateLabel` method tests that registering two subtypes with the same label in a `RuntimeTypeAdapterFactory` throws an `IllegalArgumentException` with a specific message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `RuntimeTypeAdapterFactory` for the `BillingInstrument` class.
    - Register the `CreditCard` class as a subtype with the label 'CC'.
    - Attempt to register the `BankTransfer` class as a subtype with the same label 'CC', expecting an `IllegalArgumentException`.
    - Capture the exception and assert that its message is 'types and labels must be unique'.
- **Output**:
    - The method does not return a value but asserts that an `IllegalArgumentException` is thrown with a specific message when duplicate labels are used.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testDeserializeMissingTypeField<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDeserializeMissingTypeField}} -->
The method `testDeserializeMissingTypeField` tests the deserialization of a JSON string into a `BillingInstrument` object when the required 'type' field is missing, expecting a `JsonParseException` to be thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapterFactory` is created for `BillingInstrument` and `CreditCard` using `RuntimeTypeAdapterFactory` and registered with a `Gson` instance.
    - The method attempts to deserialize a JSON string missing the 'type' field into a `BillingInstrument` object using `gson.fromJson`.
    - An `assertThrows` statement is used to verify that a `JsonParseException` is thrown during deserialization.
    - The exception message is checked to ensure it matches the expected message indicating the missing 'type' field.
- **Output**:
    - The method does not return a value but asserts that a `JsonParseException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.TypeAdapterFactory.create`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testDeserializeMissingSubtype<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testDeserializeMissingSubtype}} -->
The method `testDeserializeMissingSubtype` tests the deserialization of a JSON string into a `BillingInstrument` object when a required subtype is not registered, expecting a `JsonParseException` to be thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapterFactory` is created for `BillingInstrument` and registers only the `BankTransfer` subtype.
    - A `Gson` instance is created with the `billingAdapter` registered.
    - The method attempts to deserialize a JSON string representing a `CreditCard` into a `BillingInstrument` object using `gson.fromJson`.
    - An `assertThrows` statement is used to verify that a `JsonParseException` is thrown during deserialization.
    - The exception message is checked to ensure it indicates the missing registration of the `CreditCard` subtype.
- **Output**:
    - The method does not return a value but asserts that a `JsonParseException` is thrown with a specific error message.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.TypeAdapterFactory.create`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testSerializeMissingSubtype<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testSerializeMissingSubtype}} -->
The method `testSerializeMissingSubtype` tests the serialization process of a `CreditCard` object when its subtype is not registered, expecting a `JsonParseException` to be thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapterFactory` is created for `BillingInstrument` and a subtype `BankTransfer` is registered, but not `CreditCard`.
    - A `Gson` instance is created with the `billingAdapter` registered.
    - The method attempts to serialize a `CreditCard` object using `gson.toJson`, expecting a `JsonParseException` to be thrown.
    - The exception is caught and its message is asserted to be equal to a specific error message indicating the missing subtype registration.
- **Output**:
    - The method does not return a value but asserts that a `JsonParseException` is thrown with a specific error message.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.TypeAdapterFactory.create`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testSerializeCollidingTypeFieldName<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testSerializeCollidingTypeFieldName}} -->
The method `testSerializeCollidingTypeFieldName` tests the serialization of a `CreditCard` object using a `Gson` instance configured with a `RuntimeTypeAdapterFactory` that has a field name collision, expecting a `JsonParseException` to be thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapterFactory` is created using `RuntimeTypeAdapterFactory.of` with `BillingInstrument.class` and a type field name 'cvv', and `CreditCard.class` is registered as a subtype.
    - A `Gson` instance is created with the `billingAdapter` registered.
    - The method `assertThrows` is used to check that a `JsonParseException` is thrown when attempting to serialize a `CreditCard` object with the `Gson` instance.
    - The exception message is asserted to be equal to a specific string indicating the field name collision.
- **Output**:
    - The method does not return a value; it asserts that a `JsonParseException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.TypeAdapterFactory.create`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)


---
#### RuntimeTypeAdapterFactoryTest\.testSerializeWrappedNullValue<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.testSerializeWrappedNullValue}} -->
The method tests the serialization and deserialization of a wrapped null value using Gson with a custom type adapter factory.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapterFactory` is created using `RuntimeTypeAdapterFactory` for the `BillingInstrument` class, registering `CreditCard` and `BankTransfer` as subtypes.
    - A `Gson` instance is created with the custom type adapter factory registered.
    - A `BillingInstrumentWrapper` object is created with a `null` instrument and serialized to JSON using the `Gson` instance.
    - The serialized JSON is then deserialized back into a `BillingInstrumentWrapper` object.
    - An assertion checks that the `instrument` field of the deserialized object is `null`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify that the deserialized `instrument` is `null`.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](../../../../../../main/java/com/google/gson/typeadapters/RuntimeTypeAdapterFactory.java.driver.md#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.TypeAdapterFactory.create`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactorycreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest`](#RuntimeTypeAdapterFactoryTest)  (Base Class)



---
### BillingInstrumentWrapper<!-- {{#class:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrumentWrapper}} -->
- **Modifiers**: `static`
- **Description**: The `BillingInstrumentWrapper` class is a simple wrapper for the `BillingInstrument` class, providing a way to encapsulate a `BillingInstrument` object within another object, which can be useful for serialization or other operations that require a single object reference.
- **Fields**:
    - `instrument`: `BillingInstrument` Holds a reference to a `BillingInstrument` object.
- **Methods**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrumentWrapper.BillingInstrumentWrapper`](#BillingInstrumentWrapperBillingInstrumentWrapper)

**Methods**

---
#### BillingInstrumentWrapper\.BillingInstrumentWrapper<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrumentWrapper.BillingInstrumentWrapper}} -->
The `BillingInstrumentWrapper` constructor initializes a new instance of the `BillingInstrumentWrapper` class by assigning a given `BillingInstrument` object to its `instrument` field.
- **Inputs**:
    - `instrument`: A `BillingInstrument` object that is assigned to the `instrument` field of the `BillingInstrumentWrapper` instance.
- **Control Flow**:
    - The constructor takes a `BillingInstrument` object as a parameter.
    - It assigns the provided `BillingInstrument` object to the `instrument` field of the `BillingInstrumentWrapper` instance.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrumentWrapper`](#RuntimeTypeAdapterFactoryTest.BillingInstrumentWrapper)  (Base Class)



---
### BillingInstrument<!-- {{#class:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrument}} -->
- **Modifiers**: `static`
- **Description**: The `BillingInstrument` class represents a financial instrument associated with an owner, identified by the owner's name. It serves as a base class for more specific types of billing instruments, such as credit cards and bank transfers, in a type hierarchy used for serialization and deserialization with Gson.
- **Fields**:
    - `ownerName`: `String` A final string representing the name of the owner of the billing instrument.
- **Methods**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrument.BillingInstrument`](#BillingInstrumentBillingInstrument)

**Methods**

---
#### BillingInstrument\.BillingInstrument<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrument.BillingInstrument}} -->
The `BillingInstrument` constructor initializes a new instance of the `BillingInstrument` class with the specified owner's name.
- **Inputs**:
    - `ownerName`: A `String` representing the name of the owner of the billing instrument.
- **Control Flow**:
    - The constructor takes a single parameter `ownerName`.
    - It assigns the value of `ownerName` to the instance variable `this.ownerName`.
- **Output**:
    - The constructor does not return any value as it is used to initialize an object of the `BillingInstrument` class.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrument`](#RuntimeTypeAdapterFactoryTest.BillingInstrument)  (Base Class)



---
### CreditCard<!-- {{#class:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.CreditCard}} -->
- **Modifiers**: `static`
- **Description**: The `CreditCard` class is a subclass of `BillingInstrument` that represents a credit card with an associated CVV number. It extends the functionality of `BillingInstrument` by adding a field for the CVV, which is a security feature used in credit card transactions. The class includes a constructor that initializes the owner's name and the CVV number.
- **Fields**:
    - `cvv`: `int` An integer representing the CVV number of the credit card.
- **Methods**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.CreditCard.CreditCard`](#CreditCardCreditCard)
- **Extends/Implements**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrument`](#RuntimeTypeAdapterFactoryTest.BillingInstrument)

**Methods**

---
#### CreditCard\.CreditCard<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.CreditCard.CreditCard}} -->
The `CreditCard` constructor initializes a new instance of the `CreditCard` class with the specified owner name and CVV number.
- **Inputs**:
    - `ownerName`: A `String` representing the name of the credit card owner.
    - `cvv`: An `int` representing the CVV number of the credit card.
- **Control Flow**:
    - The constructor calls the superclass `BillingInstrument` constructor with `ownerName` to initialize the owner name.
    - The `cvv` field of the `CreditCard` instance is set to the provided `cvv` argument.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.CreditCard`](#RuntimeTypeAdapterFactoryTest.CreditCard)  (Base Class)



---
### BankTransfer<!-- {{#class:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BankTransfer}} -->
- **Modifiers**: `static`
- **Description**: The `BankTransfer` class is a subclass of `BillingInstrument` that represents a bank transfer payment method, encapsulating the bank account number associated with the transfer.
- **Fields**:
    - `bankAccount`: `int` An integer representing the bank account number associated with the bank transfer.
- **Methods**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BankTransfer.BankTransfer`](#BankTransferBankTransfer)
- **Extends/Implements**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BillingInstrument`](#RuntimeTypeAdapterFactoryTest.BillingInstrument)

**Methods**

---
#### BankTransfer\.BankTransfer<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BankTransfer.BankTransfer}} -->
The `BankTransfer` constructor initializes a new instance of the `BankTransfer` class with the specified owner name and bank account number.
- **Inputs**:
    - `ownerName`: A `String` representing the name of the owner of the bank transfer.
    - `bankAccount`: An `int` representing the bank account number associated with the bank transfer.
- **Control Flow**:
    - The constructor calls the superclass constructor with `ownerName` to initialize the inherited `ownerName` field.
    - The `bankAccount` field of the `BankTransfer` instance is set to the provided `bankAccount` value.
- **Output**:
    - This constructor does not return a value; it initializes a `BankTransfer` object.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactoryTest.BankTransfer`](#RuntimeTypeAdapterFactoryTest.BankTransfer)  (Base Class)



