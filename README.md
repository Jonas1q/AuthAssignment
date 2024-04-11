# News Site Backend Authorization Proof-of-Concept #

## Overview ##
In this project, we're building a backend system for a news site. The system includes functionalities for managing articles, comments, and user roles. The implemented authorization system adheres to specific policies outlined in the assignment.

## Policy ##
The implemented authorization system enforces the following policies:

Editor: Can edit and delete articles, edit and delete user comments.
Writer / Journalist: Can create and edit their own articles.
Subscriber / Registered User: Can comment on articles.
Guest / Public User: Can read articles.

## Schema ##
The database schema used in this project is as follows:

`CREATE TABLE IF NOT EXISTS users (
    user_id INTEGER PRIMARY KEY,
    username TEXT UNIQUE NOT NULL,
    password_hash TEXT NOT NULL
);`

`CREATE TABLE IF NOT EXISTS articles (
    article_id INTEGER PRIMARY KEY,
    title TEXT NOT NULL,
    content TEXT NOT NULL,
    author_id INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (author_id) REFERENCES users(user_id) ON DELETE CASCADE
);`

`CREATE TABLE IF NOT EXISTS comments (
    comment_id INTEGER PRIMARY KEY,
    content TEXT NOT NULL,
    article_id INTEGER NOT NULL,
    user_id INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (article_id) REFERENCES articles(article_id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES users(user_id) ON DELETE CASCADE
);`

## Deliverable ##

### The following can be used to login as the different users ###
Username  | Password
------------- | -------------
EditorUser  | EditorPassword
JournalistUser  | JournalistPassword
RegisteredUser | RegisteredPassword

Here's a step by step for a journalist user:
1. Login using the `/login` endpoint. The server will return a JWT token, you will need this to reach different endpoints so keep save it.
2. Use the `/createArticle` endpoint to create an article, you will need to pass the following to successfully create an article `{
  "articleId": 0,
  "title": "title",
  "content": "content"
}`
3. After creating an article use `/getArticle` followed by `?articleId={}` to grab your desired article.
4. Success.

To get started, follow these steps:

1. Clone the GitHub repository to your local machine.
2. Set up your preferred environment with the required dependencies.
3. Run the provided scripts to generate the database tables.
4. Start the backend server.
5. Test the endpoints using a REST client like Postman or curl.
