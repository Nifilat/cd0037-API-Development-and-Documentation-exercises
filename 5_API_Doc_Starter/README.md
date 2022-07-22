## Getting started

The Bookshelf API is organized around REST. Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

-Base URL
The website has not been deployed yet but runs locally. The default server is:
https://127.0.0.1:5000

## Error Handling

Errors are rendered in json format.
Sample:
{
"success": False,
"error": 400,
"message": "bad request"
}

### Error types

- 400: Bad Request
- 404: Resource Not Found
- 422: Unprocessable

### Endpoint Library

#### GET /books

- Overview:
  - Returns a list of book objects, success value, and total number of books
  - Results are paginated in groups of 8. Include a request argument to choose page number, starting from 1.
- Sample: `curl http://127.0.0.1:5000/books`
  Response:
  {
  "books": [
  {
  "author": "Lisa Halliday",
  "id": 2,
  "rating": 4,
  "title": "Asymmetry: A Novel"
  },
  {
  "author": "Kristin Hannah",
  "id": 3,
  "rating": 4,
  "title": "The Great Alone"
  },
  {
  "author": "Tara Westover",
  "id": 4,
  "rating": 5,
  "title": "Educated: A Memoir"
  },
  {
  "author": "Jojo Moyes",
  "id": 5,
  "rating": 1,
  "title": "Still Me: A Novel"
  },
  {
  "author": "Leila Slimani",
  "id": 6,
  "rating": 1,
  "title": "Lullaby"
  },
  {
  "author": "Amitava Kumar",
  "id": 7,
  "rating": 5,
  "title": "Immigrant, Montana"
  },
  {
  "author": "Gina Apostol",
  "id": 9,
  "rating": 5,
  "title": "Insurrecto: A Novel"
  },
  {
  "author": "Tayari Jones",
  "id": 10,
  "rating": 5,
  "title": "An American Marriage"
  }
  ],
  "success": true,
  "total_books": 16
  }

#### POST /books

- Overview:
  - Creates a new book with the specified title, author and rating
  - Returns the id of the created book, success value, total books, and book list based on current page number to update the frontend.
- Sample: `curl http://127.0.0.1:5000/books?page=3 -X POST -H "Content-Type: application/json" -d '{"title":"Anansi Boys", "author":"Neil Gaiman", "rating":"5"}'`
  Response:
  {
  "books": [
  {
  "author": "Lisa Halliday",
  "id": 2,
  "rating": 4,
  "title": "Asymmetry: A Novel"
  },
  {
  "author": "Kristin Hannah",
  "id": 3,
  "rating": 4,
  "title": "The Great Alone"
  },
  {
  "author": "Tara Westover",
  "id": 4,
  "rating": 5,
  "title": "Educated: A Memoir"
  },
  {
  "author": "Jojo Moyes",
  "id": 5,
  "rating": 1,
  "title": "Still Me: A Novel"
  },
  {
  "author": "Leila Slimani",
  "id": 6,
  "rating": 1,
  "title": "Lullaby"
  },
  {
  "author": "Amitava Kumar",
  "id": 7,
  "rating": 5,
  "title": "Immigrant, Montana"
  },
  {
  "author": "Gina Apostol",
  "id": 9,
  "rating": 5,
  "title": "Insurrecto: A Novel"
  },
  {
  "author": "Tayari Jones",
  "id": 10,
  "rating": 5,
  "title": "An American Marriage"
  }
  ],
  "created": 29,
  "success": true,
  "total_books": 17
  }

#### DELETE /books/{book_id}

- General:
  - Deletes the book of the given ID if it exists. Returns the id of the deleted book, success value, total books, and book list based on current page number to update the frontend.
- Sample: `curl -X DELETE http://127.0.0.1:5000/books/16?page=2`
- Response:
  {
  "books": [
  {
  "author": "Jordan B. Peterson",
  "id": 11,
  "rating": 5,
  "title": "12 Rules for Life: An Antidote to Chaos"
  },
  {
  "author": "Kiese Laymon",
  "id": 12,
  "rating": 1,
  "title": "Heavy: An American Memoir"
  },
  {
  "author": "Emily Giffin",
  "id": 13,
  "rating": 4,
  "title": "All We Ever Wanted"
  },
  {
  "author": "Jose Andres",
  "id": 14,
  "rating": 4,
  "title": "We Fed an Island"
  },
  {
  "author": "Rachel Kushner",
  "id": 15,
  "rating": 2,
  "title": "The Mars Room"
  },
  {
  "author": "Sandra Thorne",
  "id": 25,
  "rating": 5,
  "title": "The Hating Game"
  },
  {
  "author": "Chimamanda",
  "id": 28,
  "rating": 2,
  "title": "Nearly all men in Lagos are mad"
  },
  {
  "author": "Neil Gaiman",
  "id": 29,
  "rating": 5,
  "title": "Anansi Boys"
  }
  ],
  "deleted": 16,
  "success": true,
  "total_books": 16
  }

#### PATCH /books/{book_id}

- General:
  - If provided, updates the provided attribute of the specified book. Returns the success value and id of the modified book.
- Sample: `curl http://127.0.0.1:5000/books/15 -X PATCH -H "Content-Type: application/json" -d '{"rating":"4"}'`
- Response:
  {
  "id": 15,
  "success": true
  }
