# Purpose
The provided Java source code is a comprehensive test suite for the `TypeToken` class, which is part of the Google Gson library. The `TypeToken` class is used to capture and work with generic type information at runtime, which is typically erased due to Java's type erasure. This test suite is designed to verify the functionality and robustness of the `TypeToken` class by testing various scenarios involving type assignments, parameterized types, wildcards, and nested generics. It ensures that the `TypeToken` class correctly handles type assignments, type parameterization, and the creation of type tokens for arrays and parameterized types, while also validating that it throws appropriate exceptions for invalid type configurations.

The test suite is organized into multiple test methods, each focusing on a specific aspect of the `TypeToken` functionality. It includes tests for raw type assignments, type parameters, wildcards, nested wildcards, and parameterized types. The suite also tests the behavior of `TypeToken` when dealing with invalid type arguments, such as using primitive types as type arguments or creating type tokens with type variables. Additionally, the suite includes tests for custom and non-anonymous subclasses of `TypeToken`, ensuring that the class behaves as expected in these scenarios. The use of assertions and exception handling throughout the tests ensures that the `TypeToken` class adheres to its expected behavior and provides meaningful error messages when misused.
# Imports and Dependencies

---
- `com.google.gson.reflect`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `java.lang.reflect.GenericArrayType`
- `java.lang.reflect.Method`
- `java.lang.reflect.ParameterizedType`
- `java.lang.reflect.Type`
- `java.lang.reflect.TypeVariable`
- `java.lang.reflect.WildcardType`
- `java.util.ArrayList`
- `java.util.List`
- `java.util.Map`
- `java.util.RandomAccess`
- `java.util.Set`
- `org.junit.Test`


# Classes

---
### TypeTokenTest<!-- {{#class:com.google.gson.reflect.TypeTokenTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `TypeTokenTest` class is a comprehensive test suite designed to validate the functionality of the `TypeToken` class, which is part of the Google Gson library. It includes a variety of test methods that check the behavior of `TypeToken` in different scenarios, such as handling raw types, type parameters, wildcards, nested wildcards, and parameterized types. The class also tests the creation of `TypeToken` instances with arrays and parameterized types, ensuring that the `TypeToken` class correctly handles type arguments and throws appropriate exceptions when invalid types are used. Additionally, it verifies the constraints on subclassing `TypeToken`, ensuring that only direct subclasses are allowed. The tests make extensive use of Java reflection to access and manipulate generic types, and they employ assertions to validate expected outcomes.
- **Fields**:
    - `listOfInteger`: `List<Integer>` A list of integers, used for testing type assignments.
    - `listOfNumber`: `List<Number>` A list of numbers, used for testing type assignments.
    - `listOfString`: `List<String>` A list of strings, used for testing type assignments.
    - `listOfUnknown`: `List<?>` A list of unknown type, used for testing wildcard type assignments.
    - `listOfSetOfString`: `List<Set<String>>` A list of sets of strings, used for testing nested wildcard type assignments.
    - `listOfSetOfUnknown`: `List<Set<?>>` A list of sets of unknown type, used for testing nested wildcard type assignments.
