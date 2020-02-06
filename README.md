# quarkus-testng
Quarkus 1.2.0 now requires testng.  When running multiple test testng reports ERROR msg

There are 2 issues.
* When 2 or more tests are run testng prints an error in usage message.
* The names of the individual tests that successfully run are no longer printed.  Only a summary of total tests run is listed.


Before running the test install this archive in your local repo.
Here is the cmd to do it.

mvn install:install-file \
   -Dfile=___FIX_THIS___/lib/utils-arquillian-utils-4.5.0-SNAPSHOT.jar \
   -DgroupId=org.jboss.resteasy \
   -DartifactId=utils-arquillian-utils \
   -Dversion=4.5.0-SNAPSHOT \
   -Dpackaging=jar 

Execution env.
    jdk 11.0.2
    mvn 3.6.0
    
    maven-surefire-plugin is used with excludes. 
    see pom.xml lines 235-273

Compile the tests
   mvn clean test -DskipTests=true

Run Test
   mvn test
  
Results   
  When 2 or more tests (are excluded) and run (see pom.xml line 237, 239)
  The following msg is printed at the start of the test run.  The
  message does not seem to affect the test run but is misleading.
  
  [INFO] Running TestSuite
  
  [TestNG] [ERROR] No test suite found. Nothing to run
  
  Usage: <main class> [options] The XML suite files to run
  
    Options:
      -configfailurepolicy
         Configuration failure policy (skip or continue)
      -d
         Output directory
      -dataproviderthreadcount
         Number of threads to use when running data providers
      -excludegroups
         Comma-separated list of group names to  exclude
      -groups
         Comma-separated list of group names to be run
      -junit
         JUnit mode
         Default: false
      -listener
         List of .class files or list of class names implementing ITestListener or
         ISuiteListener
      -methods
         Comma separated of test methods
         Default: []
      -methodselectors
         List of .class files or list of class names implementing IMethodSelector
      -mixed
         Mixed mode - autodetect the type of current test and run it with
         appropriate runner
         Default: false
      -objectfactory
         List of .class files or list of class names implementing
         ITestRunnerFactory
      -parallel
         Parallel mode (methods, tests or classes)
         Possible Values: [tests, methods, classes, instances, none, true, false]
      -port
         The port
      -reporter
         Extended configuration for custom report listener
      -suitename
         Default name of test suite, if not specified in suite definition file or
         source code
      -suitethreadpoolsize
         Size of the thread pool to use to run suites
         Default: 1
      -testclass
         The list of test classes
      -testjar
         A jar file containing the tests
      -testname
         Default name of test, if not specified in suitedefinition file or source
         code
      -testnames
         The list of test names to run
      -testrunfactory, -testRunFactory
         The factory used to create tests
      -threadcount
         Number of threads to use when running tests in parallel
      -usedefaultlisteners
         Whether to use the default listeners
         Default: true
      -log, -verbose
         Level of verbosity
      -xmlpathinjar
         The full path to the xml file inside the jar file (only valid if -testjar
         was specified)
         Default: testng.xml
  

  Running just a single test, the above message is never printed.


**Quarkus issue filed:**  https://github.com/quarkusio/quarkus/issues/7036
          Issues with new requirement of testng for testing
          
The was a question about the required use of testng.
quakus arquillian is using it.  See the stacktrace provided in file
 xstacktrace.txt.       