# Engineering-Maintainable-Android-Apps
 Android App Development by Vanderbilt University Coursera Course 4/5

Coursera Quiz Answers
Week 1
Week 2
Week 3
Week 4

# Week 3 : Security 1 Quiz
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