- **Methods**:
    - [`com.google.gson.reflect.TypeTokenTest.testIsAssignableFromRawTypes`](#TypeTokenTesttestIsAssignableFromRawTypes)
    - [`com.google.gson.reflect.TypeTokenTest.testIsAssignableFromWithTypeParameters`](#TypeTokenTesttestIsAssignableFromWithTypeParameters)
    - [`com.google.gson.reflect.TypeTokenTest.testIsAssignableFromWithBasicWildcards`](#TypeTokenTesttestIsAssignableFromWithBasicWildcards)
    - [`com.google.gson.reflect.TypeTokenTest.testIsAssignableFromWithNestedWildcards`](#TypeTokenTesttestIsAssignableFromWithNestedWildcards)
    - [`com.google.gson.reflect.TypeTokenTest.testArrayFactory`](#TypeTokenTesttestArrayFactory)
    - [`com.google.gson.reflect.TypeTokenTest.testParameterizedFactory`](#TypeTokenTesttestParameterizedFactory)
    - [`com.google.gson.reflect.TypeTokenTest.testParameterizedFactory_Invalid`](#TypeTokenTesttestParameterizedFactory_Invalid)
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenNonAnonymousSubclass`](#TypeTokenTesttestTypeTokenNonAnonymousSubclass)
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenSubSubClass`](#TypeTokenTesttestTypeTokenSubSubClass)
    - [`com.google.gson.reflect.TypeTokenTest.createTypeTokenTypeVariable`](#TypeTokenTestcreateTypeTokenTypeVariable)
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable`](#TypeTokenTesttestTypeTokenTypeVariable)
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenRaw`](#TypeTokenTesttestTypeTokenRaw)

**Methods**

---
#### TypeTokenTest\.testIsAssignableFromRawTypes<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testIsAssignableFromRawTypes}} -->
The `testIsAssignableFromRawTypes` method tests the [`isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom) functionality of the `TypeToken` class using raw types.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify that `TypeToken.get(Object.class).isAssignableFrom(String.class)` returns true, indicating that `Object` is a superclass of `String`.
    - It asserts that `TypeToken.get(String.class).isAssignableFrom(Object.class)` returns false, indicating that `String` is not a superclass of `Object`.
    - The method checks that `TypeToken.get(RandomAccess.class).isAssignableFrom(ArrayList.class)` returns true, confirming that `ArrayList` implements `RandomAccess`.
    - It asserts that `TypeToken.get(ArrayList.class).isAssignableFrom(RandomAccess.class)` returns false, indicating that `RandomAccess` is not a subclass of `ArrayList`.
- **Output**:
    - The method does not return any value; it uses assertions to validate the expected behavior of the [`isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom) method.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testIsAssignableFromWithTypeParameters<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testIsAssignableFromWithTypeParameters}} -->
The method `testIsAssignableFromWithTypeParameters` tests the [`isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom) method of `TypeToken` for type parameters using reflection to verify type compatibility.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the generic type of the field `listOfInteger` and assign it to `Type a`.
    - Retrieve the generic type of the field `listOfNumber` and assign it to `Type b`.
    - Assert that `TypeToken.get(a).isAssignableFrom(a)` returns true, indicating `a` is assignable from itself.
    - Assert that `TypeToken.get(b).isAssignableFrom(b)` returns true, indicating `b` is assignable from itself.
    - Assert that `TypeToken.get(a).isAssignableFrom(b)` returns false, indicating `a` is not assignable from `b`.
    - Assert that `TypeToken.get(b).isAssignableFrom(a)` returns false, indicating `b` is not assignable from `a`.
- **Output**:
    - The method does not return any value; it uses assertions to validate type assignability.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testIsAssignableFromWithBasicWildcards<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testIsAssignableFromWithBasicWildcards}} -->
The method `testIsAssignableFromWithBasicWildcards` tests the behavior of the `TypeToken.isAssignableFrom` method with basic wildcard types and handles exceptions for unsupported types.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the generic type of the field `listOfString` and assign it to `Type a`.
    - Retrieve the generic type of the field `listOfUnknown` and assign it to `Type b`.
    - Assert that `TypeToken.get(a).isAssignableFrom(a)` returns true, indicating `a` is assignable from itself.
    - Assert that `TypeToken.get(b).isAssignableFrom(b)` returns true, indicating `b` is assignable from itself.
    - Assert that `TypeToken.get(a).isAssignableFrom(b)` returns false, indicating `a` is not assignable from `b`.
    - Assign `listOfString` to `listOfUnknown`, which compiles, indicating `b` is assignable from `a`.
    - Attempt to cast the first actual type argument of `b` to `WildcardType` and create a `TypeToken` for it.
    - Use `assertThrows` to verify that calling `wildcardTypeToken.isAssignableFrom(b)` throws an `IllegalArgumentException`.
    - Assert that the exception message matches the expected message for unsupported types.
- **Output**:
    - The method does not return any value; it performs assertions to validate type assignability and exception handling.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testIsAssignableFromWithNestedWildcards<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testIsAssignableFromWithNestedWildcards}} -->
The method `testIsAssignableFromWithNestedWildcards` tests the [`isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom) method of `TypeToken` with nested wildcard types to ensure correct type assignability behavior.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the generic type of the field `listOfSetOfString` and assign it to `Type a`.
    - Retrieve the generic type of the field `listOfSetOfUnknown` and assign it to `Type b`.
    - Assert that `TypeToken.get(a).isAssignableFrom(a)` returns true, indicating `a` is assignable from itself.
    - Assert that `TypeToken.get(b).isAssignableFrom(b)` returns true, indicating `b` is assignable from itself.
    - Assert that `TypeToken.get(a).isAssignableFrom(b)` returns false, indicating `a` is not assignable from `b`.
    - Assert that `TypeToken.get(b).isAssignableFrom(a)` returns false, indicating `b` is not assignable from `a`.
- **Output**:
    - The method does not return any value; it uses assertions to validate type assignability.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testArrayFactory<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testArrayFactory}} -->
The `testArrayFactory` method tests the `TypeToken.getArray` method for various types and checks for expected outcomes, including handling of null input.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `TypeToken` for a `String[]` and assert that `TypeToken.getArray(String.class)` returns an equivalent `TypeToken`.
    - Create a `TypeToken` for a `List<String>[]` and assert that `TypeToken.getArray(listOfString)` returns an equivalent `TypeToken`.
    - Create a `TypeToken` for an `int[]` and assert that `TypeToken.getArray(int.class)` returns an equivalent `TypeToken`.
    - Assert that calling `TypeToken.getArray` with `null` throws a `NullPointerException`.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the correctness of the `TypeToken.getArray` method for different input types and ensures it throws an exception for null input.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getArray`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetArray)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testParameterizedFactory<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testParameterizedFactory}} -->
The `testParameterizedFactory` method tests the creation of parameterized `TypeToken` instances and verifies their correctness using assertions.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `TypeToken` for `List<String>` and assert that it matches the parameterized type created using `TypeToken.getParameterized` with `List.class` and `String.class` as arguments.
    - Create a `TypeToken` for `Map<String, String>` and assert that it matches the parameterized type created using `TypeToken.getParameterized` with `Map.class`, `String.class`, and `String.class` as arguments.
    - Create a nested `TypeToken` for `List<List<List<String>>>` by creating intermediate `Type` objects for `List<String>` and `List<List<String>>`, and assert that it matches the parameterized type created using `TypeToken.getParameterized`.
    - Create a `TypeToken` for `GenericWithBound<Number>` and assert that it matches the parameterized type created using `TypeToken.getParameterized` with `GenericWithBound.class` and `Number.class` as arguments.
    - Create a `TypeToken` for `GenericWithBound<Integer>` and assert that it matches the parameterized type created using `TypeToken.getParameterized` with `GenericWithBound.class` and `Integer.class` as arguments.
    - Create a `TypeToken` for `GenericWithMultiBound<ClassSatisfyingBounds>` and assert that it matches the parameterized type created using `TypeToken.getParameterized` with `GenericWithMultiBound.class` and `ClassSatisfyingBounds.class` as arguments.
    - Create a `TypeToken` for `NestedGeneric<Integer>` and verify that the `ParameterizedType` has a null owner type, the correct raw type, and the correct actual type arguments.
    - Create a local generic class `LocalGenericClass<T>`, create a `TypeToken` for `LocalGenericClass<Integer>`, and assert that it matches the parameterized type created using `TypeToken.getParameterized`.
    - Assert that requesting a parameterized type for a non-generic class like `String` results in a `TypeToken` equivalent to `TypeToken.get(String.class)`.
- **Output**:
    - The method does not return any value; it uses assertions to verify the correctness of parameterized `TypeToken` instances.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getParameterized`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetParameterized)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testParameterizedFactory\_Invalid<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testParameterizedFactory_Invalid}} -->
The `testParameterizedFactory_Invalid` method tests various invalid scenarios for creating parameterized types using the `TypeToken.getParameterized` method, ensuring that appropriate exceptions are thrown for each case.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by asserting that a `NullPointerException` is thrown when `TypeToken.getParameterized` is called with a null raw type or a null type argument.
    - It then checks that an `IllegalArgumentException` is thrown when attempting to parameterize a `GenericArrayType` or when the number of type arguments does not match the expected number for a given raw type.
    - The method verifies that using primitive types as type arguments results in an `IllegalArgumentException`.
    - It tests that type arguments not satisfying the bounds of a generic type's type variable also throw an `IllegalArgumentException`.
    - Finally, it checks that attempting to parameterize a non-static inner class without specifying an owner type results in an `IllegalArgumentException`.
- **Output**:
    - The method does not return any value; it uses assertions to verify that exceptions are thrown as expected.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getParameterized`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetParameterized)
    - [`com.google.gson.reflect.TypeToken.getArray`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetArray)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testTypeTokenNonAnonymousSubclass<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testTypeTokenNonAnonymousSubclass}} -->
The `testTypeTokenNonAnonymousSubclass` method tests that a non-anonymous subclass of `TypeToken` correctly identifies its raw type and type as `String.class`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `CustomTypeToken` instance, which is a subclass of `TypeToken<String>`, is created.
    - The method asserts that the raw type of the `typeToken` is `String.class`.
    - The method asserts that the type of the `typeToken` is `String.class`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `TypeToken` subclass.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testTypeTokenSubSubClass<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testTypeTokenSubSubClass}} -->
The `testTypeTokenSubSubClass` method tests that creating subclasses of subclasses of `TypeToken` results in an `IllegalStateException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a local class `SubTypeToken` that extends `TypeToken<String>`.
    - Define a local class `SubSubTypeToken1` that extends `SubTypeToken<T>`.
    - Define a local class `SubSubTypeToken2` that extends `SubTypeToken<Integer>`.
    - Use `assertThrows` to verify that instantiating `SubTypeToken<Integer>` throws an `IllegalStateException` with a specific message.
    - Use `assertThrows` to verify that instantiating `SubSubTypeToken1<Integer>` throws an `IllegalStateException` with a specific message.
    - Use `assertThrows` to verify that instantiating `SubSubTypeToken2` throws an `IllegalStateException` with a specific message.
- **Output**:
    - The method does not return any value, but it verifies that creating subclasses of subclasses of `TypeToken` throws an `IllegalStateException` with the message 'Must only create direct subclasses of TypeToken'.
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.createTypeTokenTypeVariable<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.createTypeTokenTypeVariable}} -->
The `createTypeTokenTypeVariable` method creates an instance of a `TypeToken` with a type variable `M`.
- **Modifiers**: `private`, `static`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `TypeToken` is created with a type variable `M`.
    - The instance is assigned to a variable named `unused`, which is not used further in the method.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testTypeTokenTypeVariable<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable}} -->
