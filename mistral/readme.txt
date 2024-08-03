
Here’s a `README.txt` file for your notebook that provides a clear overview of its purpose, instructions, and usage:

---

# README

## Overview

This notebook demonstrates how to convert natural language queries into SQL queries using a prompt template with the Mistral client. The notebook includes a schema for a movie database and provides examples of how natural language queries are transformed into SQL queries. 

## Schema

The database schema consists of three tables:

- **Movies Table**
  - `movie_id`: Integer, Primary Key
  - `title`: String
  - `genre`: String
  - `release_year`: Integer
  - `rating`: Decimal (3,1)
  - `director`: String

- **Actors Table**
  - `actor_id`: Integer, Primary Key
  - `name`: String
  - `birth_year`: Integer

- **Cast Table**
  - `movie_id`: Integer, Foreign Key (Movies)
  - `actor_id`: Integer, Foreign Key (Actors)
  - `role`: String

## Examples

**Example 1:**
- **Input:** "List all movies released in 1993."
- **SQL Query:** `SELECT title FROM Movies WHERE release_year = 1993;`

**Example 2:**
- **Input:** "Find the names of actors who starred in the movie 'Jurassic Park'."
- **SQL Query:** `SELECT Actors.name FROM Actors JOIN Cast ON Actors.actor_id = Cast.actor_id JOIN Movies ON Cast.movie_id = Movies.movie_id WHERE Movies.title = 'Jurassic Park';`

## Instructions

1. **Install the Mistral Client Library:**
   Ensure that the Mistral client library is installed. You can install it using:
   ```bash
   pip install mistral
   ```

2. **Initialize the Mistral Client:**
   Replace `'your_mistral_api_key'` in the provided Python code with your actual Mistral API key.

3. **Define the Natural Language Query:**
   Update the `user_query` variable in the code snippet with the natural language query you wish to convert into SQL.

4. **Run the Code:**
   Execute the notebook to see the natural language query converted into SQL. The result will be printed as output.

## Code Snippet

```python
from mistral import MistralClient

# Initialize Mistral client with your API key
client = MistralClient(api_key='your_mistral_api_key')

# Define your prompt template
prompt_template = """
I have a database with the following schema:

**Movies Table**
- movie_id: Integer, Primary Key
- title: String
- genre: String
- release_year: Integer
- rating: Decimal (3,1)
- director: String

**Actors Table**
- actor_id: Integer, Primary Key
- name: String
- birth_year: Integer

**Cast Table**
- movie_id: Integer, Foreign Key (Movies)
- actor_id: Integer, Foreign Key (Actors)
- role: String

Please convert the following natural language query into SQL:

**Example 1:**
- **Input:** "List all movies released in 1993."
- **SQL Query:** SELECT title FROM Movies WHERE release_year = 1993;

**Example 2:**
- **Input:** "Find the names of actors who starred in the movie 'Jurassic Park'."
- **SQL Query:** SELECT Actors.name FROM Actors JOIN Cast ON Actors.actor_id = Cast.actor_id JOIN Movies ON Cast.movie_id = Movies.movie_id WHERE Movies.title = 'Jurassic Park';

**Natural Language Query:**
- {user_query}
"""

# Define the natural language query
user_query = "List all movies released in 2002."

# Format the prompt with the user's query
formatted_prompt = prompt_template.format(user_query=user_query)

# Request completion from Mistral
response = client.complete(prompt=formatted_prompt)

# Print the SQL query returned by Mistral
print(response['choices'][0]['text'])
```

## Contact

For any issues or questions, please contact [your_email@example.com].

---

Feel free to adjust the contact details or any other information as needed.
