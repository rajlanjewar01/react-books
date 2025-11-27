1) Create context file: 
src/context/books.js

```
import { createContext } from 'react';
const BooksContext = createContext();
export default BooksContext;
```

2) Define in main root index.js

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import BooksContext from './context/books';

const el = document.getElementById('root');
const root = ReactDOM.createRoot(el);

root.render(
   <BooksContext.Provider value={5}>
        <App />
    </BooksContext.Provider>
);
```

3) Use in component:

```
import { useContext } from 'react';
import BooksContext from '../context/books';
import BookShow from './BookShow';

function BookList({books, onDelete, onEdit}) {
	const value = useContext(BooksContext);

	const renderedBooks = books.map((book) => {
		return <BookShow onEdit={onEdit} onDelete={onDelete} key={book.id} book={book} />;
	});

	return (
		<div className="book-list">
			context value - {value}
			{renderedBooks}
		</div>
	);
```
