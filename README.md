App Phases:
1. Local, non-persisted list of books ([#1](https://github.com/rajlanjewar01/react-books/commit/745f6b60017f40b57ca9a823b1d679856f67ee96))
2. List of books persisted with outside API (https://github.com/rajlanjewar01/react-books/pull/2/)
3. Outside API + centralized store (https://github.com/rajlanjewar01/react-books/pull/4/)
4. Notable changes:

   Deploying json-server to hosting platform with Render.com [https://github.com/rajlanjewar01/react-books/pull/5]


**List of books persisted with outside API**

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

*1. **How API works**: *
| Goal | URL | Method | Request Body | Response Body |
|---|---|---|---|---|
| **Create Book** | localhost:3001/books | POST | `{"title": "Harry Potter"}` | `{"id": 1, "title": "Harry Potter"}` |
| **Get All Books** | localhost:3001/books | GET | - | `[{"id": 1, "title": "Harry Potter"}]` |
| **Update Book** | localhost:3001/books/1 | PUT | `{"id": 1, "title": "Rich Dad, Poor Dad"}` | `{"id": 1, "title": "Rich Dad, Poor Dad"}` |
| **Delete Book** | localhost:3001/books/1 | DELETE | - | `{"id": 1, "title": "Harry Potter"}` |

3. **Create/Edit/Delete a book, update the API and then update the local data**

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

2.  **On App startup make a request to API to get the current list of books**

**useEffect**
- Function that we import from React
- Used to run code when a component is **initailly rendered** and (sometimes) **when it is** _rerendered_

```javascript
useEffect(() => {
	console.log('Hi!');
}, [])
```
- First argument is a function that contains code we want to run
- Second argument is an array or nothing - this contains whether the function is executed on rerenders

- **Variations of `useEffect`**

Video notes: https://xxx.udemy.com/course/react-redux/learn/lecture/34694682#content

Practice code: https://www.codepen.io/sgrider/pen/BarEowz

1) With argument

```
  useEffect(() => {
	console.log('Hi!');
  }, [])
```
  i) Second argument is []

  ii) Called after **first render**

  iii) Never called again

  2) No argument

  ```
     useEffect(() => {
		console.log('Hi!');
     })
  ```

i) Second argument is -

ii) Called after **first render**

iii) Also called after **every rerender**

3) With argument and value

```
useEffect(() => {
	console.log('Hi!');
}, [counter])
```
i) Second argument is [ counter]

ii) called after first render

iii) Also called after rerenders if 'counter' variable changed
