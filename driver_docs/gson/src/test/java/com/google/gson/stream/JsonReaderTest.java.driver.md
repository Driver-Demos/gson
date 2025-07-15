# Purpose
The provided Java source code is a comprehensive test suite for the `JsonReader` class, which is part of the Google Gson library. This test suite is designed to validate the functionality and robustness of the `JsonReader` class, which is responsible for parsing JSON data in a streaming manner. The tests cover a wide range of scenarios, including strict and lenient parsing modes, handling of various JSON structures (arrays, objects, strings, numbers, booleans, and nulls), and edge cases such as malformed JSON, deeply nested structures, and large data inputs. The suite also tests the behavior of the `JsonReader` when encountering non-standard JSON features like comments and unquoted names or strings, ensuring that the class adheres to the expected JSON standards or gracefully handles deviations when in lenient mode.

The test suite is organized into multiple test methods, each focusing on specific aspects of JSON parsing. It uses JUnit annotations to define test cases and assertions to verify expected outcomes. The tests also include checks for proper error handling, such as throwing exceptions for malformed JSON or unexpected tokens. Additionally, the suite tests the `JsonReader`'s ability to skip values and handle different character encodings, including BOM (Byte Order Mark) handling. By covering such a broad range of scenarios, this test suite ensures that the `JsonReader` class is reliable and performs correctly under various conditions, making it a critical component for applications that rely on JSON data processing.
# Imports and Dependencies

