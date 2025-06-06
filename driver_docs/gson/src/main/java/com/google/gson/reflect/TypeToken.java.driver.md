# Purpose
The provided Java source code defines a class named [`TypeToken`](#TypeTokenTypeToken) within the `com.google.gson.reflect` package. This class is a crucial component of the Gson library, which is used for serializing and deserializing Java objects to and from JSON. The primary purpose of the [`TypeToken`](#TypeTokenTypeToken) class is to capture and represent generic type information at runtime, which is otherwise lost due to Java's type erasure. This is achieved by forcing clients to create an anonymous subclass of [`TypeToken`](#TypeTokenTypeToken), embedding the type parameter in the subclass's type hierarchy, thus allowing the retrieval of type information even after compilation.

The [`TypeToken`](#TypeTokenTypeToken) class provides several methods to facilitate the creation and manipulation of type tokens, such as [`get`](#TypeTokenget), [`getParameterized`](#TypeTokengetParameterized), and [`getArray`](#TypeTokengetArray), which allow users to create type tokens for specific types, parameterized types, and array types, respectively. It also includes methods like [`isAssignableFrom`](#TypeTokenisAssignableFrom) to check type compatibility, although these are marked as deprecated due to potential inconsistencies with Java's type system. The class handles various Java reflection types, including `ParameterizedType`, `GenericArrayType`, and `TypeVariable`, ensuring that type arguments are valid and do not contain type variables that could lead to runtime exceptions. Overall, [`TypeToken`](#TypeTokenTypeToken) is a foundational utility in Gson for managing complex type information, enabling robust JSON serialization and deserialization processes.
# Imports and Dependencies

---
- `com.google.gson.reflect`
- `com.google.gson.internal.GsonTypes`
- `com.google.gson.internal.TroubleshootingGuide`
- `java.lang.reflect.GenericArrayType`
- `java.lang.reflect.ParameterizedType`
- `java.lang.reflect.Type`
- `java.lang.reflect.TypeVariable`
- `java.lang.reflect.WildcardType`
- `java.util.HashMap`
- `java.util.Map`
- `java.util.Objects`


# Classes

---
### TypeToken<!-- {{#class:com.google.gson.reflect.TypeToken}} -->
- **Modifiers**: `public`
- **Description**: The `TypeToken` class is a utility in the Gson library that represents a generic type `T` and allows for the capture and manipulation of generic type information at runtime, overcoming Java's type erasure limitations. It is designed to be subclassed anonymously to embed type parameters in the class hierarchy, enabling the retrieval of type information even after compilation. This class provides methods to obtain raw types, check type assignability, and create type tokens for parameterized and array types, while also ensuring type safety and consistency with Java's type system.
- **Fields**:
    - `rawType`: `Class<? super T>` Holds the raw (non-generic) class type for the generic type `T`.
    - `type`: `Type` Stores the underlying `Type` instance representing the generic type `T`.
    - `hashCode`: `int` Caches the hash code of the `Type` instance for performance optimization.
- **Methods**:
    - [`com.google.gson.reflect.TypeToken.TypeToken`](#TypeTokenTypeToken)
    - [`com.google.gson.reflect.TypeToken.TypeToken`](#TypeTokenTypeToken)
    - [`com.google.gson.reflect.TypeToken.isCapturingTypeVariablesForbidden`](#TypeTokenisCapturingTypeVariablesForbidden)
    - [`com.google.gson.reflect.TypeToken.getTypeTokenTypeArgument`](#TypeTokengetTypeTokenTypeArgument)
    - [`com.google.gson.reflect.TypeToken.verifyNoTypeVariable`](#TypeTokenverifyNoTypeVariable)
    - [`com.google.gson.reflect.TypeToken.getRawType`](#TypeTokengetRawType)
    - [`com.google.gson.reflect.TypeToken.getType`](#TypeTokengetType)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
    - [`com.google.gson.reflect.TypeToken.typeEquals`](#TypeTokentypeEquals)
    - [`com.google.gson.reflect.TypeToken.buildUnsupportedTypeException`](#TypeTokenbuildUnsupportedTypeException)
    - [`com.google.gson.reflect.TypeToken.matches`](#TypeTokenmatches)
    - [`com.google.gson.reflect.TypeToken.hashCode`](#TypeTokenhashCode)
    - [`com.google.gson.reflect.TypeToken.equals`](#TypeTokenequals)
    - [`com.google.gson.reflect.TypeToken.toString`](#TypeTokentoString)
    - [`com.google.gson.reflect.TypeToken.get`](#TypeTokenget)
    - [`com.google.gson.reflect.TypeToken.get`](#TypeTokenget)
    - [`com.google.gson.reflect.TypeToken.getParameterized`](#TypeTokengetParameterized)
    - [`com.google.gson.reflect.TypeToken.getArray`](#TypeTokengetArray)

**Methods**

---
#### TypeToken\.TypeToken<!-- {{#callable:com.google.gson.reflect.TypeToken.TypeToken}} -->
The `TypeToken` constructor initializes a new instance by determining the type argument and raw type of the generic type `T`, and calculates its hash code.
- **Modifiers**: `protected`
- **Inputs**: None
- **Control Flow**:
    - The constructor calls `getTypeTokenTypeArgument()` to determine the type argument for `T`.
    - It assigns the result to the `type` field.
    - It uses `GsonTypes.getRawType(type)` to determine the raw type of `T` and assigns it to the `rawType` field, casting it to `Class<? super T>`.
    - It calculates the hash code of the `type` and assigns it to the [`hashCode`](#TypeTokenhashCode) field.
- **Output**:
    - The constructor does not return a value as it is used to initialize an instance of the `TypeToken` class.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getTypeTokenTypeArgument`](#TypeTokengetTypeTokenTypeArgument)
    - [`com.google.gson.internal.GsonTypes.getRawType`](../internal/GsonTypes.java.driver.md#GsonTypesgetRawType)
    - [`com.google.gson.reflect.TypeToken.hashCode`](#TypeTokenhashCode)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.TypeToken<!-- {{#callable:com.google.gson.reflect.TypeToken.TypeToken}} -->
The private constructor `TypeToken(Type type)` initializes a `TypeToken` instance by canonicalizing the provided type, determining its raw type, and computing its hash code.
- **Modifiers**: `private`
- **Inputs**:
    - `type`: A `Type` object representing the generic type for which the `TypeToken` is being created.
- **Control Flow**:
    - The method begins by ensuring the provided `type` is not null using `Objects.requireNonNull(type)`.
    - It then canonicalizes the `type` using `GsonTypes.canonicalize` to ensure a standard representation of the type.
    - The raw type of the canonicalized type is determined using `GsonTypes.getRawType(this.type)` and cast to `Class<? super T>`.
    - The hash code of the canonicalized type is computed and stored in the [`hashCode`](#TypeTokenhashCode) field.
- **Output**:
    - The method does not return a value as it is a constructor, but it initializes the fields `type`, `rawType`, and [`hashCode`](#TypeTokenhashCode) of the `TypeToken` instance.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.canonicalize`](../internal/GsonTypes.java.driver.md#GsonTypescanonicalize)
    - [`com.google.gson.internal.GsonTypes.getRawType`](../internal/GsonTypes.java.driver.md#GsonTypesgetRawType)
    - [`com.google.gson.reflect.TypeToken.hashCode`](#TypeTokenhashCode)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.isCapturingTypeVariablesForbidden<!-- {{#callable:com.google.gson.reflect.TypeToken.isCapturingTypeVariablesForbidden}} -->
The method checks if capturing type variables is forbidden by evaluating a system property.
- **Modifiers**: `private`, `static`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the system property 'gson.allowCapturingTypeVariables'.
    - Compare the retrieved property value to the string 'true'.
    - Return the negation of the comparison result.
- **Output**:
    - A boolean value indicating whether capturing type variables is forbidden.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.getTypeTokenTypeArgument<!-- {{#callable:com.google.gson.reflect.TypeToken.getTypeTokenTypeArgument}} -->
The `getTypeTokenTypeArgument` method retrieves the type argument of the `TypeToken` class if it is a direct subclass, ensuring it is not a raw type or a subclass of a subclass.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the generic superclass of the current class using `getClass().getGenericSuperclass()`.
    - Check if the superclass is an instance of `ParameterizedType`.
    - If it is, cast it to `ParameterizedType` and check if its raw type is `TypeToken.class`.
    - If the raw type matches, canonicalize the first actual type argument using `GsonTypes.canonicalize`.
    - If capturing type variables is forbidden, verify that the type argument does not contain any type variables using [`verifyNoTypeVariable`](#TypeTokenverifyNoTypeVariable).
    - Return the canonicalized type argument.
    - If the superclass is exactly `TypeToken.class`, throw an `IllegalStateException` indicating that a type argument is required.
    - If none of the above conditions are met, throw an `IllegalStateException` indicating that only direct subclasses of `TypeToken` are allowed.
- **Output**:
    - The method returns a `Type` object representing the canonicalized type argument of the `TypeToken` class.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getRawType`](../internal/GsonTypes.java.driver.md#ParameterizedTypeImplgetRawType)
    - [`com.google.gson.internal.GsonTypes.canonicalize`](../internal/GsonTypes.java.driver.md#GsonTypescanonicalize)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](../internal/GsonTypes.java.driver.md#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.reflect.TypeToken.isCapturingTypeVariablesForbidden`](#TypeTokenisCapturingTypeVariablesForbidden)
    - [`com.google.gson.reflect.TypeToken.verifyNoTypeVariable`](#TypeTokenverifyNoTypeVariable)
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../internal/TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.verifyNoTypeVariable<!-- {{#callable:com.google.gson.reflect.TypeToken.verifyNoTypeVariable}} -->
The `verifyNoTypeVariable` method checks if a given `Type` contains any type variables and throws an exception if it does.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `type`: The `Type` object to be verified for the presence of type variables.
- **Control Flow**:
    - Check if the `type` is an instance of `TypeVariable`; if so, throw an `IllegalArgumentException` with details about the type variable.
    - If the `type` is an instance of `GenericArrayType`, recursively call `verifyNoTypeVariable` on its generic component type.
    - If the `type` is an instance of `ParameterizedType`, check its owner type and actual type arguments recursively for type variables.
    - If the `type` is an instance of `WildcardType`, check its lower and upper bounds recursively for type variables.
    - If the `type` is `null`, throw an `IllegalArgumentException` indicating a possible compiler/runtime bug.
- **Output**:
    - The method does not return a value but throws an `IllegalArgumentException` if a type variable is found or if the type is `null`.
- **Functions called**:
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../internal/TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](../internal/GsonTypes.java.driver.md#GenericArrayTypeImplgetGenericComponentType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getOwnerType`](../internal/GsonTypes.java.driver.md#ParameterizedTypeImplgetOwnerType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](../internal/GsonTypes.java.driver.md#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getLowerBounds`](../internal/GsonTypes.java.driver.md#WildcardTypeImplgetLowerBounds)
    - [`com.google.gson.internal.GsonTypes.WildcardTypeImpl.getUpperBounds`](../internal/GsonTypes.java.driver.md#WildcardTypeImplgetUpperBounds)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.getRawType<!-- {{#callable:com.google.gson.reflect.TypeToken.getRawType}} -->
The `getRawType` method returns the raw (non-generic) class type associated with the generic type `T` of the `TypeToken` instance.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `rawType` field of the `TypeToken` instance, which is a `Class` object representing the raw type of the generic type `T`.
- **Output**:
    - A `Class<? super T>` object representing the raw type of the generic type `T`.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.getType<!-- {{#callable:com.google.gson.reflect.TypeToken.getType}} -->
The `getType` method returns the `Type` instance associated with the `TypeToken` object.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `type` field of the `TypeToken` class.
- **Output**:
    - The method returns a `Type` object representing the type associated with the `TypeToken` instance.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.isAssignableFrom<!-- {{#callable:com.google.gson.reflect.TypeToken.isAssignableFrom}} -->
The [`isAssignableFrom`](#TypeTokenisAssignableFrom) method checks if the current type is assignable from the given class type.
- **Modifiers**: `public`, `deprecated`
- **Inputs**:
    - `cls`: The class type to check against the current type for assignability.
- **Control Flow**:
    - The method takes a `Class<?>` object as input.
    - It casts the `Class<?>` object to a `Type` object.
    - It calls the overloaded `isAssignableFrom(Type from)` method with the casted `Type` object.
    - The result of the `isAssignableFrom(Type from)` method call is returned.
- **Output**:
    - A boolean value indicating whether the current type is assignable from the given class type.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.isAssignableFrom<!-- {{#callable:com.google.gson.reflect.TypeToken.isAssignableFrom}} -->
The [`isAssignableFrom`](#TypeTokenisAssignableFrom) method checks if the current type can be assigned from the specified `Type` parameter, considering various type scenarios like raw types, parameterized types, and generic array types.
- **Modifiers**: `public`, `deprecated`
- **Inputs**:
    - `from`: The `Type` object to check assignability from.
- **Control Flow**:
    - Check if the `from` type is null, returning false if it is.
    - Check if the current type is equal to the `from` type, returning true if they are equal.
    - If the current type is a `Class`, use `rawType.isAssignableFrom` with the raw type of `from`.
    - If the current type is a `ParameterizedType`, call the overloaded [`isAssignableFrom`](#TypeTokenisAssignableFrom) method with a new `HashMap` for type variables.
    - If the current type is a `GenericArrayType`, check if the raw type of `from` is assignable and recursively check the component type.
    - If none of the above conditions are met, throw an `IllegalArgumentException` for unsupported types.
- **Output**:
    - Returns a boolean indicating whether the current type is assignable from the specified `Type`.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.equals`](#TypeTokenequals)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
    - [`com.google.gson.internal.GsonTypes.getRawType`](../internal/GsonTypes.java.driver.md#GsonTypesgetRawType)
    - [`com.google.gson.reflect.TypeToken.buildUnsupportedTypeException`](#TypeTokenbuildUnsupportedTypeException)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.isAssignableFrom<!-- {{#callable:com.google.gson.reflect.TypeToken.isAssignableFrom}} -->
The [`isAssignableFrom`](#TypeTokenisAssignableFrom) method checks if the type represented by the current `TypeToken` instance is assignable from the type represented by the given `TypeToken` instance.
- **Modifiers**: `public`, `deprecated`
- **Inputs**:
    - `token`: A `TypeToken<?>` instance representing the type to check against the current `TypeToken` instance.
- **Control Flow**:
    - The method calls `isAssignableFrom(Type from)` with the type obtained from the `token` parameter using `token.getType()`.
    - The `isAssignableFrom(Type from)` method performs the actual check to determine if the current type can be assigned from the given type.
- **Output**:
    - Returns a boolean value indicating whether the current type is assignable from the type represented by the given `TypeToken`.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
    - [`com.google.gson.reflect.TypeToken.getType`](#TypeTokengetType)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.isAssignableFrom<!-- {{#callable:com.google.gson.reflect.TypeToken.isAssignableFrom}} -->
The [`isAssignableFrom`](#TypeTokenisAssignableFrom) method checks if a `Type` can be assigned to a `GenericArrayType` by comparing their component types.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `from`: The `Type` object representing the type to be checked for assignability.
    - `to`: The `GenericArrayType` object representing the target type to which assignability is being checked.
- **Control Flow**:
    - Retrieve the generic component type of the `to` parameter using `getGenericComponentType()`.
    - Check if the `toGenericComponentType` is an instance of `ParameterizedType`.
    - If `toGenericComponentType` is a `ParameterizedType`, determine the component type of `from` by checking if it is a `GenericArrayType` or a `Class<?>` and adjust `t` accordingly.
    - If `from` is a `GenericArrayType`, set `t` to its generic component type.
    - If `from` is a `Class<?>`, iterate through its component types until a non-array type is found and set `t` to this type.
    - Call the overloaded [`isAssignableFrom`](#TypeTokenisAssignableFrom) method with `t`, the `ParameterizedType` of `toGenericComponentType`, and a new `HashMap` to check for assignability.
    - If `toGenericComponentType` is not a `ParameterizedType`, return `true` to indicate that no generic constraints are defined on `to`.
- **Output**:
    - Returns a boolean indicating whether the `from` type is assignable to the `to` type based on their component types.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.GenericArrayTypeImpl.getGenericComponentType`](../internal/GsonTypes.java.driver.md#GenericArrayTypeImplgetGenericComponentType)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.isAssignableFrom<!-- {{#callable:com.google.gson.reflect.TypeToken.isAssignableFrom}} -->
The [`isAssignableFrom`](#TypeTokenisAssignableFrom) method checks if a given `Type` can be assigned to a `ParameterizedType` considering type variable mappings.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `from`: The `Type` to check for assignability.
    - `to`: The `ParameterizedType` to which the `from` type is being checked for assignability.
    - `typeVarMap`: A map of type variable names to their corresponding `Type` instances, used for resolving type variables.
- **Control Flow**:
    - Check if `from` is null, returning false if it is.
    - Check if `to` equals `from`, returning true if they are equal.
    - Determine the raw class type of `from` using `GsonTypes.getRawType(from)`.
    - If `from` is a `ParameterizedType`, extract its actual type arguments and type parameters.
    - For each type argument, resolve any type variables using `typeVarMap` and update the map with resolved types.
    - Check if the parameterized types are equivalent under the current type variable mapping using [`typeEquals`](#TypeTokentypeEquals).
    - Iterate over the generic interfaces of the class and recursively check assignability using a new type variable map.
    - If interfaces do not match, check the superclass for assignability using a new type variable map.
- **Output**:
    - Returns a boolean indicating whether the `from` type is assignable to the `to` type under the given type variable mapping.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.equals`](#TypeTokenequals)
    - [`com.google.gson.internal.GsonTypes.getRawType`](../internal/GsonTypes.java.driver.md#GsonTypesgetRawType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](../internal/GsonTypes.java.driver.md#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.reflect.TypeToken.typeEquals`](#TypeTokentypeEquals)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](#TypeTokenisAssignableFrom)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.typeEquals<!-- {{#callable:com.google.gson.reflect.TypeToken.typeEquals}} -->
The `typeEquals` method checks if two `ParameterizedType` instances are exactly equal, considering a mapping of type variables.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `from`: A `ParameterizedType` instance representing the source type to compare.
    - `to`: A `ParameterizedType` instance representing the target type to compare.
    - `typeVarMap`: A `Map` of type variable names to `Type` instances, used for resolving type variables during comparison.
- **Control Flow**:
    - Check if the raw types of `from` and `to` are equal.
    - If the raw types are equal, retrieve the actual type arguments of both `from` and `to`.
    - Iterate over the type arguments, comparing each pair using the [`matches`](#TypeTokenmatches) method.
    - If any pair of type arguments does not match, return `false`.
    - If all type arguments match, return `true`.
    - If the raw types are not equal, return `false`.
- **Output**:
    - A boolean value indicating whether the two `ParameterizedType` instances are exactly equal, considering the type variable mapping.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.getRawType`](../internal/GsonTypes.java.driver.md#GsonTypesgetRawType)
    - [`com.google.gson.internal.GsonTypes.ParameterizedTypeImpl.getActualTypeArguments`](../internal/GsonTypes.java.driver.md#ParameterizedTypeImplgetActualTypeArguments)
    - [`com.google.gson.reflect.TypeToken.matches`](#TypeTokenmatches)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.buildUnsupportedTypeException<!-- {{#callable:com.google.gson.reflect.TypeToken.buildUnsupportedTypeException}} -->
The `buildUnsupportedTypeException` method constructs an `IllegalArgumentException` with a detailed message indicating an unsupported type error.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `token`: The `Type` object representing the actual type that was encountered.
    - `expected`: A varargs array of `Class<?>` objects representing the expected types.
- **Control Flow**:
    - Initialize a `StringBuilder` with a base message indicating unsupported type and expected types.
    - Iterate over the `expected` array, appending each expected class name to the `StringBuilder`.
    - Append the actual type's class name and its string representation to the `StringBuilder`.
    - Return a new `IllegalArgumentException` with the constructed message from the `StringBuilder`.
- **Output**:
    - An `IllegalArgumentException` with a message detailing the unsupported type and expected types.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.matches<!-- {{#callable:com.google.gson.reflect.TypeToken.matches}} -->
The `matches` method checks if two types are equivalent, considering a mapping of type variables to actual types.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `from`: The source `Type` to be compared.
    - `to`: The target `Type` to be compared against.
    - `typeMap`: A `Map` that associates type variable names with their corresponding `Type` instances.
- **Control Flow**:
    - Check if the `to` type is equal to the `from` type; if so, return `true`.
    - If `from` is an instance of `TypeVariable`, retrieve its name and check if the `to` type is equal to the type mapped to this name in `typeMap`; if so, return `true`.
    - If neither condition is met, return `false`.
- **Output**:
    - Returns a boolean indicating whether the two types are equivalent, considering the type variable mappings.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.hashCode<!-- {{#callable:com.google.gson.reflect.TypeToken.hashCode}} -->
The `hashCode` method returns the precomputed hash code of the `TypeToken` instance.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns the value of the `hashCode` field of the `TypeToken` instance.
- **Output**:
    - An integer representing the hash code of the `TypeToken` instance.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.equals<!-- {{#callable:com.google.gson.reflect.TypeToken.equals}} -->
The [`equals`](../internal/GsonTypes.java.driver.md#GsonTypesequals) method checks if the given object is an instance of `TypeToken` and if its type is equal to the type of the current `TypeToken` instance.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `o`: The object to be compared with the current `TypeToken` instance for equality.
- **Control Flow**:
    - Check if the input object `o` is an instance of `TypeToken<?>`.
    - If `o` is an instance of `TypeToken<?>`, compare the `type` field of the current instance with the `type` field of `o` using `GsonTypes.equals`.
    - Return the result of the comparison.
- **Output**:
    - A boolean value indicating whether the input object is equal to the current `TypeToken` instance.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.equals`](../internal/GsonTypes.java.driver.md#GsonTypesequals)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.toString<!-- {{#callable:com.google.gson.reflect.TypeToken.toString}} -->
The `toString` method returns a string representation of the `type` field using the `GsonTypes.typeToString` method.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method calls `GsonTypes.typeToString` with the `type` field as an argument.
    - The result of the `GsonTypes.typeToString` call is returned as the output of the method.
- **Output**:
    - A `String` that represents the `type` field of the `TypeToken` class.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.typeToString`](../internal/GsonTypes.java.driver.md#GsonTypestypeToString)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.get<!-- {{#callable:com.google.gson.reflect.TypeToken.get}} -->
The `get` method returns a `TypeToken` instance for a given `Type`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `type`: A `Type` object representing the type for which a `TypeToken` is to be created.
- **Control Flow**:
    - The method creates a new instance of `TypeToken` using the provided `type` as a constructor argument.
- **Output**:
    - A `TypeToken<?>` instance representing the provided `Type`.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.get<!-- {{#callable:com.google.gson.reflect.TypeToken.get}} -->
The `get` method returns a `TypeToken` instance for a given `Class` type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `type`: The `Class` object representing the type for which a `TypeToken` is to be created.
- **Control Flow**:
    - The method takes a `Class` object as an input parameter.
    - It creates a new `TypeToken` instance using the provided `Class` type.
    - The method returns the newly created `TypeToken` instance.
- **Output**:
    - A `TypeToken<T>` instance representing the specified `Class<T>` type.
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.getParameterized<!-- {{#callable:com.google.gson.reflect.TypeToken.getParameterized}} -->
The `getParameterized` method creates a `TypeToken` for a parameterized type using a raw type and its type arguments, ensuring the validity of the type arguments against the raw type's type parameters.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `rawType`: The raw type for which a parameterized `TypeToken` is to be created; must be of type `Class`.
    - `typeArguments`: The type arguments to be applied to the raw type; must match the number and bounds of the raw type's type parameters.
- **Control Flow**:
    - Check that `rawType` and `typeArguments` are not null.
    - Verify that `rawType` is an instance of `Class`; throw `IllegalArgumentException` if not.
    - Retrieve the type parameters of `rawType` and compare their count with `typeArguments`; throw `IllegalArgumentException` if they do not match.
    - If `typeArguments` is empty, return a `TypeToken` for the raw class using `get(rawClass)`.
    - Check if `rawType` requires an owner type using `GsonTypes.requiresOwnerType`; throw `IllegalArgumentException` if it does.
    - Iterate over each type argument, ensuring it is not null and satisfies the bounds of the corresponding type variable; throw `IllegalArgumentException` if any type argument does not satisfy its bounds.
    - Return a new `TypeToken` created with a parameterized type using `GsonTypes.newParameterizedTypeWithOwner`.
- **Output**:
    - A `TypeToken<?>` representing the parameterized type created from the given raw type and type arguments.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.get`](#TypeTokenget)
    - [`com.google.gson.internal.GsonTypes.requiresOwnerType`](../internal/GsonTypes.java.driver.md#GsonTypesrequiresOwnerType)
    - [`com.google.gson.internal.GsonTypes.getRawType`](../internal/GsonTypes.java.driver.md#GsonTypesgetRawType)
    - [`com.google.gson.internal.GsonTypes.newParameterizedTypeWithOwner`](../internal/GsonTypes.java.driver.md#GsonTypesnewParameterizedTypeWithOwner)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)


---
#### TypeToken\.getArray<!-- {{#callable:com.google.gson.reflect.TypeToken.getArray}} -->
The `getArray` method returns a `TypeToken` representing an array type with elements of the specified component type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `componentType`: The `Type` of the elements that the array will contain.
- **Control Flow**:
    - The method calls `GsonTypes.arrayOf` with the `componentType` to get the array type.
    - It then creates a new `TypeToken` with the array type obtained from `GsonTypes.arrayOf`.
- **Output**:
    - A `TypeToken<?>` representing the array type of the specified component type.
- **Functions called**:
    - [`com.google.gson.internal.GsonTypes.arrayOf`](../internal/GsonTypes.java.driver.md#GsonTypesarrayOf)
- **See also**: [`com.google.gson.reflect.TypeToken`](#TypeToken)  (Base Class)



