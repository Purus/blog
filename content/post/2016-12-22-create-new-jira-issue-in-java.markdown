---
categories:
- Programming
date: 2016-12-22T16:49:34Z
date_gmt: 2016-12-22 11:19:34 +0530
published: true
status: publish
tags:
- java
- jira
title: Create a new Issue in JIRA using Java API
url: /2016/12/22/create-new-jira-issue-in-java/
---

We are now going to see how to create new JIRA issue in JAVA using the REST API library. We can use this cod with some little modifications to bulk create several issues from an Excel sheet or an CSV file.

> To know about the required Maven dependencies and how to generate the trust store file used in the code below, you can refer to [How to work with Atlassian JIRA API using Java]({{site.baseurl}}/programming/2016/09/18/how-to-use-JIRA-API-in-Java.html).

The full code is provided below to give an simple example of creating a new JIRA issue.

{{< highlight java >}}
import com.atlassian.jira.rest.client.api.AuthenticationHandler;
import com.atlassian.jira.rest.client.api.IssueRestClient;
import com.atlassian.jira.rest.client.api.JiraRestClient;
import com.atlassian.jira.rest.client.api.domain.BasicIssue;
import com.atlassian.jira.rest.client.api.domain.IssueFieldId;
import com.atlassian.jira.rest.client.api.domain.input.ComplexIssueInputFieldValue;
import com.atlassian.jira.rest.client.api.domain.input.FieldInput;
import com.atlassian.jira.rest.client.api.domain.input.IssueInput;
import com.atlassian.jira.rest.client.api.domain.input.IssueInputBuilder;
import com.atlassian.jira.rest.client.auth.BasicHttpAuthenticationHandler;
import com.atlassian.jira.rest.client.internal.async.AsynchronousJiraRestClientFactory;
import org.joda.time.DateTime;

import java.net.URI;

/**
 * Create a new JIRA Issue
 */
public class Tutorial04 {
    public static void main(String[] args) throws Exception {
        System.setProperty("javax.net.ssl.trustStore", "C:/Demo/myTrustStore");

        URI jiraServerUri = URI.create("https://local.jira.com/");

        AsynchronousJiraRestClientFactory factory = new AsynchronousJiraRestClientFactory();

        AuthenticationHandler auth = new BasicHttpAuthenticationHandler("username", "password");
        JiraRestClient restClient = factory.create(jiraServerUri, auth);
        IssueRestClient issueClient = restClient.getIssueClient();

        try {
            IssueInputBuilder iib = new IssueInputBuilder();
            iib.setProjectKey("PROJECT-KEY");
            iib.setSummary("Test Summary");
            iib.setIssueType(getIssueType());
            iib.setDescription("Test Description");
            iib.setPriorityId(3L);
            iib.setAssigneeName("Purus");
            iib.setReporterName("Godwin");
            iib.setDueDate(new DateTime());

            iib.setFieldInput(new FieldInput("cust_field_5445", "Custom Value 1"));

            iib.setFieldInput(new FieldInput("cust_field_599", ComplexIssueInputFieldValue.with("value", "Testing")));

            iib.setFieldInput(new FieldInput(IssueFieldId.COMPONENTS_FIELD, "value"));

            IssueInput issue = iib.build();
            BasicIssue issueObj = issueClient.createIssue(issue).claim();

            System.out.println("Issue " + issueObj.getKey() + " created successfully");
        } finally {
            restClient.close();
        }

    }

}

{{< / highlight >}}

In the above example, we have seen 3 ways of creating a field input.

**Type 1**

If you know the field Id of a custom field for which you need to add a value, you can directly pass it.

{{< highlight java >}}
iib.setFieldInput(new FieldInput("cust_field_5445", "Custom Value 1"));
{{< / highlight >}}

**Type 2**

If the custom field can accept complex values rather than simple text input, you have to use ComplexIssueInputFieldValue.

{{< highlight java >}}
iib.setFieldInput(new FieldInput("cust_field_599", ComplexIssueInputFieldValue.with("value", "Testing")));
{{< / highlight >}}

**Type 3**

There are some standard constants provided by Atlassian API to deal with common fields like Components. You can directly refer them as below.

{{< highlight java >}}
iib.setFieldInput(new FieldInput(IssueFieldId.COMPONENTS_FIELD, "value"));
{{< / highlight >}}         
