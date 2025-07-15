# Purpose
The provided Java source code file is part of the internal implementation of the Gson library, specifically dealing with type manipulation and reflection. The class [`GsonTypes`](#GsonTypesGsonTypes) offers a collection of static utility methods for working with Java's `Type` interface, which is crucial for handling generic types at runtime. This class provides methods to create and manipulate parameterized types, generic array types, and wildcard types, which are essential for Gson's serialization and deserialization processes. The class is designed to be non-instantiable, as indicated by its private constructor that throws an `UnsupportedOperationException`.

Key technical components of this file include methods for creating new parameterized types ([`newParameterizedTypeWithOwner`](#GsonTypesnewParameterizedTypeWithOwner)), generic array types ([`arrayOf`](#GsonTypesarrayOf)), and wildcard types ([`subtypeOf`](#GsonTypessubtypeOf), [`supertypeOf`](#GsonTypessupertypeOf)). It also includes methods for resolving and canonicalizing types, which are necessary for ensuring type consistency and correctness during runtime operations. The file defines several private static classes ([`ParameterizedTypeImpl`](#ParameterizedTypeImplParameterizedTypeImpl), [`GenericArrayTypeImpl`](#GenericArrayTypeImplGenericArrayTypeImpl), [`WildcardTypeImpl`](#WildcardTypeImplWildcardTypeImpl)) that implement Java's type interfaces and provide concrete, serializable implementations. These implementations are crucial for Gson's ability to handle complex generic type scenarios, such as nested generics and wildcard bounds, which are common in JSON data structures. Overall, this file provides narrow but essential functionality for the Gson library, focusing on the intricacies of Java's type system to facilitate robust JSON processing.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `com.google.gson.internal.GsonPreconditions.checkArgument`
- `java.util.Objects.requireNonNull`
- `java.io.Serializable`
- `java.lang.reflect.Array`
- `java.lang.reflect.GenericArrayType`
- `java.lang.reflect.GenericDeclaration`
- `java.lang.reflect.Modifier`
- `java.lang.reflect.ParameterizedType`
- `java.lang.reflect.Type`
- `java.lang.reflect.TypeVariable`
- `java.lang.reflect.WildcardType`
- `java.util.Arrays`
- `java.util.Collection`
- `java.util.HashMap`
- `java.util.Map`
- `java.util.NoSuchElementException`
- `java.util.Objects`
- `java.util.Properties`


# Classes

---
### GsonTypes<!-- {{#class:com.google.gson.internal.GsonTypes}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `GsonTypes` class provides a collection of static utility methods for working with Java's type system, particularly focusing on parameterized types, generic array types, and wildcard types. It includes methods to create new parameterized types, resolve types, and check type equality, among other functionalities. The class is designed to handle complex type manipulations and conversions, ensuring that types are canonicalized and serializable where necessary. It also includes nested static classes to implement specific type interfaces like `ParameterizedType`, `GenericArrayType`, and `WildcardType`, providing a robust framework for type handling in Java.
- **Fields**:
    - `EMPTY_TYPE_ARRAY`: `Type[]` A static final array of Type, initialized as an empty array, used as a default or placeholder in various methods.
- **Methods**:
    - [`com.google.gson.internal.GsonTypes.GsonTypes`](#GsonTypesGsonTypes)
    - [`com.google.gson.internal.GsonTypes.newParameterizedTypeWithOwner`](#GsonTypesnewParameterizedTypeWithOwner)
    - [`com.google.gson.internal.GsonTypes.arrayOf`](#GsonTypesarrayOf)
    - [`com.google.gson.internal.GsonTypes.subtypeOf`](#GsonTypessubtypeOf)
    - [`com.google.gson.internal.GsonTypes.supertypeOf`](#GsonTypessupertypeOf)
    - [`com.google.gson.internal.GsonTypes.canonicalize`](#GsonTypescanonicalize)
    - [`com.google.gson.internal.GsonTypes.getRawType`](#GsonTypesgetRawType)
    - [`com.google.gson.internal.GsonTypes.equal`](#GsonTypesequal)
    - [`com.google.gson.internal.GsonTypes.equals`](#GsonTypesequals)
    - [`com.google.gson.internal.GsonTypes.typeToString`](#GsonTypestypeToString)
    - [`com.google.gson.internal.GsonTypes.getGenericSupertype`](#GsonTypesgetGenericSupertype)
    - [`com.google.gson.internal.GsonTypes.getSupertype`](#GsonTypesgetSupertype)
    - [`com.google.gson.internal.GsonTypes.getArrayComponentType`](#GsonTypesgetArrayComponentType)
    - [`com.google.gson.internal.GsonTypes.getCollectionElementType`](#GsonTypesgetCollectionElementType)
    - [`com.google.gson.internal.GsonTypes.getMapKeyAndValueTypes`](#GsonTypesgetMapKeyAndValueTypes)
    - [`com.google.gson.internal.GsonTypes.resolve`](#GsonTypesresolve)
    - [`com.google.gson.internal.GsonTypes.resolve`](#GsonTypesresolve)
    - [`com.google.gson.internal.GsonTypes.resolveTypeVariable`](#GsonTypesresolveTypeVariable)
    - [`com.google.gson.internal.GsonTypes.indexOf`](#GsonTypesindexOf)
    - [`com.google.gson.internal.GsonTypes.declaringClassOf`](#GsonTypesdeclaringClassOf)
    - [`com.google.gson.internal.GsonTypes.checkNotPrimitive`](#GsonTypescheckNotPrimitive)
    - [`com.google.gson.internal.GsonTypes.requiresOwnerType`](#GsonTypesrequiresOwnerType)

**Methods**

---
#### GsonTypes\.GsonTypes<!-- {{#callable:com.google.gson.internal.GsonTypes.GsonTypes}} -->
The `GsonTypes` constructor is private and throws an `UnsupportedOperationException` to prevent instantiation of the class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as private, making it inaccessible from outside the class.
    - When the constructor is called, it immediately throws an `UnsupportedOperationException`.
- **Output**:
    - The method does not return any value as it is a constructor and its purpose is to throw an exception.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.newParameterizedTypeWithOwner<!-- {{#callable:com.google.gson.internal.GsonTypes.newParameterizedTypeWithOwner}} -->
The `newParameterizedTypeWithOwner` method creates a new `ParameterizedType` instance with a specified owner type, raw type, and type arguments.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `ownerType`: The `Type` that represents the owner of the parameterized type, or `null` if there is no owner.
    - `rawType`: The `Class` object representing the raw type of the parameterized type.
    - `typeArguments`: A varargs parameter of `Type` objects representing the type arguments to be applied to the raw type.
- **Control Flow**:
    - The method directly returns a new instance of `ParameterizedTypeImpl`, passing the `ownerType`, `rawType`, and `typeArguments` to its constructor.
- **Output**:
    - A `ParameterizedType` instance that is serializable and represents the parameterized type with the specified owner, raw type, and type arguments.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.arrayOf<!-- {{#callable:com.google.gson.internal.GsonTypes.arrayOf}} -->
The `arrayOf` method creates and returns a new `GenericArrayType` instance with the specified component type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `componentType`: The `Type` representing the component type of the array to be created.
- **Control Flow**:
    - The method takes a `Type` parameter named `componentType`.
    - It creates a new instance of `GenericArrayTypeImpl` using the provided `componentType`.
    - The newly created `GenericArrayTypeImpl` instance is returned.
- **Output**:
    - A `GenericArrayType` instance representing an array type with the specified component type.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.subtypeOf<!-- {{#callable:com.google.gson.internal.GsonTypes.subtypeOf}} -->
The `subtypeOf` method returns a `WildcardType` that represents an unknown type extending the specified `bound`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `bound`: A `Type` object representing the upper bound for the wildcard type.
- **Control Flow**:
    - Check if the `bound` is an instance of `WildcardType`.
    - If `bound` is a `WildcardType`, retrieve its upper bounds using `getUpperBounds()` method.
    - If `bound` is not a `WildcardType`, create an array with `bound` as its single element.
    - Create and return a new `WildcardTypeImpl` object with the determined upper bounds and an empty lower bounds array.
- **Output**:
    - A `WildcardType` object representing a type that extends the specified `bound`.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](#WildcardTypeImplgetUpperBounds)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.supertypeOf<!-- {{#callable:com.google.gson.internal.GsonTypes.supertypeOf}} -->
The `supertypeOf` method returns a wildcard type representing an unknown supertype of the given `bound` type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `bound`: A `Type` object representing the type for which a supertype wildcard is to be created.
- **Control Flow**:
    - Check if the `bound` is an instance of `WildcardType`.
    - If `bound` is a `WildcardType`, retrieve its lower bounds using `getLowerBounds()` method.
    - If `bound` is not a `WildcardType`, create a new array with `bound` as its single element.
    - Create a new `WildcardTypeImpl` object with `Object.class` as the upper bound and the determined lower bounds.
- **Output**:
    - A `WildcardType` object representing a supertype wildcard of the given `bound`.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getLowerBounds`](#WildcardTypeImplgetLowerBounds)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.canonicalize<!-- {{#callable:com.google.gson.internal.GsonTypes.canonicalize}} -->
The `canonicalize` method returns a functionally equivalent, serializable version of a given `Type` object.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `type`: The `Type` object to be canonicalized, which can be an instance of `Class`, `ParameterizedType`, `GenericArrayType`, `WildcardType`, or any other `Type`.
- **Control Flow**:
    - Check if the input `type` is an instance of `Class`; if it is an array, recursively canonicalize its component type and return a new `GenericArrayTypeImpl`, otherwise return the class itself.
    - Check if the input `type` is an instance of `ParameterizedType`; if so, create and return a new `ParameterizedTypeImpl` using its owner type, raw type, and actual type arguments.
    - Check if the input `type` is an instance of `GenericArrayType`; if so, return a new `GenericArrayTypeImpl` using its generic component type.
    - Check if the input `type` is an instance of `WildcardType`; if so, return a new `WildcardTypeImpl` using its upper and lower bounds.
    - If none of the above conditions are met, return the input `type` as it is, assuming it is either serializable as-is or unsupported.
- **Output**:
    - A `Type` object that is functionally equivalent to the input but is guaranteed to be serializable.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getOwnerType`](#ParameterizedTypeImplgetOwnerType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getRawType`](#ParameterizedTypeImplgetRawType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](#GenericArrayTypeImplgetGenericComponentType)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](#WildcardTypeImplgetUpperBounds)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getLowerBounds`](#WildcardTypeImplgetLowerBounds)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.getRawType<!-- {{#callable:com.google.gson.internal.GsonTypes.getRawType}} -->
The [`getRawType`](#ParameterizedTypeImplgetRawType) method determines and returns the raw class type of a given `Type` object.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `type`: A `Type` object representing the type whose raw class type is to be determined.
- **Control Flow**:
    - Check if the input `type` is an instance of `Class<?>`, and if so, return it as a `Class<?>`.
    - If `type` is an instance of `ParameterizedType`, retrieve its raw type, ensure it is a `Class`, and return it.
    - If `type` is an instance of `GenericArrayType`, recursively determine the raw type of its component type and return the class of an array of that type.
    - If `type` is an instance of `TypeVariable`, return `Object.class` as a general raw type.
    - If `type` is an instance of `WildcardType`, retrieve its upper bounds, assert there is only one, and return the raw type of the first bound.
    - If none of the above conditions are met, throw an `IllegalArgumentException` indicating the type is unsupported.
- **Output**:
    - Returns a `Class<?>` object representing the raw class type of the input `Type`.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getRawType`](#ParameterizedTypeImplgetRawType)
    - [`com.google.gson.internal.GsonPreconditions.checkArgument`](GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](#GenericArrayTypeImplgetGenericComponentType)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](#WildcardTypeImplgetUpperBounds)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.equal<!-- {{#callable:com.google.gson.internal.GsonTypes.equal}} -->
The `equal` method checks if two objects are equal using `Objects.equals`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `a`: The first object to be compared.
    - `b`: The second object to be compared.
- **Control Flow**:
    - The method uses `Objects.equals(a, b)` to determine if the two objects are equal.
- **Output**:
    - A boolean value indicating whether the two objects are equal.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.equals<!-- {{#callable:com.google.gson.internal.GsonTypes.equals}} -->
The [`equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals) method checks if two `Type` objects are equal by comparing their specific characteristics based on their type categories.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `a`: The first `Type` object to be compared.
    - `b`: The second `Type` object to be compared.
- **Control Flow**:
    - Check if `a` and `b` are the same object or both null, returning true if so.
    - If `a` is an instance of `Class`, use its [`equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals) method to compare with `b`.
    - If `a` is an instance of `ParameterizedType`, check if `b` is also a `ParameterizedType` and compare their owner types, raw types, and actual type arguments.
    - If `a` is an instance of `GenericArrayType`, check if `b` is also a `GenericArrayType` and compare their generic component types recursively.
    - If `a` is an instance of `WildcardType`, check if `b` is also a `WildcardType` and compare their upper and lower bounds.
    - If `a` is an instance of `TypeVariable`, check if `b` is also a `TypeVariable` and compare their generic declarations and names.
    - Return false if none of the above conditions are met, indicating that the types are not supported or not equal.
- **Output**:
    - A boolean value indicating whether the two `Type` objects are considered equal.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals)
    - [`com.google.gson.internal.GsonTypes.equal`](#GsonTypesequal)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getOwnerType`](#ParameterizedTypeImplgetOwnerType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getRawType`](#ParameterizedTypeImplgetRawType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](#GenericArrayTypeImplgetGenericComponentType)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](#WildcardTypeImplgetUpperBounds)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getLowerBounds`](#WildcardTypeImplgetLowerBounds)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.typeToString<!-- {{#callable:com.google.gson.internal.GsonTypes.typeToString}} -->
The `typeToString` method converts a `Type` object to its string representation, either by returning the class name if it's a `Class` instance or using the `toString` method otherwise.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `type`: A `Type` object that represents a Java type, which can be a class, parameterized type, generic array type, wildcard type, or type variable.
- **Control Flow**:
    - Check if the input `type` is an instance of `Class`.
    - If true, cast `type` to `Class<?>` and return its name using `getName()`.
    - If false, return the result of `type.toString()`.
- **Output**:
    - A `String` representing the name of the class if `type` is a `Class`, or the string representation of `type` otherwise.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.getGenericSupertype<!-- {{#callable:com.google.gson.internal.GsonTypes.getGenericSupertype}} -->
The `getGenericSupertype` method determines the generic supertype of a given class or interface within a specified context.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `context`: The type context from which to resolve the supertype.
    - `rawType`: The raw class type of the context.
    - `supertype`: The class or interface for which the generic supertype is being determined.
- **Control Flow**:
    - Check if the `supertype` is the same as `rawType`, and if so, return the `context` as the result.
    - If `supertype` is an interface, iterate over the interfaces implemented by `rawType`.
    - For each interface, check if it matches `supertype` and return the corresponding generic interface if it does.
    - If `supertype` is assignable from an interface, recursively call `getGenericSupertype` with the generic interface and its raw type.
    - If `rawType` is not an interface, iterate through its superclass hierarchy until reaching `Object.class`.
    - For each superclass, check if it matches `supertype` and return the corresponding generic superclass if it does.
    - If `supertype` is assignable from a superclass, recursively call `getGenericSupertype` with the generic superclass and its raw type.
    - If no match is found, return `supertype` as the default result.
- **Output**:
    - The method returns a `Type` representing the generic supertype of the specified `supertype` within the given context.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.getSupertype<!-- {{#callable:com.google.gson.internal.GsonTypes.getSupertype}} -->
The `getSupertype` method resolves and returns the generic supertype of a given context type for a specified supertype class.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `context`: The `Type` representing the context from which the supertype is to be resolved.
    - `contextRawType`: The `Class<?>` representing the raw type of the context.
    - `supertype`: The `Class<?>` representing the supertype to be resolved.
- **Control Flow**:
    - Check if the `context` is an instance of `WildcardType` and if so, replace it with its upper bound since wildcards are not useful for resolving supertypes.
    - Assert that the `supertype` is assignable from `contextRawType` using [`checkArgument`](GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument).
    - Call the [`resolve`](#GsonTypesresolve) method with the `context`, `contextRawType`, and the result of `GsonTypes.getGenericSupertype` to resolve the supertype.
- **Output**:
    - Returns a `Type` that represents the resolved generic supertype of the given context for the specified supertype class.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](#WildcardTypeImplgetUpperBounds)
    - [`com.google.gson.internal.GsonPreconditions.checkArgument`](GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument)
    - [`com.google.gson.internal.GsonTypes.resolve`](#GsonTypesresolve)
    - [`com.google.gson.internal.GsonTypes.getGenericSupertype`](#GsonTypesgetGenericSupertype)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.getArrayComponentType<!-- {{#callable:com.google.gson.internal.GsonTypes.getArrayComponentType}} -->
The `getArrayComponentType` method returns the component type of a given array type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `array`: A `Type` object representing the array whose component type is to be determined.
- **Control Flow**:
    - Check if the input `array` is an instance of `GenericArrayType`.
    - If true, cast `array` to `GenericArrayType` and return its generic component type using `getGenericComponentType()`.
    - If false, cast `array` to `Class<?>` and return its component type using `getComponentType()`.
- **Output**:
    - The method returns a `Type` object representing the component type of the input array.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](#GenericArrayTypeImplgetGenericComponentType)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.getCollectionElementType<!-- {{#callable:com.google.gson.internal.GsonTypes.getCollectionElementType}} -->
The `getCollectionElementType` method determines the element type of a collection given its context and raw type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `context`: The `Type` representing the context in which the collection is used.
    - `contextRawType`: The `Class<?>` representing the raw type of the context.
- **Control Flow**:
    - Call [`getSupertype`](#GsonTypesgetSupertype) with `context`, `contextRawType`, and `Collection.class` to get the collection type.
    - Check if the resulting `collectionType` is an instance of `ParameterizedType`.
    - If `collectionType` is a `ParameterizedType`, return the first actual type argument as the element type.
    - If `collectionType` is not a `ParameterizedType`, return `Object.class` as the default element type.
- **Output**:
    - The method returns a `Type` representing the element type of the collection, or `Object.class` if the element type cannot be determined.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.getSupertype`](#GsonTypesgetSupertype)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](#ParameterizedTypeImplgetActualTypeArguments)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.getMapKeyAndValueTypes<!-- {{#callable:com.google.gson.internal.GsonTypes.getMapKeyAndValueTypes}} -->
The `getMapKeyAndValueTypes` method returns the key and value types of a map given its context and raw type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `context`: The `Type` representing the context in which the map is used.
    - `contextRawType`: The `Class<?>` representing the raw type of the context.
- **Control Flow**:
    - Check if the `contextRawType` is assignable from `Properties.class`; if true, return an array with `String.class` for both key and value types.
    - Invoke [`getSupertype`](#GsonTypesgetSupertype) to obtain the map type from the context and context raw type.
    - Check if the obtained map type is an instance of `ParameterizedType`; if true, cast it and return its actual type arguments.
    - If the map type is not parameterized, return an array with `Object.class` for both key and value types.
- **Output**:
    - An array of `Type` objects representing the key and value types of the map.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.getSupertype`](#GsonTypesgetSupertype)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](#ParameterizedTypeImplgetActualTypeArguments)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.resolve<!-- {{#callable:com.google.gson.internal.GsonTypes.resolve}} -->
The [`resolve`](#GsonTypesresolve) method resolves a given type within a specified context and raw type, using a map to track visited type variables.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `context`: The context type in which the resolution is being performed.
    - `contextRawType`: The raw class type of the context.
    - `toResolve`: The type that needs to be resolved.
- **Control Flow**:
    - The method calls another overloaded [`resolve`](#GsonTypesresolve) method, passing the context, contextRawType, toResolve, and a new HashMap for tracking visited type variables.
    - The overloaded [`resolve`](#GsonTypesresolve) method handles different cases of the `toResolve` type, such as TypeVariable, Class, GenericArrayType, ParameterizedType, and WildcardType, to resolve the type appropriately.
    - If `toResolve` is a TypeVariable, it checks if it has been previously resolved to avoid infinite recursion, and attempts to resolve it using `resolveTypeVariable`.
    - For array types, it resolves the component type and constructs a new array type if necessary.
    - For parameterized types, it resolves the owner type and actual type arguments, creating a new parameterized type if any changes occur.
    - For wildcard types, it resolves the upper or lower bounds and constructs a new wildcard type if necessary.
    - The method updates the map of visited type variables with the final resolved type before returning it.
- **Output**:
    - The method returns the resolved Type, which may be the same as the input type if no resolution was necessary.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.resolve`](#GsonTypesresolve)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.resolve<!-- {{#callable:com.google.gson.internal.GsonTypes.resolve}} -->
The [`resolve`](#GsonTypesresolve) method recursively resolves a given `Type` to its most specific form, handling various type scenarios such as type variables, arrays, parameterized types, and wildcard types, while avoiding infinite recursion.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `context`: The context `Type` from which the resolution is initiated.
    - `contextRawType`: The raw `Class` type of the context.
    - `toResolve`: The `Type` that needs to be resolved.
    - `visitedTypeVariables`: A map tracking `TypeVariable` instances that have been visited to prevent infinite recursion.
- **Control Flow**:
    - Initialize a `TypeVariable` named `resolving` to null.
    - Enter a loop to process the `toResolve` type until it is fully resolved.
    - If `toResolve` is a `TypeVariable`, check if it has been previously resolved using `visitedTypeVariables`. If so, return the resolved type or the original if marked as `Void.TYPE`.
    - Mark the `TypeVariable` as being resolved by putting it in `visitedTypeVariables` with `Void.TYPE` as a placeholder.
    - Resolve the `TypeVariable` using [`resolveTypeVariable`](#GsonTypesresolveTypeVariable) and update `toResolve`. If it remains unchanged, break the loop.
    - If `toResolve` is a `Class` representing an array, resolve its component type recursively and update `toResolve` accordingly.
    - If `toResolve` is a `GenericArrayType`, resolve its component type recursively and update `toResolve` accordingly.
    - If `toResolve` is a `ParameterizedType`, resolve its owner type and actual type arguments recursively, and update `toResolve` if any changes occur.
    - If `toResolve` is a `WildcardType`, resolve its bounds recursively and update `toResolve` if any changes occur.
    - After exiting the loop, update any in-process resolution in `visitedTypeVariables` with the final resolved type.
    - Return the resolved `Type`.
- **Output**:
    - The method returns the resolved `Type`, which is the most specific form of the input `toResolve` type.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.put`](LinkedTreeMap.java.driver.md#LinkedTreeMapput)
    - [`com.google.gson.internal.GsonTypes.resolveTypeVariable`](#GsonTypesresolveTypeVariable)
    - [`com.google.gson.internal.GsonTypes.resolve`](#GsonTypesresolve)
    - [`com.google.gson.internal.GsonTypes.equal`](#GsonTypesequal)
    - [`com.google.gson.internal.GsonTypes.arrayOf`](#GsonTypesarrayOf)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](#GenericArrayTypeImplgetGenericComponentType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getOwnerType`](#ParameterizedTypeImplgetOwnerType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.internal.Excluder.clone`](Excluder.java.driver.md#Excluderclone)
    - [`com.google.gson.internal.GsonTypes.newParameterizedTypeWithOwner`](#GsonTypesnewParameterizedTypeWithOwner)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getRawType`](#ParameterizedTypeImplgetRawType)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getLowerBounds`](#WildcardTypeImplgetLowerBounds)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](#WildcardTypeImplgetUpperBounds)
    - [`com.google.gson.internal.GsonTypes.supertypeOf`](#GsonTypessupertypeOf)
    - [`com.google.gson.internal.GsonTypes.subtypeOf`](#GsonTypessubtypeOf)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.resolveTypeVariable<!-- {{#callable:com.google.gson.internal.GsonTypes.resolveTypeVariable}} -->
The `resolveTypeVariable` method attempts to resolve a `TypeVariable` to a concrete `Type` within a given context and its raw type.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `context`: The `Type` context in which the `TypeVariable` is being resolved.
    - `contextRawType`: The raw `Class` type of the context.
    - `unknown`: The `TypeVariable` that needs to be resolved.
- **Control Flow**:
    - Determine the declaring class of the `unknown` `TypeVariable` using [`declaringClassOf`](#GsonTypesdeclaringClassOf) method.
    - If the declaring class is `null`, return the `unknown` `TypeVariable` as it cannot be resolved further.
    - Retrieve the generic supertype of the declaring class within the context using [`getGenericSupertype`](#GsonTypesgetGenericSupertype).
    - Check if the retrieved type is an instance of `ParameterizedType`.
    - If it is a `ParameterizedType`, find the index of the `unknown` `TypeVariable` in the declaring class's type parameters.
    - Return the actual type argument at the found index from the `ParameterizedType`.
    - If not a `ParameterizedType`, return the `unknown` `TypeVariable` as it cannot be resolved further.
- **Output**:
    - The method returns a `Type` that represents the resolved type of the `TypeVariable`, or the `TypeVariable` itself if it cannot be resolved.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.declaringClassOf`](#GsonTypesdeclaringClassOf)
    - [`com.google.gson.internal.GsonTypes.getGenericSupertype`](#GsonTypesgetGenericSupertype)
    - [`com.google.gson.internal.GsonTypes.indexOf`](#GsonTypesindexOf)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](#ParameterizedTypeImplgetActualTypeArguments)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.indexOf<!-- {{#callable:com.google.gson.internal.GsonTypes.indexOf}} -->
The `indexOf` method searches for a specified object in an array and returns its index if found, or throws a `NoSuchElementException` if not found.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `array`: An array of `Object` elements to search through.
    - `toFind`: The `Object` to search for within the array.
- **Control Flow**:
    - Initialize a loop to iterate over the array from index 0 to the length of the array.
    - For each element in the array, check if it is equal to the `toFind` object using the [`equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals) method.
    - If a match is found, return the current index.
    - If the loop completes without finding a match, throw a `NoSuchElementException`.
- **Output**:
    - Returns the index of the `toFind` object in the array if found; otherwise, throws a `NoSuchElementException`.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.declaringClassOf<!-- {{#callable:com.google.gson.internal.GsonTypes.declaringClassOf}} -->
The `declaringClassOf` method returns the declaring class of a given `TypeVariable`, or `null` if it was not declared by a class.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `typeVariable`: A `TypeVariable<?>` whose declaring class is to be determined.
- **Control Flow**:
    - Retrieve the `GenericDeclaration` of the provided `typeVariable`.
    - Check if the `genericDeclaration` is an instance of `Class`.
    - If it is, cast and return it as a `Class<?>`.
    - If it is not, return `null`.
- **Output**:
    - The method returns a `Class<?>` representing the declaring class of the `typeVariable`, or `null` if the `typeVariable` was not declared by a class.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.checkNotPrimitive<!-- {{#callable:com.google.gson.internal.GsonTypes.checkNotPrimitive}} -->
The `checkNotPrimitive` method ensures that the provided `Type` is not a primitive type.
- **Modifiers**: `static`
- **Inputs**:
    - `type`: The `Type` object to be checked to ensure it is not a primitive type.
- **Control Flow**:
    - The method uses the [`checkArgument`](GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument) function to assert that the provided `type` is not an instance of `Class` or, if it is, that it is not a primitive type by checking `!((Class<?>) type).isPrimitive()`.
- **Output**:
    - The method does not return any value; it throws an exception if the condition is not met.
- **Functions called**:
    - [`com.google.gson.internal.GsonPreconditions.checkArgument`](GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument)
    - [`com.google.gson.internal.Primitives.isPrimitive`](Primitives.java.driver.md#PrimitivesisPrimitive)
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)


---
#### GsonTypes\.requiresOwnerType<!-- {{#callable:com.google.gson.internal.GsonTypes.requiresOwnerType}} -->
The `requiresOwnerType` method checks if a given `Type` requires an owner type when constructing a `ParameterizedType`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `rawType`: The `Type` object to be checked, which can be an instance of `Class<?>`.
- **Control Flow**:
    - Check if `rawType` is an instance of `Class<?>`.
    - If true, cast `rawType` to `Class<?>` and store it in `rawTypeAsClass`.
    - Return `true` if `rawTypeAsClass` is not static and has a declaring class, otherwise return `false`.
    - If `rawType` is not an instance of `Class<?>`, return `false`.
- **Output**:
    - A boolean value indicating whether the `Type` requires an owner type.
- **See also**: [`com.google.gson.internal.GsonTypes`](#GsonTypes)  (Base Class)



---
### ParameterizedTypeImpl<!-- {{#class:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `ParameterizedTypeImpl` class is a private, static, and final implementation of the `ParameterizedType` interface, designed to represent parameterized types with an optional owner type, a raw type, and an array of type arguments. It ensures that the raw type is not null and that the type arguments are not primitive types, while providing methods to retrieve the actual type arguments, raw type, and owner type. The class also overrides `equals`, `hashCode`, and `toString` methods to provide appropriate behavior for parameterized types, and it implements `Serializable` to allow instances to be serialized.
- **Fields**:
    - `ownerType`: `Type` The type that owns this parameterized type, or null if there is no owner.
    - `rawType`: `Type` The raw type of this parameterized type, which cannot be null.
    - `typeArguments`: `Type[]` An array of type arguments for this parameterized type, which are cloned to ensure immutability.
- **Methods**:
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.ParameterizedTypeImpl`](#ParameterizedTypeImplParameterizedTypeImpl)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getRawType`](#ParameterizedTypeImplgetRawType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getOwnerType`](#ParameterizedTypeImplgetOwnerType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.equals`](#ParameterizedTypeImplequals)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.hashCodeOrZero`](#ParameterizedTypeImplhashCodeOrZero)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.hashCode`](#ParameterizedTypeImplhashCode)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.toString`](#ParameterizedTypeImpltoString)
- **Extends/Implements**:
    - `ParameterizedType`
    - `Serializable`

**Methods**

---
#### ParameterizedTypeImpl\.ParameterizedTypeImpl<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.ParameterizedTypeImpl}} -->
The `ParameterizedTypeImpl` constructor initializes a parameterized type with a specified owner type, raw type, and type arguments, ensuring all inputs are valid and canonicalized.
- **Modifiers**: `public`
- **Inputs**:
    - `ownerType`: The type that owns the parameterized type, or null if there is no owner.
    - `rawType`: The raw class type that is being parameterized.
    - `typeArguments`: An array of types representing the type arguments for the parameterized type.
- **Control Flow**:
    - The method begins by ensuring the `rawType` is not null using `requireNonNull(rawType)`.
    - It checks if `ownerType` is null and if the `rawType` requires an owner type using `requiresOwnerType(rawType)`, throwing an `IllegalArgumentException` if necessary.
    - The `ownerType` is set to null or its canonicalized form, and `rawType` is set to its canonicalized form.
    - The `typeArguments` array is cloned to avoid external modifications.
    - A loop iterates over each type argument, ensuring each is not null, not primitive, and is canonicalized.
- **Output**:
    - The constructor does not return a value, as it initializes an instance of `ParameterizedTypeImpl`.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.requiresOwnerType`](#GsonTypesrequiresOwnerType)
    - [`com.google.gson.internal.GsonTypes.canonicalize`](#GsonTypescanonicalize)
    - [`com.google.gson.internal.Excluder.clone`](Excluder.java.driver.md#Excluderclone)
    - [`com.google.gson.internal.GsonTypes.checkNotPrimitive`](#GsonTypescheckNotPrimitive)
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)


---
#### ParameterizedTypeImpl\.getActualTypeArguments<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments}} -->
The `getActualTypeArguments` method returns a clone of the `typeArguments` array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns a clone of the `typeArguments` array, ensuring that the original array is not modified by the caller.
- **Output**:
    - A clone of the `typeArguments` array, which is an array of `Type` objects.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.clone`](Excluder.java.driver.md#Excluderclone)
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)


---
#### ParameterizedTypeImpl\.getRawType<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getRawType}} -->
The `getRawType` method returns the raw type of a parameterized type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `rawType` field.
- **Output**:
    - The method returns a `Type` object representing the raw type.
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)


---
#### ParameterizedTypeImpl\.getOwnerType<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getOwnerType}} -->
The `getOwnerType` method returns the owner type of a parameterized type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `ownerType` field.
- **Output**:
    - The method returns a `Type` object representing the owner type.
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)


---
#### ParameterizedTypeImpl\.equals<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.equals}} -->
The [`equals`](#GsonTypesequals) method checks if the current `ParameterizedTypeImpl` instance is equal to another object by verifying if the other object is an instance of `ParameterizedType` and then using the `GsonTypes.equals` method for further comparison.
- **Modifiers**: `public`
- **Inputs**:
    - `other`: An `Object` that is to be compared with the current instance for equality.
- **Control Flow**:
    - The method first checks if the `other` object is an instance of `ParameterizedType`.
    - If `other` is an instance of `ParameterizedType`, it calls `GsonTypes.equals` to compare the current instance with `other` cast to `ParameterizedType`.
    - The result of the `GsonTypes.equals` method is returned as the result of the [`equals`](#GsonTypesequals) method.
- **Output**:
    - A boolean value indicating whether the current instance is equal to the `other` object.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.equals`](#GsonTypesequals)
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)


---
#### ParameterizedTypeImpl\.hashCodeOrZero<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.hashCodeOrZero}} -->
The `hashCodeOrZero` method returns the hash code of an object if it is not null, otherwise it returns zero.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `o`: An object whose hash code is to be returned, or zero if the object is null.
- **Control Flow**:
    - Check if the object `o` is not null.
    - If `o` is not null, return the result of `o.hashCode()`.
    - If `o` is null, return 0.
- **Output**:
    - An integer representing the hash code of the object `o` if it is not null, or zero if `o` is null.
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)


---
#### ParameterizedTypeImpl\.hashCode<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.hashCode}} -->
The `hashCode` method computes a hash code for a `ParameterizedTypeImpl` instance using its type arguments, raw type, and owner type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls `Arrays.hashCode(typeArguments)` to compute the hash code of the `typeArguments` array.
    - It calls `rawType.hashCode()` to get the hash code of the `rawType`.
    - It calls `hashCodeOrZero(ownerType)` to get the hash code of the `ownerType`, or zero if `ownerType` is null.
    - The method combines these hash codes using the XOR (^) operator and returns the result.
- **Output**:
    - An integer representing the hash code of the `ParameterizedTypeImpl` instance.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.hashCodeOrZero`](#ParameterizedTypeImplhashCodeOrZero)
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)


---
#### ParameterizedTypeImpl\.toString<!-- {{#callable:com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.toString}} -->
The [`toString`](ConstructorConstructor.java.driver.md#ConstructorConstructortoString) method generates a string representation of a parameterized type, including its raw type and type arguments.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Determine the number of type arguments using `typeArguments.length`.
    - If there are no type arguments, return the string representation of the raw type using `typeToString(rawType)`.
    - Initialize a `StringBuilder` with an estimated capacity based on the number of type arguments.
    - Append the string representation of the raw type to the `StringBuilder`.
    - Append the string representation of the first type argument enclosed in angle brackets.
    - Iterate over the remaining type arguments, appending each one prefixed by a comma and space.
    - Append a closing angle bracket to the `StringBuilder`.
    - Convert the `StringBuilder` to a string and return it.
- **Output**:
    - A string representation of the parameterized type, including its raw type and type arguments.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.typeToString`](#GsonTypestypeToString)
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](Streams.java.driver.md#AppendableWriterappend)
    - [`com.google.gson.internal.ConstructorConstructor.toString`](ConstructorConstructor.java.driver.md#ConstructorConstructortoString)
- **See also**: [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl`](#GsonTypes.ParameterizedTypeImpl)  (Base Class)



---
### GenericArrayTypeImpl<!-- {{#class:com.google.gson.internal.GsonTypes.GenericArrayTypeImpl}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `GenericArrayTypeImpl` class is a private, static, and final implementation of the `GenericArrayType` interface, designed to represent array types with a generic component type in Java. It is part of the internal implementation of the Gson library, providing a way to handle generic array types in a serializable manner. The class ensures that the component type is non-null and canonicalized, and it overrides methods for equality, hash code generation, and string representation to facilitate its use in type comparisons and debugging.
- **Fields**:
    - `componentType`: `Type` The generic component type of the array, which is ensured to be non-null and canonicalized.
- **Methods**:
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.GenericArrayTypeImpl`](#GenericArrayTypeImplGenericArrayTypeImpl)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](#GenericArrayTypeImplgetGenericComponentType)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.equals`](#GenericArrayTypeImplequals)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.hashCode`](#GenericArrayTypeImplhashCode)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.toString`](#GenericArrayTypeImpltoString)
- **Extends/Implements**:
    - `GenericArrayType`
    - `Serializable`

**Methods**

---
#### GenericArrayTypeImpl\.GenericArrayTypeImpl<!-- {{#callable:com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.GenericArrayTypeImpl}} -->
The `GenericArrayTypeImpl` constructor initializes a new instance of the class with a specified component type, ensuring it is non-null and canonicalized.
- **Modifiers**: `public`
- **Inputs**:
    - `componentType`: The `Type` representing the component type of the generic array.
- **Control Flow**:
    - The method first checks that the `componentType` is not null using `requireNonNull(componentType)`.
    - It then assigns the `componentType` field of the instance to the result of `canonicalize(componentType)`, which ensures the type is in a standard form.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of `GenericArrayTypeImpl`.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.canonicalize`](#GsonTypescanonicalize)
- **See also**: [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl`](#GsonTypes.GenericArrayTypeImpl)  (Base Class)


---
#### GenericArrayTypeImpl\.getGenericComponentType<!-- {{#callable:com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType}} -->
The `getGenericComponentType` method returns the component type of a generic array type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the `componentType` field.
- **Output**:
    - The method returns a `Type` object representing the component type of the generic array.
- **See also**: [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl`](#GsonTypes.GenericArrayTypeImpl)  (Base Class)


---
#### GenericArrayTypeImpl\.equals<!-- {{#callable:com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.equals}} -->
The [`equals`](#GsonTypesequals) method checks if the given object is an instance of `GenericArrayType` and if so, compares it with the current instance using the `GsonTypes.equals` method.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: An object to be compared with the current instance.
- **Control Flow**:
    - The method first checks if the input object `o` is an instance of `GenericArrayType`.
    - If `o` is an instance of `GenericArrayType`, it calls `GsonTypes.equals` to compare the current instance with `o`.
    - The result of the `GsonTypes.equals` method is returned as the output of the [`equals`](#GsonTypesequals) method.
- **Output**:
    - A boolean value indicating whether the current instance is equal to the input object `o`.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.equals`](#GsonTypesequals)
- **See also**: [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl`](#GsonTypes.GenericArrayTypeImpl)  (Base Class)


---
#### GenericArrayTypeImpl\.hashCode<!-- {{#callable:com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.hashCode}} -->
The `hashCode` method returns the hash code of the `componentType` field.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling `hashCode()` on the `componentType` field.
- **Output**:
    - An integer representing the hash code of the `componentType`.
- **See also**: [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl`](#GsonTypes.GenericArrayTypeImpl)  (Base Class)


---
#### GenericArrayTypeImpl\.toString<!-- {{#callable:com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.toString}} -->
The `toString` method returns a string representation of a generic array type, appending '[]' to the string representation of its component type.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`typeToString`](#GsonTypestypeToString) with `componentType` as an argument to get the string representation of the component type.
    - It concatenates the result with '[]' to represent the array type.
    - The concatenated string is returned as the output.
- **Output**:
    - A `String` representing the array type, formatted as the component type followed by '[]'.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.typeToString`](#GsonTypestypeToString)
- **See also**: [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl`](#GsonTypes.GenericArrayTypeImpl)  (Base Class)



---
### WildcardTypeImpl<!-- {{#class:com.google.gson.internal.GsonTypes.WildcardTypeImpl}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `WildcardTypeImpl` class is a private, static, and final implementation of the `WildcardType` interface, designed to represent wildcard types with optional upper and lower bounds in Java's type system. It ensures that the wildcard type has at most one upper bound and one lower bound, with specific checks to ensure that if a lower bound is set, the upper bound must be `Object.class`. The class provides methods to retrieve these bounds and overrides `equals`, `hashCode`, and `toString` methods to ensure proper comparison and representation of wildcard types.
- **Fields**:
    - `upperBound`: `Type` The upper bound of the wildcard type, defaulting to `Object.class` if no lower bound is specified.
    - `lowerBound`: `Type` The lower bound of the wildcard type, which is null if no lower bound is specified.
- **Methods**:
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.WildcardTypeImpl`](#WildcardTypeImplWildcardTypeImpl)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](#WildcardTypeImplgetUpperBounds)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getLowerBounds`](#WildcardTypeImplgetLowerBounds)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.equals`](#WildcardTypeImplequals)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.hashCode`](#WildcardTypeImplhashCode)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.toString`](#WildcardTypeImpltoString)
- **Extends/Implements**:
    - `WildcardType`
    - `Serializable`

**Methods**

---
#### WildcardTypeImpl\.WildcardTypeImpl<!-- {{#callable:com.google.gson.internal.GsonTypes.WildcardTypeImpl.WildcardTypeImpl}} -->
The `WildcardTypeImpl` constructor initializes a wildcard type with specified upper and lower bounds, ensuring constraints on the bounds are met.
- **Modifiers**: `public`
- **Inputs**:
    - `upperBounds`: An array of `Type` objects representing the upper bounds of the wildcard type.
    - `lowerBounds`: An array of `Type` objects representing the lower bounds of the wildcard type.
- **Control Flow**:
    - Check that the length of `lowerBounds` is at most 1.
    - Check that the length of `upperBounds` is exactly 1.
    - If `lowerBounds` has one element, ensure it is not null, not primitive, and that `upperBounds[0]` is `Object.class`. Then, set `lowerBound` to the canonicalized version of `lowerBounds[0]` and `upperBound` to `Object.class`.
    - If `lowerBounds` is empty, ensure `upperBounds[0]` is not null and not primitive. Then, set `lowerBound` to `null` and `upperBound` to the canonicalized version of `upperBounds[0]`.
- **Output**:
    - An instance of `WildcardTypeImpl` with the specified upper and lower bounds.
- **Functions called**:
    - [`com.google.gson.internal.GsonPreconditions.checkArgument`](GsonPreconditions.java.driver.md#GsonPreconditionscheckArgument)
    - [`com.google.gson.internal.GsonTypes.checkNotPrimitive`](#GsonTypescheckNotPrimitive)
    - [`com.google.gson.internal.GsonTypes.canonicalize`](#GsonTypescanonicalize)
- **See also**: [`com.google.gson.internal.GsonTypes.WildcardTypeImpl`](#GsonTypes.WildcardTypeImpl)  (Base Class)


---
#### WildcardTypeImpl\.getUpperBounds<!-- {{#callable:com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds}} -->
The `getUpperBounds` method returns an array containing the upper bound of a wildcard type.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - The method creates a new array of `Type` with a single element, `upperBound`.
    - It returns this newly created array.
- **Output**:
    - An array of `Type` containing the upper bound of the wildcard type.
- **See also**: [`com.google.gson.internal.GsonTypes.WildcardTypeImpl`](#GsonTypes.WildcardTypeImpl)  (Base Class)


---
#### WildcardTypeImpl\.getLowerBounds<!-- {{#callable:com.google.gson.internal.GsonTypes.WildcardTypeImpl.getLowerBounds}} -->
The `getLowerBounds` method returns an array of lower bounds for a wildcard type, or an empty array if no lower bounds are specified.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if `lowerBound` is not null.
    - If `lowerBound` is not null, return a new array containing `lowerBound`.
    - If `lowerBound` is null, return `EMPTY_TYPE_ARRAY`.
- **Output**:
    - An array of `Type` objects representing the lower bounds of a wildcard type.
- **See also**: [`com.google.gson.internal.GsonTypes.WildcardTypeImpl`](#GsonTypes.WildcardTypeImpl)  (Base Class)


---
#### WildcardTypeImpl\.equals<!-- {{#callable:com.google.gson.internal.GsonTypes.WildcardTypeImpl.equals}} -->
The [`equals`](#GsonTypesequals) method checks if the given object is a `WildcardType` and if it is equal to the current instance using the `GsonTypes.equals` method.
- **Modifiers**: `public`
- **Inputs**:
    - `other`: An `Object` that is to be compared with the current instance for equality.
- **Control Flow**:
    - The method first checks if the `other` object is an instance of `WildcardType`.
    - If `other` is a `WildcardType`, it calls `GsonTypes.equals` to compare the current instance with `other`.
    - The result of the `GsonTypes.equals` method is returned as the result of the [`equals`](#GsonTypesequals) method.
- **Output**:
    - A `boolean` value indicating whether the `other` object is equal to the current instance.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.equals`](#GsonTypesequals)
- **See also**: [`com.google.gson.internal.GsonTypes.WildcardTypeImpl`](#GsonTypes.WildcardTypeImpl)  (Base Class)


---
#### WildcardTypeImpl\.hashCode<!-- {{#callable:com.google.gson.internal.GsonTypes.WildcardTypeImpl.hashCode}} -->
The [`hashCode`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListhashCode) method computes a hash code for a `WildcardTypeImpl` object based on its lower and upper bounds.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if `lowerBound` is not null.
    - If `lowerBound` is not null, compute the hash code as `31 + lowerBound.hashCode()`, otherwise use `1`.
    - Compute the hash code for `upperBound` as `31 + upperBound.hashCode()`.
    - Return the XOR of the two computed hash codes.
- **Output**:
    - An integer representing the hash code of the `WildcardTypeImpl` object.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.hashCode`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListhashCode)
- **See also**: [`com.google.gson.internal.GsonTypes.WildcardTypeImpl`](#GsonTypes.WildcardTypeImpl)  (Base Class)


---
#### WildcardTypeImpl\.toString<!-- {{#callable:com.google.gson.internal.GsonTypes.WildcardTypeImpl.toString}} -->
The `toString` method returns a string representation of a wildcard type, indicating its bounds.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if `lowerBound` is not null; if true, return a string in the format `? super <lowerBound>` using [`typeToString`](#GsonTypestypeToString) method.
    - If `lowerBound` is null, check if `upperBound` is `Object.class`; if true, return `?`.
    - If neither condition is met, return a string in the format `? extends <upperBound>` using [`typeToString`](#GsonTypestypeToString) method.
- **Output**:
    - A string representation of the wildcard type, indicating whether it is a supertype or subtype and its respective bound.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.typeToString`](#GsonTypestypeToString)
- **See also**: [`com.google.gson.internal.GsonTypes.WildcardTypeImpl`](#GsonTypes.WildcardTypeImpl)  (Base Class)



