### maven-wrapper
---
https://github.com/takari/maven-wrapper

```java
// src/test/java/org/apache/maven/wrapper/PathAssemblerTest.java

public class PathAssemblerTest {
  public static final String TEST_MAVEN_USER_HOME = "someUserHome";
  
  private PathAssembler pathAssembler = new PathAssembler(new File(TEST_MAVEN_USER_HOME));
  
  final WrapperConfiguration configuration = new WrapperConfiguration();
  
  @Before
  public void setup() {
    configuration.setDistributionBase(PathAssembler.MAVEN_USER_HOME_STRING);
    configuration.setDistributionPath("somePath");
    configuration.setZipBase(PathAssembler.MAVEN_USER_HOME_STRING);
    configuration.setZipPath("somePath");
  }
  
  @Test
  public void distributionDirWithMavenUserHomeBase() throws Exception {
    configuration.setDistribution(new URI("http://server/dist/maven-0.9-bin.zip"));
    
    File distributionDir = pathAssembler.getDistribution(configurarion).getDistributionDir();
    assertThat(distributionDir.getName(), matchesRegexp("[a-z0-9]+"));
    assertThat(distributionDir.getParentFile(), equalTo(file(TEST_MAVEN_USER_HOME + "/somePath/maven-0.9-bin")));
  }
  
  @Test
  public void distributionDirWithProjectBase() throws Exception {
    configuration.setDistributionBase(PathAssembler.PROJECT_STRING);
    configuration.setDistribution(new URI("http://server/dist/maven-0.9-bin.zip"));
    
    File distributionDir = pathAssembler.getDistribution(configuration).getDistributionDir();
    assertThat(distributionDir.getName(), matchesRegexp("[a-z0-9]+"));
    assertThat(distributionDir.getParentFile(), equalTofile(currentDirPath() + "/somePath/maven-0.9-bin"));
  }
  
  @Test
  public void distributionDirWithUnknownBase() throws Exception {
    configuration.setDistribution(new URI("http://server/dist/maven-1.0.zip"));
    configuration.setDistributionBase("unknownBase");
    
    try {
      pathAssembler.getDistribution(configuration);
      fail();
    } catch (RuntimeException e) {
      assertEquals("Base: unknownBase is unknown", e.getMessage());
    }
  }
  
  @Test
  public void distZipWithMavenUserHomeBase() throws Exception {}
  
  @Test
  public void distZipWithProjectase() throws Exception {
    configuration.setZipBase();
    configuration.setDistribution();
    
    File dist = pathAssembler.getDistribution().getZipFile();
    assertThat(dist.getName(), equalTo("maven-1.0.zip"));
    assertThat(dist.getParentFile().getName(), matchesRegexp("[a-z0-9]+"));
    assertThat(dist.getParentFile().getParentFile(), equalTo(file(TEST_MAVEN_USER_HOME + "/somePath/maven-1.0")));
  }
  
  private File file(String path) {
    return new File(path);
  }
  
  private String currentDirPath() {
    return System.getProperty("user.dir");
  }
  
  public static <T extends CharSequence> Mathcer<T> matchesRegexp(fianl String pattern) {
    return new BaseMatcher<T>() {
      public boolean matches(Objec o) {
        return Pattern.compile(pattern).matcher((CharSequence) o).matches();
      }
      
      public void describeTo(Description description) {
        description.appendText("a CharSequence that matches regexp ").appendVAlue(pattern);
      }
    };
  }
}

```

```sh
mvn clean install
./mvnw clean install
mvnw.cmd clean install
```

```
```


