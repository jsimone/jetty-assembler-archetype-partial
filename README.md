#Using the archetype

##Clone and build the archetype
    $ git clone git@github.com:jsimone/jetty-assembler-archetype-partial.git
    $ cd jetty-assembler-archetype-partial
    $ mvn install

##Choose your project
Go to the directory where your existing web project is.

Generate from the archetype:
    $ mvn archetype:generate -DarchetypeGroupId=net.publicstaticvoidmain -DarchetypeArtifactId=jetty-assembler-archetype-partial

Follow the prompts and choose your values for groupId, artifactId, version, and base package. 
None of these will override what is already in your project so you can choose anything you'd like.

Your project will be enhanced with a Main class for launching Jetty and the maven appassembler plugin for generating your launch script. 

##Change your packaging type to jar
Your webapp is probably packaged as a war file. Find and delete this line near the top of your pom so that it will be packaged as a jar: <packaging>war</packaging>

##Check your dependencies
The partial archetype cannot remove or alter existing dependencies so check the following in your application:

If you're using servlets be sure that you have the servlet-api and that it is not in the scope "provided"

    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>

If you're using jsps make sure that you do not have the jsp-api as a dependency or that it is in scope "provided" and make sure that you have jstl:

    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>

##Running Locally

Go to your project directory.

Build the application:

    $ mvn install

Set the location of your maven repository (usually in your home directory under .m2/repository)  into the REPO variable:

    $ export REPO="/home/user/.m2/repository"

Run the application:

    $ sh target/bin/webapp

Now you can test your application by opening a browser and going to http://localhost:8080
