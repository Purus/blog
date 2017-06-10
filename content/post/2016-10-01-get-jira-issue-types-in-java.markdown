---
categories:
- Programming
date: 2016-10-01T16:49:34Z
date_gmt: 2016-10-01 11:19:34 +0530
published: true
status: publish
title: Getting all JIRA Issue Types using Java
---

Let's see how to fetch all available issues from JIRA in JAVA using the REST API library provided by Atlassian.

> To know about the required Maven dependencies and how to generate the trust store file used in the code below, you can refer to [How to work with Atlassian JIRA API using Java](/programming/2016/09/18/how-to-use-JIRA-API-in-Java.html).

The full code is provided below to get Name and Id of all available issue types.

```java
import com.atlassian.jira.rest.client.api.JiraRestClient;
import com.atlassian.jira.rest.client.api.domain.IssueType;
import com.atlassian.jira.rest.client.auth.BasicHttpAuthenticationHandler;
import com.atlassian.jira.rest.client.internal.async.AsynchronousJiraRestClientFactory;
import com.google.common.collect.Lists;

import java.net.URI;
import java.util.ArrayList;

/**
 * Get all issue details
 */
public class Tutorial01 {
    public static void main(String[] args) throws Exception {
        System.setProperty("javax.net.ssl.trustStore", "C:/myTrustStore");

        // Your JIRA URL
        URI jiraServerUri = URI.create("https://localhost:4448/");

        AsynchronousJiraRestClientFactory factory = new AsynchronousJiraRestClientFactory();

        JiraRestClient restClient = factory.create(jiraServerUri, new BasicHttpAuthenticationHandler("username", "password"));

        try {
            ArrayList<IssueType> issueTypes = Lists.newArrayList(restClient.getMetadataClient().getIssueTypes().claim());

            for ( IssueType issue : issueTypes){
                System.out.println("Issue Name : " + issue.getName() + " , Issue ID : " + issue.getId());
            }

        } finally {
            restClient.close();
        }

    }

}
```


For the provided code you will get all the issue names and it's internal ID in the console output. Some sample is provided below for your understanding.

```
Issue Name : Task , Issue ID : 3
Issue Name : Sub-task , Issue ID : 5
Issue Name : Defect , Issue ID : 78
Issue Name : Change Request , Issue ID : 14
Issue Name : Epic , Issue ID : 11
Issue Name : Story , Issue ID : 12
Issue Name : Idea , Issue ID : 1008
Issue Name : Todo , Issue ID : 1106
```
