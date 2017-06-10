---
categories:
- Programming
- JIRA
date: 2017-01-10T16:49:34Z
date_gmt: 2017-01-10 11:19:34 +0530
published: true
status: publish
title: Getting JIRA Issues based on filter using Java
highlight : true
---

Let's see how to fetch all issues from JIRA in JAVA based on the provided JQL search filter.

> To know about the required Maven dependencies and how to generate the trust store file used in the code below, you can refer to [How to work with Atlassian JIRA API using Java](/programming/2016/09/18/how-to-use-JIRA-API-in-Java.html).

The full code is provided below to get Name and Id of all available issue types.

```java
import com.atlassian.jira.rest.client.api.AuthenticationHandler;
import com.atlassian.jira.rest.client.api.JiraRestClient;
import com.atlassian.jira.rest.client.api.SearchRestClient;
import com.atlassian.jira.rest.client.api.domain.Issue;
import com.atlassian.jira.rest.client.api.domain.SearchResult;
import com.atlassian.jira.rest.client.auth.BasicHttpAuthenticationHandler;
import com.atlassian.jira.rest.client.internal.async.AsynchronousJiraRestClientFactory;
import com.atlassian.util.concurrent.Promise;

import java.net.URI;

/**
 * Get all issues based on the search filter
 */
public class Tutorial07 {
    static JiraRestClient restClient;

    public static void main(String[] args) throws Exception {
        System.setProperty("javax.net.ssl.trustStore", "C:/Demo/myTrustStore");

        URI jiraServerUri = URI.create("https://jira.localhost.com/");

        AsynchronousJiraRestClientFactory factory = new AsynchronousJiraRestClientFactory();

        AuthenticationHandler auth = new BasicHttpAuthenticationHandler("username", "password");
        restClient = factory.create(jiraServerUri, auth);

        // Any valid search filter(JQL)
        String jql = "project = SAMPLE and reporter = Purus";

        int maxPerQuery = 100;
        int startIndex = 0;

        try {
            SearchRestClient searchRestClient = restClient.getSearchClient();

            while (true) {
                Promise<SearchResult> searchResult = searchRestClient.searchJql(jql, maxPerQuery, startIndex, null);
                SearchResult results = searchResult.claim();

                for (Issue issue : results.getIssues()) {
                    System.out.println(issue.getKey());
                }

                if (startIndex >= results.getTotal()) {
                    break;
                }

                startIndex += maxPerQuery;

                System.out.println("Fetching from Index: " + startIndex);
            }

        } finally {
            restClient.close();
        }

    }
}
```


For the provided code you will get all the issue key value based on the input JQL filter. Some sample output is provided below for your understanding.

```text
SAMPLE-101
SAMPLE-343
SAMPLE-689
```
