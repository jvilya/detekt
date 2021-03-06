# style

The Style ruleset provides rules that assert the style of the code.
This will help keep code in line with the given
code style guidelines.

## Content

1. [CollapsibleIfStatements](#collapsibleifstatements)
2. [ReturnCount](#returncount)
3. [ThrowsCount](#throwscount)
4. [NewLineAtEndOfFile](#newlineatendoffile)
5. [WildcardImport](#wildcardimport)
6. [MaxLineLength](#maxlinelength)
7. [EqualsNullCall](#equalsnullcall)
8. [ForbiddenComment](#forbiddencomment)
9. [ForbiddenImport](#forbiddenimport)
10. [FunctionOnlyReturningConstant](#functiononlyreturningconstant)
11. [SpacingBetweenPackageAndImports](#spacingbetweenpackageandimports)
12. [LoopWithTooManyJumpStatements](#loopwithtoomanyjumpstatements)
13. [MemberNameEqualsClassName](#membernameequalsclassname)
14. [VariableNaming](#variablenaming)
15. [VariableMinLength](#variableminlength)
16. [VariableMaxLength](#variablemaxlength)
17. [TopLevelPropertyNaming](#toplevelpropertynaming)
18. [ObjectPropertyNaming](#objectpropertynaming)
19. [PackageNaming](#packagenaming)
20. [ClassNaming](#classnaming)
21. [EnumNaming](#enumnaming)
22. [FunctionNaming](#functionnaming)
23. [FunctionMaxLength](#functionmaxlength)
24. [FunctionMinLength](#functionminlength)
25. [ForbiddenClassName](#forbiddenclassname)
26. [SafeCast](#safecast)
27. [UnnecessaryAbstractClass](#unnecessaryabstractclass)
28. [UnnecessaryParentheses](#unnecessaryparentheses)
29. [UnnecessaryInheritance](#unnecessaryinheritance)
30. [UtilityClassWithPublicConstructor](#utilityclasswithpublicconstructor)
31. [OptionalAbstractKeyword](#optionalabstractkeyword)
32. [OptionalWhenBraces](#optionalwhenbraces)
33. [OptionalReturnKeyword](#optionalreturnkeyword)
34. [OptionalUnit](#optionalunit)
35. [ProtectedMemberInFinalClass](#protectedmemberinfinalclass)
36. [SerialVersionUIDInSerializableClass](#serialversionuidinserializableclass)
37. [MagicNumber](#magicnumber)
38. [ModifierOrder](#modifierorder)
39. [DataClassContainsFunctions](#dataclasscontainsfunctions)
40. [UseDataClass](#usedataclass)
41. [UnusedImports](#unusedimports)
42. [ExpressionBodySyntax](#expressionbodysyntax)
43. [NestedClassesVisibility](#nestedclassesvisibility)
44. [RedundantVisibilityModifierRule](#redundantvisibilitymodifierrule)
45. [MatchingDeclarationName](#matchingdeclarationname)
## Rules in the `style` rule set:

### CollapsibleIfStatements

TODO: Specify description

#### Noncompliant Code:

```kotlin
val i = 1
if (i > 0) {
    if (i < 5) {
        println(i)
    }
}
```

#### Compliant Code:

```kotlin
val i = 1
if (i > 0 && i < 5) {
    println(i)
}
```

### ReturnCount

Restrict the number of return methods allowed in methods.

Having many exit points in a function can be confusing and impacts readability of the
code.

#### Configuration options:

* `max` (default: `2`)

   define the maximum number of return statements allowed per function

* `excludedFunctions` (default: `"equals"`)

   define functions to be ignored by this check

#### Noncompliant Code:

```kotlin
fun foo(i: Int): String {
    when (i) {
        1 -> return "one"
        2 -> return "two"
        else -> return "other"
    }
}
```

#### Compliant Code:

```kotlin
fun foo(i: Int): String {
    return when (i) {
        1 -> "one"
        2 -> "two"
        else -> "other"
    }
}
```

### ThrowsCount

TODO: Specify description

#### Configuration options:

* `max` (default: `2`)

   maximum amount of throw statements in a method

#### Noncompliant Code:

```kotlin
fun foo(i: Int) {
    when (i) {
        1 -> throw IllegalArgumentException()
        2 -> throw IllegalArgumentException()
        3 -> throw IllegalArgumentException()
    }
}
```

#### Compliant Code:

```kotlin
fun foo(i: Int) {
    when (i) {
        1,2,3 -> throw IllegalArgumentException()
    }
}
```

### NewLineAtEndOfFile

TODO: Specify description

### WildcardImport

Wildcard imports should be replaced with imports using fully qualified class names. This helps increase clarity of
which classes are imported and helps prevent naming conflicts.

Library updates can introduce naming clashes with your own classes which might result in compilation errors.

#### Configuration options:

* `excludeImports` (default: `'java.util.*,kotlinx.android.synthetic.*'`)

   Define a whitelist of package names that should be allowed to be imported
with wildcard imports.

#### Noncompliant Code:

```kotlin
package test

import io.gitlab.arturbosch.detekt.*

class DetektElements {
    val element1 = DetektElement1()
    val element2 = DetektElement2()
}
```

#### Compliant Code:

```kotlin
package test

import io.gitlab.arturbosch.detekt.DetektElement1
import io.gitlab.arturbosch.detekt.DetektElement2

class DetektElements {
    val element1 = DetektElement1()
    val element2 = DetektElement2()
}
```

### MaxLineLength

TODO: Specify description

#### Configuration options:

* `maxLineLength` (default: `120`)

   maximum line length

* `excludePackageStatements` (default: `false`)

   if package statements should be ignored

* `excludeImportStatements` (default: `false`)

   if import statements should be ignored

### EqualsNullCall

TODO: Specify description

#### Noncompliant Code:

```kotlin
fun isNull(str: String) = str.equals(null)
```

#### Compliant Code:

```kotlin
fun isNull(str: String) = str == null
```

### ForbiddenComment

TODO: Specify description

#### Configuration options:

* `values` (default: `'TODO:,FIXME:,STOPSHIP:'`)

   forbidden comment strings

#### Noncompliant Code:

```kotlin
// TODO:,FIXME:,STOPSHIP:
fun foo() { }
```

### ForbiddenImport

TODO: Specify description

#### Configuration options:

* `imports` (default: `''`)

   imports which should not be used

#### Noncompliant Code:

```kotlin
package foo

import kotlin.jvm.JvmField
import kotlin.SinceKotlin
```

### FunctionOnlyReturningConstant

TODO: Specify description

#### Configuration options:

* `ignoreOverridableFunction` (default: `true`)

   if overriden functions should be ignored

* `excludedFunctions` (default: `'describeContents'`)

   excluded functions

#### Noncompliant Code:

```kotlin
fun functionReturningConstantString() = "1"
```

#### Compliant Code:

```kotlin
const val constantString = "1"
```

### SpacingBetweenPackageAndImports

TODO: Specify description

#### Noncompliant Code:

```kotlin
package foo
import a.b
class Bar { }
```

#### Compliant Code:

```kotlin
package foo

import a.b

class Bar { }
```

### LoopWithTooManyJumpStatements

TODO: Specify description

#### Configuration options:

* `maxJumpCount` (default: `1`)

   maximum allowed jumps in a loop

#### Noncompliant Code:

```kotlin
val strs = listOf("foo, bar")
for (str in strs) {
    if (str == "bar") {
        break
    } else {
        continue
    }
}
```

### MemberNameEqualsClassName

This rule reports a member that has the same as the containing class or object.
This might result in confusion.
The member should either be renamed or changed to a constructor.
Factory functions that create an instance of the class are exempt from this rule.

#### Configuration options:

* `ignoreOverriddenFunction` (default: `true`)

   if overridden functions should be ignored

#### Noncompliant Code:

```kotlin
class MethodNameEqualsClassName {

    fun methodNameEqualsClassName() { }
}

class PropertyNameEqualsClassName {

    val propertyEqualsClassName = 0
}
```

#### Compliant Code:

```kotlin
class Manager {

    companion object {
        // factory functions can have the same name as the class
        fun manager(): Manager {
            return Manager()
        }
    }
}
```

### VariableNaming

TODO: Specify description

#### Configuration options:

* `variablePattern` (default: `'[a-z][A-Za-z0-9]*'`)

   naming pattern (default: '[a

* `privateVariablePattern` (default: `'(_)?[a-z][A-Za-z0-9]*'`)

   naming pattern ?[a

### VariableMinLength

TODO: Specify description

#### Configuration options:

* `minimumVariableNameLength` (default: `1`)

   maximum name length

### VariableMaxLength

TODO: Specify description

#### Configuration options:

* `maximumVariableNameLength` (default: `64`)

   maximum name length

### TopLevelPropertyNaming

TODO: Specify description

#### Configuration options:

* `constantPattern` (default: `'[A-Z][_A-Z0-9]*'`)

   naming pattern (default: '[A

* `propertyPattern` (default: `'[a-z][A-Za-z\d]*'`)

   naming pattern (default: '[a

* `privatePropertyPattern` (default: `'(_)?[a-z][A-Za-z0-9]*'`)

   naming pattern ?[a

### ObjectPropertyNaming

TODO: Specify description

#### Configuration options:

* `propertyPattern` (default: `'[A-Za-z][_A-Za-z0-9]*'`)

   naming pattern (default: '[A

### PackageNaming

TODO: Specify description

#### Configuration options:

* `packagePattern` (default: `'^[a-z]+(\.[a-z][a-z0-9]*)*$'`)

   naming pattern (default: '^[a

### ClassNaming

TODO: Specify description

#### Configuration options:

* `classPattern` (default: `'[A-Z$][a-zA-Z0-9$]*'`)

   naming pattern (default: '[A

### EnumNaming

TODO: Specify description

#### Configuration options:

* `enumEntryPattern` (default: `'^[A-Z$][a-zA-Z_$]*$'`)

   naming pattern (default: '^[A

### FunctionNaming

TODO: Specify description

#### Configuration options:

* `functionPattern` (default: `'^([a-z$][a-zA-Z$0-9]*)|(`.*`)$'`)

   naming pattern (default: '^([a

### FunctionMaxLength

TODO: Specify description

#### Configuration options:

* `maximumFunctionNameLength` (default: `30`)

   maximum name length

### FunctionMinLength

TODO: Specify description

#### Configuration options:

* `minimumFunctionNameLength` (default: `3`)

   minimum name length

### ForbiddenClassName

TODO: Specify description

#### Configuration options:

* `forbiddenName` (default: `''`)

   forbidden class names

### SafeCast

TODO: Specify description

#### Noncompliant Code:

```kotlin
fun numberMagic(number: Number) {
    val i = if (number is Int) number else null
    // ...
}
```

#### Compliant Code:

```kotlin
fun numberMagic(number: Number) {
    val i = number as? Int
    // ...
}
```

### UnnecessaryAbstractClass

TODO: Specify description

#### Noncompliant Code:

```kotlin
abstract class OnlyAbstractMembersInAbstractClass { // violation: no concrete members

    abstract val i: Int
    abstract fun f()
}

abstract class OnlyConcreteMembersInAbstractClass { // violation: no abstract members

    val i: Int = 0
    fun f() { }
}
```

### UnnecessaryParentheses

Reports unnecessary parentheses around expressions.

Added in v1.0.0.RC4

#### Noncompliant Code:

```kotlin
val local = (5 + 3)

if ((local == 8)) { }

fun foo() {
    function({ input -> println(input) })
}
```

#### Compliant Code:

```kotlin
val local = 5 + 3

if (local == 8) { }

fun foo() {
    function { input -> println(input) }
}
```

### UnnecessaryInheritance

TODO: Specify description

#### Noncompliant Code:

```kotlin
class A : Any()
class B : Object()
```

### UtilityClassWithPublicConstructor

TODO: Specify description

#### Noncompliant Code:

```kotlin
class UtilityClass {

    // public constructor here
    constructor() {
        // ...
    }

    companion object {
        val i = 0
    }
}
```

#### Compliant Code:

```kotlin
class UtilityClass {

    private constructor() {
        // ...
    }

    companion object {
        val i = 0
    }
}
```

### OptionalAbstractKeyword

TODO: Specify description

#### Noncompliant Code:

```kotlin
abstract interface Foo { // abstract keyword not needed

    abstract fun x() // abstract keyword not needed
    abstract var y: Int // abstract keyword not needed
}
```

#### Compliant Code:

```kotlin
interface Foo {

    fun x()
    var y: Int
}
```

### OptionalWhenBraces

TODO: Specify description

#### Noncompliant Code:

```kotlin
val i = 1
when (1) {
    1 -> { println("one") } // unnecessary curly braces since there is only one statement
    else -> println("else")
}
```

#### Compliant Code:

```kotlin
val i = 1
when (1) {
    1 -> println("one")
    else -> println("else")
}
```

### OptionalReturnKeyword

TODO: Specify description

#### Noncompliant Code:

```kotlin
val z = if (true) return x else return y
```

#### Compliant Code:

```kotlin
val z = if (true) x else y
```

### OptionalUnit

TODO: Specify description

#### Noncompliant Code:

```kotlin
fun foo(): Unit { }
```

#### Compliant Code:

```kotlin
fun foo() { }
```

### ProtectedMemberInFinalClass

TODO: Specify description

#### Noncompliant Code:

```kotlin
class ProtectedMemberInFinalClass {
    protected var i = 0
}
```

#### Compliant Code:

```kotlin
class ProtectedMemberInFinalClass {
    private var i = 0
}
```

### SerialVersionUIDInSerializableClass

TODO: Specify description

#### Noncompliant Code:

```kotlin
class IncorrectSerializable : Serializable {

    companion object {
        val serialVersionUID = 1 // wrong declaration for UID
    }
}
```

#### Compliant Code:

```kotlin
class CorrectSerializable : Serializable {

    companion object {
        const val serialVersionUID = 1L
    }
}
```

### MagicNumber

TODO: Specify description

#### Configuration options:

* `ignoreNumbers` (default: `'-1,0,1,2'`)

   numbers which do not count as magic numbers (default: '

* `ignoreHashCodeFunction` (default: `false`)

   whether magic numbers in hashCode functions should be ignored

* `ignorePropertyDeclaration` (default: `false`)

   whether magic numbers in property declarations should be ignored

* `ignoreConstantDeclaration` (default: `true`)

   whether magic numbers in property declarations should be ignored

* `ignoreCompanionObjectPropertyDeclaration` (default: `true`)

   whether magic numbers in companion object
declarations should be ignored

* `ignoreAnnotation` (default: `false`)

   whether magic numbers in annotations should be ignored

* `ignoreNamedArgument` (default: `true`)

   whether magic numbers in named arguments should be ignored

* `ignoreEnums` (default: `false`)

   whether magic numbers in enums should be ignored

#### Noncompliant Code:

```kotlin
class User {

    fun checkName(name: String) {
        if (name.length > 42) {
            throw IllegalArgumentException("username is too long")
        }
        // ...
    }
}
```

#### Compliant Code:

```kotlin
class User {

    fun checkName(name: String) {
        if (name.length > MAX_USERNAME_SIZE) {
            throw IllegalArgumentException("username is too long")
        }
        // ...
    }

    companion object {
        private const val MAX_USERNAME_SIZE = 42
    }
}
```

### ModifierOrder

TODO: Specify description

#### Noncompliant Code:

```kotlin
lateinit internal private val str: String
```

#### Compliant Code:

```kotlin
private internal lateinit val str: String
```

### DataClassContainsFunctions

TODO: Specify description

#### Configuration options:

* `conversionFunctionPrefix` (default: `'to'`)

   allowed conversion function names

#### Noncompliant Code:

```kotlin
data class DataClassWithFunctions(val i: Int) {
    fun foo() { }
}
```

### UseDataClass

TODO: Specify description

#### Noncompliant Code:

```kotlin
class DataClassCandidate(val i: Int) {

    val i2: Int = 0
}
```

#### Compliant Code:

```kotlin
data class DataClass(val i: Int, val i2: Int)
```

### UnusedImports

TODO: Specify description

### ExpressionBodySyntax

TODO: Specify description

#### Noncompliant Code:

```kotlin
fun stuff(): Int {
    return 5
}
```

#### Compliant Code:

```kotlin
fun stuff() = 5
```

### NestedClassesVisibility

TODO: Specify description

#### Noncompliant Code:

```kotlin
internal class NestedClassesVisibility {

    public class NestedPublicClass // should not be public
}
```

#### Compliant Code:

```kotlin
internal class NestedClassesVisibility {

    internal class NestedPublicClass
}
```

### RedundantVisibilityModifierRule

TODO: Specify description

#### Noncompliant Code:

```kotlin
public interface Foo { // public per default

    public fun bar() // public per default
}
```

#### Compliant Code:

```kotlin
interface Foo {

    fun bar()
}
```

### MatchingDeclarationName

"If a Kotlin file contains a single class (potentially with related top-level declarations),
its name should be the same as the name of the class, with the .kt extension appended.
If a file contains multiple classes, or only top-level declarations,
choose a name describing what the file contains, and name the file accordingly.
Use camel humps with an uppercase first letter (e.g. ProcessDeclarations.kt).

The name of the file should describe what the code in the file does.
Therefore, you should avoid using meaningless words such as "Util" in file names." - Official Kotlin Style Guide

More information at: http://kotlinlang.org/docs/reference/coding-conventions.html

#### Noncompliant Code:

```kotlin
class Foo // FooUtils.kt

fun Bar.toFoo(): Foo = ...
fun Foo.toBar(): Bar = ...
```

#### Compliant Code:

```kotlin
class Foo { // Foo.kt
    fun stuff() = 42
}

fun Bar.toFoo(): Foo = ...
```
