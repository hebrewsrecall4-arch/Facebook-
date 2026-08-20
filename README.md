<!DOCTYPE html>
<html>
<head><title>Facebook Clone Feed</title></head>
<body>
  <header>
    <span>Logged in as: <strong>{{ request.user.username }}</strong></span>
    <form action="{% url 'logout' %}" method="post" style="display:inline;">
      {% csrf_token %}
      <button type="submit">Logout</button>
    </form>
  </header>

  <main>
    <!-- Post Creation Box -->
    <form method="POST">
      {% csrf_token %}
      <textarea name="content" placeholder="What's on your mind?"></textarea>
      <button type="submit">Post</button>
    </form>

    <hr>

    <!-- News Feed -->
    {% for post in posts %}
      <div style="border:1px solid #ccc; padding: 10px; margin-bottom: 10px;">
        <strong>{{ post.author.username }}</strong> 
        <small>{{ post.created_at|timesince }} ago</small>
        <p>{{ post.content }}</p>
        <button>Like ({{ post.likes.count }})</button>
      </div>
    {% empty %}
      <p>No posts yet. Add friends or make a post!</p>
    {% endfor %}
  </main>
</body>
</html>

