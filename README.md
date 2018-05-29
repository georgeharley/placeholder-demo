# Config server Git with URI placeholder
Created to demonstrate issue with application placeholders in config server Git URIs that is new with Finchley RC2.  
  
After cloning this project please carry out the following steps:  
1. Build using `./gradlew clean build`
2. Start the config server application using `./gradlew bootRun`
3. In a separate terminal try pulling some configuration from the server using `curl localhost:8080/morningtoncrescent/default`  
  You should see the config server throw an exception and the `curl` command fail  
4. Stop the running config server by issuing a ctrl-C in its terminal
5. Edit the file `src/main/resources/application.properties` and change the value of property `spring.cloud.config.server.git.uri` from **https://bitbucket.org/harleyg/{application}-config.git** to **https://bitbucket.org/harleyg/morningtoncrescent-config.git**
6. Save the changes, rebuild the config server and then restart it
7. Once the server has successfully started then, in the other terminal, repeat the command `curl localhost:8080/morningtoncrescent/default`
  The `curl` should now succeed.  
  
    
To demonstrate that this problem is new in RC2 please carry out the following steps:
1. Stop the config server if it is running. 
2. In file `src/main/resources/application.properties` restore the `spring.cloud.config.server.git.uri` property to the value that includes
the application placeholder (**https://bitbucket.org/harleyg/{application}-config.git**)
3. Edit `build.gradle` and change `springBootVersion` from **2.0.2.RELEASE** to **2.0.1.RELEASE**. Change `springCloudVersion` from 
**Finchley.RC2** to **Finchley.RC1**
4. Save the changes, rebuild the config server and then restart it
5. Send a new `curl localhost:8080/morningtoncrescent/default` request to the config server. This should succeed.


  
