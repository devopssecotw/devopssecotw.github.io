# dos
## bp
### java 
#### google

##### Minimize dependencies 
##### Minimize API surface
##### Use Semantic Versioning
##### Avoid dependencies on unstable libraries and features
##### Do not include a class in more than one classpath entry
##### Rename artifacts and packages together
##### Make breaking transitions easy
##### Advance widely used functionality to a stable version
##### Support the minimum Java version of your consumers
##### Maintain API stability as long as needed for consumers
##### Keep dependencies up to date
##### Make level of support and API stability clear
##### Remove references to deprecated features in dependencies at the first opportunity
##### Specify a single, overridable version of each dependency
##### Publish a BOM for multi-module projects
##### Ensure upper version alignment of dependencies for consumers
##### Coordinate rollout of breaking changes
##### Only shade dependencies as a last resort
##### Place each package in only one module
##### Give each JAR file a module name
##### Upload artifacts to Maven Central
##### Declare all direct dependencies


#### java.exe
##### java [-options] class [args...] (to execute a class)
##### java [-options] -jar jarfile [args...] (to execute a jar file)
##### options
-    -d32          use a 32-bit data model if available
-    -d64          use a 64-bit data model if available
-    -server       to select the "server" VM


-    -cp <class search path of directories and zip/jar files>
-    -classpath <class search path of directories and zip/jar files>
     A ; separated list of directories, JAR archives,
     and ZIP archives to search for class files.
-    -D<name>=<value>
     set a system property
-    -verbose:[class|gc|jni]
     enable verbose output
-    -version      print product version and exit
-    -version:<value>
     require the specified version to run
-    -showversion  print product version and continue
-    -jre-restrict-search | -no-jre-restrict-search
     include/exclude user private JREs in the version search
-    -? -help      print this help message
-    -X            print help on non-standard options
-    -ea[:<packagename>...|:<classname>]
-    -enableassertions[:<packagename>...|:<classname>]
     enable assertions with specified granularity
-    -da[:<packagename>...|:<classname>]
-    -disableassertions[:<packagename>...|:<classname>]
     disable assertions with specified granularity
-    -esa | -enablesystemassertions
     enable system assertions
-    -dsa | -disablesystemassertions
     disable system assertions
-    -agentlib:<libname>[=<options>]
     load native agent library <libname>, e.g. -agentlib:hprof
     see also, -agentlib:jdwp=help and -agentlib:hprof=help
-    -agentpath:<pathname>[=<options>]
     load native agent library by full pathname
-    -javaagent:<jarpath>[=<options>]
     load Java programming language agent, see java.lang.instrument
-    -splash:<imagepath>
     show splash screen with specified image

###
####
###


### references
#### links
- <https://jlbp.dev/>