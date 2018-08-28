# Hello World POC for Jenkins CICD

This application is a poc demonstrating the cicd process with GitHub as Source Code Versioning Tool, Mulesoft Cloudhub as runtime
and Jenkins for CICD pipeline.

## CICD Config

### Maven Configuration
    The Mule project needs to be Mavenised. In the pom file following entry needs to be added for the cloudhub runtime.
	
	```
	  <build>
		<plugins>
			<plugin>
				<groupId>org.mule.tools.maven</groupId>
				<artifactId>mule-maven-plugin</artifactId>
				<version>2.1</version>
				<configuration>
					<deploymentType>cloudhub</deploymentType>
					<!-- muleVersion is the runtime version as it appears on the CloudHub 
						interface -->
					<muleVersion>3.9.0</muleVersion>
					<username>CloudHub_USERNAME</username>
					<password>CloudHub_PasswordE</password>
					<region>ap-southeast-2</region>
					<environment>Sandbox</environment>
					<workerType>Micro</workerType>
					<redeploy>true</redeploy>
					<applicationName>helloworldjentest</applicationName>
				</configuration>
				<executions>
					<execution>
						<id>deploy</id>
						<phase>deploy</phase>
						<goals>
							<goal>deploy</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
	```
###Jenkins Configuration
   1. When creating a new item in Jenkins, select Maven Project.
   
   2. Next in General Tab, Configure your Git repository url
      ![ScreenShot](https://raw.githubusercontent.com/indiramallick1988/Demo2/master/cicd/Source_code.PNG)
	  
   3. Configure the Build trigger so whenever any change is pushed to github it will trigger the new build in Jenkins
      ![ScreenShot](https://raw.githubusercontent.com/indiramallick1988/Demo2/master/cicd/BuildTriggers.PNG)
	  
   4.  Configure the deploy command. Once the application is build successfully, 
       it will be redeployed to CloudHub. 	  
      ![ScreenShot](https://raw.githubusercontent.com/indiramallick1988/Demo2/master/cicd/Build_pre.PNG)
      
###GitHub Configuration 
   1. Next in General Tab, Configure your Git repository url
      ![ScreenShot](https://raw.githubusercontent.com/indiramallick1988/Demo2/master/cicd/GitHubWebHook.png)
	  
   2. In the Jenkins url section provide the url as : http://iib.icraftsoft.net:8080/github-webhook/