---
- `com.google.gson.stream`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.stream.JsonToken.BEGIN_ARRAY`
- `com.google.gson.stream.JsonToken.BEGIN_OBJECT`
- `com.google.gson.stream.JsonToken.BOOLEAN`
- `com.google.gson.stream.JsonToken.END_ARRAY`
- `com.google.gson.stream.JsonToken.END_OBJECT`
- `com.google.gson.stream.JsonToken.NAME`
- `com.google.gson.stream.JsonToken.NULL`
- `com.google.gson.stream.JsonToken.NUMBER`
- `com.google.gson.stream.JsonToken.STRING`
- `org.junit.Assert.assertThrows`
- `com.google.gson.Strictness`
- `java.io.EOFException`
- `java.io.IOException`
- `java.io.Reader`
- `java.io.StringReader`
- `java.util.Arrays`
- `org.junit.Ignore`
- `org.junit.Test`


# Classes

---
### JsonReaderTest<!-- {{#class:com.google.gson.stream.JsonReaderTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonReaderTest` class is a comprehensive suite of unit tests designed to validate the functionality and robustness of the `JsonReader` class, particularly focusing on its ability to handle various JSON parsing scenarios, including strict and lenient modes, handling of malformed JSON, and edge cases such as deeply nested structures and very long strings.
- **Methods**:
    - [`com.google.gson.stream.JsonReaderTest.testDefaultStrictness`](#JsonReaderTesttestDefaultStrictness)
    - [`com.google.gson.stream.JsonReaderTest.testSetLenientTrue`](#JsonReaderTesttestSetLenientTrue)
    - [`com.google.gson.stream.JsonReaderTest.testSetLenientFalse`](#JsonReaderTesttestSetLenientFalse)
    - [`com.google.gson.stream.JsonReaderTest.testSetStrictness`](#JsonReaderTesttestSetStrictness)
    - [`com.google.gson.stream.JsonReaderTest.testSetStrictnessNull`](#JsonReaderTesttestSetStrictnessNull)
    - [`com.google.gson.stream.JsonReaderTest.testEscapedNewlineNotAllowedInStrictMode`](#JsonReaderTesttestEscapedNewlineNotAllowedInStrictMode)
    - [`com.google.gson.stream.JsonReaderTest.testEscapedNewlineAllowedInDefaultMode`](#JsonReaderTesttestEscapedNewlineAllowedInDefaultMode)
    - [`com.google.gson.stream.JsonReaderTest.testStrictModeFailsToParseUnescapedControlCharacter`](#JsonReaderTesttestStrictModeFailsToParseUnescapedControlCharacter)
    - [`com.google.gson.stream.JsonReaderTest.testStrictModeAllowsOtherControlCharacters`](#JsonReaderTesttestStrictModeAllowsOtherControlCharacters)
    - [`com.google.gson.stream.JsonReaderTest.testNonStrictModeParsesUnescapedControlCharacter`](#JsonReaderTesttestNonStrictModeParsesUnescapedControlCharacter)
    - [`com.google.gson.stream.JsonReaderTest.testCapitalizedTrueFailWhenStrict`](#JsonReaderTesttestCapitalizedTrueFailWhenStrict)
    - [`com.google.gson.stream.JsonReaderTest.testCapitalizedFalseFailWhenStrict`](#JsonReaderTesttestCapitalizedFalseFailWhenStrict)
    - [`com.google.gson.stream.JsonReaderTest.testCapitalizedNullFailWhenStrict`](#JsonReaderTesttestCapitalizedNullFailWhenStrict)
    - [`com.google.gson.stream.JsonReaderTest.testReadArray`](#JsonReaderTesttestReadArray)
    - [`com.google.gson.stream.JsonReaderTest.testReadEmptyArray`](#JsonReaderTesttestReadEmptyArray)
    - [`com.google.gson.stream.JsonReaderTest.testReadObject`](#JsonReaderTesttestReadObject)
    - [`com.google.gson.stream.JsonReaderTest.testReadEmptyObject`](#JsonReaderTesttestReadEmptyObject)
    - [`com.google.gson.stream.JsonReaderTest.testHasNextEndOfDocument`](#JsonReaderTesttestHasNextEndOfDocument)
    - [`com.google.gson.stream.JsonReaderTest.testSkipArray`](#JsonReaderTesttestSkipArray)
    - [`com.google.gson.stream.JsonReaderTest.testSkipArrayAfterPeek`](#JsonReaderTesttestSkipArrayAfterPeek)
    - [`com.google.gson.stream.JsonReaderTest.testSkipTopLevelObject`](#JsonReaderTesttestSkipTopLevelObject)
    - [`com.google.gson.stream.JsonReaderTest.testSkipObject`](#JsonReaderTesttestSkipObject)
    - [`com.google.gson.stream.JsonReaderTest.testSkipObjectAfterPeek`](#JsonReaderTesttestSkipObjectAfterPeek)
    - [`com.google.gson.stream.JsonReaderTest.testSkipObjectName`](#JsonReaderTesttestSkipObjectName)
    - [`com.google.gson.stream.JsonReaderTest.testSkipObjectNameSingleQuoted`](#JsonReaderTesttestSkipObjectNameSingleQuoted)
    - [`com.google.gson.stream.JsonReaderTest.testSkipObjectNameUnquoted`](#JsonReaderTesttestSkipObjectNameUnquoted)
    - [`com.google.gson.stream.JsonReaderTest.testSkipInteger`](#JsonReaderTesttestSkipInteger)
    - [`com.google.gson.stream.JsonReaderTest.testSkipDouble`](#JsonReaderTesttestSkipDouble)
    - [`com.google.gson.stream.JsonReaderTest.testSkipValueAfterEndOfDocument`](#JsonReaderTesttestSkipValueAfterEndOfDocument)
    - [`com.google.gson.stream.JsonReaderTest.testSkipValueAtArrayEnd`](#JsonReaderTesttestSkipValueAtArrayEnd)
    - [`com.google.gson.stream.JsonReaderTest.testSkipValueAtObjectEnd`](#JsonReaderTesttestSkipValueAtObjectEnd)
    - [`com.google.gson.stream.JsonReaderTest.testHelloWorld`](#JsonReaderTesttestHelloWorld)
    - [`com.google.gson.stream.JsonReaderTest.testInvalidJsonInput`](#JsonReaderTesttestInvalidJsonInput)
    - [`com.google.gson.stream.JsonReaderTest.testNulls`](#JsonReaderTesttestNulls)
    - [`com.google.gson.stream.JsonReaderTest.testEmptyString`](#JsonReaderTesttestEmptyString)
    - [`com.google.gson.stream.JsonReaderTest.testCharacterUnescaping`](#JsonReaderTesttestCharacterUnescaping)
    - [`com.google.gson.stream.JsonReaderTest.testReaderDoesNotTreatU2028U2029AsNewline`](#JsonReaderTesttestReaderDoesNotTreatU2028U2029AsNewline)
    - [`com.google.gson.stream.JsonReaderTest.testEscapeCharacterQuoteInStrictMode`](#JsonReaderTesttestEscapeCharacterQuoteInStrictMode)
    - [`com.google.gson.stream.JsonReaderTest.testEscapeCharacterQuoteWithoutStrictMode`](#JsonReaderTesttestEscapeCharacterQuoteWithoutStrictMode)
    - [`com.google.gson.stream.JsonReaderTest.testUnescapingInvalidCharacters`](#JsonReaderTesttestUnescapingInvalidCharacters)
    - [`com.google.gson.stream.JsonReaderTest.testUnescapingTruncatedCharacters`](#JsonReaderTesttestUnescapingTruncatedCharacters)
    - [`com.google.gson.stream.JsonReaderTest.testUnescapingTruncatedSequence`](#JsonReaderTesttestUnescapingTruncatedSequence)
    - [`com.google.gson.stream.JsonReaderTest.testIntegersWithFractionalPartSpecified`](#JsonReaderTesttestIntegersWithFractionalPartSpecified)
    - [`com.google.gson.stream.JsonReaderTest.testDoubles`](#JsonReaderTesttestDoubles)
    - [`com.google.gson.stream.JsonReaderTest.testStrictNonFiniteDoubles`](#JsonReaderTesttestStrictNonFiniteDoubles)
    - [`com.google.gson.stream.JsonReaderTest.testStrictQuotedNonFiniteDoubles`](#JsonReaderTesttestStrictQuotedNonFiniteDoubles)
    - [`com.google.gson.stream.JsonReaderTest.testLenientNonFiniteDoubles`](#JsonReaderTesttestLenientNonFiniteDoubles)
    - [`com.google.gson.stream.JsonReaderTest.testLenientQuotedNonFiniteDoubles`](#JsonReaderTesttestLenientQuotedNonFiniteDoubles)
    - [`com.google.gson.stream.JsonReaderTest.testStrictNonFiniteDoublesWithSkipValue`](#JsonReaderTesttestStrictNonFiniteDoublesWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testLongs`](#JsonReaderTesttestLongs)
    - [`com.google.gson.stream.JsonReaderTest.testNumberWithOctalPrefix`](#JsonReaderTesttestNumberWithOctalPrefix)
    - [`com.google.gson.stream.JsonReaderTest.testBooleans`](#JsonReaderTesttestBooleans)
    - [`com.google.gson.stream.JsonReaderTest.testPeekingUnquotedStringsPrefixedWithBooleans`](#JsonReaderTesttestPeekingUnquotedStringsPrefixedWithBooleans)
    - [`com.google.gson.stream.JsonReaderTest.testMalformedNumbers`](#JsonReaderTesttestMalformedNumbers)
    - [`com.google.gson.stream.JsonReaderTest.assertNotANumber`](#JsonReaderTestassertNotANumber)
    - [`com.google.gson.stream.JsonReaderTest.testPeekingUnquotedStringsPrefixedWithIntegers`](#JsonReaderTesttestPeekingUnquotedStringsPrefixedWithIntegers)
    - [`com.google.gson.stream.JsonReaderTest.testPeekLongMinValue`](#JsonReaderTesttestPeekLongMinValue)
    - [`com.google.gson.stream.JsonReaderTest.testPeekLongMaxValue`](#JsonReaderTesttestPeekLongMaxValue)
    - [`com.google.gson.stream.JsonReaderTest.testLongLargerThanMaxLongThatWrapsAround`](#JsonReaderTesttestLongLargerThanMaxLongThatWrapsAround)
    - [`com.google.gson.stream.JsonReaderTest.testLongLargerThanMinLongThatWrapsAround`](#JsonReaderTesttestLongLargerThanMinLongThatWrapsAround)
    - [`com.google.gson.stream.JsonReaderTest.testNegativeZero`](#JsonReaderTesttestNegativeZero)
    - [`com.google.gson.stream.JsonReaderTest.testPeekLargerThanLongMaxValue`](#JsonReaderTesttestPeekLargerThanLongMaxValue)
    - [`com.google.gson.stream.JsonReaderTest.testPeekLargerThanLongMinValue`](#JsonReaderTesttestPeekLargerThanLongMinValue)
    - [`com.google.gson.stream.JsonReaderTest.testHighPrecisionLong`](#JsonReaderTesttestHighPrecisionLong)
    - [`com.google.gson.stream.JsonReaderTest.testPeekMuchLargerThanLongMinValue`](#JsonReaderTesttestPeekMuchLargerThanLongMinValue)
    - [`com.google.gson.stream.JsonReaderTest.testQuotedNumberWithEscape`](#JsonReaderTesttestQuotedNumberWithEscape)
    - [`com.google.gson.stream.JsonReaderTest.testMixedCaseLiterals`](#JsonReaderTesttestMixedCaseLiterals)
    - [`com.google.gson.stream.JsonReaderTest.testMissingValue`](#JsonReaderTesttestMissingValue)
    - [`com.google.gson.stream.JsonReaderTest.testPrematureEndOfInput`](#JsonReaderTesttestPrematureEndOfInput)
    - [`com.google.gson.stream.JsonReaderTest.testPrematurelyClosed`](#JsonReaderTesttestPrematurelyClosed)
    - [`com.google.gson.stream.JsonReaderTest.testNextFailuresDoNotAdvance`](#JsonReaderTesttestNextFailuresDoNotAdvance)
    - [`com.google.gson.stream.JsonReaderTest.testIntegerMismatchFailuresDoNotAdvance`](#JsonReaderTesttestIntegerMismatchFailuresDoNotAdvance)
    - [`com.google.gson.stream.JsonReaderTest.testStringNullIsNotNull`](#JsonReaderTesttestStringNullIsNotNull)
    - [`com.google.gson.stream.JsonReaderTest.testNullLiteralIsNotAString`](#JsonReaderTesttestNullLiteralIsNotAString)
    - [`com.google.gson.stream.JsonReaderTest.testStrictNameValueSeparator`](#JsonReaderTesttestStrictNameValueSeparator)
    - [`com.google.gson.stream.JsonReaderTest.testLenientNameValueSeparator`](#JsonReaderTesttestLenientNameValueSeparator)
    - [`com.google.gson.stream.JsonReaderTest.testStrictNameValueSeparatorWithSkipValue`](#JsonReaderTesttestStrictNameValueSeparatorWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testCommentsInStringValue`](#JsonReaderTesttestCommentsInStringValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictComments`](#JsonReaderTesttestStrictComments)
    - [`com.google.gson.stream.JsonReaderTest.testLenientComments`](#JsonReaderTesttestLenientComments)
    - [`com.google.gson.stream.JsonReaderTest.testStrictCommentsWithSkipValue`](#JsonReaderTesttestStrictCommentsWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictUnquotedNames`](#JsonReaderTesttestStrictUnquotedNames)
    - [`com.google.gson.stream.JsonReaderTest.testLenientUnquotedNames`](#JsonReaderTesttestLenientUnquotedNames)
    - [`com.google.gson.stream.JsonReaderTest.testStrictUnquotedNamesWithSkipValue`](#JsonReaderTesttestStrictUnquotedNamesWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedNames`](#JsonReaderTesttestStrictSingleQuotedNames)
    - [`com.google.gson.stream.JsonReaderTest.testLenientSingleQuotedNames`](#JsonReaderTesttestLenientSingleQuotedNames)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedNamesWithSkipValue`](#JsonReaderTesttestStrictSingleQuotedNamesWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictUnquotedStrings`](#JsonReaderTesttestStrictUnquotedStrings)
    - [`com.google.gson.stream.JsonReaderTest.testStrictUnquotedStringsWithSkipValue`](#JsonReaderTesttestStrictUnquotedStringsWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testLenientUnquotedStrings`](#JsonReaderTesttestLenientUnquotedStrings)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedStrings`](#JsonReaderTesttestStrictSingleQuotedStrings)
    - [`com.google.gson.stream.JsonReaderTest.testLenientSingleQuotedStrings`](#JsonReaderTesttestLenientSingleQuotedStrings)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedStringsWithSkipValue`](#JsonReaderTesttestStrictSingleQuotedStringsWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedArray`](#JsonReaderTesttestStrictSemicolonDelimitedArray)
    - [`com.google.gson.stream.JsonReaderTest.testLenientSemicolonDelimitedArray`](#JsonReaderTesttestLenientSemicolonDelimitedArray)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedArrayWithSkipValue`](#JsonReaderTesttestStrictSemicolonDelimitedArrayWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedNameValuePair`](#JsonReaderTesttestStrictSemicolonDelimitedNameValuePair)
    - [`com.google.gson.stream.JsonReaderTest.testLenientSemicolonDelimitedNameValuePair`](#JsonReaderTesttestLenientSemicolonDelimitedNameValuePair)
    - [`com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedNameValuePairWithSkipValue`](#JsonReaderTesttestStrictSemicolonDelimitedNameValuePairWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictUnnecessaryArraySeparators`](#JsonReaderTesttestStrictUnnecessaryArraySeparators)
    - [`com.google.gson.stream.JsonReaderTest.testLenientUnnecessaryArraySeparators`](#JsonReaderTesttestLenientUnnecessaryArraySeparators)
    - [`com.google.gson.stream.JsonReaderTest.testStrictUnnecessaryArraySeparatorsWithSkipValue`](#JsonReaderTesttestStrictUnnecessaryArraySeparatorsWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictMultipleTopLevelValues`](#JsonReaderTesttestStrictMultipleTopLevelValues)
    - [`com.google.gson.stream.JsonReaderTest.testLenientMultipleTopLevelValues`](#JsonReaderTesttestLenientMultipleTopLevelValues)
    - [`com.google.gson.stream.JsonReaderTest.testStrictMultipleTopLevelValuesWithSkipValue`](#JsonReaderTesttestStrictMultipleTopLevelValuesWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testTopLevelValueTypes`](#JsonReaderTesttestTopLevelValueTypes)
    - [`com.google.gson.stream.JsonReaderTest.testTopLevelValueTypeWithSkipValue`](#JsonReaderTesttestTopLevelValueTypeWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testStrictNonExecutePrefix`](#JsonReaderTesttestStrictNonExecutePrefix)
    - [`com.google.gson.stream.JsonReaderTest.testStrictNonExecutePrefixWithSkipValue`](#JsonReaderTesttestStrictNonExecutePrefixWithSkipValue)
    - [`com.google.gson.stream.JsonReaderTest.testLenientNonExecutePrefix`](#JsonReaderTesttestLenientNonExecutePrefix)
    - [`com.google.gson.stream.JsonReaderTest.testLenientNonExecutePrefixWithLeadingWhitespace`](#JsonReaderTesttestLenientNonExecutePrefixWithLeadingWhitespace)
    - [`com.google.gson.stream.JsonReaderTest.testLenientPartialNonExecutePrefix`](#JsonReaderTesttestLenientPartialNonExecutePrefix)
    - [`com.google.gson.stream.JsonReaderTest.testBomIgnoredAsFirstCharacterOfDocument`](#JsonReaderTesttestBomIgnoredAsFirstCharacterOfDocument)
    - [`com.google.gson.stream.JsonReaderTest.testBomForbiddenAsOtherCharacterInDocument`](#JsonReaderTesttestBomForbiddenAsOtherCharacterInDocument)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionGreaterThanBufferSize`](#JsonReaderTesttestFailWithPositionGreaterThanBufferSize)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionOverSlashSlashEndOfLineComment`](#JsonReaderTesttestFailWithPositionOverSlashSlashEndOfLineComment)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionOverHashEndOfLineComment`](#JsonReaderTesttestFailWithPositionOverHashEndOfLineComment)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionOverCStyleComment`](#JsonReaderTesttestFailWithPositionOverCStyleComment)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionOverQuotedString`](#JsonReaderTesttestFailWithPositionOverQuotedString)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionOverUnquotedString`](#JsonReaderTesttestFailWithPositionOverUnquotedString)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithEscapedNewlineCharacter`](#JsonReaderTesttestFailWithEscapedNewlineCharacter)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionIsOffsetByBom`](#JsonReaderTesttestFailWithPositionIsOffsetByBom)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPositionDeepPath`](#JsonReaderTesttestFailWithPositionDeepPath)
    - [`com.google.gson.stream.JsonReaderTest.testStrictVeryLongNumber`](#JsonReaderTesttestStrictVeryLongNumber)
    - [`com.google.gson.stream.JsonReaderTest.testLenientVeryLongNumber`](#JsonReaderTesttestLenientVeryLongNumber)
    - [`com.google.gson.stream.JsonReaderTest.testVeryLongUnquotedLiteral`](#JsonReaderTesttestVeryLongUnquotedLiteral)
    - [`com.google.gson.stream.JsonReaderTest.testDeeplyNestedArrays`](#JsonReaderTesttestDeeplyNestedArrays)
    - [`com.google.gson.stream.JsonReaderTest.testDeeplyNestedObjects`](#JsonReaderTesttestDeeplyNestedObjects)
    - [`com.google.gson.stream.JsonReaderTest.testNestingLimitDefault`](#JsonReaderTesttestNestingLimitDefault)
    - [`com.google.gson.stream.JsonReaderTest.testNestingLimit`](#JsonReaderTesttestNestingLimit)
    - [`com.google.gson.stream.JsonReaderTest.testStringEndingInSlash`](#JsonReaderTesttestStringEndingInSlash)
    - [`com.google.gson.stream.JsonReaderTest.testDocumentWithCommentEndingInSlash`](#JsonReaderTesttestDocumentWithCommentEndingInSlash)
    - [`com.google.gson.stream.JsonReaderTest.testStringWithLeadingSlash`](#JsonReaderTesttestStringWithLeadingSlash)
    - [`com.google.gson.stream.JsonReaderTest.testUnterminatedObject`](#JsonReaderTesttestUnterminatedObject)
    - [`com.google.gson.stream.JsonReaderTest.testVeryLongQuotedString`](#JsonReaderTesttestVeryLongQuotedString)
    - [`com.google.gson.stream.JsonReaderTest.testVeryLongUnquotedString`](#JsonReaderTesttestVeryLongUnquotedString)
    - [`com.google.gson.stream.JsonReaderTest.testVeryLongUnterminatedString`](#JsonReaderTesttestVeryLongUnterminatedString)
    - [`com.google.gson.stream.JsonReaderTest.testSkipVeryLongUnquotedString`](#JsonReaderTesttestSkipVeryLongUnquotedString)
    - [`com.google.gson.stream.JsonReaderTest.testSkipTopLevelUnquotedString`](#JsonReaderTesttestSkipTopLevelUnquotedString)
    - [`com.google.gson.stream.JsonReaderTest.testSkipVeryLongQuotedString`](#JsonReaderTesttestSkipVeryLongQuotedString)
    - [`com.google.gson.stream.JsonReaderTest.testSkipTopLevelQuotedString`](#JsonReaderTesttestSkipTopLevelQuotedString)
    - [`com.google.gson.stream.JsonReaderTest.testStringAsNumberWithTruncatedExponent`](#JsonReaderTesttestStringAsNumberWithTruncatedExponent)
    - [`com.google.gson.stream.JsonReaderTest.testStringAsNumberWithDigitAndNonDigitExponent`](#JsonReaderTesttestStringAsNumberWithDigitAndNonDigitExponent)
    - [`com.google.gson.stream.JsonReaderTest.testStringAsNumberWithNonDigitExponent`](#JsonReaderTesttestStringAsNumberWithNonDigitExponent)
    - [`com.google.gson.stream.JsonReaderTest.testEmptyStringName`](#JsonReaderTesttestEmptyStringName)
    - [`com.google.gson.stream.JsonReaderTest.testStrictExtraCommasInMaps`](#JsonReaderTesttestStrictExtraCommasInMaps)
    - [`com.google.gson.stream.JsonReaderTest.testLenientExtraCommasInMaps`](#JsonReaderTesttestLenientExtraCommasInMaps)
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonReaderTest.testMalformedDocuments`](#JsonReaderTesttestMalformedDocuments)
    - [`com.google.gson.stream.JsonReaderTest.testUnterminatedStringFailure`](#JsonReaderTesttestUnterminatedStringFailure)
    - [`com.google.gson.stream.JsonReaderTest.testReadAcrossBuffers`](#JsonReaderTesttestReadAcrossBuffers)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
    - [`com.google.gson.stream.JsonReaderTest.assertUnexpectedStructureError`](#JsonReaderTestassertUnexpectedStructureError)
    - [`com.google.gson.stream.JsonReaderTest.assertDocument`](#JsonReaderTestassertDocument)
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)

**Methods**

---
#### JsonReaderTest\.testDefaultStrictness<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testDefaultStrictness}} -->
Tests that the default strictness of the `JsonReader` is set to `LEGACY_STRICT`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `JsonReader` is created with an empty JSON object as input.
    - The method `getStrictness()` is called on the `JsonReader` instance to retrieve its current strictness setting.
    - The retrieved strictness is then asserted to be equal to `Strictness.LEGACY_STRICT`.
- **Output**:
    - The method does not return any value; it asserts that the default strictness is `LEGACY_STRICT`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSetLenientTrue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSetLenientTrue}} -->
Tests the behavior of the `JsonReader` when set to lenient mode.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `JsonReader` is created with a JSON string containing an empty object.
    - The [`setLenient`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetLenient) method is called on the `JsonReader` instance with a value of `true`.
    - The test asserts that the strictness of the `JsonReader` is set to `Strictness.LENIENT`.
- **Output**:
    - The method does not return a value but asserts that the strictness of the `JsonReader` is `Strictness.LENIENT`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setLenient`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetLenient)
    - [`com.google.gson.stream.JsonReader.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSetLenientFalse<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSetLenientFalse}} -->
Tests the behavior of the `JsonReader` when setting lenient mode to false.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `JsonReader` is created with an empty JSON object as input.
    - The [`setLenient`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetLenient) method of the `JsonReader` instance is called with `false` to enforce strict parsing.
    - The strictness of the `JsonReader` is then asserted to be equal to `Strictness.LEGACY_STRICT`.
- **Output**:
    - The method does not return a value; it asserts that the strictness of the reader is set to `Strictness.LEGACY_STRICT`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setLenient`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetLenient)
    - [`com.google.gson.stream.JsonReader.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSetStrictness<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSetStrictness}} -->
Tests the [`setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness) method of the `JsonReader` class to ensure it correctly sets the strictness level.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `JsonReader` is created with an empty JSON object as input.
    - The [`setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness) method is called on the `JsonReader` instance with `Strictness.STRICT` as the argument.
    - The [`getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetStrictness) method is called to retrieve the current strictness level of the `JsonReader`.
    - An assertion is made to check if the retrieved strictness level is equal to `Strictness.STRICT`.
- **Output**:
    - The method does not return a value; it asserts that the strictness level has been set correctly.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
    - [`com.google.gson.stream.JsonReader.getStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSetStrictnessNull<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSetStrictnessNull}} -->
Tests that setting the strictness of a `JsonReader` to null throws a `NullPointerException`.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with an empty JSON object.
- **Control Flow**:
    - Creates a new instance of `JsonReader` with an empty JSON object.
    - Calls the [`setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness) method of `JsonReader` with a null argument.
    - Asserts that a `NullPointerException` is thrown.
- **Output**:
    - The method does not return a value; it asserts that a `NullPointerException` is thrown when attempting to set strictness to null.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testEscapedNewlineNotAllowedInStrictMode<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testEscapedNewlineNotAllowedInStrictMode}} -->
Tests that an IOException is thrown when an escaped newline character is encountered in strict mode.
- **Modifiers**: `public`, `Test`
- **Inputs**:
    - `json`: A string containing a JSON representation with an escaped newline character.
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with the JSON string and set to strict mode.
- **Control Flow**:
    - A `JsonReader` is created with a JSON string that contains an escaped newline character.
    - The strictness of the `JsonReader` is set to `Strictness.STRICT`.
    - The method `nextString` is called on the `JsonReader`, which is expected to throw an `IOException`.
    - The thrown exception is caught and verified to have a specific message indicating the error.
- **Output**:
    - An `IOException` is thrown with a message indicating that escaping a newline character is not allowed in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testEscapedNewlineAllowedInDefaultMode<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testEscapedNewlineAllowedInDefaultMode}} -->
Tests that an escaped newline character is correctly interpreted in default mode.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `json`: A string containing a JSON representation with an escaped newline character.
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with the JSON string.
- **Control Flow**:
    - Creates a JSON string with an escaped newline character.
    - Initializes a `JsonReader` with the JSON string.
    - Calls `nextString()` on the `JsonReader` to read the string value.
    - Asserts that the output of `nextString()` is equal to the expected newline character.
- **Output**:
    - The method does not return a value but asserts that the output of `nextString()` is equal to the newline character.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictModeFailsToParseUnescapedControlCharacter<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictModeFailsToParseUnescapedControlCharacter}} -->
Tests that strict mode fails to parse unescaped control characters in JSON.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `json`: A string representing JSON input that may contain unescaped control characters.
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with the JSON string.
    - `expected`: An `IOException` expected to be thrown when parsing unescaped control characters.
- **Control Flow**:
    - The method initializes a `JsonReader` with a JSON string containing an unescaped control character.
    - It sets the strictness of the `JsonReader` to `Strictness.STRICT`.
    - It attempts to read the next string from the `JsonReader` using `nextString()`.
    - If an `IOException` is thrown, it checks that the message starts with a specific error message indicating unescaped control characters are not allowed.
    - This process is repeated for different JSON strings containing various unescaped control characters.
- **Output**:
    - The method does not return a value but asserts that an `IOException` is thrown with the expected message for each test case.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictModeAllowsOtherControlCharacters<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictModeAllowsOtherControlCharacters}} -->
Tests that strict mode allows control characters outside the range U+0000 to U+001F.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A JSON string containing control characters U+007F and U+009F is defined.
    - A `JsonReader` instance is created with the JSON string.
    - The strictness of the `JsonReader` is set to `Strictness.STRICT`.
    - The method `nextString()` is called to read the string from the JSON.
    - The result is asserted to be equal to the expected string containing the control characters.
- **Output**:
    - The method does not return a value but asserts that the output of `nextString()` matches the expected string containing the control characters.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNonStrictModeParsesUnescapedControlCharacter<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNonStrictModeParsesUnescapedControlCharacter}} -->
Tests that the `JsonReader` can parse an unescaped control character in non-strict mode.
- **Inputs**:
    - `json`: A string containing JSON data with an unescaped control character (tab character in this case).
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with the JSON string.
- **Control Flow**:
    - Creates a JSON string containing a tab character.
    - Initializes a `JsonReader` with the JSON string.
    - Calls `nextString()` on the `JsonReader` to read the string value.
    - Asserts that the output of `nextString()` is equal to the expected tab character.
- **Output**:
    - The method does not return a value but asserts that the parsed string from the JSON input matches the expected tab character.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testCapitalizedTrueFailWhenStrict<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testCapitalizedTrueFailWhenStrict}} -->
Tests that the `JsonReader` fails to parse capitalized boolean values when strictness is set to strict.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing the boolean value 'TRUE'.
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing the boolean value 'True'.
- **Control Flow**:
    - Creates a `JsonReader` instance with the string 'TRUE' and sets its strictness to `Strictness.STRICT`.
    - Asserts that calling `nextBoolean` on the reader throws an `IOException` with a specific message.
    - Creates another `JsonReader` instance with the string 'True' and sets its strictness to `Strictness.STRICT`.
    - Asserts that calling `nextBoolean` on this second reader also throws an `IOException` with the same specific message.
- **Output**:
    - An `IOException` is thrown for both cases, indicating that the input is not accepted in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testCapitalizedFalseFailWhenStrict<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testCapitalizedFalseFailWhenStrict}} -->
Tests that the `JsonReader` fails to parse capitalized boolean values as `false` when strictness is set to `STRICT`.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with the input string 'FALSE' and sets its strictness to `Strictness.STRICT`.
    - Asserts that calling `nextBoolean` on the reader throws an `IOException` with a specific message.
    - Creates another `JsonReader` instance with the input string 'FaLse' and sets its strictness to `Strictness.STRICT`.
    - Asserts that calling `nextBoolean` on the new reader also throws an `IOException` with the same specific message.
- **Output**:
    - The method does not return a value but asserts that specific exceptions are thrown when invalid boolean values are parsed.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testCapitalizedNullFailWhenStrict<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testCapitalizedNullFailWhenStrict}} -->
Tests that the `JsonReader` fails to parse capitalized 'NULL' and 'nulL' in strict mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with the input 'NULL' and sets strictness to `Strictness.STRICT`.
    - Asserts that calling `nextNull` throws an `IOException` with a specific message.
    - Creates another `JsonReader` instance with the input 'nulL' and sets strictness to `Strictness.STRICT`.
    - Asserts that calling `nextNull` again throws an `IOException` with the same specific message.
- **Output**:
    - The method does not return a value; it asserts that exceptions are thrown as expected.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testReadArray<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testReadArray}} -->
Tests the reading of a JSON array containing boolean values.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array string '[true, true]'.
    - Begins reading the array with `beginArray()`.
    - Reads the first boolean value using `nextBoolean()` and asserts it is true.
    - Reads the second boolean value using `nextBoolean()` and asserts it is true.
    - Ends the array reading with `endArray()`.
    - Asserts that the next token is `END_DOCUMENT` using `peek()`.
- **Output**:
    - No output is returned; assertions are made to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.endArray`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendArray)
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testReadEmptyArray<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testReadEmptyArray}} -->
Tests the behavior of `JsonReader` when reading an empty JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with an empty JSON array as input.
    - Begins reading the array using `reader.beginArray()`.
    - Checks if there are any elements in the array using `reader.hasNext()`, which should return false for an empty array.
    - Ends the array reading with `reader.endArray()`.
    - Peeks at the next token using `reader.peek()`, which should indicate the end of the document.
- **Output**:
    - The method does not return a value but asserts that the array is empty and that the end of the document is reached.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.hasNext`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderhasNext)
    - [`com.google.gson.stream.JsonReader.endArray`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendArray)
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testReadObject<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testReadObject}} -->
Tests the reading of a JSON object using `JsonReader`.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing two key-value pairs.
    - Begins reading the JSON object.
    - Asserts that the first key read is 'a' and its corresponding value is 'android'.
    - Asserts that the second key read is 'b' and its corresponding value is 'banana'.
    - Ends the JSON object reading.
    - Asserts that the next token is the end of the document.
- **Output**:
    - No output is returned; the method performs assertions to validate the reading of the JSON object.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.endObject`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendObject)
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testReadEmptyObject<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testReadEmptyObject}} -->
Tests the behavior of `JsonReader` when reading an empty JSON object.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with an empty JSON object represented as a string '{}'.
    - Begins reading the JSON object using `reader.beginObject()`.
    - Checks if there are any elements in the object using `reader.hasNext()`, which should return false for an empty object.
    - Ends the JSON object reading with `reader.endObject()`.
    - Asserts that the next token is `JsonToken.END_DOCUMENT`, indicating the end of the input.
- **Output**:
    - The method does not return a value but asserts that the `JsonReader` behaves correctly when reading an empty object.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginObject)
    - [`com.google.gson.stream.JsonReader.hasNext`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderhasNext)
    - [`com.google.gson.stream.JsonReader.endObject`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testHasNextEndOfDocument<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testHasNextEndOfDocument}} -->
Tests the [`hasNext`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderhasNext) method of `JsonReader` to verify it returns false at the end of a JSON object.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `JsonReader` with an empty JSON object.
    - Begins reading the JSON object using `beginObject()`.
    - Ends reading the JSON object using `endObject()`.
    - Asserts that `hasNext()` returns false, indicating there are no more elements to read.
- **Output**:
    - The method does not return a value but asserts that `reader.hasNext()` is false, confirming the end of the JSON object.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonReader.hasNext`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderhasNext)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipArray<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipArray}} -->
Tests the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method of `JsonReader` to ensure it correctly skips over a JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an object with an array and an integer.
    - Begins reading the JSON object.
    - Reads the first name in the object, which is 'a'.
    - Calls `skipValue()` to skip the array associated with 'a'.
    - Reads the next name in the object, which is 'b'.
    - Reads the integer value associated with 'b' and asserts it equals 123.
    - Ends the JSON object.
    - Asserts that the next token is `END_DOCUMENT`.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipArrayAfterPeek<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipArrayAfterPeek}} -->
Tests the behavior of `JsonReader` when skipping an array after peeking.
- **Modifiers**: `public`, `void`, `throws`, `Exception`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an object with an array and an integer.
    - Begins reading the JSON object.
    - Retrieves the name of the first property, which is expected to be 'a'.
    - Peeks at the next token, which should indicate the beginning of an array.
    - Calls `skipValue()` to skip the array associated with the property 'a'.
    - Retrieves the name of the next property, which is expected to be 'b'.
    - Reads the integer value associated with property 'b', which should be 123.
    - Ends the JSON object.
    - Peeks at the next token, which should indicate the end of the document.
- **Output**:
    - The method does not return a value but asserts that the expected values are correctly read from the JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipTopLevelObject<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipTopLevelObject}} -->
This method tests the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) functionality of the `JsonReader` class.
- **Modifiers**: `public`, `void`, `throws`, `Exception`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string containing an object with an array and a number.
    - The [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method is called on the `JsonReader` instance, which skips the top-level object.
    - The method then asserts that the next token to be read is `END_DOCUMENT`, indicating that the end of the JSON input has been reached.
- **Output**:
    - The method does not return a value but asserts that the `JsonReader` has reached the end of the document after skipping the top-level object.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipObject<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipObject}} -->
Tests the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method of the `JsonReader` class to ensure it correctly skips over JSON objects.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an object with two properties: 'a' and 'b'.
    - Begins reading the JSON object.
    - Reads the first name, which is expected to be 'a', and verifies it using an assertion.
    - Calls `skipValue()` to skip the value associated with 'a'.
    - Reads the next name, which is expected to be 'b', and verifies it using an assertion.
    - Calls `skipValue()` again to skip the value associated with 'b'.
    - Ends the JSON object reading.
    - Asserts that the next token is `END_DOCUMENT`, indicating the end of the JSON input.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipObjectAfterPeek<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipObjectAfterPeek}} -->
Tests the behavior of `JsonReader` when skipping objects after peeking.
- **Inputs**:
    - `json`: A JSON string representing an object with three properties: 'one', 'two', and 'three', each containing an object with a numeric property.
- **Control Flow**:
    - Creates a `JsonReader` instance with the provided JSON string.
    - Begins reading the JSON object.
    - Reads the first name and checks it is 'one'.
    - Peeks at the next token to confirm it is the beginning of an object.
    - Skips the value associated with 'one'.
    - Reads the next name and checks it is 'two'.
    - Peeks at the next token to confirm it is the beginning of an object.
    - Skips the value associated with 'two'.
    - Reads the next name and checks it is 'three'.
    - Skips the value associated with 'three'.
    - Ends the JSON object.
    - Peeks at the next token to confirm it is the end of the document.
- **Output**:
    - Confirms that the `JsonReader` has successfully skipped the values of the specified keys and reached the end of the document.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipObjectName<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipObjectName}} -->
Tests the behavior of `JsonReader` when skipping an object name.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a JSON string containing an object with a single key-value pair.
    - Begins reading the JSON object using `beginObject()`.
    - Skips the value associated with the first key using `skipValue()`.
    - Checks the next token using `peek()` to ensure it is a number.
    - Verifies the path of the reader using `getPath()` to confirm the skipped value is represented as `<skipped>`.
    - Reads the next integer value using `nextInt()` and asserts it equals 1.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipObjectNameSingleQuoted<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipObjectNameSingleQuoted}} -->
Tests the behavior of `JsonReader` when skipping a single-quoted object name.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing a single-quoted object.
- **Control Flow**:
    - The method begins by creating a `JsonReader` instance with a JSON string that has single quotes.
    - It sets the strictness of the reader to `LENIENT` to allow for non-standard JSON formats.
    - The method then begins reading the JSON object.
    - It skips the value associated with the first key in the object.
    - After skipping, it checks the next token to ensure it is a number.
    - It verifies the path of the reader to confirm that the skipped value is recorded correctly.
    - Finally, it reads the next integer value from the JSON object.
- **Output**:
    - The method does not return a value but asserts that the next token is a number and verifies the path and integer value read.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipObjectNameUnquoted<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipObjectNameUnquoted}} -->
Tests the behavior of `JsonReader` when skipping an unquoted object name.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an unquoted object name.
    - Sets the strictness of the reader to `LENIENT` to allow unquoted names.
    - Begins reading the JSON object.
    - Skips the value associated with the unquoted name.
    - Asserts that the next token is a number.
    - Asserts that the path reflects the skipped value.
    - Reads and asserts the integer value of the next token.
- **Output**:
    - The method does not return a value but asserts conditions to verify the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipInteger<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipInteger}} -->
Tests the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method of `JsonReader` for integer values.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing two integer values.
- **Control Flow**:
    - The method begins by creating a `JsonReader` instance with a JSON string containing two integer values.
    - It then starts reading the JSON object using `beginObject()`.
    - The first name in the object is read using `nextName()` and is expected to be 'a'.
    - The value associated with 'a' is skipped using `skipValue()`.
    - The next name in the object is read using `nextName()` and is expected to be 'b'.
    - The value associated with 'b' is also skipped using `skipValue()`.
    - The method ends the JSON object with `endObject()`.
    - Finally, it checks that the next token is `END_DOCUMENT` using `peek()`.
- **Output**:
    - The method does not return a value but asserts that the JSON reader correctly skips the integer values and reaches the end of the document.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipDouble<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipDouble}} -->
Tests the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method of `JsonReader` for double values.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing two double values.
    - Begins reading the JSON object.
    - Reads the first name in the object and asserts it is 'a'.
    - Calls `skipValue()` to skip the value associated with 'a'.
    - Reads the next name in the object and asserts it is 'b'.
    - Calls `skipValue()` to skip the value associated with 'b'.
    - Ends the JSON object.
    - Asserts that the next token is `END_DOCUMENT`.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipValueAfterEndOfDocument<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipValueAfterEndOfDocument}} -->
Tests the behavior of `JsonReader` when attempting to skip a value after reaching the end of a JSON document.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with an empty JSON object.
    - Begins reading the JSON object and immediately ends it.
    - Asserts that the next token is `END_DOCUMENT`.
    - Asserts that the current path is `$`.
    - Calls `skipValue()` on the reader, which should not change the state since it's at the end of the document.
    - Asserts that the next token is still `END_DOCUMENT`.
    - Asserts that the current path remains `$`.
- **Output**:
    - The method does not return a value but asserts that the state of the `JsonReader` remains consistent after attempting to skip a value at the end of the document.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipValueAtArrayEnd<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipValueAtArrayEnd}} -->
Tests the behavior of `JsonReader` when skipping a value at the end of an empty JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with an empty JSON array as input.
    - Begins reading the array using `beginArray()`.
    - Calls `skipValue()` to skip the current value (which is non-existent in this case).
    - Asserts that the next token is `END_DOCUMENT`, indicating the end of the input.
    - Asserts that the current path is `$`, indicating the root of the JSON structure.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipValueAtObjectEnd<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipValueAtObjectEnd}} -->
Tests the behavior of `JsonReader` when skipping a value at the end of an object.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with an empty JSON object.
    - Begins reading the JSON object.
    - Calls `skipValue()` to skip the current value (which is non-existent in this case).
    - Asserts that the next token is `END_DOCUMENT`, indicating the end of the JSON input.
    - Asserts that the current path is `$`, indicating the root of the JSON structure.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testHelloWorld<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testHelloWorld}} -->
Tests the parsing of a JSON object containing a boolean and an array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a JSON string with a boolean and an array.
    - Initializes a `JsonReader` with the JSON string.
    - Begins reading the JSON object.
    - Asserts that the first name is 'hello' and its value is true.
    - Asserts that the next name is 'foo' and begins reading the array.
    - Asserts that the first string in the array is 'world'.
    - Ends the array and the object.
    - Asserts that the next token is END_DOCUMENT.
- **Output**:
    - No output is returned; the method performs assertions to validate the JSON parsing.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testInvalidJsonInput<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testInvalidJsonInput}} -->
Tests the behavior of `JsonReader` when provided with invalid JSON input.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string with an invalid escape sequence is defined.
    - A `JsonReader` instance is created using the invalid JSON string.
    - The method begins reading the JSON object.
    - An assertion is made to check if a `MalformedJsonException` is thrown when attempting to read the next name.
    - The exception message is verified to match the expected error message.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNulls<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNulls}} -->
Tests that a `NullPointerException` is thrown when attempting to create a `JsonReader` with a null input.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check if a `NullPointerException` is thrown.
    - It attempts to create a new instance of `JsonReader` with a null argument.
- **Output**:
    - The method does not return a value; it asserts that a `NullPointerException` is thrown.
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testEmptyString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testEmptyString}} -->
Tests that an empty JSON string throws EOFException when attempting to begin an array or an object.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check for exceptions.
    - It attempts to create a `JsonReader` with an empty string and calls `beginArray()` which should throw an `EOFException`.
    - It repeats the same process for `beginObject()` to ensure both cases throw the expected exception.
- **Output**:
    - The method does not return a value; it asserts that an `EOFException` is thrown for both cases.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testCharacterUnescaping<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testCharacterUnescaping}} -->
Tests the unescaping of various JSON character sequences.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string is defined containing various escaped characters.
    - A `JsonReader` is created to read the JSON string.
    - The reader begins reading an array.
    - Each expected string is read from the JSON array and assertions are made to check if the unescaped value matches the expected value.
    - The reader ends the array and checks if the end of the document is reached.
- **Output**:
    - The method does not return a value but asserts that the unescaped strings match expected values, throwing an assertion error if any do not.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testReaderDoesNotTreatU2028U2029AsNewline<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testReaderDoesNotTreatU2028U2029AsNewline}} -->
Tests that the `JsonReader` does not treat Unicode characters U+2028 and U+2029 as newline characters.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a JSON string with U+2028 and checks that an IOException is thrown when trying to read a string.
    - Creates a JSON string with U+2029 and checks that an IOException is thrown when trying to read a string.
    - Creates a valid JSON string with a newline character and verifies that the string is read correctly.
    - Creates a valid JSON string containing U+2028 and U+2029 in strict mode and verifies that the string is read correctly.
- **Output**:
    - The method does not return a value but asserts that specific exceptions are thrown and that the expected string values are returned.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testEscapeCharacterQuoteInStrictMode<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testEscapeCharacterQuoteInStrictMode}} -->
Tests that an IOException is thrown when an invalid escaped character is encountered in strict mode.
- **Modifiers**: `public`, `void`, `@Test`
- **Inputs**:
    - `json`: A string containing a JSON representation with an invalid escaped character ("\'").
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with the JSON string and set to strict mode.
- **Control Flow**:
    - A `JsonReader` is created with the input JSON string containing an invalid escape sequence.
    - The strictness of the `JsonReader` is set to `Strictness.STRICT`.
    - An `IOException` is expected to be thrown when calling `nextString()` on the `JsonReader`.
    - The exception message is asserted to start with 'Invalid escaped character "'" in strict mode'.
- **Output**:
    - An `IOException` is thrown indicating that an invalid escaped character was encountered in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testEscapeCharacterQuoteWithoutStrictMode<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testEscapeCharacterQuoteWithoutStrictMode}} -->
Tests the behavior of `JsonReader` when escaping a single quote character in a JSON string without strict mode.
- **Inputs**:
    - `json`: A JSON string containing an escaped single quote character.
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with the JSON string.
- **Control Flow**:
    - The method initializes a JSON string with an escaped single quote.
    - A `JsonReader` instance is created using the JSON string.
    - The method calls `nextString()` on the `JsonReader` instance to read the string value.
    - The result is asserted to be equal to a single quote character.
- **Output**:
    - The method does not return a value but asserts that the output of `nextString()` is a single quote character ('), indicating successful parsing.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testUnescapingInvalidCharacters<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testUnescapingInvalidCharacters}} -->
Tests the behavior of `JsonReader` when encountering invalid Unicode escape sequences.
- **Inputs**:
    - `json`: A string representing a JSON array containing an invalid Unicode escape sequence.
- **Control Flow**:
    - Creates a `JsonReader` instance with the provided JSON string.
    - Begins reading the JSON array.
    - Asserts that invoking `nextString()` throws a `MalformedJsonException` due to the invalid escape sequence.
    - Verifies that the exception message matches the expected error message.
- **Output**:
    - Throws a `MalformedJsonException` indicating the presence of an invalid Unicode escape sequence.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testUnescapingTruncatedCharacters<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testUnescapingTruncatedCharacters}} -->
Tests the behavior of `JsonReader` when encountering truncated Unicode escape sequences.
- **Inputs**:
    - `json`: A string representing a JSON array containing a truncated Unicode escape sequence.
- **Control Flow**:
    - Creates a `JsonReader` instance with the provided JSON string.
    - Begins reading the JSON array.
    - Asserts that calling `nextString()` throws a `MalformedJsonException` due to the truncated escape sequence.
    - Verifies that the exception message matches the expected error message.
- **Output**:
    - Throws a `MalformedJsonException` indicating an unterminated escape sequence.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testUnescapingTruncatedSequence<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testUnescapingTruncatedSequence}} -->
Tests the behavior of `JsonReader` when encountering a truncated escape sequence in a JSON string.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string is defined with a truncated escape sequence: '["\'.
    - A `JsonReader` instance is created to read the JSON string.
    - The reader begins reading an array.
    - An assertion is made to check that a `MalformedJsonException` is thrown when calling `nextString()`.
    - The exception's message is verified to ensure it indicates an unterminated escape sequence.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testIntegersWithFractionalPartSpecified<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testIntegersWithFractionalPartSpecified}} -->
Tests the behavior of `JsonReader` when reading integers from a JSON array with fractional parts.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array containing three `1.0` values.
    - Begins reading the JSON array.
    - Reads the first value as a `double` and asserts it equals `1.0`.
    - Reads the second value as an `int` and asserts it equals `1`.
    - Reads the third value as a `long` and asserts it equals `1L`.
- **Output**:
    - No output is returned; assertions are made to verify the correctness of the values read from the JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testDoubles<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testDoubles}} -->
Tests the parsing of various double values from a JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing an array of double values is defined.
    - A `JsonReader` instance is created to read the JSON string.
    - The reader begins reading the array.
    - Each double value is read from the array and asserted against expected values using `assertThat`.
    - The reader ends the array after reading all values.
    - Finally, it checks that the reader has reached the end of the document.
- **Output**:
    - The method does not return a value but asserts that the parsed double values match the expected values.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictNonFiniteDoubles<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictNonFiniteDoubles}} -->
Tests that a strict JSON reader throws a MalformedJsonException when encountering NaN.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string containing NaN is defined.
    - A `JsonReader` is created to read the JSON string.
    - The reader begins reading an array.
    - An assertion is made to check that calling `nextDouble()` throws a `MalformedJsonException`.
    - The exception is checked to ensure it contains the correct error message indicating the location of the error.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictQuotedNonFiniteDoubles<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictQuotedNonFiniteDoubles}} -->
Tests that a strict JSON reader throws a MalformedJsonException when encountering a strictly quoted non-finite double.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string containing a quoted 'NaN' is defined.
    - A `JsonReader` is created to read the JSON string.
    - The reader begins reading an array.
    - An assertion is made to check that calling `nextDouble()` throws a `MalformedJsonException`.
    - The exception message is verified to ensure it indicates that NaN and infinities are forbidden in JSON.
- **Output**:
    - The method does not return a value; instead, it asserts that an exception is thrown with the expected message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientNonFiniteDoubles<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientNonFiniteDoubles}} -->
Tests the `JsonReader` for lenient parsing of non-finite double values.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A JSON string containing NaN, -Infinity, and Infinity is defined.
    - A `JsonReader` is created with the JSON string and its strictness is set to `LENIENT`.
    - The reader begins reading an array.
    - The first value is read and asserted to be NaN.
    - The second value is read and asserted to be Double.NEGATIVE_INFINITY.
    - The third value is read and asserted to be Double.POSITIVE_INFINITY.
    - The reader ends the array.
- **Output**:
    - The method does not return a value but asserts that the values read from the JSON are as expected.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientQuotedNonFiniteDoubles<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientQuotedNonFiniteDoubles}} -->
Tests the `JsonReader` for lenient parsing of quoted non-finite double values.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string containing quoted non-finite double values is defined.
    - A `JsonReader` instance is created with the JSON string and set to lenient mode.
    - The reader begins reading an array.
    - The first value is read and asserted to be NaN.
    - The second value is read and asserted to be negative infinity.
    - The third value is read and asserted to be positive infinity.
    - The reader ends the array.
- **Output**:
    - The method does not return a value but asserts that the values read from the JSON are as expected.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictNonFiniteDoublesWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictNonFiniteDoublesWithSkipValue}} -->
Tests that attempting to skip a non-finite double value in strict mode results in a MalformedJsonException.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a JSON string containing a non-finite double value (NaN).
    - Initializes a `JsonReader` with the JSON string and begins reading an array.
    - Attempts to skip the value using `reader.skipValue()` and expects a `MalformedJsonException` to be thrown.
    - Asserts that the exception message indicates the correct line, column, and path of the error.
- **Output**:
    - Throws a `MalformedJsonException` indicating that non-finite double values are not allowed in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLongs<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLongs}} -->
Tests the reading of various long values from a JSON array.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**:
    - `json`: A string representing a JSON array containing various long values.
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with the JSON string.
- **Control Flow**:
    - The method begins by creating a JSON string that represents an array of long values.
    - A `JsonReader` is instantiated with the JSON string and begins reading the array.
    - The method reads several long, int, and double values from the array and asserts their correctness using assertions.
    - It checks for exceptions when trying to read values that exceed the range of int.
    - Finally, it checks that the reader has reached the end of the document after reading all values.
- **Output**:
    - The method does not return a value but asserts that the values read from the JSON array match expected values and that exceptions are thrown for invalid reads.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNumberWithOctalPrefix<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNumberWithOctalPrefix}} -->
Tests the behavior of the `JsonReader` when encountering a number with an octal prefix.
- **Inputs**:
    - `number`: A string representing a number with an octal prefix, specifically '01'.
    - `expectedLocation`: A string indicating the expected error location in the JSON input.
- **Control Flow**:
    - The method begins by defining a string `number` with the value '01' and an `expectedLocation` string.
    - It then attempts to read the `number` using a `JsonReader` and expects a `MalformedJsonException` to be thrown.
    - For each method call on the `JsonReader` (peek, nextInt, nextLong, nextDouble, nextString), it asserts that a `MalformedJsonException` is thrown.
    - Each exception is checked against the `expectedLocation` to ensure the error message is accurate.
- **Output**:
    - The method does not return a value; instead, it asserts that specific exceptions are thrown for invalid JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testBooleans<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testBooleans}} -->
Tests the reading of boolean values from a JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array containing boolean values.
    - Begins reading the JSON array.
    - Reads the first boolean value and asserts it is true.
    - Reads the second boolean value and asserts it is false.
    - Ends the JSON array.
    - Asserts that the next token is the end of the document.
- **Output**:
    - No output is returned; assertions are made to validate the boolean values read from the JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPeekingUnquotedStringsPrefixedWithBooleans<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPeekingUnquotedStringsPrefixedWithBooleans}} -->
Tests the behavior of `JsonReader` when peeking unquoted strings prefixed with booleans.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an unquoted string prefixed by a boolean.
    - Sets the strictness of the reader to `LENIENT` to allow for non-standard JSON.
    - Begins reading an array from the JSON input.
    - Peeks the next token and asserts that it is of type `STRING`.
    - Attempts to read the next value as a boolean, which should throw an `IllegalStateException` due to the unexpected structure.
    - Asserts that the exception message indicates the expected and actual token types.
    - Reads the next string value and asserts that it matches the expected unquoted string.
    - Ends the array reading.
- **Output**:
    - The method does not return a value but asserts conditions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReaderTest.assertUnexpectedStructureError`](#JsonReaderTestassertUnexpectedStructureError)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testMalformedNumbers<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testMalformedNumbers}} -->
Tests various malformed number formats to ensure they are correctly identified as invalid.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Calls [`assertNotANumber`](#JsonReaderTestassertNotANumber) with various malformed number strings to validate that they are not recognized as valid numbers.
    - Each malformed number format is tested individually, including cases with leading zeros, invalid exponents, and trailing characters.
- **Output**:
    - No output is returned; instead, the method asserts that each malformed number format raises an exception.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.assertNotANumber`](#JsonReaderTestassertNotANumber)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.assertNotANumber<!-- {{#callable:com.google.gson.stream.JsonReaderTest.assertNotANumber}} -->
Asserts that a given string is not a valid number by checking its parsing behavior with a lenient and strict `JsonReader`.
- **Inputs**:
    - `s`: A string that is expected to be invalid as a number.
- **Control Flow**:
    - Creates a `JsonReader` instance with lenient parsing mode using the input string `s`.
    - Checks if the next token is a string and verifies that it matches the input string `s`.
    - Creates another `JsonReader` instance with strict parsing mode using the same input string `s`.
    - Attempts to read the next value as a double from the strict reader, expecting a `MalformedJsonException` to be thrown.
    - Asserts that the exception message starts with a specific error message indicating the need for lenient mode.
- **Output**:
    - No output is returned; instead, the method asserts conditions and may throw an exception if the assertions fail.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPeekingUnquotedStringsPrefixedWithIntegers<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPeekingUnquotedStringsPrefixedWithIntegers}} -->
Tests the behavior of `JsonReader` when peeking unquoted strings prefixed with integers.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an unquoted string prefixed with a number.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow for non-standard JSON formats.
    - Begins reading an array from the JSON input.
    - Peeks at the next token in the JSON input to verify it is a string.
    - Attempts to read the next value as an integer, which should throw a `NumberFormatException` due to the invalid format.
    - Reads the next value as a string, which should succeed and return the unquoted string.
- **Output**:
    - The method does not return a value but asserts that the peeked token is a string and that the next string read is equal to '12.34e5x'.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPeekLongMinValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPeekLongMinValue}} -->
Tests the `JsonReader`'s ability to correctly peek and read the minimum long value from a JSON array.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing the minimum long value in an array.
- **Control Flow**:
    - The method begins by creating a `JsonReader` instance with a JSON string that contains the minimum long value (-9223372036854775808) wrapped in an array.
    - It sets the strictness of the `JsonReader` to `LENIENT` to allow for more flexible parsing.
    - The method then calls `beginArray()` to start reading the JSON array.
    - It uses `peek()` to check the type of the next token, asserting that it is a `NUMBER` token.
    - Finally, it calls `nextLong()` to read the long value from the array and asserts that it equals the expected minimum long value.
- **Output**:
    - The method does not return a value but asserts that the peeked token is of type `NUMBER` and that the value read is equal to -9223372036854775808.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPeekLongMaxValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPeekLongMaxValue}} -->
Tests the `JsonReader`'s ability to correctly peek and read the maximum value of a long integer from a JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a JSON string containing the maximum long value.
    - Sets the strictness of the reader to `LENIENT` to allow for more flexible parsing.
    - Begins reading a JSON array.
    - Peeks at the next token to ensure it is a number.
    - Reads the next long value and asserts it equals the maximum long value.
- **Output**:
    - The method does not return a value but asserts that the peeked token is a number and that the next long read equals 9223372036854775807.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLongLargerThanMaxLongThatWrapsAround<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLongLargerThanMaxLongThatWrapsAround}} -->
Tests the behavior of `JsonReader` when attempting to read a long value that exceeds the maximum value for a long.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON array containing a long value that exceeds the maximum long value.
- **Control Flow**:
    - The method begins by creating a `JsonReader` instance with a JSON string that contains a long number larger than `Long.MAX_VALUE`.
    - The strictness of the `JsonReader` is set to `LENIENT` to allow for more flexible parsing.
    - The method then starts reading the JSON array using `beginArray()`.
    - It checks the type of the next token using `peek()` to ensure it is a number.
    - Finally, it asserts that calling `nextLong()` throws a `NumberFormatException` due to the overflow.
- **Output**:
    - The method does not return a value but asserts that a `NumberFormatException` is thrown when attempting to read a long value that exceeds the maximum limit.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLongLargerThanMinLongThatWrapsAround<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLongLargerThanMinLongThatWrapsAround}} -->
Tests the behavior of `JsonReader` when attempting to read a long value that exceeds the minimum long value and wraps around.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a long value that is less than the minimum long value.
    - Sets the strictness of the `JsonReader` to `LENIENT` mode.
    - Begins reading an array from the JSON input.
    - Peeks at the next token to ensure it is a number.
    - Attempts to read the next long value, expecting a `NumberFormatException` to be thrown.
- **Output**:
    - The method does not return a value; it asserts that a `NumberFormatException` is thrown when trying to read a long value that is out of range.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNegativeZero<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNegativeZero}} -->
Tests the parsing of negative zero in a JSON array.
- **Modifiers**: `public`, `void`, `throws`, `Exception`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string representing an array containing negative zero.
    - Sets the strictness of the `JsonReader` to `LEGACY_STRICT`.
    - Begins reading the JSON array.
    - Asserts that the next token is of type `NUMBER`.
    - Reads the next string from the JSON array and asserts that it equals '-0'.
- **Output**:
    - No output is returned; assertions are made to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPeekLargerThanLongMaxValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPeekLargerThanLongMaxValue}} -->
Tests the behavior of `JsonReader` when attempting to read a number larger than the maximum value for a long.
- **Modifiers**: `public`, `test`, `ignore`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a number larger than `Long.MAX_VALUE`.
    - Sets the strictness of the reader to `LENIENT` to allow for parsing of non-standard JSON.
    - Begins reading an array from the JSON input.
    - Peeks at the next token to ensure it is a number.
    - Attempts to read the next long value, which should throw a `NumberFormatException` due to the value exceeding the long range.
- **Output**:
    - No output is returned; instead, the method verifies that a `NumberFormatException` is thrown when trying to read a long value that exceeds the maximum limit.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPeekLargerThanLongMinValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPeekLargerThanLongMinValue}} -->
Tests the behavior of `JsonReader` when peeking a number larger than the minimum value of a long.
- **Modifiers**: `public`, `test`, `ignore`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is created with a JSON string containing a number smaller than the minimum long value.
    - The strictness of the reader is set to lenient mode.
    - The reader begins reading an array.
    - The method checks the token type at the current position using `peek()` and asserts it is a number.
    - An attempt is made to read the number as a long using `nextLong()`, which is expected to throw a `NumberFormatException`.
    - The method then reads the number as a double using `nextDouble()` and asserts it equals the expected double value.
- **Output**:
    - The method does not return a value but asserts conditions and may throw exceptions based on the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testHighPrecisionLong<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testHighPrecisionLong}} -->
Tests the ability of `JsonReader` to correctly parse a high precision long value from a JSON array.
- **Modifiers**: `public`, `@Test`, `@Ignore`
- **Inputs**:
    - `json`: A JSON string representing an array containing a high precision long value.
- **Control Flow**:
    - Creates a `JsonReader` instance from the JSON string.
    - Begins reading the JSON array.
    - Reads the next long value from the array.
    - Asserts that the read long value equals the expected high precision long value.
    - Ends the JSON array.
- **Output**:
    - No output is returned; the method asserts that the parsed long value matches the expected value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPeekMuchLargerThanLongMinValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPeekMuchLargerThanLongMinValue}} -->
Tests the behavior of `JsonReader` when peeking a number larger than the minimum value of a long.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): An instance of `JsonReader` initialized with a JSON array containing a number that exceeds the minimum value of a long.
- **Control Flow**:
    - Suppresses warnings for floating point literal precision.
    - Initializes a double variable `d` with the value -92233720368547758080d.
    - Creates a `JsonReader` instance with a JSON array containing the number -92233720368547758080.
    - Sets the strictness of the reader to `LENIENT`.
    - Begins reading the array.
    - Asserts that the next token is of type `NUMBER` using `peek()`.
    - Asserts that calling `nextLong()` throws a `NumberFormatException` due to the number being too large.
    - Asserts that calling `nextDouble()` returns the expected double value `d`.
- **Output**:
    - The method does not return a value but performs assertions to validate the behavior of the `JsonReader` when handling a number larger than the minimum long value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextLong)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testQuotedNumberWithEscape<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testQuotedNumberWithEscape}} -->
Tests the parsing of a quoted number with an escape sequence in a JSON array.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a quoted number with an escape sequence.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow for flexible parsing.
    - Begins reading the JSON array.
    - Checks the type of the next token to ensure it is a string.
    - Reads the next integer from the JSON, which is expected to be the parsed value of the quoted number.
- **Output**:
    - The method does not return a value but asserts that the parsed integer equals 1234.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testMixedCaseLiterals<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testMixedCaseLiterals}} -->
Tests the `JsonReader` class's ability to handle mixed case boolean and null literals.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array containing mixed case literals.
    - Begins reading the JSON array.
    - Asserts that the first two literals are interpreted as `true`.
    - Asserts that the next two literals are interpreted as `false`.
    - Reads two null values from the array.
    - Ends the JSON array.
    - Asserts that the reader has reached the end of the document.
- **Output**:
    - No output is returned; the method performs assertions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testMissingValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testMissingValue}} -->
Tests the behavior of `JsonReader` when encountering a missing value in JSON.
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string that has a missing value.
    - Begins reading the JSON object.
    - Asserts that the next name in the object is 'a'.
    - Attempts to read the next string value, which is expected to fail due to the missing value.
    - Catches the `MalformedJsonException` and asserts that the exception message matches the expected error message.
- **Output**:
    - Throws a `MalformedJsonException` indicating that a value was expected at a specific location in the JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPrematureEndOfInput<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPrematureEndOfInput}} -->
Tests the behavior of `JsonReader` when encountering a premature end of input.
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string that ends prematurely.
    - Begins reading a JSON object using `beginObject()`.
    - Reads the next name in the object, expecting it to be 'a'.
    - Reads the next boolean value, expecting it to be true.
    - Attempts to read another name, which should throw an `EOFException` due to the premature end of input.
- **Output**:
    - The method does not return a value; instead, it asserts that an `EOFException` is thrown when trying to read past the end of the input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testPrematurelyClosed<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testPrematurelyClosed}} -->
Tests the behavior of `JsonReader` when attempting to read from a closed reader.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string and begins reading an object.
    - Closes the reader and asserts that an `IllegalStateException` is thrown when trying to read the next name.
    - Creates another `JsonReader`, closes it, and asserts that an `IllegalStateException` is thrown when trying to begin reading an object.
    - Creates a third `JsonReader`, begins reading an object, reads a name, peeks the next token, closes the reader, and asserts that an `IllegalStateException` is thrown when trying to read a boolean.
- **Output**:
    - The method does not return a value but asserts that specific exceptions are thrown when attempting to read from a closed `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNextFailuresDoNotAdvance<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNextFailuresDoNotAdvance}} -->
Tests that calling `next` methods on a `JsonReader` does not advance the reader's position when an `IllegalStateException` is thrown.
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is initialized with a JSON object containing a single boolean field.
    - The method begins by attempting to read a string value, which is expected to fail, and asserts that an `IllegalStateException` is thrown.
    - The next name is read successfully, which is 'a'.
    - Subsequent attempts to read a name, begin an array, end an array, begin an object, and end an object are made, each expected to throw an `IllegalStateException` due to the current state of the reader.
    - After reading the boolean value successfully, further attempts to read a string, name, begin an array, and end an array are made, all expected to throw an `IllegalStateException`.
    - Finally, the object is ended, and the method checks that the reader's peek returns `END_DOCUMENT` before closing the reader.
- **Output**:
    - The method does not return a value but asserts that the expected exceptions are thrown and verifies the final state of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReaderTest.assertUnexpectedStructureError`](#JsonReaderTestassertUnexpectedStructureError)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testIntegerMismatchFailuresDoNotAdvance<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testIntegerMismatchFailuresDoNotAdvance}} -->
Tests that a `NumberFormatException` is thrown when attempting to read an integer from a JSON array containing a floating-point number.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array containing a floating-point number (1.5).
    - Begins reading the array using `reader.beginArray()`.
    - Asserts that calling `reader.nextInt()` throws a `NumberFormatException` due to the mismatch.
    - Reads the next value as a double using `reader.nextDouble()` and asserts it equals 1.5.
    - Ends the array with `reader.endArray()`.
- **Output**:
    - No output is returned; the method verifies the behavior of the `JsonReader` when encountering a type mismatch.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStringNullIsNotNull<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStringNullIsNotNull}} -->
