
<script>
fetch('post.json')
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    return response.json();
  })
  .then((json) => initialize(json))
  .catch((err) => console.error(`Fetch problem: ${err.message}`));
  const request = new XMLHttpRequest();

try {
  request.open('GET', 'post.json');

  request.responseType = 'json';

  request.addEventListener('load', () => initialize(request.response));
  request.addEventListener('error', () => console.error('XHR error'));

  request.send();

} catch (error) {
  console.error(`XHR error ${request.status}`);
}
</script>
    <!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org"
      xmlns:sec="http://www.thymeleaf.org/extras/spring-security">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Blog:: Home </title>
</head>
<body>
<div class="container">
<script>
    <a th:href="@{/}">Home</a>
    <h1>Spring Boot Blog Application</h1>
    <hr />
    <ul>
        <li><a th:href="@{/posts/new}">New Post</a></li>
    </ul>
    <div class="posts-container">
        <div class="post" th:each="post : ${posts}">
            <h2><a th:href="@{'/posts/' + ${post.id}}" th:text="${post.title}">Title</a></h2>
            <h5 th:text="'Written by ' + ${post.account.firstName}">Account First Name</h5>
            <h5 th:text="'Published at ' + ${post.createdAt}">Created At</h5>
            <h5 th:text="'Updated at ' + ${post.updatedAt}">Updated At</h5>
            <p th:text="${post.body}">body text</p>
            <br>
        </div>
    </div>
    <hr />
    <ul sec:authorize="!isAuthenticated()">
        <li><a th:href="@{/signup}">signup</a></li>
        <li><a th:href="@{/login}">Login</a></li>
    </ul>
    <div sec:authorize="isAuthenticated()">
        <form th:action="@{/logout}"
              method="POST">
            <div>
                <label>Hi, <span sec:authentication="name">Username</span></label>
            </div>
            <button type="submit">Logout</button>
        </form>
    </div>

</div>

</body>
</html>
