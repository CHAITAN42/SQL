#📊 Social Media Database Case Study

## 📌 Business Task
The goal of this project is to design and analyze a **social media platform database**.  
The schema models users, posts, comments, likes, follows, hashtags, and logins.  

We aim to answer important business questions such as:
- Who are the most active or inactive users?  
- What hashtags and posts are trending?  
- Which users might be bots?  
- How engaged is the community?  

---

## 🏗️ Entity Relationship Diagram
The following ER diagram illustrates the database schema:

![ER Diagram](social_media_er.png)

---

## 📂 Dataset Structure
This project is divided into three main SQL scripts:

1. **Database Schema** – Defines the tables and relationships.  
   📄 `Database schema.sql`

2. **Database Tables (Sample Data)** – Inserts test records for users, follows, and interactions.  
   📄 `Database Tables.sql`

3. **Analytical SQL Queries** – Extracts insights and answers business questions.  
   📄 `SQL Queries.sql`

---

## 📊 Sample Questions & Solutions

### 🔹 1. Most Followed Hashtags
```sql
SELECT 
    hashtag_name AS 'Hashtags', COUNT(hashtag_follow.hashtag_id) AS 'Total Follows' 
FROM hashtag_follow, hashtags 
WHERE hashtags.hashtag_id = hashtag_follow.hashtag_id
GROUP BY hashtag_follow.hashtag_id
ORDER BY COUNT(hashtag_follow.hashtag_id) DESC LIMIT 5;
```

---

### 🔹 2. Average Post per User
```sql
SELECT ROUND((COUNT(post_id) / COUNT(DISTINCT user_id) ),2) AS 'Average Post per User' 
FROM post;
```

---

### 🔹 3. Detecting Bot Activity (Users Who Liked Every Post)
```sql
SELECT username, Count(*) AS num_likes 
FROM users 
INNER JOIN post_likes ON users.user_id = post_likes.user_id 
GROUP BY post_likes.user_id 
HAVING num_likes = (SELECT Count(*) FROM post);
```

---

### 🔹 4. Longest Captions in Posts
```sql
SELECT user_id, caption, LENGTH(post.caption) AS caption_length 
FROM post
ORDER BY caption_length DESC LIMIT 5;
```

---

### 🔹 5. Users Not Following Anyone
```sql
SELECT user_id, username AS 'User Not Following Anyone'
FROM users
WHERE user_id NOT IN (SELECT follower_id FROM follows);
```

---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/social-media-sql.git
   cd social-media-sql
   ```

2. Load schema in MySQL:
   ```sql
   source Database\ schema.sql;
   ```

3. Insert sample data:
   ```sql
   source Database\ Tables.sql;
   ```

4. Run analytical queries:
   ```sql
   source SQL\ Queries.sql;
   ```

---

## 🎯 Key Insights
- Identified **most inactive users** and **users who never commented**.  
- Extracted **most liked posts** and **trending hashtags**.  
- Detected potential **bot accounts** based on engagement patterns.  
- Analyzed **community growth** through followers/following data.  

---
