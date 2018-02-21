# rj_schema ![build](https://travis-ci.org/foxtacles/rj_schema.svg?branch=master)
Fast JSON schema validation with RapidJSON (https://github.com/Tencent/rapidjson)
# Usage
```
require 'rj_schema'
```
Create an instance of `RjSchema::Validator` and provide a JSON schema and a JSON document. You can pass a `File`, `Hash`, or `String`:
```
RjSchema::Validator.new.validate(File.new("schema/my_schema.json"), '{"stuff": 1}')
```
It is possible to resolve remote schemas by specifying them in the initializer. For example, if your schema contains `"$ref": "generic#/definitions/something"`:
```
RjSchema::Validator.new(
  'generic' => File.new("definitions/generic.json")
).validate(File.new("schema/my_schema.json"), '{"stuff": 1}')
```
`validate` will return an array containing hashes which describe the errors encountered during validation. If the array is empty, the JSON document is valid according to the schema.
An `ArgumentError` exception will be raised if any of the inputs are malformed or missing.
# Limitations

Some limitations apply due to RapidJSON:

- only JSON schema draft-04 is supported
- the `format` keyword is not supported
- there are a few edge cases with regards to `$ref` that will cause issues (for more details, see the tests)