The `testTypeTokenTypeVariable` method tests the behavior of `TypeToken` when used with type variables, ensuring that it throws an `IllegalArgumentException` when a type variable is used as a type argument, unless a specific system property is set.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method defines an inner class `Enclosing<T>` to access the type variable `T` and contains a nested `Inner` class.
    - Within `Enclosing`, the [`test`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.test) method is defined to check that creating a `TypeToken` with a type variable `T` throws an `IllegalArgumentException` with a specific message.
    - Several variations of `TypeToken` instantiations with `T` are tested, including nested lists and arrays, all expected to throw the same exception.
    - A system property `gson.allowCapturingTypeVariables` is temporarily set to a non-true value to verify that it does not affect the exception behavior, and then set to `true` to allow capturing type variables, which changes the behavior to not throw an exception.
    - The [`testMethodTypeVariable`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.testMethodTypeVariable) method is defined to test method type variables, ensuring that using a method type variable `M` in a `TypeToken` also throws an `IllegalArgumentException`.
    - The `Enclosing` class is instantiated, and its [`test`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.test) and [`testMethodTypeVariable`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.testMethodTypeVariable) methods are called to execute the tests.
    - A separate test is performed to ensure that using a type variable in a factory method is allowed and behaves as expected, without throwing an exception.
- **Output**:
    - The method does not return a value but performs assertions to verify that `TypeToken` throws `IllegalArgumentException` when used with type variables, unless a specific system property is set.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing.test`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.test)
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing.testMethodTypeVariable`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.testMethodTypeVariable)
    - [`com.google.gson.reflect.TypeTokenTest.createTypeTokenTypeVariable`](#TypeTokenTestcreateTypeTokenTypeVariable)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.reflect.TypeToken.getParameterized`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetParameterized)
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)


