# Generate Converters & Helpers

- [@deriving(accessors)](https://rescript-lang.org/docs/manual/latest/generate-converters-accessors#generate-functions--plain-values-for-variants)
- [@deriving(jsConverter)](https://rescript-lang.org/docs/manual/latest/generate-converters-accessors#generate-converters-for-js-integer-enums-and-variants)
- [@deriving({jsConverter: newType})](https://rescript-lang.org/docs/manual/latest/generate-converters-accessors#more-safety)
- [@deriving(abstract)](https://rescript-lang.org/docs/manual/latest/generate-converters-accessors#usage-example)
    - [@optional](https://rescript-lang.org/docs/manual/latest/generate-converters-accessors#tips--tricks)
    - [@obj](https://rescript-lang.org/docs/manual/latest/generate-converters-accessors#convert-external-into-js-object-creation-function)

Use `@deriving` to
- Automatically generate functions that convert between ReScript's internal and JS runtime values (e.g. variants).
- Convert a record type into an abstract type with generated creation, accessor and method functions.
- Generate some other helper functions, such as functions from record attribute names.

