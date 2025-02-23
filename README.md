# AvroToJavaDataModel
This repository converts the given avro schema into java data model which can be further utilized for consuming and producing the data from Kafka.

# data model
The code contains the logic to build java data model based on avro schemas

## How to make changes in avro schema

1. Create a new feature branch
2. Make your change in appropriate schema in src/main/avro.
    - If "type" attribute assigned with single value, ensure absence of square brackets. Otherwise, plugin will generate Object type instead of expected one.  
      Examples:  
      ```"type": ["string"] - wrong```  
      ```"type": "string" - correct```   
      ```"type": ["null", "string"] - correct```
    - Optional attributes must have ```null``` as one of type and ```"default": null``` attribute.
    - Please don't forget to provide the schema with correct format.
3. Run ```mvn clean compile``` and verify that generated objects has recent changes
4. Update artifact version in pom.xml
5. Push changes and open pull request to master.
6. In avro sequence is also important.


## Generate models and dependency jar

```sh
mvn clean install
```
It will generate the sources, compile and package them into a jar file.
Eg: target\data-model-x.x.x.jar

## Check validity of local changes to the schema files

```sh
mvn schema-registry:validate -D schema.registry.url=<schema registry url>
```
## Test compatibility of new version with current version in schema registry

```sh
mvn schema-registry:test-compatibility -D schema.registry.url=<schema registry url>
```

## Publish new version to schema registry

```sh
mvn schema-registry:register -D schema.registry.url=<schema registry url>
```