Tests that calling `nextNull()` on a JSON string containing 'null' throws an `IllegalStateException`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string that contains a single element array with the string 'null'.
    - Begins reading the array using `beginArray()`.
    - Attempts to read the next value as null using `nextNull()`, which is expected to throw an `IllegalStateException`.
    - Catches the exception and verifies that it is indeed an `IllegalStateException`.
- **Output**:
    - An `IllegalStateException` is thrown when trying to read 'null' as a null value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReaderTest.assertUnexpectedStructureError`](#JsonReaderTestassertUnexpectedStructureError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNullLiteralIsNotAString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNullLiteralIsNotAString}} -->
Tests that a null literal is not treated as a string in JSON.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array containing a null literal.
    - Begins reading the array using `reader.beginArray()`.
    - Attempts to read the next value as a string using `reader.nextString()`, which is expected to throw an `IllegalStateException`.
    - Catches the exception and verifies that it matches the expected structure error using `assertUnexpectedStructureError()`.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown when trying to read a null literal as a string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReaderTest.assertUnexpectedStructureError`](#JsonReaderTestassertUnexpectedStructureError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictNameValueSeparator<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictNameValueSeparator}} -->
Tests the behavior of `JsonReader` when encountering strict name-value separators in JSON.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string using '=' as a separator.
    - Begins reading the JSON object and asserts the first name is 'a'.
    - Attempts to read the next value as a boolean, expecting a `MalformedJsonException` to be thrown.
    - Asserts the error message for the first malformed JSON.
    - Creates a second `JsonReader` instance with a different malformed JSON string using '=>' as a separator.
    - Begins reading the second JSON object and asserts the first name is 'a'.
    - Attempts to read the next value as a boolean, expecting a `MalformedJsonException` to be thrown.
    - Asserts the error message for the second malformed JSON.
- **Output**:
    - Both attempts to read a boolean value after the name 'a' should throw a `MalformedJsonException` due to incorrect name-value separators.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientNameValueSeparator<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientNameValueSeparator}} -->
