# Purpose
The provided Java source code defines an abstract class `UnsafeAllocator` within the `com.google.gson.internal` package. This class is designed to facilitate the creation of instances of classes without invoking their constructors, a technique often referred to as "unsafe" object allocation. The primary functionality of this class is encapsulated in the abstract method `newInstance(Class<T> c)`, which is implemented in various ways depending on the underlying Java Virtual Machine (JVM) or Android runtime environment. The class attempts to leverage different mechanisms, such as the `sun.misc.Unsafe` class, `ObjectStreamClass`, and `ObjectInputStream`, to achieve this functionality. If none of these methods are successful, it defaults to an implementation that throws an `UnsupportedOperationException`.

The `UnsafeAllocator` class is a critical component for libraries like Gson, which require the ability to instantiate objects without calling their constructors, often for deserialization purposes. The class includes a static method `create()` that determines the most appropriate method for object allocation based on the runtime environment. This method ensures compatibility across different platforms, including various versions of the JVM and Android's Dalvik VM. The class also includes a safeguard method, `assertInstantiable(Class<?> c)`, to ensure that the class being instantiated is valid and does not lead to JVM crashes. Overall, `UnsafeAllocator` provides a specialized and narrow functionality focused on low-level object instantiation, which is essential for certain serialization and deserialization tasks.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `java.io.ObjectInputStream`
- `java.io.ObjectStreamClass`
- `java.lang.reflect.Field`
- `java.lang.reflect.Method`


# Classes

---
### UnsafeAllocator<!-- {{#class:com.google.gson.internal.UnsafeAllocator}} -->
- **Modifiers**: `public`, `abstract`
- **Description**: The `UnsafeAllocator` class is an abstract utility designed to create instances of classes without invoking their constructors, leveraging various methods depending on the runtime environment, such as using `sun.misc.Unsafe` for JVM or native methods for Dalvik VM. It includes a singleton instance `INSTANCE` that attempts to allocate objects using different strategies, and it ensures that the classes are instantiable to prevent JVM crashes. If all strategies fail, it throws an `UnsupportedOperationException`, indicating that the runtime is not configured correctly for such operations.
- **Fields**:
    - `INSTANCE`: `UnsafeAllocator` A static final instance of `UnsafeAllocator` created using the `create` method.
- **Methods**:
    - [`com.google.gson.internal.UnsafeAllocator.newInstance`](#UnsafeAllocatornewInstance)
    - [`com.google.gson.internal.UnsafeAllocator.assertInstantiable`](#UnsafeAllocatorassertInstantiable)
    - [`com.google.gson.internal.UnsafeAllocator.create`](#UnsafeAllocatorcreate)

**Methods**

---
#### UnsafeAllocator\.newInstance<!-- {{#callable:com.google.gson.internal.UnsafeAllocator.newInstance}} -->
The `newInstance` method creates a new instance of a specified class without invoking its constructor.
- **Modifiers**: `public`, `abstract`
- **Inputs**:
    - `c`: The class type for which a new instance is to be created.
- **Control Flow**:
    - The method is abstract and is implemented in anonymous subclasses created in the `create` method.
    - Each implementation first calls `assertInstantiable` to ensure the class can be instantiated.
    - Depending on the implementation, it uses different techniques to create an instance: using `sun.misc.Unsafe`, `ObjectStreamClass`, or `ObjectInputStream`.
    - If none of the techniques are applicable, an `UnsupportedOperationException` is thrown.
- **Output**:
    - Returns a new instance of the specified class `T`.
- **See also**: [`com.google.gson.internal.UnsafeAllocator`](#UnsafeAllocator)  (Base Class)


---
#### UnsafeAllocator\.assertInstantiable<!-- {{#callable:com.google.gson.internal.UnsafeAllocator.assertInstantiable}} -->
The `assertInstantiable` method checks if a given class is instantiable and throws an `AssertionError` if it is not.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `c`: The class object to be checked for instantiability.
- **Control Flow**:
    - Call `ConstructorConstructor.checkInstantiable(c)` to determine if the class `c` is instantiable.
    - Store the result in `exceptionMessage`.
    - If `exceptionMessage` is not null, throw an `AssertionError` with a message indicating that `UnsafeAllocator` is used for a non-instantiable type.
- **Output**:
    - The method does not return any value; it throws an `AssertionError` if the class is not instantiable.
- **Functions called**:
    - [`com.google.gson.internal.ConstructorConstructor.checkInstantiable`](ConstructorConstructor.java.driver.md#ConstructorConstructorcheckInstantiable)
- **See also**: [`com.google.gson.internal.UnsafeAllocator`](#UnsafeAllocator)  (Base Class)


---
#### UnsafeAllocator\.create<!-- {{#callable:com.google.gson.internal.UnsafeAllocator.create}} -->
The `create` method attempts to create an instance of `UnsafeAllocator` using various methods to allocate objects without invoking their constructors.
- **Modifiers**: `private`, `static`
- **Inputs**: None
- **Control Flow**:
    - The method first attempts to use the `sun.misc.Unsafe` class to allocate instances by accessing the private field `theUnsafe` and invoking the `allocateInstance` method.
    - If the first attempt fails, it tries to use the `ObjectStreamClass` methods `getConstructorId` and `newInstance` to allocate instances, which is specific to Dalvik VM post-Gingerbread.
    - If the second attempt fails, it tries to use the `ObjectInputStream` method `newInstance` for Dalvik VM pre-Gingerbread.
    - If all attempts fail, it returns an `UnsafeAllocator` that throws an `UnsupportedOperationException` when `newInstance` is called.
- **Output**:
    - Returns an instance of `UnsafeAllocator` that can allocate objects without invoking their constructors, or throws an exception if allocation is not possible.
- **Functions called**:
    - [`com.google.gson.internal.UnsafeAllocator.assertInstantiable`](#UnsafeAllocatorassertInstantiable)
- **See also**: [`com.google.gson.internal.UnsafeAllocator`](#UnsafeAllocator)  (Base Class)



