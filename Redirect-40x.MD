**Navigate to the following path on Jira Server.**
```
<JIRA-install>/atlassian-jira/WEB-INF/web.xml
```

You will find that Jira already has error code pages defined for it, we need to tell this page where to look for our own custom html file. 
You can change the existing <error-code>404 tag for example, which has a default value of
```
<error-page>
 <error-code>404</error-code>
 <location>/secure/404.jspa</location>
</error-page>
```
and change this to be
```
<error-page>
 <error-code>404</error-code>
 <location>/404.html</location>
</error-page>
``` 

Save that web.xml file

**Create a new file 404.html under <jira-install>/atlassian-jira/. We can use any HTML script like following to modify the custom page.**
```
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <meta http-equiv="refresh" content="0;url=https://myserver.ru" />
    </head>

    <body>
        <script language="javascript">
            window.location = "https://myserver.ru";
        </script>
    </body>
</html>
``` 

**Restart Jira.**
