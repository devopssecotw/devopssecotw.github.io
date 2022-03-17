# dos
## Maven
### mind
#### top
- mvn install:install-file -Dfile=ojdbc7.jar -DgroupId=oracle -DartifactId=ojdbc7 -Dversion=12.1.0.2.0 -Dpackaging=jar -DgeneratePom=true
- mvn clean package -DskipTests
- mvn package -Dmaven.test.skip=true
- mvn clean compile
- mvn clean package
- mvn clean install

#### lifecycle
- Validate
- Test
- Compile
- Verify
- Install
- Deploy