Tests the `JsonReader`'s ability to parse name-value pairs with lenient separators.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a name-value pair using '=' as the separator.
    - Sets the strictness of the reader to `Strictness.LENIENT`.
    - Begins reading the JSON object and asserts that the next name is 'a' and the next boolean value is true.
    - Repeats the above steps with a different JSON string using '=>' as the separator.
- **Output**:
    - No output is returned; assertions are made to verify the correctness of the parsed values.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictNameValueSeparatorWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictNameValueSeparatorWithSkipValue}} -->
Tests the behavior of the `JsonReader` when encountering strict name-value separators with the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string using '=' as a separator.
    - Begins reading the JSON object and asserts the first name is 'a'.
    - Attempts to skip the value associated with 'a', expecting a `MalformedJsonException` to be thrown.
    - Asserts that the exception message indicates the error location.
    - Repeats the process with another malformed JSON string using '=>' as a separator.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown for both malformed JSON strings.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testCommentsInStringValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testCommentsInStringValue}} -->
Tests the handling of comments within string values in JSON.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with various JSON strings containing comments.
- **Control Flow**:
    - The method initializes a `JsonReader` with a JSON array containing a string with a comment and verifies the output.
    - It then initializes another `JsonReader` with a JSON object containing a key-value pair where the value is a string with a comment, and checks the key and value.
    - Finally, it initializes a `JsonReader` with a JSON object where the key itself contains a comment and checks both the key and the associated value.
