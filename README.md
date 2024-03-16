# Engineering-Maintainable-Android-Apps
 Android App Development by Vanderbilt University Coursera Course 4/5

Coursera Quiz Answers
Week 1
Week 2
Week 3
Week 4
# Week 2 : Testing 2 Quiz #
### Question 1: What is an Android Instrumentation Test (select all that apply)? ###
**Answer:**
***an integration test that includes the Android runtime libraries.***

### Question 2: Which of the following are true of unit tests vs. integration tests (select all that apply)? ###
**Answer:**
***The failure of a unit test often more directly points to the source of the failure than an integration test,***
***Unit tests isolate individual components while integration tests check the interactions of multiple components.***
***Integration tests are often slower than unit tests.***

### Question 3: Which of the following creates a valid mock PostalCodeProvider that will return "37212" for the following call (select all that apply): ###
```
postalCodeProvider.getPostalCode(2.11, 3.09)
```
**Answer:**
```
@RunWith(MockitoJUnitRunner.class)
public class GeoUtilsTest {

    @Mock
    private PostalCodeProvider postalCodeProvider;

    @Before
    public void setUp() {
        when(
          postalCodeProvider
            .getPostalCode(anyDouble(), anyDouble())).thenReturn("37212");
    }
}
```
```
@RunWith(MockitoJUnitRunner.class)
public class GeoUtilsTest {

    @Mock
    private PostalCodeProvider postalCodeProvider;

    @Before
    public void setUp() {
        when(
          postalCodeProvider
            .getPostalCode(anyDouble(), 3.09)).thenReturn("37212");
    }
}
```

### Question 4: Which of the following are true (select all that apply)? ###
**Answer:**
***Mocks can be used to help isolate components for unit tests.***
***Mocks can be used to help make tests run faster by eliminating slow running components.***

### Question 5: What will be the result of line 19 (select all that apply)? ###
```
@RunWith(MockitoJUnitRunner.class)
public class GeoUtilsTest {

    @Mock
    private Foo foo;

    @Mock
    private Bar bar;

    @Before
    public void setUp(){
       when(foo.getBar(anyInt()).thenReturn(bar);
       when(bar.getFoo(1)).thenReturn(null);
       when(bar.getFoo(2)).thenReturn(foo));
    }

    @Test
    public void coordinatesWithNoZipCodeReturnNull() {
       Foo f = foo.getBar(2).getFoo(1);
    }
```
**Answers**
***null will be assigned to the variable "f"***

### Question 6: What could be added on line 6 below to ensure that the view with ID R.id.errorMessage is visible on screen and has the contents "Bad password" (select all that apply)? ###
```
    @Test
    public void testPasswordLengthRuleTriggersErrorMsg() {
        onView(withId(R.id.passwordEditText)).perform(typeText("abc"));
        onView(withId(R.id.loginButton)).perform(click());

        // What should be added here
    }
```
**Answer**
```
onView(withId(R.id.errorMessage))
        .check(matches(isDisplayed()));
onView(withId(R.id.errorMessage))
        .check(matches(withText("Bad password")));
```
```
onView(withId(R.id.errorMessage))
        .check(matches(isDisplayed()))
        .check(matches(withText("Bad password")));
```

### Question 7: Which of the following are true of refactoring (select all that apply)? ###
**Answer:**
***Refactoring does not introduce new end-user features.***

### Question 8: What code could be added to insert text into the R.id.welcome TextView (select all that apply)? ###
**Answer:**
```
 onView(withId(R.id.welcome)).perform(typeText("abc"));
```

### Question 9: What is the purpose of regression testing (select all that apply)? ###
**Answer:**
***to check that changes to a code base have not introduced changes in expected behavior of interfaces***
***to check that changes to a code base have not introduced bugs in previously working code***

### Question 10: Which of the following are non-functional properties (select all that apply)? ###
**Answers:**
***how much memory a method consumes***
***how fast a method executes***
***how secure a method is***
***how extensible a method is***

# Week 3 : Security 1 Quiz #
### Question 1: Which of the following is true of the economy of mechanism design principle (select all that apply)? ###
**Answer:**
* Using less code to implement the same functionality will always mean that the code is less extensible and modular.
* Using less code to implement the same functionality simplifies security audits.
* Using less complicated code to implement the same functionality simplifies security audits.

