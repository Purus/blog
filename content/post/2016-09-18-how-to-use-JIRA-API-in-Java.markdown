---
categories:
- Programming
date: 2016-09-18T16:49:34Z
date_gmt: 2016-09-18 16:49:34 +0530
published: true
status: publish
title: How to work with Atlassian JIRA API using Java
---

To work with JIRA REST API in Java, we need to import the required Java packages and we might also need to import the trust-store file.

Java Package Dependencies
=========================
If you are using Maven, you can easily add the below dependencies in your pom.xml file for working with Atlassian JIRA API.

```xml
    <dependency>
        <groupId>com.atlassian.jira</groupId>
        <artifactId>jira-rest-java-client-core</artifactId>
        <version>3.0.0</version>
    </dependency>

    <dependency>
        <groupId>com.atlassian.jira</groupId>
        <artifactId>jira-rest-java-client-api</artifactId>
        <version>3.0.0</version>
    </dependency>
```

# Creating Trust Store File 
Now, you will need to add your certificate to the trust store so that Java can connect to your API backend. 

## Method 1
If you have OpenSSL installed you can relax. :) You can use the below commands to generate your trust-store file for your JIRA server.

The *s_client* command will get the certificate and provided it. An then we are saving the server certificate to a file called certfile.cer. Please note to replace *jira.website.com:8888* with your own JIRA server URL.

```shell
echo "" | openssl s_client -connect jira.website.com:8888 -showcerts | openssl x509 -out certfile.cer
```

Next step is to import the generated cer file to the trust store.

```shell
keytool -import -keystore myTrustStore -file certfile.cer
```

And now, you can use the myTrustStore file in your Java code to connect to JIRA API.

Method 2
========

Refer to <a href="http://docs.bvstools.com/home/ssl-documentation/exporting-certificate-authorities-cas-from-a-website" target="_blank">Export CER file using browser</a>. You can export the .cer file as mentioend in the link and then you can use the keyimport tool mentioned in the above step.
