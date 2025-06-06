# Purpose
The provided Java source code file defines a utility class named [`ReflectionHelper`](#ReflectionHelperReflectionHelper) within the `com.google.gson.internal.reflect` package. This class is part of the Gson library, which is used for converting Java objects to JSON and vice versa. The primary purpose of [`ReflectionHelper`](#ReflectionHelperReflectionHelper) is to facilitate reflection-based operations, particularly in making Java reflection objects such as fields, methods, and constructors accessible. It provides methods to handle accessibility issues that may arise due to Java's module system or visibility constraints, throwing a `JsonIOException` when such operations fail. Additionally, the class includes functionality to support Java records, a feature introduced in Java 14, by determining if a class is a record and retrieving record component information.

The [`ReflectionHelper`](#ReflectionHelperReflectionHelper) class is composed of several static methods and an internal abstraction for handling records, represented by the `RecordHelper` abstract class and its two concrete implementations: [`RecordSupportedHelper`](#RecordSupportedHelperRecordSupportedHelper) and `RecordNotSupportedHelper`. These implementations determine the behavior of the class based on whether the JVM supports records. The class also includes methods for generating human-readable descriptions of reflection objects, checking class modifiers, and handling exceptions related to illegal access. The class does not define public APIs or external interfaces but serves as an internal utility to enhance the Gson library's reflection capabilities, ensuring compatibility with different Java versions and environments.
# Imports and Dependencies

---
- `com.google.gson.internal.reflect`
- `com.google.gson.JsonIOException`
- `com.google.gson.internal.GsonBuildConfig`
- `com.google.gson.internal.TroubleshootingGuide`
- `java.lang.reflect.AccessibleObject`
- `java.lang.reflect.Constructor`
- `java.lang.reflect.Field`
- `java.lang.reflect.Method`
- `java.lang.reflect.Modifier`


# Classes

---
### ReflectionHelper<!-- {{#class:com.google.gson.internal.reflect.ReflectionHelper}} -->
- **Modifiers**: `public`
- **Description**: The `ReflectionHelper` class provides utility methods for handling Java reflection, particularly focusing on making inaccessible objects accessible, describing accessible objects, and handling Java records. It includes methods to make fields, methods, and constructors accessible, describe them in a human-readable format, and handle Java records if supported by the JVM. The class also includes nested helper classes to abstract the handling of records, depending on whether the JVM supports them or not.
- **Fields**:
    - `RECORD_HELPER`: `RecordHelper` A static final instance of RecordHelper used to handle record-related operations, initialized based on JVM support for records.
- **Methods**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.ReflectionHelper`](#ReflectionHelperReflectionHelper)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getInaccessibleTroubleshootingSuffix`](#ReflectionHelpergetInaccessibleTroubleshootingSuffix)
    - [`com.google.gson.internal.reflect.ReflectionHelper.makeAccessible`](#ReflectionHelpermakeAccessible)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getAccessibleObjectDescription`](#ReflectionHelpergetAccessibleObjectDescription)
    - [`com.google.gson.internal.reflect.ReflectionHelper.fieldToString`](#ReflectionHelperfieldToString)
    - [`com.google.gson.internal.reflect.ReflectionHelper.constructorToString`](#ReflectionHelperconstructorToString)
    - [`com.google.gson.internal.reflect.ReflectionHelper.appendExecutableParameters`](#ReflectionHelperappendExecutableParameters)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isStatic`](#ReflectionHelperisStatic)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isAnonymousOrNonStaticLocal`](#ReflectionHelperisAnonymousOrNonStaticLocal)
    - [`com.google.gson.internal.reflect.ReflectionHelper.tryMakeAccessible`](#ReflectionHelpertryMakeAccessible)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isRecord`](#ReflectionHelperisRecord)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getRecordComponentNames`](#ReflectionHelpergetRecordComponentNames)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getAccessor`](#ReflectionHelpergetAccessor)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getCanonicalRecordConstructor`](#ReflectionHelpergetCanonicalRecordConstructor)
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForUnexpectedIllegalAccess`](#ReflectionHelpercreateExceptionForUnexpectedIllegalAccess)
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException)

**Methods**

---
#### ReflectionHelper\.ReflectionHelper<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.ReflectionHelper}} -->
The `ReflectionHelper` constructor is a private method that prevents instantiation of the `ReflectionHelper` class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as private, which means it cannot be accessed from outside the class.
    - This effectively makes the `ReflectionHelper` class non-instantiable, as there are no public or protected constructors available.
- **Output**:
    - There is no output from this constructor as it is designed to prevent instantiation.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.getInaccessibleTroubleshootingSuffix<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.getInaccessibleTroubleshootingSuffix}} -->
The method `getInaccessibleTroubleshootingSuffix` generates a troubleshooting URL suffix based on the type and message of an exception.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `e`: An exception object that is checked to determine if it is an instance of `InaccessibleObjectException`.
- **Control Flow**:
    - Check if the class name of the exception `e` is `java.lang.reflect.InaccessibleObjectException`.
    - If true, retrieve the message from the exception `e`.
    - Determine the `troubleshootingId` based on whether the message contains the string 'to module com.google.gson'.
    - If the message contains 'to module com.google.gson', set `troubleshootingId` to 'reflection-inaccessible-to-module-gson'; otherwise, set it to 'reflection-inaccessible'.
    - Return a string that includes a URL generated by `TroubleshootingGuide.createUrl` with the `troubleshootingId`.
    - If the exception is not an `InaccessibleObjectException`, return an empty string.
- **Output**:
    - A string containing a troubleshooting URL suffix if the exception is an `InaccessibleObjectException`, otherwise an empty string.
- **Functions called**:
    - [`com.google.gson.internal.reflect.Java17ReflectionHelperTest.PrincipalImpl.getName`](../../../../../../../test/java/com/google/gson/internal/reflect/Java17ReflectionHelperTest.java.driver.md#PrincipalImplgetName)
    - [`com.google.gson.internal.reflect.Java17ReflectionHelperTest.PrincipalImpl.equals`](../../../../../../../test/java/com/google/gson/internal/reflect/Java17ReflectionHelperTest.java.driver.md#PrincipalImplequals)
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.makeAccessible<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.makeAccessible}} -->
The `makeAccessible` method attempts to set an `AccessibleObject` to be accessible, throwing a `JsonIOException` if it fails.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `object`: The `AccessibleObject` instance that should be made accessible.
- **Control Flow**:
    - The method tries to set the `AccessibleObject`'s accessibility to `true` using `setAccessible(true)`.
    - If an exception occurs during this process, it catches the exception and constructs a description of the `AccessibleObject` using [`getAccessibleObjectDescription`](#ReflectionHelpergetAccessibleObjectDescription).
    - It then throws a `JsonIOException` with a detailed error message, including troubleshooting information obtained from [`getInaccessibleTroubleshootingSuffix`](#ReflectionHelpergetInaccessibleTroubleshootingSuffix).
- **Output**:
    - The method does not return a value but may throw a `JsonIOException` if making the object accessible fails.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.getAccessibleObjectDescription`](#ReflectionHelpergetAccessibleObjectDescription)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getInaccessibleTroubleshootingSuffix`](#ReflectionHelpergetInaccessibleTroubleshootingSuffix)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.getAccessibleObjectDescription<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.getAccessibleObjectDescription}} -->
The `getAccessibleObjectDescription` method generates a human-readable description of an `AccessibleObject`, optionally capitalizing the first letter.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `object`: An `AccessibleObject` instance, which can be a `Field`, `Method`, `Constructor`, or another type.
    - `uppercaseFirstLetter`: A boolean flag indicating whether the first letter of the description should be capitalized.
- **Control Flow**:
    - Check if the `object` is an instance of `Field`, and if so, create a description using [`fieldToString`](#ReflectionHelperfieldToString) method.
    - If the `object` is an instance of `Method`, build a method signature using the method's name and parameters, then create a description including the declaring class and method signature.
    - If the `object` is an instance of `Constructor`, create a description using [`constructorToString`](#ReflectionHelperconstructorToString) method.
    - If the `object` is none of the above, create a description indicating an unknown `AccessibleObject`.
    - If `uppercaseFirstLetter` is true and the first character of the description is lowercase, capitalize the first letter of the description.
    - Return the constructed description.
- **Output**:
    - A `String` representing a human-readable description of the `AccessibleObject`, with optional capitalization of the first letter.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.fieldToString`](#ReflectionHelperfieldToString)
    - [`com.google.gson.internal.reflect.Java17ReflectionHelperTest.PrincipalImpl.getName`](../../../../../../../test/java/com/google/gson/internal/reflect/Java17ReflectionHelperTest.java.driver.md#PrincipalImplgetName)
    - [`com.google.gson.internal.reflect.ReflectionHelper.appendExecutableParameters`](#ReflectionHelperappendExecutableParameters)
    - [`com.google.gson.internal.reflect.ReflectionHelper.constructorToString`](#ReflectionHelperconstructorToString)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.fieldToString<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.fieldToString}} -->
The `fieldToString` method generates a string representation of a `Field` object by concatenating its declaring class name and field name, separated by a '#' character.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `field`: A `Field` object from which the method will extract the declaring class name and field name to create a string representation.
- **Control Flow**:
    - Retrieve the name of the class that declares the field using `field.getDeclaringClass().getName()`.
    - Retrieve the name of the field using `field.getName()`.
    - Concatenate the class name and field name with a '#' character in between.
    - Return the resulting string.
- **Output**:
    - A `String` that represents the field in the format 'DeclaringClassName#FieldName'.
- **Functions called**:
    - [`com.google.gson.internal.reflect.Java17ReflectionHelperTest.PrincipalImpl.getName`](../../../../../../../test/java/com/google/gson/internal/reflect/Java17ReflectionHelperTest.java.driver.md#PrincipalImplgetName)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.constructorToString<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.constructorToString}} -->
The `constructorToString` method generates a string representation of a given constructor, including its declaring class and parameter types.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `constructor`: A `Constructor<?>` object representing the constructor to be converted to a string.
- **Control Flow**:
    - Initialize a `StringBuilder` with the name of the class that declares the constructor.
    - Call [`appendExecutableParameters`](#ReflectionHelperappendExecutableParameters) to append the constructor's parameter types to the `StringBuilder`.
    - Convert the `StringBuilder` to a string and return it.
- **Output**:
    - A `String` representing the constructor, including its declaring class and parameter types.
- **Functions called**:
    - [`com.google.gson.internal.reflect.Java17ReflectionHelperTest.PrincipalImpl.getName`](../../../../../../../test/java/com/google/gson/internal/reflect/Java17ReflectionHelperTest.java.driver.md#PrincipalImplgetName)
    - [`com.google.gson.internal.reflect.ReflectionHelper.appendExecutableParameters`](#ReflectionHelperappendExecutableParameters)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.appendExecutableParameters<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.appendExecutableParameters}} -->
The `appendExecutableParameters` method appends a string representation of the parameter types of a given method or constructor to a `StringBuilder`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `executable`: An `AccessibleObject` which is either a `Method` or a `Constructor` whose parameter types are to be appended.
    - `stringBuilder`: A `StringBuilder` object to which the parameter types will be appended.
- **Control Flow**:
    - The method starts by appending an opening parenthesis '(' to the `StringBuilder`.
    - It checks if the `executable` is an instance of `Method` or `Constructor` and retrieves the parameter types accordingly.
    - It iterates over the array of parameter types.
    - For each parameter type, it appends its simple name to the `StringBuilder`, adding a comma and space before each subsequent parameter type after the first one.
    - Finally, it appends a closing parenthesis ')' to the `StringBuilder`.
- **Output**:
    - The method does not return a value; it modifies the `StringBuilder` passed as an argument by appending the parameter types of the `executable`.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.isStatic<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.isStatic}} -->
The `isStatic` method checks if a given class is declared as static.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `clazz`: The class object to be checked for the static modifier.
- **Control Flow**:
    - Retrieve the modifiers of the class using `clazz.getModifiers()`.
    - Check if the static modifier is present using `Modifier.isStatic()` and return the result.
- **Output**:
    - A boolean value indicating whether the class is static.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.isAnonymousOrNonStaticLocal<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.isAnonymousOrNonStaticLocal}} -->
The method checks if a given class is either anonymous or a non-static local class.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `clazz`: The class object to be checked for being anonymous or a non-static local class.
- **Control Flow**:
    - The method first checks if the class is not static by calling the isStatic method.
    - It then checks if the class is either an anonymous class or a local class using clazz.isAnonymousClass() and clazz.isLocalClass() respectively.
    - The method returns true if the class is not static and is either anonymous or local, otherwise it returns false.
- **Output**:
    - A boolean value indicating whether the class is anonymous or a non-static local class.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.isStatic`](#ReflectionHelperisStatic)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.tryMakeAccessible<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.tryMakeAccessible}} -->
The `tryMakeAccessible` method attempts to make a given constructor accessible and returns an error message if it fails.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `constructor`: The constructor object that the method attempts to make accessible.
- **Control Flow**:
    - The method tries to set the constructor's accessibility to true using `constructor.setAccessible(true);`.
    - If the operation is successful, the method returns `null`.
    - If an exception occurs, the method catches it and constructs an error message.
    - The error message includes the constructor's string representation, a suggestion to increase its visibility or use a custom InstanceCreator or TypeAdapter, the exception's message, and a troubleshooting suffix if applicable.
    - The constructed error message is then returned.
- **Output**:
    - A `String` that is `null` if the constructor was successfully made accessible, or an error message if it was not.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.constructorToString`](#ReflectionHelperconstructorToString)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getInaccessibleTroubleshootingSuffix`](#ReflectionHelpergetInaccessibleTroubleshootingSuffix)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.isRecord<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.isRecord}} -->
The [`isRecord`](#RecordHelperisRecord) method checks if a given class is a record type, utilizing a helper class to determine support for records on the current JVM.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `raw`: A `Class<?>` object representing the class to be checked if it is a record.
- **Control Flow**:
    - The method calls [`isRecord`](#RecordHelperisRecord) on the `RECORD_HELPER` instance, passing the `raw` class as an argument.
    - The `RECORD_HELPER` is an instance of either `RecordSupportedHelper` or `RecordNotSupportedHelper`, depending on whether the JVM supports records.
    - If the JVM supports records, `RecordSupportedHelper` uses reflection to invoke the [`isRecord`](#RecordHelperisRecord) method on the `Class` object.
    - If the JVM does not support records, `RecordNotSupportedHelper` always returns `false`.
- **Output**:
    - A boolean value indicating whether the specified class is a record.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.isRecord`](#RecordHelperisRecord)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.getRecordComponentNames<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.getRecordComponentNames}} -->
The [`getRecordComponentNames`](#RecordSupportedHelpergetRecordComponentNames) method retrieves the names of the record components for a given class if records are supported by the JVM.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `raw`: A `Class<?>` object representing the class for which record component names are to be retrieved.
- **Control Flow**:
    - The method calls [`getRecordComponentNames`](#RecordSupportedHelpergetRecordComponentNames) on the `RECORD_HELPER` instance, passing the `raw` class as an argument.
    - The `RECORD_HELPER` instance is either a `RecordSupportedHelper` or a `RecordNotSupportedHelper`, depending on whether the JVM supports records.
    - If records are supported, `RecordSupportedHelper` uses reflection to retrieve the record component names.
    - If records are not supported, `RecordNotSupportedHelper` throws an `UnsupportedOperationException`.
- **Output**:
    - An array of `String` containing the names of the record components for the specified class.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.getRecordComponentNames`](#RecordSupportedHelpergetRecordComponentNames)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.getAccessor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.getAccessor}} -->
The [`getAccessor`](#RecordHelpergetAccessor) method retrieves the accessor method for a given field in a record class.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `raw`: The `Class<?>` object representing the record class from which the accessor method is to be retrieved.
    - `field`: The `Field` object representing the field for which the accessor method is to be retrieved.
- **Control Flow**:
    - The method calls [`getAccessor`](#RecordHelpergetAccessor) on the `RECORD_HELPER` instance, passing the `raw` class and `field` as arguments.
    - The `RECORD_HELPER` is an instance of either `RecordSupportedHelper` or `RecordNotSupportedHelper`, depending on whether records are supported on the JVM.
    - If records are supported, `RecordSupportedHelper` attempts to retrieve the accessor method by invoking `getMethod` on the `raw` class with the field's name.
    - If records are not supported, `RecordNotSupportedHelper` throws an `UnsupportedOperationException`.
- **Output**:
    - The method returns a `Method` object representing the accessor method for the specified field in the record class.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getAccessor`](#RecordHelpergetAccessor)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.getCanonicalRecordConstructor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.getCanonicalRecordConstructor}} -->
The [`getCanonicalRecordConstructor`](#RecordHelpergetCanonicalRecordConstructor) method retrieves the canonical constructor for a given record class if records are supported on the JVM.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `raw`: The class object representing the record type for which the canonical constructor is to be retrieved.
- **Control Flow**:
    - The method calls [`getCanonicalRecordConstructor`](#RecordHelpergetCanonicalRecordConstructor) on the `RECORD_HELPER` instance, passing the `raw` class as an argument.
    - The `RECORD_HELPER` is an instance of either `RecordSupportedHelper` or `RecordNotSupportedHelper`, depending on whether records are supported on the JVM.
    - If records are supported, `RecordSupportedHelper` attempts to retrieve the canonical constructor using reflection.
    - If records are not supported, `RecordNotSupportedHelper` throws an `UnsupportedOperationException`.
- **Output**:
    - The method returns a `Constructor<T>` object representing the canonical constructor of the specified record class `raw`.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getCanonicalRecordConstructor`](#RecordHelpergetCanonicalRecordConstructor)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.createExceptionForUnexpectedIllegalAccess<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.createExceptionForUnexpectedIllegalAccess}} -->
The method throws a RuntimeException when an unexpected IllegalAccessException occurs, providing a detailed error message.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `exception`: An IllegalAccessException that triggered the unexpected access issue.
- **Control Flow**:
    - The method takes an IllegalAccessException as an input parameter.
    - It throws a new RuntimeException with a detailed message about the unexpected IllegalAccessException, including the Gson version and a note about ReflectionAccessFilter requirements.
    - The original IllegalAccessException is passed as the cause of the new RuntimeException.
- **Output**:
    - The method does not return a value as it throws a RuntimeException.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)


---
#### ReflectionHelper\.createExceptionForRecordReflectionException<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.createExceptionForRecordReflectionException}} -->
The method throws a RuntimeException when a ReflectiveOperationException occurs during record reflection operations.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `exception`: A ReflectiveOperationException that was caught during record reflection operations.
- **Control Flow**:
    - The method immediately throws a new RuntimeException.
    - The exception message indicates that an unexpected ReflectiveOperationException occurred while using reflection to handle Java records.
    - The message includes the Gson version and explains that this exception is unexpected because it occurs after confirming that records exist in the JVM.
    - The original ReflectiveOperationException is passed as the cause of the new RuntimeException.
- **Output**:
    - The method does not return a value as it throws a RuntimeException.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper`](#ReflectionHelper)  (Base Class)



---
### RecordHelper<!-- {{#class:com.google.gson.internal.reflect.ReflectionHelper.RecordHelper}} -->
- **Modifiers**: `private`, `abstract`, `static`
- **Description**: The `RecordHelper` class is an abstract static class designed to provide an abstraction layer for handling Java records through reflection, offering methods to check if a class is a record, retrieve record component names, obtain the canonical constructor for a record, and access record fields via accessor methods.
- **Methods**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.isRecord`](#RecordHelperisRecord)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getRecordComponentNames`](#RecordHelpergetRecordComponentNames)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getCanonicalRecordConstructor`](#RecordHelpergetCanonicalRecordConstructor)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getAccessor`](#RecordHelpergetAccessor)

**Methods**

---
#### RecordHelper\.isRecord<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.isRecord}} -->
The `isRecord` method determines if a given class is a record class, utilizing a helper class to handle JVM compatibility.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `raw`: The class object to be checked if it is a record class.
- **Control Flow**:
    - The method calls `isRecord` on the `RECORD_HELPER` instance, which is either `RecordSupportedHelper` or `RecordNotSupportedHelper`, depending on JVM support for records.
    - If the JVM supports records, `RecordSupportedHelper` uses reflection to invoke the `isRecord` method on the class object.
    - If the JVM does not support records, `RecordNotSupportedHelper` always returns false.
- **Output**:
    - A boolean value indicating whether the specified class is a record class.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper`](#ReflectionHelper.RecordHelper)  (Base Class)


---
#### RecordHelper\.getRecordComponentNames<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getRecordComponentNames}} -->
The `getRecordComponentNames` method retrieves the names of the record components for a given class if records are supported on the JVM.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `clazz`: The class object for which the record component names are to be retrieved.
- **Control Flow**:
    - The method delegates the call to the `getRecordComponentNames` method of the `RECORD_HELPER` instance, which is either a `RecordSupportedHelper` or `RecordNotSupportedHelper`.
    - If the JVM supports records, `RecordSupportedHelper` is used, which uses reflection to obtain the record component names.
    - If the JVM does not support records, `RecordNotSupportedHelper` is used, which throws an `UnsupportedOperationException`.
- **Output**:
    - An array of strings containing the names of the record components for the specified class.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper`](#ReflectionHelper.RecordHelper)  (Base Class)


---
#### RecordHelper\.getCanonicalRecordConstructor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getCanonicalRecordConstructor}} -->
The `getCanonicalRecordConstructor` method retrieves the canonical constructor for a given record class if records are supported on the JVM.
- **Modifiers**: `public`
- **Inputs**:
    - `raw`: The class object representing the record type for which the canonical constructor is to be retrieved.
- **Control Flow**:
    - The method delegates the task to the `RECORD_HELPER` instance, which is either a `RecordSupportedHelper` or `RecordNotSupportedHelper` depending on JVM support for records.
    - If records are supported, `RecordSupportedHelper` uses reflection to obtain the record components and their types, then retrieves the declared constructor matching these types.
    - If records are not supported, `RecordNotSupportedHelper` throws an `UnsupportedOperationException`.
- **Output**:
    - The method returns a `Constructor<T>` object representing the canonical constructor of the specified record class `raw` if records are supported; otherwise, it throws an exception.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper`](#ReflectionHelper.RecordHelper)  (Base Class)


---
#### RecordHelper\.getAccessor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordHelper.getAccessor}} -->
The `getAccessor` method retrieves the accessor method for a given field in a record class.
- **Modifiers**: `public`, `abstract`
- **Inputs**:
    - `raw`: The `Class<?>` object representing the record class from which the accessor method is to be retrieved.
    - `field`: The `Field` object representing the field for which the accessor method is to be retrieved.
- **Control Flow**:
    - The method is abstract and is implemented in the `RecordSupportedHelper` class.
    - In `RecordSupportedHelper`, it attempts to retrieve the method from the class `raw` that has the same name as the field `field`.
    - If the method retrieval fails due to a `ReflectiveOperationException`, it throws a runtime exception using `createExceptionForRecordReflectionException`.
- **Output**:
    - The method returns a `Method` object representing the accessor method for the specified field in the record class.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper`](#ReflectionHelper.RecordHelper)  (Base Class)



---
### RecordSupportedHelper<!-- {{#class:com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `RecordSupportedHelper` class is a specialized helper class that extends `RecordHelper` to provide reflection-based operations for Java records, assuming records are supported in the JVM. It uses reflection to dynamically access methods related to records, such as checking if a class is a record, retrieving record component names, obtaining the canonical constructor, and accessing record component accessor methods. This class is instantiated only if the JVM supports records, and it handles reflective operations with appropriate exception handling to manage unexpected reflective operation exceptions.
- **Fields**:
    - `isRecord`: `Method` A `Method` object representing the `isRecord` method of the `Class` class.
    - `getRecordComponents`: `Method` A `Method` object representing the `getRecordComponents` method of the `Class` class.
    - `getName`: `Method` A `Method` object representing the `getName` method of the `RecordComponent` class.
    - `getType`: `Method` A `Method` object representing the `getType` method of the `RecordComponent` class.
- **Methods**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.RecordSupportedHelper`](#RecordSupportedHelperRecordSupportedHelper)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.isRecord`](#RecordSupportedHelperisRecord)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.getRecordComponentNames`](#RecordSupportedHelpergetRecordComponentNames)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.getCanonicalRecordConstructor`](#RecordSupportedHelpergetCanonicalRecordConstructor)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.getAccessor`](#RecordSupportedHelpergetAccessor)
- **Extends/Implements**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper`](#ReflectionHelper.RecordHelper)

**Methods**

---
#### RecordSupportedHelper\.RecordSupportedHelper<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.RecordSupportedHelper}} -->
The `RecordSupportedHelper` constructor initializes methods for handling Java record components using reflection.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor attempts to retrieve the `isRecord` method from the `Class` class using reflection.
    - It retrieves the `getRecordComponents` method from the `Class` class using reflection.
    - It loads the `RecordComponent` class using `Class.forName`.
    - It retrieves the `getName` method from the `RecordComponent` class using reflection.
    - It retrieves the `getType` method from the `RecordComponent` class using reflection.
- **Output**:
    - The constructor does not return any value, but it initializes several `Method` fields for later use.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper`](#ReflectionHelper.RecordSupportedHelper)  (Base Class)


---
#### RecordSupportedHelper\.isRecord<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.isRecord}} -->
The `isRecord` method checks if a given class is a record type using reflection.
- **Modifiers**: `@Override`
- **Inputs**:
    - `raw`: A `Class<?>` object representing the class to be checked if it is a record.
- **Control Flow**:
    - Attempts to invoke the `isRecord` method on the provided class using reflection.
    - If the invocation is successful, it returns the result as a boolean indicating whether the class is a record.
    - If a `ReflectiveOperationException` occurs during the invocation, it throws a runtime exception created by [`createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException).
- **Output**:
    - A boolean value indicating whether the specified class is a record.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper`](#ReflectionHelper.RecordSupportedHelper)  (Base Class)


---
#### RecordSupportedHelper\.getRecordComponentNames<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.getRecordComponentNames}} -->
The `getRecordComponentNames` method retrieves the names of the record components for a given class using reflection.
- **Modifiers**: ``
- **Inputs**:
    - `raw`: The class object representing the record whose component names are to be retrieved.
- **Control Flow**:
    - Invoke the `getRecordComponents` method on the `raw` class to obtain an array of record components.
    - Initialize a `String` array `componentNames` with the same length as the `recordComponents` array.
    - Iterate over each record component, invoking the `getName` method to retrieve the name of each component and store it in the `componentNames` array.
    - Return the `componentNames` array containing the names of all record components.
    - If a `ReflectiveOperationException` occurs during the process, catch the exception and throw a runtime exception using [`createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException).
- **Output**:
    - A `String` array containing the names of the record components of the specified class.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper`](#ReflectionHelper.RecordSupportedHelper)  (Base Class)


---
#### RecordSupportedHelper\.getCanonicalRecordConstructor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.getCanonicalRecordConstructor}} -->
The `getCanonicalRecordConstructor` method retrieves the canonical constructor of a record class using reflection.
- **Modifiers**: `public`
- **Inputs**:
    - `raw`: The class object representing the record type for which the canonical constructor is to be retrieved.
- **Control Flow**:
    - Invoke the `getRecordComponents` method on the `raw` class to obtain an array of its record components.
    - Initialize an array `recordComponentTypes` to store the types of each record component.
    - Iterate over the `recordComponents` array, invoking the `getType` method on each component to populate the `recordComponentTypes` array with the corresponding types.
    - Use the `getDeclaredConstructor` method on the `raw` class with `recordComponentTypes` to retrieve the canonical constructor.
    - If a `ReflectiveOperationException` occurs, throw a custom runtime exception using [`createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException).
- **Output**:
    - Returns the canonical constructor of the specified record class.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper`](#ReflectionHelper.RecordSupportedHelper)  (Base Class)


---
#### RecordSupportedHelper\.getAccessor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper.getAccessor}} -->
The `getAccessor` method retrieves the accessor method for a given field in a record class.
- **Modifiers**: `public`
- **Inputs**:
    - `raw`: The `Class<?>` object representing the record class from which the accessor method is to be retrieved.
    - `field`: The `Field` object representing the field for which the accessor method is to be retrieved.
- **Control Flow**:
    - The method attempts to retrieve the accessor method of the field by calling `raw.getMethod(field.getName())`, which assumes that the accessor method has the same name as the field.
    - If a `ReflectiveOperationException` is thrown during this process, the method catches the exception and throws a new runtime exception using `createExceptionForRecordReflectionException(e)`.
- **Output**:
    - The method returns a `Method` object representing the accessor method for the specified field in the record class.
- **Functions called**:
    - [`com.google.gson.internal.reflect.Java17ReflectionHelperTest.PrincipalImpl.getName`](../../../../../../../test/java/com/google/gson/internal/reflect/Java17ReflectionHelperTest.java.driver.md#PrincipalImplgetName)
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForRecordReflectionException`](#ReflectionHelpercreateExceptionForRecordReflectionException)
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordSupportedHelper`](#ReflectionHelper.RecordSupportedHelper)  (Base Class)



---
### RecordNotSupportedHelper<!-- {{#class:com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `RecordNotSupportedHelper` class is a specialized implementation of the `RecordHelper` abstract class, designed to handle scenarios where Java records are not supported on the current JVM. It overrides methods to provide default behavior, such as returning false for `isRecord` and throwing `UnsupportedOperationException` for methods that would otherwise interact with record components, constructors, or accessors, indicating that these operations are not applicable in the current environment.
- **Methods**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.isRecord`](#RecordNotSupportedHelperisRecord)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.getRecordComponentNames`](#RecordNotSupportedHelpergetRecordComponentNames)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.getCanonicalRecordConstructor`](#RecordNotSupportedHelpergetCanonicalRecordConstructor)
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.getAccessor`](#RecordNotSupportedHelpergetAccessor)
- **Extends/Implements**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.RecordHelper`](#ReflectionHelper.RecordHelper)

**Methods**

---
#### RecordNotSupportedHelper\.isRecord<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.isRecord}} -->
The `isRecord` method determines if a given class is a record class, but always returns false in this implementation.
- **Modifiers**: `@Override`
- **Inputs**:
    - `clazz`: The class object to be checked if it is a record class.
- **Control Flow**:
    - The method is overridden from a superclass or interface.
    - It takes a single parameter, `clazz`, which is a `Class<?>` type.
    - The method directly returns `false`, indicating that the class is not a record.
- **Output**:
    - The method returns a boolean value, which is always `false` in this implementation.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper`](#ReflectionHelper.RecordNotSupportedHelper)  (Base Class)


---
#### RecordNotSupportedHelper\.getRecordComponentNames<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.getRecordComponentNames}} -->
The `getRecordComponentNames` method throws an `UnsupportedOperationException` indicating that records are not supported on the current JVM.
- **Modifiers**: ``
- **Inputs**:
    - `clazz`: The `Class<?>` object representing the class for which record component names are to be retrieved.
- **Control Flow**:
    - The method immediately throws an `UnsupportedOperationException` with a message stating that records are not supported on this JVM.
- **Output**:
    - The method does not return any value as it always throws an exception.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper`](#ReflectionHelper.RecordNotSupportedHelper)  (Base Class)


---
#### RecordNotSupportedHelper\.getCanonicalRecordConstructor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.getCanonicalRecordConstructor}} -->
The `getCanonicalRecordConstructor` method throws an `UnsupportedOperationException` indicating that records are not supported on the current JVM.
- **Modifiers**: `public`
- **Inputs**:
    - `raw`: A `Class<T>` object representing the class for which the canonical record constructor is to be retrieved.
- **Control Flow**:
    - The method immediately throws an `UnsupportedOperationException` with a message stating that records are not supported on this JVM.
- **Output**:
    - The method does not return any value as it always throws an exception.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper`](#ReflectionHelper.RecordNotSupportedHelper)  (Base Class)


---
#### RecordNotSupportedHelper\.getAccessor<!-- {{#callable:com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper.getAccessor}} -->
The `getAccessor` method throws an UnsupportedOperationException indicating that records are not supported on the current JVM.
- **Modifiers**: `public`
- **Inputs**:
    - `raw`: A `Class<?>` object representing the class from which the accessor method is to be retrieved.
    - `field`: A `Field` object representing the field for which the accessor method is to be retrieved.
- **Control Flow**:
    - The method immediately throws an `UnsupportedOperationException` with a message indicating that records are not supported on the current JVM.
- **Output**:
    - The method does not return any value as it always throws an exception.
- **See also**: [`com.google.gson.internal.reflect.ReflectionHelper.RecordNotSupportedHelper`](#ReflectionHelper.RecordNotSupportedHelper)  (Base Class)



