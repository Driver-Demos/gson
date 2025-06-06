# Purpose
The [`ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelperReflectionAccessFilterHelper) class is an internal utility class within the Google Gson library, designed to assist with reflection access filtering. It provides methods to determine the type of a class, specifically whether it belongs to Java, Android, or other platform-specific types such as Kotlin or Scala. This functionality is crucial for libraries like Gson that need to handle different platform-specific classes differently, ensuring compatibility and correct behavior across various environments. The class also includes a method to evaluate a list of `ReflectionAccessFilter` instances against a given class, returning the first decisive result or allowing access if all filters are indecisive. This mechanism is essential for controlling access to class members based on custom filtering logic.

Additionally, the class includes a nested abstract static class `AccessChecker`, which provides a method to check if an `AccessibleObject` can be accessed, leveraging Java's reflection capabilities. This is particularly relevant for environments running Java 9 or later, where access checks are more stringent. The `AccessChecker` uses a version-specific approach to determine accessibility, defaulting to assuming accessibility if the Java version is earlier or if the necessary method is unavailable. This ensures that the library can operate smoothly across different Java versions, maintaining backward compatibility while taking advantage of newer Java features when available.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `com.google.gson.ReflectionAccessFilter`
- `com.google.gson.ReflectionAccessFilter.FilterResult`
- `java.lang.reflect.AccessibleObject`
- `java.lang.reflect.Method`
- `java.util.List`


# Classes

---
### ReflectionAccessFilterHelper<!-- {{#class:com.google.gson.internal.ReflectionAccessFilterHelper}} -->
- **Modifiers**: `public`
- **Description**: The `ReflectionAccessFilterHelper` class is a utility class designed to assist with reflection access filtering, particularly in the context of determining platform-specific types and managing access permissions in Java environments. It provides static methods to identify if a class belongs to Java, Android, or other platform types, and to apply a series of reflection access filters to determine access permissions. The class also includes an internal `AccessChecker` mechanism to handle access checks, especially for Java 9 and later, using reflection to invoke the `canAccess` method on `AccessibleObject` instances.
- **Methods**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelperReflectionAccessFilterHelper)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isJavaType`](#ReflectionAccessFilterHelperisJavaType)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isJavaType`](#ReflectionAccessFilterHelperisJavaType)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isAndroidType`](#ReflectionAccessFilterHelperisAndroidType)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isAndroidType`](#ReflectionAccessFilterHelperisAndroidType)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isAnyPlatformType`](#ReflectionAccessFilterHelperisAnyPlatformType)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.getFilterResult`](#ReflectionAccessFilterHelpergetFilterResult)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.canAccess`](#ReflectionAccessFilterHelpercanAccess)

**Methods**

---
#### ReflectionAccessFilterHelper\.ReflectionAccessFilterHelper<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.ReflectionAccessFilterHelper}} -->
The `ReflectionAccessFilterHelper` constructor is a private method that prevents instantiation of the class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as private, which means it cannot be accessed from outside the class.
    - This effectively makes the class non-instantiable, enforcing its use as a utility class with static methods only.
- **Output**:
    - There is no output as this is a constructor method.
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)


---
#### ReflectionAccessFilterHelper\.isJavaType<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.isJavaType}} -->
The [`isJavaType`](#ReflectionAccessFilterHelperisJavaType) method checks if a given class is a Java type by evaluating its name.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `c`: A `Class<?>` object representing the class to be checked.
- **Control Flow**:
    - The method takes a `Class<?>` object as input.
    - It retrieves the name of the class using `c.getName()`.
    - It calls the private `isJavaType(String className)` method with the class name as an argument.
    - The private method checks if the class name starts with "java." or "javax.".
    - The result of this check is returned as a boolean value.
- **Output**:
    - A boolean value indicating whether the class is a Java type (true) or not (false).
- **Functions called**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isJavaType`](#ReflectionAccessFilterHelperisJavaType)
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)


---
#### ReflectionAccessFilterHelper\.isJavaType<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.isJavaType}} -->
The `isJavaType` method checks if a given class name belongs to the Java or Javax package.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `className`: A string representing the name of the class to be checked.
- **Control Flow**:
    - The method checks if the input string `className` starts with the prefix 'java.' or 'javax.'.
    - If either condition is true, the method returns `true`.
    - If neither condition is true, the method returns `false`.
- **Output**:
    - A boolean value indicating whether the class name starts with 'java.' or 'javax.'.
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)


---
#### ReflectionAccessFilterHelper\.isAndroidType<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.isAndroidType}} -->
The [`isAndroidType`](#ReflectionAccessFilterHelperisAndroidType) method checks if a given class belongs to the Android platform or is a Java type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `c`: A `Class<?>` object representing the class to be checked.
- **Control Flow**:
    - The method retrieves the name of the class using `c.getName()`.
    - It calls the overloaded private method `isAndroidType(String className)` with the class name as the argument.
    - The private method checks if the class name starts with 'android.', 'androidx.', or if it is a Java type by calling `isJavaType(className)`.
- **Output**:
    - Returns a boolean value indicating whether the class is an Android type or a Java type.
- **Functions called**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isAndroidType`](#ReflectionAccessFilterHelperisAndroidType)
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)