- **Output**:
    - The method does not return a value but asserts that the strings read from the JSON match the expected values, confirming that comments are correctly handled.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictComments<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictComments}} -->
Tests the behavior of the `JsonReader` when encountering strict comments in JSON.
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array containing a comment and a boolean value.
    - Begins reading the array and expects a `MalformedJsonException` when trying to read the boolean value.
    - Asserts that the exception message indicates the location of the error.
    - Repeats the process for different comment styles (single-line and multi-line comments).
- **Output**:
    - Throws a `MalformedJsonException` when strict comments are encountered in the JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientComments<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientComments}} -->
Tests the `JsonReader` class's ability to handle comments in JSON input when in lenient mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a single boolean value preceded by a single-line comment.
    - Sets the strictness of the reader to `Strictness.LENIENT`.
    - Begins reading an array and asserts that the next boolean value is `true`.
    - Repeats the above steps for JSON strings with different comment styles: hash (`#`), and block (`/* ... */`).
- **Output**:
    - The method does not return a value but asserts that the `JsonReader` correctly parses boolean values from JSON strings with comments.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictCommentsWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictCommentsWithSkipValue}} -->
Tests the behavior of `JsonReader` when encountering strict comments with the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON array containing comments.
    - `reader2`: A second `JsonReader` instance initialized with a JSON array containing a different comment.
    - `reader3`: A third `JsonReader` instance initialized with a JSON array containing a C-style comment.
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array that includes a single-line comment and begins reading the array.
    - Asserts that calling `skipValue()` throws a `MalformedJsonException` and checks the error message for the expected location.
    - Repeats the process for a JSON array with a hash comment and checks for the same exception.
    - Repeats the process for a JSON array with a C-style comment and checks for the same exception.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown for each case, indicating that comments are not allowed in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictUnquotedNames<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictUnquotedNames}} -->
