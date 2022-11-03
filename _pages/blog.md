---
layout: page
title:  Blog
permalink: /blog/
---

<!-- HTML table fragment for page -->
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Blog</title>
</head>
<body>
<div class="container">
    <h1>Spring Boot Blog Application</h1>
    <hr />
    <div class="posts-container">
        <div class="post" th:each="post : ${posts}">
            <h2><a th:href="@{'/posts/' + ${post.id}}" 
                th:text="${post.title}">Title</a>
            </h2>
            <h5 th:text="'Written By ' + ${post.account.firstName}+ ' '+${post.account.lastName}">Account Name</h5>
            <h5 th:text="'Published at ' + ${post.createdAt}">Created At</h5>
            <p th:text="${post.body}">body text</p>
            <br/>
    </div>
    <hr />
</body>
</html>

<!-- Script is layed out in a sequence (no function) and will execute when page is loaded -->
<script>
  // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");
  const resultContainer = document.getElementById("result");

  // prepare fetch options
  const url = "https://team555.tk/blog";
  const options = {
    method: 'GET', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'omit', // include, *same-origin, omit
    headers: {
      'Content-Type': 'application/json'
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
  };

fetch(url, options)
	.then(response => response.json())
	.then(response => console.log(response))
	.catch(err => console.error(err));
</script>