---
#### ReflectionAccessFilterHelper\.isAndroidType<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.isAndroidType}} -->
The `isAndroidType` method checks if a given class name belongs to the Android or Java platform by examining its package prefix.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `className`: A `String` representing the fully qualified name of a class to be checked.
- **Control Flow**:
    - The method first checks if the `className` starts with the prefix 'android.' and returns true if it does.
    - If the first check fails, it then checks if the `className` starts with the prefix 'androidx.' and returns true if it does.
    - If both Android-specific checks fail, it calls the [`isJavaType`](#ReflectionAccessFilterHelperisJavaType) method to determine if the class name belongs to the Java platform, returning true if it does.
- **Output**:
    - A `boolean` value indicating whether the class name is an Android or Java type.
- **Functions called**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isJavaType`](#ReflectionAccessFilterHelperisJavaType)
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)


---
#### ReflectionAccessFilterHelper\.isAnyPlatformType<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.isAnyPlatformType}} -->
The `isAnyPlatformType` method checks if a given class belongs to a recognized platform type such as Android, Java, Kotlin, or Scala.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `c`: A `Class<?>` object representing the class to be checked.
- **Control Flow**:
    - Retrieve the name of the class using `c.getName()` and store it in `className`.
    - Check if `className` is an Android type by calling `isAndroidType(className)`, which also covers Java types.
    - Check if `className` starts with the prefix 'kotlin.', 'kotlinx.', or 'scala.'.
    - Return `true` if any of the above checks are true, otherwise return `false`.
- **Output**:
    - A boolean value indicating whether the class is a platform type (true) or not (false).
- **Functions called**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.isAndroidType`](#ReflectionAccessFilterHelperisAndroidType)
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)


---
#### ReflectionAccessFilterHelper\.getFilterResult<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.getFilterResult}} -->
The `getFilterResult` method evaluates a list of `ReflectionAccessFilter` objects against a given class and returns the first non-indecisive filter result, or `ALLOW` if all filters are indecisive.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `reflectionFilters`: A list of `ReflectionAccessFilter` objects to be applied to the class `c`.
    - `c`: The `Class<?>` object representing the class to be checked against the filters.
