# Purpose
The provided Java source code defines the [`JsonObject`](#JsonObjectJsonObject) class, which is part of the Google Gson library, a popular library for converting Java objects to JSON and vice versa. The [`JsonObject`](#JsonObjectJsonObject) class represents a JSON object, which is a collection of name-value pairs where the names are strings and the values are instances of `JsonElement`. This class provides a structured way to build and manipulate JSON objects in Java, allowing for the creation of complex JSON structures by nesting other `JsonElement` types, such as `JsonArray` and `JsonPrimitive`, within a [`JsonObject`](#JsonObjectJsonObject).

The [`JsonObject`](#JsonObjectJsonObject) class offers a variety of methods to manage its members, including adding, removing, and retrieving elements by their property names. It also provides convenience methods for adding properties with specific data types, such as strings, numbers, booleans, and characters, automatically converting them to `JsonPrimitive` instances. Additionally, the class includes methods to check for the presence of a member, obtain the size of the object, and retrieve a set of keys or entries. The class does not implement the `Map` interface directly but offers a `Map` view through the `asMap()` method, allowing for integration with other Java collections. The [`JsonObject`](#JsonObjectJsonObject) class ensures that null values are handled gracefully by converting them to `JsonNull` instances, maintaining the integrity of the JSON structure.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.internal.LinkedTreeMap`
- `java.util.Map`
- `java.util.Set`


# Classes

---
### JsonObject<!-- {{#class:com.google.gson.JsonObject}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonObject` class represents a JSON object, which is a collection of name-value pairs where names are strings and values are any type of `JsonElement`. It allows for the creation of a tree of `JsonElements` and maintains the order of elements as they are added. The class provides methods to add, remove, and retrieve members, as well as to check for the presence of members and to obtain a mutable map view of the object. It handles `null` values by converting them to `JsonNull` and supports deep copying of its elements.
- **Fields**:
    - `members`: `LinkedTreeMap<String, JsonElement>` A `LinkedTreeMap` that stores the name-value pairs of the JSON object, maintaining the order of insertion.
- **Methods**:
    - [`com.google.gson.JsonObject.JsonObject`](#JsonObjectJsonObject)
    - [`com.google.gson.JsonObject.deepCopy`](#JsonObjectdeepCopy)
    - [`com.google.gson.JsonObject.add`](#JsonObjectadd)
    - [`com.google.gson.JsonObject.remove`](#JsonObjectremove)
    - [`com.google.gson.JsonObject.addProperty`](#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.addProperty`](#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.addProperty`](#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.addProperty`](#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.entrySet`](#JsonObjectentrySet)
    - [`com.google.gson.JsonObject.keySet`](#JsonObjectkeySet)
    - [`com.google.gson.JsonObject.size`](#JsonObjectsize)
    - [`com.google.gson.JsonObject.isEmpty`](#JsonObjectisEmpty)
    - [`com.google.gson.JsonObject.has`](#JsonObjecthas)
    - [`com.google.gson.JsonObject.get`](#JsonObjectget)
    - [`com.google.gson.JsonObject.getAsJsonPrimitive`](#JsonObjectgetAsJsonPrimitive)
    - [`com.google.gson.JsonObject.getAsJsonArray`](#JsonObjectgetAsJsonArray)
    - [`com.google.gson.JsonObject.getAsJsonObject`](#JsonObjectgetAsJsonObject)
    - [`com.google.gson.JsonObject.asMap`](#JsonObjectasMap)
    - [`com.google.gson.JsonObject.equals`](#JsonObjectequals)
    - [`com.google.gson.JsonObject.hashCode`](#JsonObjecthashCode)
- **Extends/Implements**:
    - [`com.google.gson.JsonElement`](JsonElement.java.driver.md#JsonElement)

**Methods**

---
#### JsonObject\.JsonObject<!-- {{#callable:com.google.gson.JsonObject.JsonObject}} -->
The `JsonObject` constructor initializes an empty JSON object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor is annotated with `@SuppressWarnings("deprecation")` to suppress warnings related to the use of deprecated methods in the superclass constructor.
    - The constructor initializes a `JsonObject` instance without any parameters, setting up an empty `LinkedTreeMap` to hold the JSON object's members.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.deepCopy<!-- {{#callable:com.google.gson.JsonObject.deepCopy}} -->
The [`deepCopy`](JsonElement.java.driver.md#JsonElementdeepCopy) method creates and returns a deep copy of the current `JsonObject` instance, including all its member elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a new `JsonObject` named `result`.
    - Iterate over each entry in the `members` map of the current `JsonObject`.
    - For each entry, call [`deepCopy`](JsonElement.java.driver.md#JsonElementdeepCopy) on the `JsonElement` value and add the result to the `result` `JsonObject` with the same key.
    - Return the `result` `JsonObject`.
- **Output**:
    - A new `JsonObject` that is a deep copy of the current instance, including all its member elements.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](#JsonObjectadd)
    - [`com.google.gson.internal.LinkedTreeMap.Node.getKey`](internal/LinkedTreeMap.java.driver.md#NodegetKey)
    - [`com.google.gson.internal.LinkedTreeMap.Node.getValue`](internal/LinkedTreeMap.java.driver.md#NodegetValue)
    - [`com.google.gson.JsonElement.deepCopy`](JsonElement.java.driver.md#JsonElementdeepCopy)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.add<!-- {{#callable:com.google.gson.JsonObject.add}} -->
The `add` method adds a name-value pair to the `JsonObject`, converting `null` values to `JsonNull`.
- **Modifiers**: `public`
- **Inputs**:
    - `property`: The name of the member to be added, represented as a `String`.
    - `value`: The value of the member to be added, represented as a `JsonElement`. If `null`, it is converted to `JsonNull`.
- **Control Flow**:
    - The method checks if the `value` is `null`.
    - If `value` is `null`, it assigns `JsonNull.INSTANCE` to the value.
    - The method then puts the `property` and the determined `value` into the `members` map.
- **Output**:
    - This method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.put`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapput)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.remove<!-- {{#callable:com.google.gson.JsonObject.remove}} -->
The [`remove`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapremove) method removes a member from the `JsonObject` by its property name and returns the removed `JsonElement`.
- **Modifiers**: `public`
- **Inputs**:
    - `property`: The name of the member to be removed from the `JsonObject`.
- **Control Flow**:
    - The method accesses the `members` map, which is a `LinkedTreeMap` of `String` to `JsonElement`.
    - It calls the [`remove`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapremove) method on the `members` map with the provided `property` as the key.
    - The [`remove`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapremove) method of the map removes the entry with the specified key and returns the associated `JsonElement`, or `null` if no such entry exists.
- **Output**:
    - The method returns the `JsonElement` that was removed, or `null` if no member with the specified property name exists.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.remove`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapremove)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.addProperty<!-- {{#callable:com.google.gson.JsonObject.addProperty}} -->
The `addProperty` method adds a string property to the `JsonObject`, converting the value to a `JsonPrimitive` or `JsonNull` if the value is null.
- **Modifiers**: `public`
- **Inputs**:
    - `property`: The name of the member to be added, which must be a string.
    - `value`: The string value associated with the member, which can be null.
- **Control Flow**:
    - The method checks if the `value` is null.
    - If `value` is null, it uses `JsonNull.INSTANCE` as the value.
    - If `value` is not null, it creates a new `JsonPrimitive` with the given `value`.
    - It calls the [`add`](#JsonObjectadd) method with the `property` and the determined `JsonElement` (either `JsonNull` or `JsonPrimitive`).
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](#JsonObjectadd)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.addProperty<!-- {{#callable:com.google.gson.JsonObject.addProperty}} -->
The `addProperty` method adds a number property to the `JsonObject`, converting the number to a `JsonPrimitive` or using `JsonNull` if the value is null.
- **Modifiers**: `public`
- **Inputs**:
    - `property`: The name of the member to be added, represented as a String.
    - `value`: The number value associated with the member, which can be null.
- **Control Flow**:
    - The method checks if the `value` is null.
    - If `value` is null, it uses `JsonNull.INSTANCE` as the value to be added.
    - If `value` is not null, it creates a new `JsonPrimitive` with the `value`.
    - It calls the [`add`](#JsonObjectadd) method with the `property` and the determined `JsonElement` (either `JsonNull` or `JsonPrimitive`).
- **Output**:
    - The method does not return any value; it modifies the `JsonObject` by adding a new property.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](#JsonObjectadd)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.addProperty<!-- {{#callable:com.google.gson.JsonObject.addProperty}} -->
The `addProperty` method adds a boolean property to the `JsonObject`, converting the boolean value to a `JsonPrimitive` or `JsonNull` if null.
- **Modifiers**: `public`
- **Inputs**:
    - `property`: The name of the member to be added, represented as a String.
    - `value`: The boolean value associated with the member, which can be null.
- **Control Flow**:
    - The method checks if the `value` is null.
    - If `value` is null, it uses `JsonNull.INSTANCE` as the value.
    - If `value` is not null, it converts the boolean value to a `JsonPrimitive`.
    - It calls the [`add`](#JsonObjectadd) method with the `property` and the converted `value`.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](#JsonObjectadd)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.addProperty<!-- {{#callable:com.google.gson.JsonObject.addProperty}} -->
The `addProperty` method adds a character property to the `JsonObject`, converting the character to a `JsonPrimitive` or using `JsonNull` if the value is null.
- **Modifiers**: `public`
- **Inputs**:
    - `property`: The name of the member to be added, represented as a `String`.
    - `value`: The character value associated with the member, represented as a `Character`.
- **Control Flow**:
    - The method checks if the `value` is `null`.
    - If `value` is `null`, it uses `JsonNull.INSTANCE` as the value to be added.
    - If `value` is not `null`, it creates a new `JsonPrimitive` with the `value`.
    - It calls the [`add`](#JsonObjectadd) method with the `property` and the determined `JsonElement` (either `JsonNull` or `JsonPrimitive`).
- **Output**:
    - The method does not return any value; it modifies the `JsonObject` by adding a new property.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](#JsonObjectadd)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.entrySet<!-- {{#callable:com.google.gson.JsonObject.entrySet}} -->
The [`entrySet`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapentrySet) method returns a set view of the mappings contained in the `JsonObject`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling `entrySet()` on the `members` field, which is a `LinkedTreeMap` of `String` keys and `JsonElement` values.
- **Output**:
    - A `Set` of `Map.Entry<String, JsonElement>` representing the key-value pairs in the `JsonObject`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.entrySet`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapentrySet)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.keySet<!-- {{#callable:com.google.gson.JsonObject.keySet}} -->
The [`keySet`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapkeySet) method returns a set of all the keys present in the `JsonObject`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling `keySet()` on the `members` field, which is a `LinkedTreeMap` of the `JsonObject`.
- **Output**:
    - A `Set<String>` containing all the keys in the `JsonObject`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.keySet`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapkeySet)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.size<!-- {{#callable:com.google.gson.JsonObject.size}} -->
The [`size`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapsize) method returns the number of key/value pairs in the `JsonObject`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling the [`size`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapsize) method on the `members` field, which is a `LinkedTreeMap`.
- **Output**:
    - An integer representing the number of key/value pairs in the `JsonObject`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.size`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapsize)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.isEmpty<!-- {{#callable:com.google.gson.JsonObject.isEmpty}} -->
The [`isEmpty`](JsonArray.java.driver.md#JsonArrayisEmpty) method checks if the `JsonObject` has no key/value pairs.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly calls the [`isEmpty`](JsonArray.java.driver.md#JsonArrayisEmpty) method on the `members` field, which is a `LinkedTreeMap`, to determine if it contains any entries.
- **Output**:
    - A boolean value indicating whether the `JsonObject` is empty (true if there are no key/value pairs, false otherwise).
- **Functions called**:
    - [`com.google.gson.JsonArray.isEmpty`](JsonArray.java.driver.md#JsonArrayisEmpty)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.has<!-- {{#callable:com.google.gson.JsonObject.has}} -->
The `has` method checks if a member with the specified name exists in the `JsonObject`.
- **Modifiers**: `public`
- **Inputs**:
    - `memberName`: The name of the member to check for presence in the `JsonObject`.
- **Control Flow**:
    - The method calls [`containsKey`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapcontainsKey) on the `members` map with `memberName` as the argument.
    - It returns the result of the [`containsKey`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapcontainsKey) method, which is a boolean indicating the presence of the key.
- **Output**:
    - A boolean value indicating whether the `JsonObject` contains a member with the specified name.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.containsKey`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapcontainsKey)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.get<!-- {{#callable:com.google.gson.JsonObject.get}} -->
The [`get`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapget) method retrieves a `JsonElement` associated with a specified member name from the `JsonObject`.
- **Modifiers**: `public`
- **Inputs**:
    - `memberName`: The name of the member to retrieve from the `JsonObject`.
- **Control Flow**:
    - The method accesses the `members` map using the provided `memberName` as the key.
    - It returns the `JsonElement` associated with the given `memberName`.
- **Output**:
    - The method returns the `JsonElement` associated with the specified `memberName`, or `null` if no such member exists.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.get`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapget)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.getAsJsonPrimitive<!-- {{#callable:com.google.gson.JsonObject.getAsJsonPrimitive}} -->
The `getAsJsonPrimitive` method retrieves a member from the `JsonObject` as a `JsonPrimitive` based on the provided member name.
- **Modifiers**: `public`
- **Inputs**:
    - `memberName`: The name of the member to be retrieved as a `JsonPrimitive`.
- **Control Flow**:
    - The method accesses the `members` map using the provided `memberName` as the key.
    - It attempts to cast the retrieved `JsonElement` to a `JsonPrimitive`.
- **Output**:
    - The method returns the `JsonPrimitive` corresponding to the specified member name, or `null` if no such member exists. A `ClassCastException` is thrown if the member is not of type `JsonPrimitive`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.get`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapget)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.getAsJsonArray<!-- {{#callable:com.google.gson.JsonObject.getAsJsonArray}} -->
The `getAsJsonArray` method retrieves a member from the `JsonObject` as a `JsonArray` based on the provided member name.
- **Modifiers**: `public`
- **Inputs**:
    - `memberName`: The name of the member to be retrieved as a `JsonArray`.
- **Control Flow**:
    - The method accesses the `members` map using the provided `memberName` as the key.
    - It attempts to cast the retrieved `JsonElement` to a `JsonArray`.
- **Output**:
    - The method returns the `JsonArray` corresponding to the specified member name, or `null` if no such member exists. A `ClassCastException` is thrown if the member is not of type `JsonArray`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.get`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapget)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.getAsJsonObject<!-- {{#callable:com.google.gson.JsonObject.getAsJsonObject}} -->
The `getAsJsonObject` method retrieves a member from the `JsonObject` by its name and casts it to a `JsonObject`.
- **Modifiers**: `public`
- **Inputs**:
    - `memberName`: The name of the member to retrieve from the `JsonObject`.
- **Control Flow**:
    - Retrieve the member associated with the given `memberName` from the `members` map.
    - Cast the retrieved member to a `JsonObject`.
- **Output**:
    - The method returns the `JsonObject` corresponding to the specified member name, or `null` if no such member exists. A `ClassCastException` is thrown if the member is not of type `JsonObject`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.get`](internal/LinkedTreeMap.java.driver.md#LinkedTreeMapget)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.asMap<!-- {{#callable:com.google.gson.JsonObject.asMap}} -->
The `asMap` method returns a mutable `Map` view of the `JsonObject`'s members.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `members` field, which is a `LinkedTreeMap` of `String` keys and `JsonElement` values.
- **Output**:
    - A `Map<String, JsonElement>` representing the members of the `JsonObject`.
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.equals<!-- {{#callable:com.google.gson.JsonObject.equals}} -->
The [`equals`](../../../../../test/java/com/google/gson/GsonTest.java.driver.md#DummyFactoryequals) method checks if the given object is equal to the current `JsonObject` instance by comparing their members.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: The object to be compared with the current `JsonObject` instance.
- **Control Flow**:
    - The method first checks if the input object `o` is the same instance as `this` using the `==` operator.
    - If the first condition is false, it checks if `o` is an instance of `JsonObject`.
    - If `o` is an instance of `JsonObject`, it casts `o` to `JsonObject` and compares its `members` with the `members` of the current instance using the [`equals`](../../../../../test/java/com/google/gson/GsonTest.java.driver.md#DummyFactoryequals) method of the `members` map.
- **Output**:
    - The method returns `true` if the input object is the same instance as `this` or if it is a `JsonObject` with equal members; otherwise, it returns `false`.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](../../../../../test/java/com/google/gson/GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)


---
#### JsonObject\.hashCode<!-- {{#callable:com.google.gson.JsonObject.hashCode}} -->
The `hashCode` method returns the hash code of the `members` map in the `JsonObject` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling `hashCode()` on the `members` field, which is a `LinkedTreeMap` of the `JsonObject`.
- **Output**:
    - An integer representing the hash code of the `members` map.
- **See also**: [`com.google.gson.JsonObject`](#JsonObject)  (Base Class)