Tests that strict mode fails to parse unquoted names in JSON.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an unquoted name.
    - Begins reading the JSON object.
    - Asserts that calling `nextName()` throws a `MalformedJsonException`.
    - Verifies that the exception message indicates the error location.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientUnquotedNames<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientUnquotedNames}} -->
Tests the `JsonReader`'s ability to read unquoted names in a JSON object when in lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a JSON string containing an unquoted name.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow unquoted names.
    - Begins reading the JSON object.
    - Reads the next name from the JSON object and asserts that it equals 'a'.
- **Output**:
    - No output is returned; the method asserts that the next name read is 'a'.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictUnquotedNamesWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictUnquotedNamesWithSkipValue}} -->
Tests that a `MalformedJsonException` is thrown when attempting to skip a value with strict unquoted names.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an unquoted name.
    - Begins reading the JSON object.
    - Asserts that a `MalformedJsonException` is thrown when calling `skipValue()`.
    - Verifies that the exception message indicates the error location.
- **Output**:
    - The method does not return a value but asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSingleQuotedNames<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedNames}} -->
Tests that a JSON object with single-quoted names throws a MalformedJsonException in strict mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing single-quoted names.
    - Begins reading the JSON object using `reader.beginObject()`.
    - Asserts that calling `reader.nextName()` throws a `MalformedJsonException`.
    - Validates that the exception message indicates the error location in the JSON string.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientSingleQuotedNames<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientSingleQuotedNames}} -->
Tests the `JsonReader`'s ability to read single-quoted names in a lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a JSON string containing a single-quoted name.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow single-quoted names.
    - Begins reading the JSON object.
    - Reads the next name from the JSON object and asserts that it equals 'a'.
- **Output**:
    - No output is returned; the method asserts that the next name read is 'a', which will throw an assertion error if the condition is not met.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSingleQuotedNamesWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedNamesWithSkipValue}} -->
This method tests the behavior of the `JsonReader` when encountering single-quoted names in strict mode.
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string containing a single-quoted name.
    - The method begins reading the JSON object using `reader.beginObject()`.
    - It attempts to skip the value associated with the single-quoted name using `reader.skipValue()`.
    - An exception of type `MalformedJsonException` is expected to be thrown due to the strict parsing rules.
    - The exception is caught and verified to contain the correct error message indicating the location of the error.
- **Output**:
    - The method does not return a value; instead, it asserts that a `MalformedJsonException` is thrown with the expected error message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictUnquotedStrings<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictUnquotedStrings}} -->
Tests that strict mode fails to parse unquoted strings.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an unquoted string.
    - Begins reading an array from the JSON input.
    - Asserts that calling `nextString()` throws a `MalformedJsonException` due to the unquoted string.
    - Validates that the error message indicates the correct line and column of the error.
- **Output**:
    - Throws a `MalformedJsonException` indicating that unquoted strings are not allowed in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictUnquotedStringsWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictUnquotedStringsWithSkipValue}} -->
Tests that skipping a value in strict mode raises a MalformedJsonException for unquoted strings.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON array containing an unquoted string.
    - Begins reading the array using `reader.beginArray()`.
    - Attempts to skip the value at the current position using `reader.skipValue()`.
    - Asserts that a `MalformedJsonException` is thrown due to the unquoted string.
    - Validates that the exception message indicates the correct line and column of the error.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientUnquotedStrings<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientUnquotedStrings}} -->
Tests the `JsonReader`'s ability to read unquoted strings in lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a JSON string containing an unquoted string '[a]'.
    - Sets the strictness of the `JsonReader` to `Strictness.LENIENT` to allow unquoted strings.
    - Begins reading an array from the JSON input.
    - Reads the next string from the array and asserts that it equals 'a'.
- **Output**:
    - No output is returned; the method asserts that the read string matches the expected value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSingleQuotedStrings<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedStrings}} -->
Tests that a strict JSON reader throws a `MalformedJsonException` when encountering single-quoted strings.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a single-quoted string.
    - Begins reading an array from the JSON input.
    - Asserts that calling `nextString()` on the reader throws a `MalformedJsonException`.
    - Verifies that the exception message indicates the correct line and column of the error.
- **Output**:
    - Throws a `MalformedJsonException` indicating that single-quoted strings are not allowed in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientSingleQuotedStrings<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientSingleQuotedStrings}} -->
Tests the `JsonReader`'s ability to read single-quoted strings in lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a JSON string containing a single-quoted string.
    - Sets the strictness of the `JsonReader` to `LENIENT`.
    - Begins reading an array from the JSON input.
    - Reads the next string from the array and asserts that it equals 'a'.
- **Output**:
    - No output is returned; the method asserts that the read string matches the expected value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSingleQuotedStringsWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSingleQuotedStringsWithSkipValue}} -->
Tests that skipping a single-quoted string in strict mode throws a MalformedJsonException.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a single-quoted string input.
    - Begins reading an array from the `JsonReader`.
    - Asserts that calling `skipValue()` throws a `MalformedJsonException`.
    - Validates that the exception message indicates the correct line and column of the error.
- **Output**:
    - Throws a `MalformedJsonException` indicating the error in parsing the single-quoted string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSemicolonDelimitedArray<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedArray}} -->
Tests that a semicolon-delimited array in strict mode throws a MalformedJsonException.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a semicolon-delimited array string '[true;true]'.
    - Begins reading the array using `reader.beginArray()`.
    - Asserts that calling `reader.nextBoolean()` throws a `MalformedJsonException` due to the invalid delimiter.
    - Verifies that the exception message indicates the error location in the JSON input.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientSemicolonDelimitedArray<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientSemicolonDelimitedArray}} -->
Tests the `JsonReader`'s ability to parse a semicolon-delimited array in lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a semicolon-delimited JSON array string '[true;true]'.
    - Sets the strictness of the `JsonReader` to `Strictness.LENIENT` to allow for non-standard JSON formats.
    - Begins reading the array with `beginArray()`.
    - Reads the first boolean value using `nextBoolean()` and asserts it is true.
    - Reads the second boolean value using `nextBoolean()` and asserts it is true.
- **Output**:
    - The method does not return a value but asserts that two boolean values read from the JSON array are both true.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSemicolonDelimitedArrayWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedArrayWithSkipValue}} -->
Tests that a strict semicolon-delimited array throws a MalformedJsonException.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a semicolon-delimited array input.
    - Begins reading the array using `reader.beginArray()`.
    - Asserts that calling `reader.skipValue()` throws a `MalformedJsonException`.
    - Verifies that the exception message indicates the error location in the JSON input.
- **Output**:
    - Throws a `MalformedJsonException` indicating the error in the JSON structure.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSemicolonDelimitedNameValuePair<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedNameValuePair}} -->
Tests that a semicolon-delimited name-value pair in JSON throws a MalformedJsonException in strict mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string containing a semicolon instead of a comma.
    - Begins reading the JSON object.
    - Asserts that the first name read is 'a'.
    - Attempts to read the boolean value associated with 'a', expecting a `MalformedJsonException` to be thrown.
    - Asserts that the exception message indicates the error location.
- **Output**:
    - Throws a `MalformedJsonException` indicating the error in the JSON structure.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientSemicolonDelimitedNameValuePair<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientSemicolonDelimitedNameValuePair}} -->
Tests the `JsonReader`'s ability to parse a semicolon-delimited name-value pair in lenient mode.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing semicolon-delimited name-value pairs.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow parsing of non-standard JSON.
    - Begins reading the JSON object.
    - Reads the first name and asserts it equals 'a'.
    - Reads the corresponding boolean value and asserts it is true.
    - Reads the next name and asserts it equals 'b'.
- **Output**:
    - The method does not return a value but asserts that the parsed names and values are as expected.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictSemicolonDelimitedNameValuePairWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictSemicolonDelimitedNameValuePairWithSkipValue}} -->
Tests the behavior of `JsonReader` when encountering a semicolon-delimited name-value pair in strict mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string that uses semicolons instead of commas.
    - Begins reading the JSON object.
    - Asserts that the first name read is 'a'.
    - Attempts to skip the value associated with 'a', expecting a `MalformedJsonException` to be thrown.
    - Asserts that the exception message indicates the error location in the JSON.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown with the expected error message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictUnnecessaryArraySeparators<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictUnnecessaryArraySeparators}} -->
Tests the strict parsing behavior of unnecessary array separators in JSON.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing unnecessary array separators.
- **Control Flow**:
    - Creates multiple `JsonReader` instances with different JSON strings that include unnecessary array separators.
    - Begins reading the array for each `JsonReader` instance.
    - Asserts that the first boolean value is read correctly.
    - Attempts to read a null value using `nextNull()` and expects a `MalformedJsonException` to be thrown.
    - Asserts that the exception message contains the correct line and column information for the error.
- **Output**:
    - The method does not return a value but asserts that specific exceptions are thrown when attempting to read null values from improperly formatted JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientUnnecessaryArraySeparators<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientUnnecessaryArraySeparators}} -->
Tests the behavior of the `JsonReader` when parsing JSON arrays with unnecessary separators in lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing unnecessary array separators.
    - Sets the strictness of the reader to `LENIENT` to allow parsing of malformed JSON.
    - Begins reading the array and processes each element, including handling redundant separators as null values.
    - Asserts that the expected boolean values are read correctly from the array.
    - Repeats the process for different JSON strings with various configurations of unnecessary separators.
- **Output**:
    - The method does not return a value but asserts that the `JsonReader` correctly interprets the JSON input according to the lenient parsing rules.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictUnnecessaryArraySeparatorsWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictUnnecessaryArraySeparatorsWithSkipValue}} -->
Tests the behavior of `JsonReader` when encountering unnecessary array separators in strict mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates multiple instances of `JsonReader` with different JSON strings containing unnecessary array separators.
    - For each `JsonReader`, it begins reading the array and checks the first boolean value.
    - It then attempts to skip the next value, expecting a `MalformedJsonException` to be thrown due to the strict parsing rules.
    - The expected error messages are asserted to ensure they match the expected format.
- **Output**:
    - The method does not return a value but asserts that specific exceptions are thrown with the correct messages.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictMultipleTopLevelValues<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictMultipleTopLevelValues}} -->
Tests that a `JsonReader` throws a `MalformedJsonException` when multiple top-level values are present.
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is created with a string containing two empty JSON arrays separated by a space.
    - The `beginArray()` method is called to start reading the first array.
    - The `endArray()` method is called to close the first array.
    - The `peek()` method is called, which is expected to throw a `MalformedJsonException` due to the presence of the second array.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown with a specific error message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientMultipleTopLevelValues<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientMultipleTopLevelValues}} -->
Tests the behavior of `JsonReader` when parsing multiple top-level values in lenient mode.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an empty array, a boolean true, and an empty object.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow parsing of multiple top-level values.
    - Begins reading an array and immediately ends it, confirming it is empty.
    - Reads the next boolean value, which is expected to be true.
    - Begins reading an object and immediately ends it, confirming it is empty.
    - Checks that the next token is `END_DOCUMENT`, indicating the end of the input.
- **Output**:
    - The method does not return a value but asserts that the boolean read is true and that the end of the document is reached.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictMultipleTopLevelValuesWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictMultipleTopLevelValuesWithSkipValue}} -->
Tests that a `MalformedJsonException` is thrown when attempting to skip a value in a strict JSON reader with multiple top-level values.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is initialized with a JSON string containing two empty arrays.
    - The reader begins and ends an array, effectively parsing the first empty array.
    - An assertion is made to check that a `MalformedJsonException` is thrown when calling `skipValue()` on the reader.
    - The exception is validated to ensure it contains the expected error message indicating the location of the error.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown with the expected message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testTopLevelValueTypes<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testTopLevelValueTypes}} -->
Tests the `JsonReader` class for reading various top-level value types from JSON.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates multiple instances of `JsonReader` for different JSON value types: boolean, null, integer, double, and string.
    - For each `JsonReader`, it reads the value using the appropriate method ([`nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean), [`nextNull`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull), [`nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt), [`nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble), [`nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)) and asserts the expected output.
    - After reading each value, it checks the next token using `peek()` to ensure it is `END_DOCUMENT` after the value has been read.
- **Output**:
    - The method does not return a value but asserts that the values read from the JSON match the expected values and that the end of the document is reached.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testTopLevelValueTypeWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testTopLevelValueTypeWithSkipValue}} -->
Tests the behavior of `JsonReader` when skipping a top-level value.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string representing a boolean value ("true").
- **Control Flow**:
    - Creates a new `JsonReader` instance with the input JSON string.
    - Calls the `skipValue()` method on the `JsonReader` instance to skip the current value.
    - Asserts that the next token to be read is `END_DOCUMENT`, indicating that the end of the input has been reached.
- **Output**:
    - The method does not return a value but asserts that the next token is `END_DOCUMENT`, confirming that the value was successfully skipped.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictNonExecutePrefix<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictNonExecutePrefix}} -->
Tests that a malformed JSON input with a strict non-execute prefix throws a MalformedJsonException.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a malformed JSON string that includes a non-execute prefix.
    - Asserts that invoking `beginArray()` on the reader throws a `MalformedJsonException`.
    - Calls [`assertStrictError`](#JsonReaderTestassertStrictError) to verify the exception message and location.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictNonExecutePrefixWithSkipValue<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictNonExecutePrefixWithSkipValue}} -->
Tests that a `MalformedJsonException` is thrown when attempting to skip a value in strict mode with a non-executable prefix.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing a non-executable prefix followed by an empty array.
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string that has a non-executable prefix.
    - Calls `reader.skipValue()` within an assertion to check for exceptions.
    - Asserts that a `MalformedJsonException` is thrown with the expected error message.
- **Output**:
    - Throws a `MalformedJsonException` indicating that the JSON is malformed due to the non-executable prefix.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientNonExecutePrefix<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientNonExecutePrefix}} -->
This method tests the behavior of the `JsonReader` when parsing a JSON array with a lenient non-execute prefix.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string that includes a non-execute prefix followed by an empty array.
    - The strictness of the `JsonReader` is set to `Strictness.LENIENT` to allow for lenient parsing.
    - The method begins reading the JSON array using `beginArray()`.
    - The method ends the array with `endArray()`.
    - Finally, it asserts that the next token is `END_DOCUMENT`, indicating that the reader has reached the end of the input.