- **Control Flow**:
    - Iterate over each `ReflectionAccessFilter` in the `reflectionFilters` list.
    - For each filter, call the [`check`](../ReflectionAccessFilter.java.driver.md#ReflectionAccessFiltercheck) method with the class `c` to get a `FilterResult`.
    - If the `FilterResult` is not `INDECISIVE`, return this result immediately.
    - If all filters return `INDECISIVE`, return `FilterResult.ALLOW` as the default result.
- **Output**:
    - The method returns a `FilterResult` which is either the first non-indecisive result from the filters or `ALLOW` if all filters are indecisive.
- **Functions called**:
    - [`com.google.gson.ReflectionAccessFilter.check`](../ReflectionAccessFilter.java.driver.md#ReflectionAccessFiltercheck)
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)


---
#### ReflectionAccessFilterHelper\.canAccess<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.canAccess}} -->
The [`canAccess`](#AccessCheckercanAccess) method checks if a given `AccessibleObject` can be accessed by a specified object using an `AccessChecker` instance.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `accessibleObject`: An instance of `AccessibleObject` that represents the object whose accessibility is being checked.
    - `object`: The object attempting to access the `AccessibleObject`.
- **Control Flow**:
    - The method delegates the accessibility check to the [`canAccess`](#AccessCheckercanAccess) method of the `AccessChecker.INSTANCE`.
    - The `AccessChecker` is initialized based on the Java version, using reflection to call `AccessibleObject.canAccess(Object)` if available.
    - If the [`canAccess`](#AccessCheckercanAccess) method is not available (pre-Java 9), it defaults to assuming all objects are accessible.
- **Output**:
    - Returns a boolean indicating whether the `AccessibleObject` can be accessed by the specified object.
- **Functions called**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker.canAccess`](#AccessCheckercanAccess)
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper`](#ReflectionAccessFilterHelper)  (Base Class)



---
### AccessChecker<!-- {{#class:com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker}} -->
- **Modifiers**: `private`, `abstract`, `static`
- **Description**: The `AccessChecker` class is a private, abstract, and static helper class designed to determine if an `AccessibleObject` can be accessed by a given object, with specific behavior for Java 9 and later versions. It uses reflection to invoke the `canAccess` method if available, otherwise defaults to assuming accessibility. The class provides a singleton instance, `INSTANCE`, which is initialized based on the Java version at runtime.
- **Fields**:
    - `INSTANCE`: `AccessChecker` A static final instance of `AccessChecker` that is initialized based on the Java version to determine accessibility of objects.
- **Methods**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker.canAccess`](#AccessCheckercanAccess)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker.canAccess`](#AccessCheckercanAccess)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker.canAccess`](#AccessCheckercanAccess)

**Methods**

---
#### AccessChecker\.canAccess<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker.canAccess}} -->
The `canAccess` method checks if a given `AccessibleObject` can be accessed by a specified object using reflection.
- **Modifiers**: `public`
- **Inputs**:
    - `accessibleObject`: An instance of `AccessibleObject` that represents the object whose accessibility is being checked.
    - `object`: The object attempting to access the `AccessibleObject`.
- **Control Flow**:
    - The method attempts to invoke the `canAccess` method on the `accessibleObject` using reflection, passing the `object` as an argument.
    - If the invocation is successful, it returns the result as a boolean value indicating accessibility.
    - If an exception occurs during the invocation, it catches the exception and throws a `RuntimeException` with a message indicating failure.
- **Output**:
    - A boolean value indicating whether the `AccessibleObject` can be accessed by the specified object.
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker`](#ReflectionAccessFilterHelper.AccessChecker)  (Base Class)


---
#### AccessChecker\.canAccess<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker.canAccess}} -->
The `canAccess` method determines if a given `AccessibleObject` can be accessed by a specified object, defaulting to true if the determination cannot be made.
- **Modifiers**: `public`
- **Inputs**:
    - `accessibleObject`: An instance of `AccessibleObject` that represents the object whose accessibility is being checked.
    - `object`: The object attempting to access the `AccessibleObject`.
- **Control Flow**:
    - The method is overridden from an abstract class `AccessChecker`.
    - It returns `true` unconditionally, indicating that the accessibility check is assumed to be successful.
- **Output**:
    - A boolean value `true`, indicating that the `AccessibleObject` is assumed to be accessible by the specified object.
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker`](#ReflectionAccessFilterHelper.AccessChecker)  (Base Class)


---
#### AccessChecker\.canAccess<!-- {{#callable:com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker.canAccess}} -->
The `canAccess` method determines if a given `AccessibleObject` can be accessed by a specified object, using Java reflection.
- **Modifiers**: `public`, `abstract`
- **Inputs**:
    - `accessibleObject`: An instance of `AccessibleObject` that represents the object whose accessibility is being checked.
    - `object`: The object attempting to access the `AccessibleObject`.
- **Control Flow**:
    - The method is abstract and is implemented by an anonymous subclass of `AccessChecker`.
    - If the Java version is 9 or later, it attempts to use reflection to invoke the `canAccess` method on the `AccessibleObject` with the provided object.
    - If the reflection call is successful, it returns the result of the `canAccess` method invocation.
    - If the reflection call fails or the Java version is earlier than 9, it defaults to assuming the object can be accessed and returns `true`.
- **Output**:
    - A boolean value indicating whether the `AccessibleObject` can be accessed by the specified object.
- **See also**: [`com.google.gson.internal.ReflectionAccessFilterHelper.AccessChecker`](#ReflectionAccessFilterHelper.AccessChecker)  (Base Class)



