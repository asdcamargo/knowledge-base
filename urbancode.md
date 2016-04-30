# Urban Code Deploy (UCD)
## Tool to automate application deployment

## Concepts
* Components - Smallest atomic artifact that represents a functional unit and can be deployed a sole (e.g. WAR, jar, static content, etc).
* Application - A set of components that can be organized to be deployed as a package.
* Enviroment - Target location where the files will be deployed (e.g. DST, QA, Production, etc).
* Resources - Represents a logical target within the Environment where the files will be deployed e.g. database. Normally the resources will point to a agent.
* Agent - UCD component that lives within the environment to execute the deployment tasks (e.g. download the files, clean dirs, copy files, etc).

-Component Processes: Each component will have its own deployment proccess which is the steps that need to be done to deploy that component.
For example: 1) Download files from repository. 2) Remove the content in /web directory. 3) Copy the downloaded files to /web.

-Application Processes: Steps that involves the components proccesses which will be performed in other to make the application deployment. 

-Plugins: are designed to help in the deployment process of components. For example, tomcat plugin come with several tasks such as start and stop.

## How these concepts are related to each other:

- Components are organized to deploy the application.
- Environments gather multiple resources around a single concept which refers to the stage where the application is: DEVELOPMENT, TEST, PRE PRODUCTION, PRODUCTION and others.
- The resource is where the agent lives and where the components are deployed to.

## Agents states: The state can be view in the agent tab on the UCD UI
- Online: UCD agent is able to connect and read the response from the server.
- Connected: UCD agent is able to connect with the UCD server, however the response from the server is not getting to the agent.
- Offline: UCD agent is not reaching the server. Need to check if the connection port (usually JMX port: 7918) is open on the server.

## Useful links:
* Basic concepts: https://www.youtube.com/watch?v=oVv6a8mUwXo
* Official site: https://developer.ibm.com/urbancode/products/urbancode-deploy/
* Knowledge center: https://www.ibm.com/support/knowledgecenter/SS4GSP_6.1.1/com.ibm.udeploy.doc/topics/part_using.html?lang=en
