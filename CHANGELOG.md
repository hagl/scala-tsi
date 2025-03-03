## 0.8.2 - 2013-02-02

Improves Scala 3 support by adding [Type Class Derivation](https://docs.scala-lang.org/scala3/reference/contextual/derivation.html) for `TSType`.
This adds support for some unsupported scenario's mentioned in the 0.8.0 release notes.

The Scala 3 version should now have feature parity with the Scala 2 version.

## 0.8.1 - 2013-02-01

Fixes [an issue with the 0.8.0 SBT plugin](https://github.com/scala-tsi/scala-tsi/issues/282), rendering it inusable.

## 0.8.0 - 2023-01-30

* Scala 3 is now mostly supported, thanks @jdsalchow for the initial contribution!
  * Automatic recursive definitions are still unsupported: [#278](https://github.com/scala-tsi/scala-tsi/issues/278)
  * Auto-generated definitions inside generics types (`Seq[YourClass]`) will not always work: [#278](https://github.com/scala-tsi/scala-tsi/issues/278)
* Failures in finding the `TSType` of a type are now reported as compile warnings and as messages in the generated Typescript code instead of aborting compilation. 

## 0.7.0 - 2022-07-13

* Add support for string enums in `TSEnum` (#236 by @b-eyselein) and several factory methods in the `TSType` companion object.
* Fix a bug where custom definitions did not always work when used as a generic parameter (#242)

Breaking changes:
* `TSEnum` `entries` changed from `ListMap[String, Option[Int]]` to `ListMap[String, Option[TSLiteralType[_]]`

## 0.6.1 - 2022-06-12

* Add initial support for function types ([#136](https://github.com/scala-tsi/scala-tsi/pull/136) by @vincentdehaan)

## 0.6.0 - 2022-01-05

Improvements:
* Adds `unknown` type
* Unions are now flattened more often

Breaking changes:
* `TSTuple` is no longer generic

Removed deprecated features:

* sbt-plugin no longer automatically activates, `.enablePlugins(ScalaTsiPlugin)` is now required, recommended since 0.4.1 
* Library is no longer published under `nl.codestar.scalatsi`, deprecated since 0.3.0
* All deprecated methods and settings have been removed

## 0.5.1 - 2021-11-08

* When using your own classes inside generic types like `Seq[T]`, it is no longer requires to explicitly create the `implicit val`s  (bugfix: #180)

## 0.5.0 - 2021-03-14

* Sealed traits will now add a field with the class name to the output, defaulting to `type: "ClassName"`. (#140 by @vincentdehaan)
     This behavior can be disabled with the `typescriptTaggedUnionDiscriminator` SBT setting
* Add a configurable header to the generated file (#137 by @vincentdehaan )
  Defaults to a notice about the file being generated by scala-tsi, configurable with `typescriptHeader` SBT setting
* `extends DefaultTSTypes` or `import DefaultTSTypes._` is now usually superfluous (#141)
* Support higher amount of nested classes (bugfix: #146)

## 0.4.1 - 2020-30-09

* Exporter application will now be deleted after generation (#106)
* It is now recommended adding `.enablePlugins(ScalaTsiPlugin)` to your sbt project. This will become mandatory in a future release (#110)
* Improve error message on missing implicits (#111)

## 0.4.0 - 2020-09-11

* Generate typescript based on TSType, not just TSNamedType (#98)
* Rename typescriptClassesToGenerateFor sbt setting to typescriptExports


## 0.3.2 - 2020-08-28

* Support Scala and Java enumerations out of the box (#75)
* Fix bug where no error was given when no typescript mapping is available for a non-abstract sealed class (#80)

## 0.3.1 - 2020-08-22

Fixes the compiler crashing on circular references with this plugin (#67)

## 0.3.0 - 2020-06-12

* Change package from `nl.codestar` to `com.scalatsi`

Libraries will be published under both organizations on maven central for backwards-compatibility initially.

## 0.2.2 - 2020-05-29

* Add ability to rename generated types
* Output will now be generated even if parent directories do not exists yet and improve error messages
* Fixed unused import warning when generating model

## 0.2.1 - 2020-05-22

* Add support for [Literal types](https://docs.scala-lang.org/sips/42.type.html) under Scala 2.13

## 0.2.0 - 2020-05-22

Implicits aren't needed anymore in most cases, the plugin will use the standard generation by default!

* Scala 2.13 support
* Plugin now requires SBT 1.3
* Case classes and sealed trait are now automatically generated
* Sealed traits are now converted into a Typescript Discriminated Union
* Add experimental semicolon support with `typescriptStyleSemicolons` sbt setting (#62)
* `TSExternalName` was renamed to `TSTypeReference` (#43)
* Types are now always outputted in alphabetical order
* Output now has constined and no superflous whitespace


## 0.1.3 - 2018-03-08

* Add `export` to all typescript definitions for easier importing from other files (#31, Fixes #28)
* Add `TSObject` for the Typescript `object` type (#25)
* Map `scala.Any` to Typescript `any`
* Map `scala.AnyRef` and `java.lang.Object` to `object` (#25)
* Map `java.time.*` and `java.util.Date` to `string`
   changeable by overriding `val java8TimeTSType` from `JavaTSTypes` or`DefaultTSTypes` (#26)
* Map java numeric types to `Number` (#26)
* Fix collection types not automatically being converted to an array of the collection element (#27)

## 0.1.2 - 2018-06-08

* Fixes exception when using the plugin in SBT 1.1+ (#23)

## 0.1.1 - 2018-03-16

* `scala-tsi` artifact now contains all dependencies, does not depend on a macro project any more

## 0.1.0 - 2018-03-16

Initial Release of scala-tsi

Features:
* Sbt plugin to generate a typescript file from your domain definition
* Matchings (`TSType`) from a good set of built-in Java and Scala types
* macro to generate typescript interfaces from your case classes
* DSL to write your own typescript definitions
* AST that can model the whole typescript type system (afaik)