### Question 2: Assuming that "runner" is the only implementation of Runner and never needs to be changed, which of the following refactorings of the code shown below would best demonstrate the economy of mechanism design principle (select all that apply)? ###
**Answer:**
```
public class DataHandler {

 private final ExecutorService executor = Executors.newFixedThreadPool(1);
  
 public void fetchData() {
   executor.submit(new FetchDataTask());
 }
  
 public void writeData() {
   executor.submit(new WriteDataTask());
 }

}
```
### Question 3: Which of the following are reasons why the principle of least privilege is important (select all that apply)? ###
**Answer:**
***Each privilege that your code possesses creates an additional security responsibility to protect that
privilege.***

### Question 4: In Android, which of the following are true of apps that do not apply the principle of least privilege (select all that apply)?
**Answer:**
***They increase the chance that an app will gain access to a capability that requires a uses-permission
without declaring the associated uses-permission.***

### Question 5: Which of the following could be examples of secure defaults (select all that apply)? ###
**Answer:**
***forcing the user to set a password on first use***

### Question 6: Why are secure defaults important (select all that apply)? ###
**Answer:**
***A user may assume that the default settings are secure.***
***A user may not have the expertise to change default settings in a secure manner.***
***A user may not bother changing default settings.***
***A user may not know there are any default settings to change.***

### Question 7: Which of the following is an example of secure defaults (select all that apply)? ###
**Answer:**
```
Map<String, StorageEngine> storageEngines = new HashMap<>();

private encryptedEngine = new EncryptedStorageEngine();

public void init() {
  storageEngines.put("secure", encryptedEngine);
  storageEngines.put("plain", new PlainTextStorageEngine());
}

public void store(String type, String data){
  if(storageEngines.get(type)!=null){
    storageEngines.get(type).store( data);
  }
else {
  encryptedEngine.store(data);
  }
}
```

### Question 8: A number of recent news articles have highlighted apps that asked for a large number of uses-permissions. Which design principle are these apps most likely to violate (select all that apply)? ###
**Answer:**
***Least Privilege***

### Question 9: What is wrong with the code below (select all that apply)? ###
```
public static int SECURE = 1;
public static int MOST_SECURE = 2;
public static int INSECURE = 0;

public void sendData (int securityLevel, String data){
  if(securityLevel > 0){
     sendEncrypted)(data);
  }
  else if(securityLevel == 0){
     sendPlainText(data);
  }
}
```
**Answer:**
***The flags for the security levels are not final, which could lead to runtime changes of their values and unexpected behavior.***
***In Java, new integer variables are initialized to zero, which will cause the default behavior to be insecure.***

### Question 10: When is it appropriate to ignore these security principles in order to develop new functionality (select all that apply)? ###
**Answer:**
***never***

# Result: 100% #

# Week 4 : Security 2 Quiz #
### Question 1: Which of the following are ways that Android protects your app (select all that apply)? ###
**Answer:**
***It ensures data that is stored privately by your app is not accessible to Other apps.***

### Question 2: Question 2 What is the potential security issue with the code shown below (select all that apply)? ###
```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    setContentView(R.layout.main);

    // Get the intent that started this activity
    Intent intent = getIntent();
    String uri = intent.getStringExtra("uri");
    startDownload(uri);
}

public void onDownloadComplete(String downloadedData) {
  Intent result = ...
  result.putExtra("data", downloadedData); 
  setResult(Activity.RESULT_OK, result);
  finish();
}
```
**Answer:**
***The code may lead to a privilege escalation if the calling app does not have the Internet permission.***

### Question 3: Security mistakes are made due to which of the following reasons (select all that apply)? ###
**Answers:**
***The inherent complexity of software makes it difficult not to make mistakes.***

### Question 4: On an Android device, when is a Linux user account created (select all that apply)? ###
**Answers:**
***when app is installed***

### Question 5: Which Of the following are true on Android (select all that apply)? ###
**Answers**
Apps can declare new permissions that Other apps can use.
There is a limited set Of permissions that can be used.
An app can provide access to a privileged resource to another app.
An app can not provide access to a privileged resource to another app unless the other app also has the appropriate uses-permission.

# Result 100% #
