---
categories:
- Programming
date: 2016-11-12T16:49:34Z
date_gmt: 2016-11-12 11:19:34 +0530
published: true
status: publish
title: Get JIRA Field ID using Java
---

Let's see how to fetch the field Id from JIRA in JAVA using the REST API library provided by Atlassian.

> To know about the required Maven dependencies and how to generate the trust store file used in the code below, you can refer to [How to work with Atlassian JIRA API using Java](/programming/2016/09/18/how-to-use-JIRA-API-in-Java.html).

The full code is provided below to get the ID value of a "Module Priority" field for the issue type "Defect" present in the project "PROJECT-KEY".

```java
import com.atlassian.jira.rest.client.api.AuthenticationHandler;
import com.atlassian.jira.rest.client.api.GetCreateIssueMetadataOptions;
import com.atlassian.jira.rest.client.api.GetCreateIssueMetadataOptionsBuilder;
import com.atlassian.jira.rest.client.api.JiraRestClient;
import com.atlassian.jira.rest.client.api.domain.CimFieldInfo;
import com.atlassian.jira.rest.client.api.domain.CimIssueType;
import com.atlassian.jira.rest.client.api.domain.CimProject;
import com.atlassian.jira.rest.client.auth.BasicHttpAuthenticationHandler;
import com.atlassian.jira.rest.client.internal.async.AsynchronousJiraRestClientFactory;

import java.net.URI;
import java.util.Iterator;
import java.util.List;
import java.util.Map;

/**
 * Get the ID for a given field for a given issue type
 */
public class Tutorial05 {
    static JiraRestClient restClient;

    public static void main(String[] args) throws Exception {
        System.setProperty("javax.net.ssl.trustStore", "C:/Demo/myTrustStore");

        URI jiraServerUri = URI.create("https://jira.locahost.com/");

        AsynchronousJiraRestClientFactory factory = new AsynchronousJiraRestClientFactory();

        AuthenticationHandler auth = new BasicHttpAuthenticationHandler("username", "password");
        restClient = factory.create(jiraServerUri, auth);

        try {
            System.out.println(getFieldId("Defect","Module Priority"));

        } finally {
            restClient.close();
        }

    }

    private static String getFieldId(String type, String fieldName) {
        String fieldId = null;

        GetCreateIssueMetadataOptions options = new GetCreateIssueMetadataOptionsBuilder()
                .withExpandedIssueTypesFields()
                .withProjectKeys("PROJECT-KEY")
                .build();

        List myList = (List) restClient.getIssueClient().getCreateIssueMetadata(options).claim();

        Iterator<CimProject> it1 = myList.iterator();

        while (it1.hasNext()) {
            CimProject c = it1.next();
            List issueT = (List) c.getIssueTypes();
            java.util.Iterator<CimIssueType> it2 = issueT.iterator();

            while (it2.hasNext()) {
                CimIssueType issueType = it2.next();

                if (!issueType.getName().equalsIgnoreCase(type)) {
                    continue;
                }

                Map<String, CimFieldInfo> fieldList = issueType.getFields();
                for (Map.Entry<String, CimFieldInfo> entry : fieldList.entrySet()) {
                    CimFieldInfo field = entry.getValue();

                    if (!field.getName().equals(fieldName)) {
                        continue;
                    }

                    fieldId = field.getId();
                }
            }
        }

        return fieldId;
    }

}
```


The output will be the ID value of the "Module Priority" field as shown below. You can use this ID for updates or while creating new issues. Refer to other blog posts for understanding in detail.

```
customfield_1645
```
