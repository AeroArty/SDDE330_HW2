## Data Model Definition:

**Tables/Collections:**

## Author Table
| Field Name | Data Type | Description |
|---|---|---|
| user_id | INT | Unique identifier (Primary Key) for each user. |
| username | VARCHAR(255), Unique | User's chosen username for login (must be unique). |
| email | VARCHAR(255), Unique | User's email address (must be unique). |
| password | VARCHAR(255) | Hashed password for secure authentication (store hashed value, not plain text). |
| bio | TEXT | Optional user biography or description. |
| profile_picture | VARCHAR(255) | Optional URL path to the user's profile picture. |


## BlogEntry Table

| Field Name | Data Type | Description |
|---|---|---|
| post_id | INT | Unique identifier (Primary Key) for each blog post. |
| user_id | INT, Foreign Key | References the user who wrote the post (user_id in Users table). |
| title | VARCHAR(255) | Title of the blog post. |
| content | TEXT | The main content of the blog post (consider using a rich text format). |
| created_at | DATETIME | Date and time the post was created. |
| updated_at | DATETIME | Date and time the post was last updated. |
| is_published | BOOLEAN | Flag indicating if the post is publicly visible (True/False). |


## Tags Table (Optional)

| Field Name | Data Type | Description |
|---|---|---|
| tag_id | INT | Unique identifier (Primary Key) for each tag. |
| name | VARCHAR(255), Unique | Name of the tag category (must be unique). |



**Relationships:**

- One user can have many posts (One-to-Many)
- One post belongs to one user (Many-to-One)
- One post can have many tags (Many-to-Many) (Optional) - Requires the Post_Tags table
- One tag can belong to many posts (Many-to-Many) (Optional) - Requires the Post_Tags table
- One post can have many comments (One-to-Many) (Optional)
- One comment belongs to one post (Many-to-One) (Optional)

**Improvements:**

- Added an optional Tags table and Post_Tags table for categorizing posts with tags (Many-to-Many relationship).
- Clarified data types for some fields.

## Data Encoding:

**Encoding Method:**

- Text data like titles, content, and usernames should be encoded using UTF-8 for maximum compatibility.
- Images or binary data embedded within the post might require Base64 encoding for safe storage within the chosen data format (relational database or JSON).