- **Output**:
    - The method does not return a value but asserts that the `JsonReader` correctly identifies the end of the document after parsing the input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientNonExecutePrefixWithLeadingWhitespace<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientNonExecutePrefixWithLeadingWhitespace}} -->
This method tests the behavior of the `JsonReader` when parsing a JSON array with leading whitespace in lenient mode.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string containing leading whitespace followed by a non-executable prefix and an empty array.
    - The strictness of the `JsonReader` is set to `Strictness.LENIENT` to allow for lenient parsing.
    - The method begins reading the JSON array using `beginArray()`.
    - The method ends the array with `endArray()`.
    - Finally, it asserts that the next token is `END_DOCUMENT` to confirm that the entire input has been consumed correctly.
- **Output**:
    - The method does not return a value but asserts that the `JsonReader` correctly identifies the end of the document after parsing the input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientPartialNonExecutePrefix<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientPartialNonExecutePrefix}} -->
Tests the behavior of `JsonReader` when parsing a lenient JSON string with a non-executable prefix.
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing a non-executable prefix.
- **Control Flow**:
    - Sets the strictness of the `JsonReader` to `LENIENT`.
    - Reads the first string from the JSON input, expecting it to be a valid string.
    - Asserts that the first string read is equal to the expected value ")".
    - Attempts to read the next string, which is expected to fail due to malformed JSON.
    - Catches the `MalformedJsonException` and asserts that the exception message matches the expected error message.
- **Output**:
    - The method does not return a value but asserts that the first string read is ")" and that a `MalformedJsonException` is thrown on the second read attempt.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testBomIgnoredAsFirstCharacterOfDocument<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testBomIgnoredAsFirstCharacterOfDocument}} -->
Tests that a Byte Order Mark (BOM) is ignored when it appears as the first character of a JSON document.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `JsonReader` instance with a JSON string containing a BOM followed by an empty array.
    - Begins reading an array using `reader.beginArray()`.
    - Ends the array reading with `reader.endArray()`.
- **Output**:
    - The method does not return any value but verifies that the JSON reader can successfully parse an empty array even when preceded by a BOM.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testBomForbiddenAsOtherCharacterInDocument<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testBomForbiddenAsOtherCharacterInDocument}} -->
Tests that a BOM (Byte Order Mark) character is not allowed as a non-leading character in a JSON document.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a BOM character.
    - Begins reading an array using `reader.beginArray()`.
    - Asserts that an exception of type `MalformedJsonException` is thrown when attempting to end the array with `reader.endArray()`.
    - Validates that the exception message indicates the position of the error in the JSON input.
- **Output**:
    - The method does not return a value; it asserts that a `MalformedJsonException` is thrown due to the presence of a BOM character in an invalid position.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPosition<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPosition}} -->
This method tests the failure of JSON parsing with a specific error message and JSON input.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**:
    - `message`: A string that describes the expected error message when parsing the JSON.
    - `json`: A string containing the malformed JSON input that is expected to trigger the error.
- **Control Flow**:
    - Calls the [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method with a specific error message and malformed JSON string.
    - The [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method is expected to throw a `MalformedJsonException` when parsing the provided JSON.
- **Output**:
    - The method does not return a value but is expected to throw an exception if the JSON parsing fails as intended.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionGreaterThanBufferSize<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionGreaterThanBufferSize}} -->
Tests the failure of JSON parsing when the position exceeds the buffer size.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a string of 8192 spaces.
    - Calls the method [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) with a specific error message and a JSON string that includes the spaces.
- **Output**:
    - The method does not return a value but is expected to throw an IOException if the JSON parsing fails.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionOverSlashSlashEndOfLineComment<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionOverSlashSlashEndOfLineComment}} -->
This method tests the failure of JSON parsing when encountering a specific malformed JSON input with comments.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**:
    - `expectedMessage`: A string representing the expected error message when parsing fails.
    - `json`: A string containing the malformed JSON input to be tested.
- **Control Flow**:
    - Calls the [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method with the specified expected error message and malformed JSON input.
    - The [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method is expected to throw an exception if the JSON parsing fails as anticipated.
- **Output**:
    - The method does not return a value but asserts that an exception is thrown with the expected message when parsing the provided malformed JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionOverHashEndOfLineComment<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionOverHashEndOfLineComment}} -->
This method tests the failure of JSON parsing when encountering a hash end-of-line comment.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `expectedMessage`: A string representing the expected error message when parsing fails.
    - `json`: A string containing the JSON input that is expected to cause a parsing failure.
- **Control Flow**:
    - Calls the [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method with the specified expected error message and JSON input.
    - The [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method is expected to throw an exception when parsing the provided JSON.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown with the expected message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionOverCStyleComment<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionOverCStyleComment}} -->
This method tests the failure of JSON parsing when encountering a C-style comment in the input.
- **Modifiers**: `public`, `void`, `throws`
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Calls the [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method with a specific error message and a JSON string containing a C-style comment.
    - The [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method is expected to throw an exception indicating the position of the error in the JSON string.
- **Output**:
    - This method does not return a value but is expected to throw an exception if the JSON parsing fails.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionOverQuotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionOverQuotedString}} -->
This method tests the failure of JSON parsing when a quoted string is improperly formatted.
- **Inputs**:
    - `message`: A string that describes the expected error message when parsing fails.
    - `json`: A JSON string that is expected to cause a parsing error due to improper formatting.
- **Control Flow**:
    - The method calls [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) with a specific error message and a JSON string that contains a quoted string.
    - The JSON string is designed to trigger a parsing error, which is then validated against the expected error message.
- **Output**:
    - The method does not return a value but asserts that the expected error message is thrown during the parsing of the provided JSON string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionOverUnquotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionOverUnquotedString}} -->
This method tests the failure of parsing a JSON string with an unquoted string.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `Expected value at line 5 column 2 path $[1]`: A string that describes the expected error message when parsing fails.
    - `[

abcd

,}`: A JSON string that is malformed due to an unquoted string.
- **Control Flow**:
    - The method calls [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) with a specific error message and a malformed JSON string.
    - The [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method is expected to throw an exception when it encounters the malformed JSON.
- **Output**:
    - The method does not return a value but is expected to throw an exception indicating the failure to parse the JSON string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithEscapedNewlineCharacter<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithEscapedNewlineCharacter}} -->
This method tests the failure of JSON parsing when an escaped newline character is present.
- **Inputs**:
    - `message`: A string that specifies the expected error message when parsing fails.
    - `json`: A string representing the JSON input that contains an escaped newline character.
- **Control Flow**:
    - Calls the [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method with the expected error message and the JSON string.
    - The [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method is expected to throw an exception when parsing the provided JSON.
- **Output**:
    - The method does not return a value but asserts that an exception is thrown with the expected message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionIsOffsetByBom<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionIsOffsetByBom}} -->
This method tests the failure of JSON parsing when the position is offset by a Byte Order Mark (BOM).
- **Inputs**:
    - `message`: A string that describes the expected error message when parsing fails.
    - `json`: A string representing the JSON input that is expected to cause a parsing error.
- **Control Flow**:
    - Calls the [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method with a specific error message and a JSON string containing a BOM character.
    - The [`testFailWithPosition`](#JsonReaderTesttestFailWithPosition) method is expected to throw a `MalformedJsonException` due to the malformed JSON structure.
- **Output**:
    - The method does not return a value but asserts that a specific exception is thrown when parsing the provided JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.testFailWithPosition`](#JsonReaderTesttestFailWithPosition)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPosition<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPosition}} -->
Tests the behavior of `JsonReader` when encountering malformed JSON, ensuring that appropriate exceptions are thrown with correct messages.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `message`: A string that describes the expected error message when a malformed JSON is encountered.
    - `json`: A string representing the JSON input that is expected to be malformed.
- **Control Flow**:
    - Creates a `JsonReader` instance with the provided `json` string and sets its strictness to `LENIENT`.
    - Begins reading an array from the `JsonReader` and attempts to read the first string value.
    - Asserts that a `MalformedJsonException` is thrown when calling `peek()` on the reader after reading the first string.
    - Validates that the exception message matches the expected `message` with additional troubleshooting information.
    - Creates a second `JsonReader` instance with the same `json` string and sets its strictness to `LENIENT`.
    - Begins reading an array from the second `JsonReader` and skips the first value.
    - Asserts that a `MalformedJsonException` is thrown when calling `peek()` on the second reader after skipping the value.
    - Validates that the exception message matches the expected `message` with additional troubleshooting information.
- **Output**:
    - No return value; the method is void and is used for testing purposes, primarily to ensure that exceptions are thrown as expected.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testFailWithPositionDeepPath<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testFailWithPositionDeepPath}} -->
Tests the behavior of `JsonReader` when encountering malformed JSON at a deep path.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string.
    - Begins reading an array from the JSON input.
    - Reads an integer from the array.
    - Begins reading an object from the JSON input.
    - Reads the name of the first property in the object.
    - Begins reading an array from the property.
    - Attempts to read two integers from the array.
    - Asserts that a `MalformedJsonException` is thrown when peeking at the next value.
    - Verifies that the exception message contains the expected error details.
- **Output**:
    - Throws a `MalformedJsonException` indicating the expected value at a specific line and column in the JSON input.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictVeryLongNumber<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictVeryLongNumber}} -->
Tests that a very long number in strict mode results in a MalformedJsonException.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a very long number.
    - Begins reading an array from the `JsonReader`.
    - Asserts that calling `nextDouble()` throws a `MalformedJsonException` due to the long number.
    - Verifies that the exception message indicates the correct line and column of the error.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonReaderTest.assertStrictError`](#JsonReaderTestassertStrictError)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientVeryLongNumber<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientVeryLongNumber}} -->
Tests the `JsonReader`'s ability to parse a very long number in lenient mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a very long number.
    - Sets the strictness of the `JsonReader` to `LENIENT`.
    - Begins reading an array from the JSON input.
    - Checks the type of the next token, expecting it to be a `STRING`.
    - Reads the next double value, expecting it to be equal to 1.0.
    - Ends the array reading.
    - Checks that the next token is `END_DOCUMENT`.
- **Output**:
    - No output is returned; assertions are made to verify the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextDouble)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testVeryLongUnquotedLiteral<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testVeryLongUnquotedLiteral}} -->
Tests the parsing of a very long unquoted literal in a JSON array.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A string `literal` is constructed by concatenating 'a', a repeated character 'b' 8192 times, and 'c'.
    - A `JsonReader` instance is created with a JSON array containing the `literal`.
    - The strictness of the `JsonReader` is set to `LENIENT` to allow for unquoted strings.
    - The reader begins reading the array.
    - The method asserts that the next string read from the JSON matches the `literal`.
    - The reader ends the array.
- **Output**:
    - The method does not return a value but asserts that the parsed string matches the expected long unquoted literal.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testDeeplyNestedArrays<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testDeeplyNestedArrays}} -->
Tests the behavior of `JsonReader` when processing deeply nested JSON arrays.
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string that contains 40 levels of nested arrays.
    - Begins reading 40 nested arrays using a loop that calls `beginArray()` 40 times.
    - Asserts that the path of the reader matches the expected path after processing the nested arrays.
    - Ends the 40 nested arrays using a loop that calls `endArray()` 40 times.
    - Asserts that the next token is `END_DOCUMENT` to confirm the end of the JSON input.
- **Output**:
    - The method does not return a value but asserts the correctness of the path and the end of the document state.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testDeeplyNestedObjects<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testDeeplyNestedObjects}} -->
Tests the ability of `JsonReader` to handle deeply nested JSON objects.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A JSON string is constructed to represent a deeply nested object structure, 40 levels deep.
    - A `JsonReader` is created to read the constructed JSON string.
    - The method enters a loop to begin reading 40 nested objects, asserting that each object's name is 'a'.
    - After reading the last object, it asserts that the path to the current object is correct.
    - The method then reads a boolean value, expecting it to be true.
    - Finally, it ends the 40 nested objects and checks that the reader has reached the end of the document.
- **Output**:
    - The method does not return a value but asserts various conditions to validate the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNestingLimitDefault<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNestingLimitDefault}} -->
Tests the default nesting limit of the `JsonReader` class.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Retrieve the default nesting limit from `JsonReader.DEFAULT_NESTING_LIMIT`.
    - Create a JSON string that exceeds the default nesting limit by one level.
    - Instantiate a `JsonReader` with the created JSON string.
    - Assert that the nesting limit of the reader matches the default limit.
    - Begin a loop to call `beginArray()` for the number of times equal to the default limit.
    - Assert that calling `beginArray()` one more time throws a `MalformedJsonException`.
    - Check that the exception message indicates the nesting limit has been reached.
- **Output**:
    - The method does not return a value but asserts conditions and checks for exceptions.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.getNestingLimit`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetNestingLimit)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testNestingLimit<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testNestingLimit}} -->
Tests the behavior of the `JsonReader` class with respect to nesting limits.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string and sets a nesting limit.
    - Asserts that the nesting limit is correctly set.
    - Begins reading a JSON array and object, asserting the values read.
    - Tests exceeding the nesting limit and expects a `MalformedJsonException`.
    - Tests setting the nesting limit to zero and expects exceptions on further nesting.
    - Tests reading a value when the nesting limit is zero, which should succeed.
    - Tests multiple top-level arrays with a nesting limit and expects exceptions on exceeding it.
    - Tests setting a negative nesting limit and expects an `IllegalArgumentException`.
- **Output**:
    - The method does not return a value but asserts various conditions to validate the behavior of the `JsonReader` under different nesting limits.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.setNestingLimit`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetNestingLimit)
    - [`com.google.gson.stream.JsonReader.getNestingLimit`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetNestingLimit)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStringEndingInSlash<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStringEndingInSlash}} -->
Tests the behavior of `JsonReader` when the input string ends with a slash.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `JsonReader` with a string input that consists of a single slash ('/').
    - Sets the strictness of the `JsonReader` to `LENIENT` mode.
    - Attempts to peek at the next token in the `JsonReader`, which is expected to throw a `MalformedJsonException` due to the invalid input.
    - Asserts that the thrown exception has the expected message indicating the malformed JSON.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown with a specific error message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testDocumentWithCommentEndingInSlash<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testDocumentWithCommentEndingInSlash}} -->
Tests the behavior of `JsonReader` when parsing a JSON document that ends with a comment followed by a slash.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string that contains a comment ending with a slash.
    - The strictness of the `JsonReader` is set to `LENIENT` to allow for more flexible parsing.
    - An assertion is made to check that a `MalformedJsonException` is thrown when attempting to peek at the next token.
    - The exception's message is verified to ensure it indicates the expected value was not found.
