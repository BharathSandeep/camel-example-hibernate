Camel Hibernate Example
=======================

This example shows how to exchange data using a shared database table.

The example has two Camel routes. The first route insert new data into the table,
triggered by a timer to run every 5th second.

The second route pickup the newly inserted rows from the table,
process the row(s), and mark the row(s) as processed when done;
to avoid picking up the same rows again.

You will need to compile this example first:
  mvn compile

To run the example type
  mvn camel:run

To stop the example hit ctrl + c

This example uses Spring to setup and configure the database,
as well the CamelContext. You can see this in the following file:
In the src/main/resources/META-INF/spring/camel-context.xml

This example is documented at
  http://camel.apache.org/hibernate-example.html

If you hit any problems please talk to us on the Camel Forums
  http://camel.apache.org/discussion-forums.html

Please help us make Apache Camel better - we appreciate any feedback you
may have.  Enjoy!

------------------------
The Camel riders!














Hi, Gareth


I attached a camel-hibernate example to this ticket and please take a look at it. The example was taken from camel-extra project but with some modification. The original camel-example-hibernate was for upcoming Apache Camel 2.11 therefore it is not possible to get it to work with Fuse ESB 7.1. One of major reasons is that the original example uses org.springframework.orm.hibernate4 package but it is only supported by Spring-orm from 3.1 release and onwards. Therefore, in order to get the original camel-hibernate example to work, you will need Spring version 3.1 release or higher. Unfortunately, it is not a trivial job at all to upgrade Spring version in Fuse ESB 7.1 to 3.1 release or higher.

Here is a step by step instruction to run the test sample:
1. untar camel-example-hibernate.tar to your local file system;
2. rebuild the sample with command "mvn clean install";
3. start Fuse ESB 7.1 clean;
4. install jpa-hibernate feature by command "features:install jpa-hibernate";
5. install camel-hibernate component 2.10.1 by command
"install -s mvn:org.apache-extras.camel-extra/camel-hibernate/2.10.1"
6. since this sample uses embedded Derby database, therefore, you need to install derby jar by command
"install -s mvn:org.apache.derby/derby/10.7.1.1"
7. install newly built camel-example-hibernate sample by command
"osgi:install -s mvn:org.apache-extras.camel-extra/camel-example-hibernate/2.10.1"

You can then monitor the camel route processing via fuse esb log file. Note, the camel-timer endpoint in the first camel route was configured with period of 15 seconds so it will take a bit time for the first message to show up from fuse esb logs. 

The camel-hibernate is still under development [1] so I am not sure how mature it is at this stage. And as you might have already known that we can not ship Hibernate product as well as camel-hibernate component in our Fuse ESB 7.1 distribution due to it's incompatible GPL license with Apache license.

Alternatively, camel-jpa component [2] might be another choice. So you can use standard JPA layer to wrap Object/Relational Mapping (ORM) products such as Hibernate to store and retrieve Java objects from persistent storage.

Just FYI, Hibernate team is still working on providing better OSGi support. There are a couple of hibernate tickets created [3] [4] for OSGi support. 

[1] https://issues.apache.org/jira/browse/CAMEL-5882
[2] http://camel.apache.org/jpa.html
[3] https://hibernate.onjira.com/browse/HHH-7993
[4] https://hibernate.onjira.com/browse/HHH-7525

Hope it helps and please feel free to let me know if you have more questions.

Best Regards,
Vicky

