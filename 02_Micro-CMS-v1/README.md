# Micro-CMS-v1

- Difficulty: Easy
- Skills: Web
- Challenges: 4

## Overview

Micro-CMS-v1 is a content management web application. The home page contains three links: **Testing** (`page/1`), **Markdown Test** (`page/2`), and **Create a new page** (`page/create`).

```html
<!doctype html>
<html>
    <head>
        <title>Micro-CMS</title>
    </head>
    <body>
        <ul>
            <li><a href="page/1">Testing</a></li>
            <li><a href="page/2">Markdown Test</a></li>
        </ul>
        <a href="page/create">Create a new page</a>
    </body>
</html>
```

## Solutions

### XSS on Page Title

The application is vulnerable to XSS when injecting malicious scripts into the article title — this can be done on the edit page or when creating a new page. For example: `<script>alert(document.domain);</script>`. This becomes especially problematic when the payload is rendered on less protected areas of the system, such as the home page.

### XSS on Article Body

The article body is vulnerable to another XSS vector. You can execute it via an `<img>` tag, for example: `<img src="x" onerror="alert('XSS')">`. After the `alert()` fires, you will find the flag exposed as an image tag attribute, e.g. `flag="^FLAG^YOUR-FLAG-ID$FLAG$"`.

[Create Page](./assets/create-page.png)

### SQL Injection on Page Edit

The application contains a few pre-created pages (e.g. **Testing** and **Markdown Test**). Visit the **Testing** page and click the edit button — you will be redirected to `page/edit/1`. This page is vulnerable to **SQL Injection**. Add an apostrophe at the end of the URL to trigger a SQL injection error (`page/edit/1'`) and receive your flag.

### Broken Access Control on Page Edit

The application contains a protected page that returns a **403** status code when accessed directly. You can discover it by fuzzing. *In my case it was `page/4`.*

[Protected Page](./assets/protected-page.png)

The application has broken authorization rules for this page. While it denies direct access to the page content, it does not implement proper authorization on the edit endpoint, allowing any user to edit it. This means you can view the page content at `/page/edit/4` and retrieve your flag directly from the edit form.