- **Output**:
    - The method does not return a value; instead, it asserts that a `MalformedJsonException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStringWithLeadingSlash<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStringWithLeadingSlash}} -->
Tests the behavior of `JsonReader` when encountering a string with a leading slash.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a new instance of `JsonReader` with a string input that contains a leading slash.
    - Sets the strictness of the `JsonReader` to `LENIENT` mode.
    - Asserts that a `MalformedJsonException` is thrown when calling `peek()` on the reader.
    - Verifies that the exception message matches the expected error message.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testUnterminatedObject<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testUnterminatedObject}} -->
Tests the behavior of `JsonReader` when encountering an unterminated JSON object.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a malformed JSON string that represents an unterminated object.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow for more flexible parsing.
    - Begins reading the JSON object with `beginObject()`.
    - Reads the next name in the object, expecting it to be 'a'.
    - Reads the next string value associated with the name 'a', expecting it to be 'android'.
    - Attempts to peek at the next token, which should fail due to the unterminated object.
    - Asserts that a `MalformedJsonException` is thrown and checks the exception message for correctness.
- **Output**:
    - Throws a `MalformedJsonException` indicating that the JSON object is unterminated, along with a message detailing the location of the error.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testVeryLongQuotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testVeryLongQuotedString}} -->
Tests the ability of `JsonReader` to read a very long quoted string from JSON.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a character array of size 16384 filled with the character 'x'.
    - Constructs a JSON string that contains the long quoted string.
    - Initializes a `JsonReader` with the JSON string.
    - Begins reading an array from the `JsonReader`.
    - Reads the next string from the array and asserts that it equals the long quoted string.
    - Ends the array reading.
- **Output**:
    - No output is returned; the method asserts that the read string matches the expected long string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testVeryLongUnquotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testVeryLongUnquotedString}} -->
Tests the ability of `JsonReader` to read a very long unquoted string.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A character array of size 16384 is created and filled with the character 'x'.
    - This character array is converted into a `String` and wrapped in square brackets to form a JSON array.
    - A `JsonReader` is instantiated with the JSON string and set to lenient mode.
    - The reader begins reading the array and retrieves the next string.
    - The retrieved string is asserted to be equal to the original long string.
    - The reader ends the array.
- **Output**:
    - The method does not return a value but asserts that the string read from the JSON matches the expected long string.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testVeryLongUnterminatedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testVeryLongUnterminatedString}} -->
Tests the behavior of `JsonReader` when reading a very long unterminated string.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - A character array of size 16384 is created and filled with the character 'x'.
    - A string is constructed from the character array, resulting in a very long string.
    - A JSON string is created that starts with an opening bracket followed by the long string.
    - A `JsonReader` is initialized with the JSON string and set to lenient mode.
    - The method begins reading an array from the `JsonReader`.
    - The method asserts that the next string read from the `JsonReader` matches the long string.
    - The method then asserts that an `EOFException` is thrown when attempting to peek at the next token.
- **Output**:
    - The method does not return a value but asserts that the expected string is read and that an `EOFException` is thrown.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipVeryLongUnquotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipVeryLongUnquotedString}} -->
This method tests the ability of the `JsonReader` to skip a very long unquoted string.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string containing a very long unquoted string (8192 'x' characters).
    - The strictness of the `JsonReader` is set to `LENIENT` to allow for unquoted strings.
    - The method begins reading an array using `beginArray()`.
    - The `skipValue()` method is called to skip the long unquoted string.
    - The method ends the array with `endArray()`.
- **Output**:
    - The method does not return any value but ensures that the `JsonReader` can successfully skip the long unquoted string without throwing an exception.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipTopLevelUnquotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipTopLevelUnquotedString}} -->
This method tests the ability of the `JsonReader` to skip a top-level unquoted string.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a string of 8192 'x' characters.
    - The strictness of the reader is set to `Strictness.LENIENT`.
    - The `skipValue()` method is called to skip the top-level unquoted string.
    - The `peek()` method is called to check the next token after skipping.
- **Output**:
    - The method asserts that the next token after skipping the unquoted string is `JsonToken.END_DOCUMENT`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipVeryLongQuotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipVeryLongQuotedString}} -->
Tests the ability of `JsonReader` to skip a very long quoted string.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing a very long quoted string (8192 'x' characters).
    - Begins reading an array using `reader.beginArray()`.
    - Calls `reader.skipValue()` to skip the long quoted string.
    - Ends the array with `reader.endArray()`.
- **Output**:
    - The method does not return any value; it verifies that the `JsonReader` can successfully skip the long quoted string without throwing an exception.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testSkipTopLevelQuotedString<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testSkipTopLevelQuotedString}} -->
Tests the [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method of `JsonReader` to ensure it correctly skips a top-level quoted string.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string containing a quoted string of 8192 'x' characters.
    - The strictness of the `JsonReader` is set to `LENIENT`.
    - The [`skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue) method is called to skip the top-level quoted string.
    - The [`peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek) method is called to check the next token after skipping.
- **Output**:
    - The method asserts that the next token after skipping the quoted string is `END_DOCUMENT`, indicating that the entire input has been consumed.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReaderTest.repeat`](#JsonReaderTestrepeat)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStringAsNumberWithTruncatedExponent<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStringAsNumberWithTruncatedExponent}} -->
Tests the behavior of `JsonReader` when parsing a JSON string with a truncated exponent.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `JsonReader` with a JSON string containing a truncated exponent.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow for non-standard JSON formats.
    - Begins reading an array from the JSON input.
    - Checks the type of the next token using `peek()` method.
- **Output**:
    - The method does not return a value but asserts that the next token is of type `STRING`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStringAsNumberWithDigitAndNonDigitExponent<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStringAsNumberWithDigitAndNonDigitExponent}} -->
Tests the behavior of `JsonReader` when parsing a string representation of a number with a digit and a non-digit exponent.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `JsonReader` with a JSON string containing a number with a non-digit exponent.
    - Sets the strictness of the `JsonReader` to `LENIENT` to allow for non-standard JSON formats.
    - Begins reading an array from the JSON input.
    - Asserts that the next token to be read is of type `STRING`.
- **Output**:
    - The method does not return a value but asserts that the next token is a string, indicating that the input was parsed leniently.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStringAsNumberWithNonDigitExponent<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStringAsNumberWithNonDigitExponent}} -->
Tests the behavior of `JsonReader` when parsing a string representation of a number with a non-digit exponent.
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` instance is created with a JSON string containing a number with a non-digit exponent.
    - The strictness of the `JsonReader` is set to `LENIENT` to allow for non-standard JSON formats.
    - The method begins reading an array from the JSON input.
    - The method checks the type of the next token using `peek()`.
- **Output**:
    - The output is the type of the next token, which is expected to be `STRING` due to the lenient parsing of the malformed number.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testEmptyStringName<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testEmptyStringName}} -->
Tests the behavior of `JsonReader` when reading a JSON object with an empty string as a key.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an empty string as a key.
    - Sets the strictness of the reader to `LENIENT` mode.
    - Checks if the next token is the beginning of an object.
    - Begins reading the object.
    - Checks if the next token is a name and retrieves the name, which should be an empty string.
    - Checks if the next token is a boolean and retrieves its value, which should be true.
    - Checks if the next token is the end of the object.
    - Ends the object reading.
    - Checks if the next token is the end of the document.
- **Output**:
    - The method does not return a value but asserts that the JSON structure is correctly parsed, confirming the expected behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testStrictExtraCommasInMaps<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testStrictExtraCommasInMaps}} -->
Tests that a JSON object with an extra comma at the end is handled correctly in strict mode.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string containing an extra comma.
    - Begins reading the JSON object.
    - Asserts that the first name read is 'a'.
    - Asserts that the corresponding string value is 'b'.
    - Attempts to peek at the next token, which should fail due to the extra comma.
    - Asserts that a `MalformedJsonException` is thrown with the expected error message.
- **Output**:
    - Throws a `MalformedJsonException` indicating that a name was expected at a specific position in the JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testLenientExtraCommasInMaps<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testLenientExtraCommasInMaps}} -->
Tests the behavior of the `JsonReader` when parsing JSON with lenient strictness, specifically handling extra commas in maps.
- **Modifiers**: `public`, `void`, `throws`, `@Test`
- **Inputs**:
    - [`reader`](#JsonReaderTestreader): A `JsonReader` instance initialized with a JSON string containing an extra comma.
- **Control Flow**:
    - The method begins by creating a `JsonReader` instance with a JSON string that has an extra comma.
    - It sets the strictness of the `JsonReader` to `LENIENT` to allow for parsing of malformed JSON.
    - The method then begins reading the JSON object.
    - It asserts that the first name read is 'a'.
    - It asserts that the corresponding string value is 'b'.
    - Finally, it checks that an attempt to peek at the next token throws a `MalformedJsonException` due to the extra comma.
- **Output**:
    - The method does not return a value but asserts that a `MalformedJsonException` is thrown when attempting to peek after reading the valid parts of the JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.repeat<!-- {{#callable:com.google.gson.stream.JsonReaderTest.repeat}} -->
The `repeat` method generates a string consisting of a specified character repeated a given number of times.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `c`: A character that will be repeated in the resulting string.
    - `count`: An integer specifying how many times the character should be repeated.
- **Control Flow**:
    - A character array of size `count` is created to hold the repeated characters.
    - The `Arrays.fill` method is used to fill the array with the specified character `c`.
    - A new `String` is created from the filled character array and returned.
- **Output**:
    - Returns a new string that consists of the character `c` repeated `count` times.
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testMalformedDocuments<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testMalformedDocuments}} -->
Tests various malformed JSON documents to ensure they throw the appropriate exceptions.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`assertDocument`](#JsonReaderTestassertDocument) multiple times with different malformed JSON strings.
    - Each call to [`assertDocument`](#JsonReaderTestassertDocument) checks if the JSON string throws the expected exception type.
    - The expected exceptions include `MalformedJsonException` and `EOFException` for various malformed inputs.
- **Output**:
    - The method does not return a value; it asserts that specific exceptions are thrown for malformed JSON inputs.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.assertDocument`](#JsonReaderTestassertDocument)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testUnterminatedStringFailure<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testUnterminatedStringFailure}} -->
Tests the behavior of `JsonReader` when encountering an unterminated string.
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonReader` instance with a JSON string that has an unterminated string.
    - Sets the strictness of the reader to `LENIENT` to allow for more flexible parsing.
    - Begins reading an array from the JSON input.
    - Checks the token type at the current position to ensure it is a string.
    - Attempts to read the next string, expecting a `MalformedJsonException` to be thrown due to the unterminated string.
    - Asserts that the exception message matches the expected error message.
- **Output**:
    - Throws a `MalformedJsonException` indicating that the string is unterminated, along with the specific location in the JSON.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.testReadAcrossBuffers<!-- {{#callable:com.google.gson.stream.JsonReaderTest.testReadAcrossBuffers}} -->
Tests the ability of `JsonReader` to read across buffer boundaries.
- **Modifiers**: `public`, `void`, `throws`, `IOException`
- **Inputs**: None
- **Control Flow**:
    - A `StringBuilder` is initialized with a single '#' character.
    - A loop appends spaces to the `StringBuilder` until it reaches a length of `JsonReader.BUFFER_SIZE - 3`.
    - The `StringBuilder` is appended with a newline, a closing bracket, a single quote, and the number '3'.
    - A new `JsonReader` instance is created using the string from the `StringBuilder`.
    - The strictness of the `JsonReader` is set to `Strictness.LENIENT`.
    - The method `peek()` is called on the `JsonReader` to retrieve the next token without consuming it.
    - An assertion checks that the token returned is of type `JsonToken.NUMBER`.
- **Output**:
    - The method does not return a value but asserts that the next token is a number.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonReader.toString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadertoString)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.assertStrictError<!-- {{#callable:com.google.gson.stream.JsonReaderTest.assertStrictError}} -->
Asserts that a `MalformedJsonException` contains a specific error message related to strict JSON parsing.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `exception`: An instance of `MalformedJsonException` that is expected to contain a specific error message.
    - `expectedLocation`: A `String` representing the expected location in the JSON where the error occurred.
- **Control Flow**:
    - The method uses the `assertThat` assertion to check the `exception` object.
    - It retrieves the message from the `exception` using `hasMessageThat()` and compares it to a constructed error message.
    - The constructed message includes a suggestion to set the strictness of the `JsonReader` and the `expectedLocation`.
- **Output**:
    - The method does not return a value; it throws an assertion error if the message does not match the expected format.
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.assertUnexpectedStructureError<!-- {{#callable:com.google.gson.stream.JsonReaderTest.assertUnexpectedStructureError}} -->
Asserts that an `IllegalStateException` contains a specific error message format based on the expected and actual tokens.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `exception`: An `IllegalStateException` that is expected to contain a specific error message.
    - `expectedToken`: A `String` representing the token that was expected.
    - `actualToken`: A `String` representing the token that was actually found.
    - `expectedLocation`: A `String` indicating the location in the JSON where the error occurred.
- **Control Flow**:
    - Determines the troubleshooting ID based on whether the actual token is 'NULL'.
    - Constructs an error message that includes the expected token, actual token, and expected location.
    - Uses the `assertThat` method to check if the exception's message matches the constructed error message.
- **Output**:
    - The method does not return a value; it asserts that the exception's message matches the expected format.
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.assertDocument<!-- {{#callable:com.google.gson.stream.JsonReaderTest.assertDocument}} -->
Asserts that a JSON document matches a series of expected structures and values.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `document`: A string representing the JSON document to be validated.
    - `expectations`: A variable-length argument list of expected JSON structures and values.
- **Control Flow**:
    - Creates a `JsonReader` instance from the provided `document` string.
    - Sets the reader's strictness to `LENIENT` to allow for flexible parsing.
    - Iterates over each `expectation` in the `expectations` array.
    - For each `expectation`, checks its type and performs the corresponding action on the `JsonReader`.
    - If an unsupported expectation is encountered, an `AssertionError` is thrown.
- **Output**:
    - The method does not return a value; it throws exceptions if the document does not match the expectations.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderTest.reader`](#JsonReaderTestreader)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonWriter.peek`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)


---
#### JsonReaderTest\.reader<!-- {{#callable:com.google.gson.stream.JsonReaderTest.reader}} -->
Creates a `Reader` instance that reads from a given string.
- **Inputs**:
    - `s`: A `String` input from which the `Reader` will read.
- **Control Flow**:
    - The method immediately returns a new `StringReader` instance initialized with the input string `s`.
    - The commented-out code suggests an alternative implementation that would create an anonymous `Reader` subclass, but this code is not executed.
- **Output**:
    - Returns a `Reader` object that reads characters from the provided string `s`.
- **See also**: [`com.google.gson.stream.JsonReaderTest`](#JsonReaderTest)  (Base Class)



