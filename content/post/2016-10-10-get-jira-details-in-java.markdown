---
categories:
- Programming
date: 2016-10-10T16:49:34Z
date_gmt: 2016-10-10 11:19:34 +0530
published: true
status: publish
title: Getting all JIRA Issue Details using Java
---

Let's see how to fetch all details of a given JIRA issue in JAVA using the REST API library provided by Atlassian.

> To know about the required Maven dependencies and how to generate the trust store file used in the code below, you can refer to [How to work with Atlassian JIRA API using Java](/programming/2016/09/18/how-to-use-JIRA-API-in-Java.html).

The full code is provided below to get few basic details of an example issue called PROJECT-359.

```java
import com.atlassian.jira.rest.client.api.IssueRestClient;
import com.atlassian.jira.rest.client.api.JiraRestClient;
import com.atlassian.jira.rest.client.api.domain.*;
import com.atlassian.jira.rest.client.auth.BasicHttpAuthenticationHandler;
import com.atlassian.jira.rest.client.internal.async.AsynchronousJiraRestClientFactory;

import java.io.IOException;
import java.net.URI;
import java.util.Iterator;

// Get details of a given JIRA Issue
public class Tutorial01 {
    public static void main(String[] args) throws IOException {
        System.setProperty("javax.net.ssl.trustStore", "C:/Users/PurusR/myTrustStore");

        URI jiraServerUri = URI.create("https://localhost/jira/");

        AsynchronousJiraRestClientFactory factory = new AsynchronousJiraRestClientFactory();

        JiraRestClient restClient = factory.create(jiraServerUri, new BasicHttpAuthenticationHandler("username", "password"));
        IssueRestClient issueClient = restClient.getIssueClient();

        try {
            Issue issue = issueClient.getIssue("PROJECT-359").claim();

            System.out.println("Key : " + issue.getKey());
            System.out.println("Summary : " + issue.getSummary());
            System.out.println("Description : " + issue.getDescription());
            System.out.println("Status : " + issue.getStatus().getName());
            System.out.println("Issue Type : " + issue.getIssueType().getName());
            System.out.println("Assignee : " + issue.getAssignee().getDisplayName());
            System.out.println("Reporter : " + issue.getReporter().getDisplayName());

            Iterator<BasicComponent> allComponents = issue.getComponents().iterator();
            while (allComponents.hasNext()){
                BasicComponent component = allComponents.next();
                System.out.println("Component : " + component.getName());
            }

            Iterator<String> allLabels = issue.getLabels().iterator();
            while (allLabels.hasNext()){
                String label = allLabels.next();
                System.out.println("Label : " + label);
            }

            Iterator<IssueLink> linkedIssues = issue.getIssueLinks().iterator();
            while (linkedIssues.hasNext()){
                IssueLink link = linkedIssues.next();
                System.out.println("Linked Issue : " + link.getTargetIssueKey() + " - " + link.getIssueLinkType());
            }

            Iterator<Comment> comments = issue.getComments().iterator();
            while (comments.hasNext()){
                Comment comment = comments.next();
                System.out.println("Comment : " + comment.getBody() + " by " + comment.getAuthor().getDisplayName());
            }

            Iterator<Attachment> attachments  = issue.getAttachments().iterator();
            while (attachments.hasNext()){
                Attachment attachment = attachments.next();
                System.out.println("Attachment : " + attachment.getFilename());
            }
        } finally {
            restClient.close();
        }

    }
}
```
