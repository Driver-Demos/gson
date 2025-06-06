# Purpose
The provided Java source code defines the [`JsonArray`](#JsonArrayJsonArray) class, which is part of the Google Gson library, a popular library for converting Java objects to JSON and vice versa. The [`JsonArray`](#JsonArrayJsonArray) class represents an array type in JSON, allowing for the storage and manipulation of a list of `JsonElement` objects. This class provides a broad range of functionality for handling JSON arrays, including methods for adding, removing, and accessing elements, as well as for checking the size and emptiness of the array. It supports various data types such as `Boolean`, `Character`, `Number`, and `String`, converting `null` values to `JsonNull` to maintain JSON compatibility. The class also implements the `Iterable` interface, allowing for iteration over its elements, and provides a method to obtain a `List` view of the array.

The [`JsonArray`](#JsonArrayJsonArray) class is a crucial component of the Gson library, facilitating the manipulation of JSON arrays in Java applications. It does not implement the `List` interface directly but offers a `List` view through the `asList()` method, which ensures that changes to the list are reflected in the [`JsonArray`](#JsonArrayJsonArray) and vice versa. The class includes methods for deep copying, equality checks, and hash code generation, ensuring robust handling of JSON data structures. By providing a comprehensive API for JSON array manipulation, the [`JsonArray`](#JsonArrayJsonArray) class serves as a foundational element for developers working with JSON data in Java, enabling seamless integration and manipulation of JSON arrays within Java applications.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.internal.NonNullElementWrapperList`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `java.util.ArrayList`
- `java.util.Iterator`
- `java.util.List`


# Classes

---
### JsonArray<!-- {{#class:com.google.gson.JsonArray}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonArray` class represents an array structure in JSON, allowing for the storage and manipulation of a list of `JsonElement` objects, each of which can be of a different type. It maintains the order of elements as they are added and provides various methods to add, remove, and access elements, as well as to convert the array to different data types if it contains a single element. The class does not support `null` values directly, converting them to `JsonNull` instead, and offers a mutable `List` view of the array for further manipulation.
- **Fields**:
    - `elements`: `ArrayList<JsonElement>` A private final `ArrayList` that stores the `JsonElement` objects in the `JsonArray`.
- **Methods**:
    - [`com.google.gson.JsonArray.JsonArray`](#JsonArrayJsonArray)
    - [`com.google.gson.JsonArray.JsonArray`](#JsonArrayJsonArray)
    - [`com.google.gson.JsonArray.deepCopy`](#JsonArraydeepCopy)
    - [`com.google.gson.JsonArray.add`](#JsonArrayadd)
    - [`com.google.gson.JsonArray.add`](#JsonArrayadd)
    - [`com.google.gson.JsonArray.add`](#JsonArrayadd)
    - [`com.google.gson.JsonArray.add`](#JsonArrayadd)
    - [`com.google.gson.JsonArray.add`](#JsonArrayadd)
    - [`com.google.gson.JsonArray.addAll`](#JsonArrayaddAll)
    - [`com.google.gson.JsonArray.set`](#JsonArrayset)
    - [`com.google.gson.JsonArray.remove`](#JsonArrayremove)
    - [`com.google.gson.JsonArray.remove`](#JsonArrayremove)
    - [`com.google.gson.JsonArray.contains`](#JsonArraycontains)
    - [`com.google.gson.JsonArray.size`](#JsonArraysize)
    - [`com.google.gson.JsonArray.isEmpty`](#JsonArrayisEmpty)
    - [`com.google.gson.JsonArray.iterator`](#JsonArrayiterator)
    - [`com.google.gson.JsonArray.get`](#JsonArrayget)
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonArray.getAsNumber`](#JsonArraygetAsNumber)
    - [`com.google.gson.JsonArray.getAsString`](#JsonArraygetAsString)
    - [`com.google.gson.JsonArray.getAsDouble`](#JsonArraygetAsDouble)
    - [`com.google.gson.JsonArray.getAsBigDecimal`](#JsonArraygetAsBigDecimal)
    - [`com.google.gson.JsonArray.getAsBigInteger`](#JsonArraygetAsBigInteger)
    - [`com.google.gson.JsonArray.getAsFloat`](#JsonArraygetAsFloat)
    - [`com.google.gson.JsonArray.getAsLong`](#JsonArraygetAsLong)
    - [`com.google.gson.JsonArray.getAsInt`](#JsonArraygetAsInt)
    - [`com.google.gson.JsonArray.getAsByte`](#JsonArraygetAsByte)
    - [`com.google.gson.JsonArray.getAsCharacter`](#JsonArraygetAsCharacter)
    - [`com.google.gson.JsonArray.getAsShort`](#JsonArraygetAsShort)
    - [`com.google.gson.JsonArray.getAsBoolean`](#JsonArraygetAsBoolean)
    - [`com.google.gson.JsonArray.asList`](#JsonArrayasList)
    - [`com.google.gson.JsonArray.equals`](#JsonArrayequals)
    - [`com.google.gson.JsonArray.hashCode`](#JsonArrayhashCode)
- **Extends/Implements**:
    - [`com.google.gson.JsonElement`](JsonElement.java.driver.md#JsonElement)

**Methods**

---
#### JsonArray\.JsonArray<!-- {{#callable:com.google.gson.JsonArray.JsonArray}} -->
The `JsonArray` constructor initializes an empty JSON array by creating an empty `ArrayList` to hold `JsonElement` objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor is called to create a new instance of `JsonArray`.
    - An empty `ArrayList` is instantiated and assigned to the `elements` field of the `JsonArray` instance.
- **Output**:
    - A new `JsonArray` object with an empty list of elements is created.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.JsonArray<!-- {{#callable:com.google.gson.JsonArray.JsonArray}} -->
The `JsonArray` constructor initializes a new `JsonArray` with a specified initial capacity for its internal list of elements.
- **Modifiers**: `public`
- **Inputs**:
    - `capacity`: The initial capacity for the internal `ArrayList` that will store the `JsonElement` objects.
- **Control Flow**:
    - The constructor is called with an integer parameter `capacity`.
    - An `ArrayList` is instantiated with the specified `capacity` and assigned to the `elements` field.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.deepCopy<!-- {{#callable:com.google.gson.JsonArray.deepCopy}} -->
The [`deepCopy`](JsonElement.java.driver.md#JsonElementdeepCopy) method creates a deep copy of the `JsonArray` and all its elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `elements` list is not empty.
    - If not empty, create a new `JsonArray` with the same size as `elements`.
    - Iterate over each `JsonElement` in `elements`.
    - For each element, call its [`deepCopy`](JsonElement.java.driver.md#JsonElementdeepCopy) method and add the result to the new `JsonArray`.
    - Return the new `JsonArray` with deep-copied elements.
    - If `elements` is empty, return a new empty `JsonArray`.
- **Output**:
    - A new `JsonArray` instance that is a deep copy of the original array.
- **Functions called**:
    - [`com.google.gson.JsonObject.isEmpty`](JsonObject.java.driver.md#JsonObjectisEmpty)
    - [`com.google.gson.internal.NonNullElementWrapperList.size`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListsize)
    - [`com.google.gson.internal.NonNullElementWrapperList.add`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListadd)
    - [`com.google.gson.JsonElement.deepCopy`](JsonElement.java.driver.md#JsonElementdeepCopy)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.add<!-- {{#callable:com.google.gson.JsonArray.add}} -->
The `add` method adds a boolean value to the `JsonArray`, converting it to a `JsonPrimitive` or `JsonNull` if null.
- **Modifiers**: `public`
- **Inputs**:
    - `bool`: The boolean value to be added to the `JsonArray`. If null, it is converted to `JsonNull`.
- **Control Flow**:
    - Check if the input `bool` is null.
    - If `bool` is null, add `JsonNull.INSTANCE` to the `elements` list.
    - If `bool` is not null, create a `JsonPrimitive` with the boolean value and add it to the `elements` list.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.add<!-- {{#callable:com.google.gson.JsonArray.add}} -->
The `add` method adds a character to the `JsonArray`, converting it to a `JsonPrimitive` or `JsonNull` if null.
- **Modifiers**: `public`
- **Inputs**:
    - `character`: The character to be added to the `JsonArray`. If null, it will be converted to `JsonNull`.
- **Control Flow**:
    - Check if the input `character` is null.
    - If `character` is null, use `JsonNull.INSTANCE`; otherwise, create a new `JsonPrimitive` with the `character`.
    - Add the resulting `JsonElement` to the `elements` list of the `JsonArray`.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.add<!-- {{#callable:com.google.gson.JsonArray.add}} -->
The `add` method adds a `Number` to the `JsonArray`, converting it to a `JsonPrimitive` or `JsonNull` if null.
- **Modifiers**: `public`
- **Inputs**:
    - `number`: The `Number` object to be added to the `JsonArray`. If it is null, it will be converted to `JsonNull`.
- **Control Flow**:
    - Check if the `number` is null.
    - If `number` is null, use `JsonNull.INSTANCE`; otherwise, create a new `JsonPrimitive` with the `number`.
    - Add the resulting `JsonElement` to the `elements` list of the `JsonArray`.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.add<!-- {{#callable:com.google.gson.JsonArray.add}} -->
The `add` method adds a string to the `JsonArray`, converting it to a `JsonPrimitive` or `JsonNull` if the string is null.
- **Modifiers**: `public`
- **Inputs**:
    - `string`: The string to be added to the `JsonArray`.
- **Control Flow**:
    - Check if the input string is null.
    - If the string is null, add `JsonNull.INSTANCE` to the `elements` list.
    - If the string is not null, create a `JsonPrimitive` from the string and add it to the `elements` list.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.add<!-- {{#callable:com.google.gson.JsonArray.add}} -->
The `add` method adds a `JsonElement` to the `JsonArray`, converting `null` inputs to `JsonNull`.
- **Modifiers**: `public`
- **Inputs**:
    - `element`: The `JsonElement` to be added to the `JsonArray`. If `null`, it will be converted to `JsonNull`.
- **Control Flow**:
    - Check if the input `element` is `null`.
    - If `element` is `null`, assign `JsonNull.INSTANCE` to `element`.
    - Add the `element` to the `elements` list of the `JsonArray`.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.addAll<!-- {{#callable:com.google.gson.JsonArray.addAll}} -->
The `addAll` method appends all elements from a given `JsonArray` to the current `JsonArray`.
- **Modifiers**: `public`
- **Inputs**:
    - `array`: The `JsonArray` whose elements are to be added to the current array.
- **Control Flow**:
    - The method accesses the `elements` list of the current `JsonArray` instance.
    - It calls the `addAll` method on this list, passing the `elements` list of the input `JsonArray` as an argument.
    - This operation appends all elements from the input `JsonArray` to the current `JsonArray`.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.set<!-- {{#callable:com.google.gson.JsonArray.set}} -->
The [`set`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListset) method replaces an element at a specified index in the `JsonArray` with a given `JsonElement`, converting `null` to `JsonNull`, and returns the replaced element.
- **Modifiers**: `public`
- **Inputs**:
    - `index`: The index of the element to replace in the `JsonArray`.
    - `element`: The `JsonElement` to be stored at the specified position, with `null` being converted to `JsonNull`.
- **Control Flow**:
    - The method checks if the `element` is `null` and if so, assigns `JsonNull.INSTANCE` to it.
    - It then calls the [`set`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListset) method on the `elements` list with the provided `index` and the `element`, replacing the element at the specified index.
    - The method returns the element that was previously at the specified index.
- **Output**:
    - The method returns the `JsonElement` that was previously at the specified index in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.set`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListset)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.remove<!-- {{#callable:com.google.gson.JsonArray.remove}} -->
The [`remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove) method removes the first occurrence of a specified `JsonElement` from the `JsonArray` and returns a boolean indicating if the element was present and removed.
- **Modifiers**: `public`
- **Inputs**:
    - `element`: The `JsonElement` to be removed from the `JsonArray`.
- **Control Flow**:
    - The method calls the [`remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove) method on the `elements` ArrayList with the specified `JsonElement` as the argument.
    - The [`remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove) method of the ArrayList attempts to remove the first occurrence of the specified element.
    - If the element is found and removed, the method returns `true`; otherwise, it returns `false`.
- **Output**:
    - A boolean value indicating whether the specified `JsonElement` was present in the `JsonArray` and successfully removed.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.remove<!-- {{#callable:com.google.gson.JsonArray.remove}} -->
The [`remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove) method removes and returns the `JsonElement` at the specified index from the `JsonArray`.
- **Modifiers**: `public`
- **Inputs**:
    - `index`: The index of the element to be removed from the array.
- **Control Flow**:
    - The method accesses the `elements` list, which is an `ArrayList` of `JsonElement` objects.
    - It calls the [`remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove) method on the `elements` list with the provided `index`.
    - The [`remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove) method of `ArrayList` removes the element at the specified position and returns it.
- **Output**:
    - The method returns the `JsonElement` that was removed from the specified index in the array.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.remove`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListremove)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.contains<!-- {{#callable:com.google.gson.JsonArray.contains}} -->
The [`contains`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListcontains) method checks if a specified `JsonElement` is present in the `JsonArray`.
- **Modifiers**: `public`
- **Inputs**:
    - `element`: The `JsonElement` whose presence in the `JsonArray` is to be tested.
- **Control Flow**:
    - The method calls the [`contains`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListcontains) method on the `elements` list, passing the `element` as an argument.
- **Output**:
    - Returns `true` if the `JsonArray` contains the specified `JsonElement`, otherwise returns `false`.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.contains`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListcontains)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.size<!-- {{#callable:com.google.gson.JsonArray.size}} -->
The `size` method returns the number of elements in the `JsonArray`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling `size()` on the `elements` ArrayList, which holds the elements of the `JsonArray`.
- **Output**:
    - An integer representing the number of elements in the `JsonArray`.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.isEmpty<!-- {{#callable:com.google.gson.JsonArray.isEmpty}} -->
The [`isEmpty`](JsonObject.java.driver.md#JsonObjectisEmpty) method checks if the `JsonArray` contains no elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly calls the [`isEmpty`](JsonObject.java.driver.md#JsonObjectisEmpty) method on the `elements` ArrayList to determine if it is empty.
- **Output**:
    - A boolean value indicating whether the `JsonArray` is empty (true) or not (false).
- **Functions called**:
    - [`com.google.gson.JsonObject.isEmpty`](JsonObject.java.driver.md#JsonObjectisEmpty)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.iterator<!-- {{#callable:com.google.gson.JsonArray.iterator}} -->
The `iterator` method returns an iterator for the `JsonElement` objects contained in the `JsonArray`.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of calling the `iterator` method on the `elements` ArrayList, which contains `JsonElement` objects.
- **Output**:
    - An `Iterator<JsonElement>` that can be used to iterate over the elements in the `JsonArray`.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.get<!-- {{#callable:com.google.gson.JsonArray.get}} -->
The [`get`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListget) method retrieves the `JsonElement` at the specified index from the `JsonArray`.
- **Modifiers**: `public`
- **Inputs**:
    - `i`: The index of the element to retrieve from the `JsonArray`.
- **Control Flow**:
    - The method accesses the `elements` list, which is an `ArrayList` of `JsonElement`, and retrieves the element at the specified index `i`.
- **Output**:
    - The method returns the `JsonElement` located at the specified index `i` in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.get`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListget)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsSingleElement<!-- {{#callable:com.google.gson.JsonArray.getAsSingleElement}} -->
The `getAsSingleElement` method retrieves the sole element from the `elements` list if it contains exactly one element, otherwise it throws an `IllegalStateException`.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Determine the size of the `elements` list and store it in the variable [`size`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListsize).
    - Check if [`size`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListsize) is equal to 1.
    - If [`size`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListsize) is 1, return the first element of the `elements` list.
    - If [`size`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListsize) is not 1, throw an `IllegalStateException` with a message indicating the actual size of the array.
- **Output**:
    - Returns the single `JsonElement` from the `elements` list if its size is 1, otherwise throws an `IllegalStateException`.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.size`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListsize)
    - [`com.google.gson.internal.NonNullElementWrapperList.get`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListget)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsNumber<!-- {{#callable:com.google.gson.JsonArray.getAsNumber}} -->
The [`getAsNumber`](JsonElement.java.driver.md#JsonElementgetAsNumber) method returns the single element of the `JsonArray` as a `Number` if the array contains exactly one element.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Calls the [`getAsSingleElement`](#JsonArraygetAsSingleElement) method to retrieve the single element from the `JsonArray`.
    - Invokes the [`getAsNumber`](JsonElement.java.driver.md#JsonElementgetAsNumber) method on the retrieved `JsonElement` to convert it to a `Number`.
- **Output**:
    - Returns a `Number` representation of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsNumber`](JsonElement.java.driver.md#JsonElementgetAsNumber)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsString<!-- {{#callable:com.google.gson.JsonArray.getAsString}} -->
The [`getAsString`](JsonElement.java.driver.md#JsonElementgetAsString) method returns the string representation of the single element in the `JsonArray` if it contains exactly one element.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getAsSingleElement()` to retrieve the single element from the `JsonArray`.
    - It then calls `getAsString()` on the retrieved `JsonElement` to obtain its string representation.
    - If the `JsonArray` does not contain exactly one element, `getAsSingleElement()` throws an `IllegalStateException`.
- **Output**:
    - The method returns a `String` representation of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsString`](JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsDouble<!-- {{#callable:com.google.gson.JsonArray.getAsDouble}} -->
The [`getAsDouble`](JsonElement.java.driver.md#JsonElementgetAsDouble) method returns the single element of the `JsonArray` as a double, if the array contains exactly one element.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Calls the [`getAsSingleElement`](#JsonArraygetAsSingleElement) method to retrieve the single element from the `JsonArray`.
    - Invokes the [`getAsDouble`](JsonElement.java.driver.md#JsonElementgetAsDouble) method on the retrieved `JsonElement` to convert it to a double.
    - Returns the double value obtained from the `JsonElement`.
- **Output**:
    - A double value representing the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsDouble`](JsonElement.java.driver.md#JsonElementgetAsDouble)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsBigDecimal<!-- {{#callable:com.google.gson.JsonArray.getAsBigDecimal}} -->
The [`getAsBigDecimal`](JsonElement.java.driver.md#JsonElementgetAsBigDecimal) method returns the single element of the `JsonArray` as a `BigDecimal` if the array contains exactly one element.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Calls the [`getAsSingleElement`](#JsonArraygetAsSingleElement) method to retrieve the single element from the `JsonArray`.
    - Invokes the [`getAsBigDecimal`](JsonElement.java.driver.md#JsonElementgetAsBigDecimal) method on the retrieved `JsonElement` to convert it to a `BigDecimal`.
- **Output**:
    - Returns a `BigDecimal` representation of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsBigDecimal`](JsonElement.java.driver.md#JsonElementgetAsBigDecimal)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsBigInteger<!-- {{#callable:com.google.gson.JsonArray.getAsBigInteger}} -->
The [`getAsBigInteger`](JsonElement.java.driver.md#JsonElementgetAsBigInteger) method returns the single element of the `JsonArray` as a `BigInteger` if the array contains exactly one element.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Invoke the [`getAsSingleElement`](#JsonArraygetAsSingleElement) method to retrieve the single element from the `JsonArray`.
    - Call the [`getAsBigInteger`](JsonElement.java.driver.md#JsonElementgetAsBigInteger) method on the retrieved `JsonElement` to convert it to a `BigInteger`.
    - Return the `BigInteger` value.
- **Output**:
    - A `BigInteger` representation of the single element in the `JsonArray` if the array contains exactly one element; otherwise, an `IllegalStateException` is thrown.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsBigInteger`](JsonElement.java.driver.md#JsonElementgetAsBigInteger)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsFloat<!-- {{#callable:com.google.gson.JsonArray.getAsFloat}} -->
The [`getAsFloat`](JsonElement.java.driver.md#JsonElementgetAsFloat) method returns the single element of the `JsonArray` as a float, if the array contains exactly one element.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getAsSingleElement()` to retrieve the single element from the `JsonArray`.
    - It then calls `getAsFloat()` on the retrieved `JsonElement` to convert it to a float.
    - If the `JsonArray` does not contain exactly one element, `getAsSingleElement()` throws an `IllegalStateException`.
- **Output**:
    - A float representation of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsFloat`](JsonElement.java.driver.md#JsonElementgetAsFloat)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsLong<!-- {{#callable:com.google.gson.JsonArray.getAsLong}} -->
The [`getAsLong`](JsonElement.java.driver.md#JsonElementgetAsLong) method returns the long value of a single element in the `JsonArray` if the array contains exactly one element.
- **Modifiers**: `public`, `long`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getAsSingleElement()` to retrieve the single element from the `JsonArray`.
    - It then calls `getAsLong()` on the retrieved `JsonElement` to obtain its long value.
    - If the `JsonArray` does not contain exactly one element, `getAsSingleElement()` throws an `IllegalStateException`.
- **Output**:
    - The method returns a `long` value representing the long value of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsLong`](JsonElement.java.driver.md#JsonElementgetAsLong)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsInt<!-- {{#callable:com.google.gson.JsonArray.getAsInt}} -->
The [`getAsInt`](JsonElement.java.driver.md#JsonElementgetAsInt) method returns the integer representation of a single element in the `JsonArray` if it contains exactly one element.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Calls the [`getAsSingleElement`](#JsonArraygetAsSingleElement) method to retrieve the single element from the `JsonArray`.
    - Invokes the [`getAsInt`](JsonElement.java.driver.md#JsonElementgetAsInt) method on the retrieved `JsonElement` to obtain its integer value.
    - Returns the integer value obtained from the `JsonElement`.
- **Output**:
    - The method returns an `int` which is the integer representation of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsInt`](JsonElement.java.driver.md#JsonElementgetAsInt)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsByte<!-- {{#callable:com.google.gson.JsonArray.getAsByte}} -->
The [`getAsByte`](JsonElement.java.driver.md#JsonElementgetAsByte) method returns the single element of the `JsonArray` as a byte, if the array contains exactly one element.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getAsSingleElement()` to retrieve the single element from the `JsonArray`.
    - It then calls `getAsByte()` on the retrieved `JsonElement` to convert it to a byte.
    - If the `JsonArray` does not contain exactly one element, `getAsSingleElement()` throws an `IllegalStateException`.
- **Output**:
    - The method returns a byte representation of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsByte`](JsonElement.java.driver.md#JsonElementgetAsByte)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsCharacter<!-- {{#callable:com.google.gson.JsonArray.getAsCharacter}} -->
The [`getAsCharacter`](JsonPrimitive.java.driver.md#JsonPrimitivegetAsCharacter) method returns the first character of the single element in the `JsonArray` if it contains exactly one element.
- **Modifiers**: `public`, `deprecated`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getAsSingleElement()` to retrieve the single element from the `JsonArray`.
    - It then calls `getAsCharacter()` on the retrieved element to obtain its character representation.
    - If the `JsonArray` does not contain exactly one element, `getAsSingleElement()` throws an `IllegalStateException`.
- **Output**:
    - The method returns a `char` representing the first character of the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonPrimitive.getAsCharacter`](JsonPrimitive.java.driver.md#JsonPrimitivegetAsCharacter)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsShort<!-- {{#callable:com.google.gson.JsonArray.getAsShort}} -->
The [`getAsShort`](JsonElement.java.driver.md#JsonElementgetAsShort) method returns the single element of the `JsonArray` as a short if the array contains exactly one element.
- **Modifiers**: `public`, `short`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getAsSingleElement()` to retrieve the single element from the `JsonArray`.
    - It then calls `getAsShort()` on the retrieved `JsonElement` to convert it to a short.
    - If the `JsonArray` does not contain exactly one element, `getAsSingleElement()` throws an `IllegalStateException`.
- **Output**:
    - The method returns a `short` value representing the single element in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsShort`](JsonElement.java.driver.md#JsonElementgetAsShort)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.getAsBoolean<!-- {{#callable:com.google.gson.JsonArray.getAsBoolean}} -->
The [`getAsBoolean`](JsonElement.java.driver.md#JsonElementgetAsBoolean) method returns the boolean value of the single element in the `JsonArray` if it contains exactly one element.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Calls the [`getAsSingleElement`](#JsonArraygetAsSingleElement) method to retrieve the single element from the `JsonArray`.
    - Invokes the [`getAsBoolean`](JsonElement.java.driver.md#JsonElementgetAsBoolean) method on the retrieved `JsonElement` to obtain its boolean value.
    - Returns the boolean value obtained from the `JsonElement`.
- **Output**:
    - A boolean value representing the single element in the `JsonArray` if it contains exactly one element; otherwise, an exception is thrown.
- **Functions called**:
    - [`com.google.gson.JsonArray.getAsSingleElement`](#JsonArraygetAsSingleElement)
    - [`com.google.gson.JsonElement.getAsBoolean`](JsonElement.java.driver.md#JsonElementgetAsBoolean)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.asList<!-- {{#callable:com.google.gson.JsonArray.asList}} -->
The `asList` method returns a mutable List view of the JsonArray's elements, wrapped to disallow null values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method creates a new instance of `NonNullElementWrapperList` using the `elements` field of the `JsonArray`.
    - It returns this newly created list.
- **Output**:
    - A `List<JsonElement>` that reflects the elements of the `JsonArray`, with null values disallowed.
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.equals<!-- {{#callable:com.google.gson.JsonArray.equals}} -->
The [`equals`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals) method checks if the given object is equal to the current `JsonArray` instance by comparing their elements.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: The object to be compared with the current `JsonArray` instance.
- **Control Flow**:
    - The method first checks if the given object `o` is the same instance as `this` using the `==` operator.
    - If not, it checks if `o` is an instance of `JsonArray`.
    - If `o` is a `JsonArray`, it compares the `elements` list of `o` with the `elements` list of `this` using the [`equals`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals) method of the list.
- **Output**:
    - The method returns `true` if the given object is the same instance as `this` or if it is a `JsonArray` with equal elements; otherwise, it returns `false`.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.equals`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)


---
#### JsonArray\.hashCode<!-- {{#callable:com.google.gson.JsonArray.hashCode}} -->
The [`hashCode`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListhashCode) method returns the hash code of the `JsonArray` based on its elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`hashCode`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListhashCode) method on the `elements` ArrayList, which contains the elements of the `JsonArray`.
    - The hash code of the `elements` ArrayList is returned as the hash code of the `JsonArray`.
- **Output**:
    - An integer representing the hash code of the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.internal.NonNullElementWrapperList.hashCode`](internal/NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListhashCode)
- **See also**: [`com.google.gson.JsonArray`](#JsonArray)  (Base Class)



