Things we need to do:
1) Create the API and undertand how it works.
2) When app start ups, make a request to API to get the current list of books.
3) When user Create/Edit/Delete a book, update the API and then update the local data.

JSON server setup:
1) Install JSON-server with NPM at the terminal
2) Create db.json file. This is where data will be stored
3) Create a command to run a JSON-Server
4) Run the command

Run the application:
Two commands to start project - 
1) `npm start` - Start the React Dev server
2) `npm run json-server` - Starts JSON-Server

*1. How API works: *
| Goal | URL | Method | Request Body | Response Body |
|---|---|---|---|---|
| **Create Book** | localhost:3001/books | POST | `{"title": "Harry Potter"}` | `{"id": 1, "title": "Harry Potter"}` |
| **Get All Books** | localhost:3001/books | GET | - | `[{"id": 1, "title": "Harry Potter"}]` |
| **Update Book** | localhost:3001/books/1 | PUT | `{"id": 1, "title": "Rich Dad, Poor Dad"}` | `{"id": 1, "title": "Rich Dad, Poor Dad"}` |
| **Delete Book** | localhost:3001/books/1 | DELETE | - | `{"id": 1, "title": "Harry Potter"}` |

3. Create/Edit/Delete a book, update the API and then update the local data
   install `axios`

   App.js

```javascript
   import axios from 'axios';

   const createBook = async(title) => {
		const response = await axios.post('http://localhost:3001/books', {
			title
		});

		const updatedBooks = [
			...books,
			response.data
		];
		setBooks(updatedBooks);
	}
```
