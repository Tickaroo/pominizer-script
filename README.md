# Pominizer
This script resolves inner module dependencies (i.e. module A depends on module B) for generated `pom.xml` files in the same gradle project.

## Usage
```groovy
apply from: 'https://raw.githubusercontent.com/Tickaroo/pominizer-script/master/pominizer.gradle'
```

## Define POM properties
**Use the project sroot** `gradle.properties` file to specify `VERSION_NAME` and `GROUP_ID`:

Example:
```
GROUP_ID = com.tickaroo.tiklib
VERSION_NAME = 1.0.4
```

As default the modules name will be the artifact id for the modles `pom.xml file`. However, you can override this with `ARTIFACT_ID` **in the modules** `gradle.properties` file:
Example:

```
ARTIFACT_ID=string
```

You could also override `GROUP_ID` and `VERSION_ID` in each modules `gradle.properties` file, but only do that if you have a very good reason for doing that. The preferred way is to have project specific things like `GROUP_ID`, `VERSION_NAME` **in projects root** `gradle.properties` file and `ARTIFACT_ID` **in modules** `gradle.properties` file


So a typically setup of a multi module project looks like this:
```
   - root
          gradle.properties ( containing GROUP_ID, VERSION_NAME )
     
        - libA 
              gradle.properties ( containing ARTIFACT_ID = "bla" )
    
        - libB 
              gradle.properties ( containinig ARTIFACT_ID = "foo" )
        
        - libC    // No gradle.properties --> module name "libC" will be used as ARTIFACT_ID
```
