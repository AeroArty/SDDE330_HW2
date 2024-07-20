## Data Model Definition:
Data model selection: Relational
Justification: The listing of blog posts is relatively structured. There will be a listing of blog entries that can be identified using unique IDs and each blog entry must have a title, content, author/user information, creation time, update time, etc. Information about the author and the BlogEntry can be stored in different tables since each blog entry may have different authors. 
**Tables/Collections:**

## Author Table

| Field Name | Data Type | Description | Encoding |
|---|---|---|---|
| user_id | INT | Unique identifier (Primary Key) for each user. | N/A |
| username | VARCHAR(255), Unique | User's chosen username for login (must be unique). | UTF-8 |
| email | VARCHAR(255), Unique | User's email address (must be unique). | UTF-8 |
| password | VARCHAR(255) | Hashed password for secure authentication (store hashed value, not plain text). | N/A (hashed value) |
| bio | TEXT | Optional user biography or description. | UTF-8 |
| profile_picture | VARCHAR(255) | Optional URL path to the user's profile picture. | UTF-8 (URL) |

## BlogEntry Table

| Field Name | Data Type | Description | Encoding |
|---|---|---|---|
| post_id | INT | Unique identifier (Primary Key) for each blog post. | N/A |
| user_id | INT, Foreign Key | References the user who wrote the post (user_id in Author table). | N/A |
| title | TEXT | Title of the blog post. | UTF-8 |
| subtitle | TEXT | Optional subtitle for blog post. | UTF-8 |
| blurb | TEXT | Summary content of the blog post. | UTF-8 |
| content | TEXT | The main content of the blog post (consider using a rich text format). | UTF-8 |
| time_created | DATETIME | Date and time the post was created. | N/A |
| time_updated | DATETIME | Date and time the post was last updated. | N/A |
| is_published | BOOLEAN | Flag indicating if the post is publicly visible (True/False). | N/A |

## Tags Table (Optional)

| Field Name | Data Type | Description | Encoding |
|---|---|---|---|
| tag_id | INT | Unique identifier (Primary Key) for each tag. | N/A |
| name | VARCHAR(255), Unique | Name of the tag category (must be unique). | UTF-8 |


**Relationships:**

- One Author can have many BlogEntry (One-to-Many)
- One BlogEntry belongs to one Author (Many-to-One)
- One BlogEntry can have many Tags (Many-to-Many) (Optional)
- One Tag can belong to many BlogEntry (Many-to-Many) (Optional)

## Data Encoding:

### Blog Entry Structure
Using JSON, the blog entry structure looks like this:
```JSON
{
  "post_id": NUMBER, //Unique BlogEntry id for a given post
  "title": "STRING", // Title of the blog post
  "subtitle": "STRING", // Optional subtitle of the blog post
  "blurb": "STRING", // Optional short blurb of the blog post
  "content": "STRING", // Main content of the post (consider using a rich text format)
  "author": {
    "user_id": NUMBER, // ID of the user who wrote the post (references Users table)
    "username": "STRING" // Username of the author
  },
  "tags": [ "STRING", ... ], // Array of tag names (optional)
  "time_created": "STRING", // Date and time the post was created (consider ISO 8601 format: YYYY-MM-DDTHH:mm:ssZ)
  "time_updated": "STRING", // Date and time the post was last updated (consider ISO 8601 format)
  "is_published": BOOLEAN  // Flag indicating if the post is publicly visible
}
```

**Encoding Method:**
- Text data like titles, content, and usernames should be encoded using UTF-8 for maximum compatibility.
- Images or binary data embedded within the post might require Base64 encoding for safe storage within the chosen data format (relational database or JSON).