---
#### TypeTokenTest\.testTypeTokenRaw<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testTypeTokenRaw}} -->
The `testTypeTokenRaw` method tests that creating a raw `TypeToken` without a type argument throws an `IllegalStateException` with a specific error message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that creating a new `TypeToken` without a type argument results in an `IllegalStateException`.
    - The exception is captured in variable `e`.
    - The method then uses `assertThat` to check that the message of the exception `e` matches the expected error message, which advises that `TypeToken` must be created with a type argument and provides a link to troubleshooting documentation.
- **Output**:
    - The method does not return any value; it is a test method that asserts expected behavior.
- **See also**: [`com.google.gson.reflect.TypeTokenTest`](#TypeTokenTest)  (Base Class)



---
### NestedGeneric<!-- {{#class:com.google.gson.reflect.TypeTokenTest.NestedGeneric}} -->
- **Modifiers**: `static`
- **Description**: The `NestedGeneric` class is a static nested class that is parameterized with a generic type `T`, allowing it to be used with any object type. It serves as a simple example of a generic class that can be instantiated with different types, demonstrating the use of generics in Java to create type-safe data structures or methods.


---
### LocalGenericClass<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testParameterizedFactory.LocalGenericClass}} -->
- **Description**: The `LocalGenericClass` is a simple generic class defined within a method in the `TypeTokenTest` class. It is used to demonstrate the creation of a `TypeToken` for a local generic class with a specific type parameter, in this case, `Integer`. This class serves as an example to test the functionality of the `TypeToken` class in handling local generic classes.


---
### Outer<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testParameterizedFactory_Invalid.Outer}} -->
- **Description**: The `Outer` class is a simple container class that contains a non-static inner class named `NonStaticInner`. This inner class is generic, allowing it to handle objects of any type specified by the type parameter `T`. The `Outer` class itself does not have any fields or methods, and its primary purpose is to serve as an enclosing class for the `NonStaticInner` class. The `NonStaticInner` class is annotated with `@SuppressWarnings("ClassCanBeStatic")`, indicating that it could potentially be made static, but is intentionally kept non-static for the purposes of the surrounding code context.


---
### NonStaticInner<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testParameterizedFactory_Invalid.Outer.NonStaticInner}} -->
- **Description**: The `NonStaticInner` class is a generic inner class that is defined within another class, but it is not static, meaning it maintains a reference to its enclosing class. This class is parameterized with a type variable `T`, allowing it to be used with different data types. The class is annotated with `@SuppressWarnings("ClassCanBeStatic")`, indicating that it could potentially be made static, but is intentionally kept non-static for specific use cases, possibly to access members of the enclosing class.


---
### CustomTypeToken<!-- {{#class:com.google.gson.reflect.TypeTokenTest.CustomTypeToken}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `CustomTypeToken` class is a private static subclass of `TypeToken` specifically parameterized with the `String` type, used within the `TypeTokenTest` class to test the behavior of non-anonymous subclasses of `TypeToken`.


---
### SubTypeToken<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testTypeTokenSubSubClass.SubTypeToken}} -->
- **Description**: The `SubTypeToken` class is a generic class that extends the `TypeToken` class with a specific type of `String`. It serves as a specialized version of `TypeToken` for handling type tokens of `String` types, allowing for type-safe operations and type reflection specific to `String`. This class is part of a test suite for the `TypeToken` class, which is used to capture and manipulate generic type information at runtime.


---
### SubSubTypeToken1<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testTypeTokenSubSubClass.SubSubTypeToken1}} -->
- **Description**: The `SubSubTypeToken1` class is a generic subclass of `SubTypeToken`, which itself is a subclass of `TypeToken`. This class is designed to demonstrate the restriction that users must only create direct subclasses of `TypeToken` and not subclasses of subclasses. It is used in the context of testing type token behavior in the `TypeTokenTest` class.


---
### SubSubTypeToken2<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testTypeTokenSubSubClass.SubSubTypeToken2}} -->
- **Description**: The `SubSubTypeToken2` class is a specialized subclass of `SubTypeToken` that is parameterized with the `Integer` type. It serves as a concrete implementation of a type token, which is a common pattern used to capture and manipulate generic type information at runtime. This class is part of a test suite for the `TypeToken` class, which is used to handle generic type information in the Gson library. The class itself does not define any additional fields or methods beyond those inherited from its superclass.


---
### Enclosing<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing}} -->
- **Description**: The `Enclosing` class is a generic class designed to test the behavior of `TypeToken` with type variables, particularly focusing on ensuring that type arguments do not contain type variables due to type erasure issues. It contains an inner class `Inner` and methods that assert exceptions are thrown when `TypeToken` is used with type variables, demonstrating the limitations and expected error messages. The class also tests the effect of a system property on the behavior of `TypeToken` and includes a method to test type variables declared within methods.
- **Methods**:
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing.test`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.test)
    - [`com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing.testMethodTypeVariable`](#TypeTokenTesttestTypeTokenTypeVariable.Enclosing.testMethodTypeVariable)

**Methods**

---
#### Enclosing\.test<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing.test}} -->
The `test` method verifies that creating a `TypeToken` with a type variable throws an `IllegalArgumentException` unless a specific system property is set to 'true', in which case it allows the creation and checks the type.
- **Modifiers**: ``
- **Inputs**: None
- **Control Flow**:
    - Define a string `expectedMessage` containing the expected error message for `IllegalArgumentException`.
    - Use `assertThrows` to verify that creating a `TypeToken` with various type variable configurations throws an `IllegalArgumentException` with the `expectedMessage`.
    - Set a system property `gson.allowCapturingTypeVariables` to a non-'true' value and verify that creating a `TypeToken` still throws the exception.
    - Set the system property to 'true', create a `TypeToken` with a type variable, and verify that the type matches the expected type parameter of the enclosing class.
    - Clear the system property after each test block.
- **Output**:
    - The method does not return any value; it performs assertions to verify expected exceptions and conditions.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
- **See also**: [`com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing`](#TypeTokenTest.testTypeTokenTypeVariable.Enclosing)  (Base Class)


---
#### Enclosing\.testMethodTypeVariable<!-- {{#callable:com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing.testMethodTypeVariable}} -->
The `testMethodTypeVariable` method tests that creating a `TypeToken` with a type variable results in an `IllegalArgumentException` with a specific error message.
- **Modifiers**: `<M>`, `void`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the `Method` object for the `testMethodTypeVariable` method using reflection.
    - Use `assertThrows` to verify that creating a `TypeToken` with a type variable `M` throws an `IllegalArgumentException`.
    - Check that the exception message matches one of the expected error messages, which indicate that type variables are not allowed in `TypeToken` arguments.
- **Output**:
    - The method does not return any value, but it verifies that an `IllegalArgumentException` is thrown with a specific message when a `TypeToken` is created with a type variable.
- **See also**: [`com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing`](#TypeTokenTest.testTypeTokenTypeVariable.Enclosing)  (Base Class)



---
### Inner<!-- {{#class:com.google.gson.reflect.TypeTokenTest.testTypeTokenTypeVariable.Enclosing.Inner}} -->
- **Description**: The `Inner` class is a simple, non-static inner class within the `TypeTokenTest` class, primarily used for testing purposes. It is annotated with `@SuppressWarnings("ClassCanBeStatic")` to suppress warnings about it potentially being a static class, indicating that it is intentionally designed to be non-static for the context of the tests.


---
### GenericWithBound<!-- {{#class:com.google.gson.reflect.GenericWithBound}} -->
- **Description**: The `GenericWithBound` class is a generic class that defines a type parameter `T` which is constrained to be a subclass of `Number`. This means that any type used as a type argument for `T` must be a subclass of `Number`, ensuring that the class can only be instantiated with numeric types. This class is typically used in scenarios where operations on numeric types are required, and it enforces type safety by restricting the type parameter to numeric types only.


---
### GenericWithMultiBound<!-- {{#class:com.google.gson.reflect.GenericWithMultiBound}} -->
- **Description**: The `GenericWithMultiBound` class is a generic class that defines a type parameter `T` with multiple bounds, specifically requiring that any type argument for `T` must be a subclass of `Number` and implement the `CharSequence` interface. This class is used to demonstrate the concept of multiple bounds in Java generics, where a type parameter can be constrained to extend multiple classes or interfaces, providing flexibility and type safety in generic programming.


---
### ClassSatisfyingBounds<!-- {{#class:com.google.gson.reflect.ClassSatisfyingBounds}} -->
- **Modifiers**: `abstract`
- **Description**: The `ClassSatisfyingBounds` is an abstract class that extends `Number` and implements `CharSequence`, serving as a demonstration of a class that satisfies multiple type bounds, specifically for use in testing scenarios involving generic type parameters with multiple bounds.
- **Extends/Implements**:
    - `Number`
    - `CharSequence`


