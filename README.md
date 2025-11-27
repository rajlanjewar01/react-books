Changing value in useContext:

1) update book context

src/context/books.js

```
import { createContext, useState } from 'react';

const BooksContext = createContext();

function Provider({ children }) {
	const [count, setCount] = useState(5);

	const  valueToShare = {
		count,
		incrementCount: () => {
			setCount(count + 1);
		},
	};

	return <BooksContext.Provider value={ valueToShare }>
		{ children }
	</BooksContext.Provider>
}

export { Provider }; // names export 
export default BooksContext; // default export
```

2) Declare Provider in main src/index.js

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { Provider } from './context/books';

const el = document.getElementById('root');
const root = ReactDOM.createRoot(el);

root.render(
	<Provider>
		<App />
	</Provider>
);
```

3) Use in src/components/BookList.js

```
import BookShow from './BookShow';

function BookList({books, onDelete, onEdit}) {
	const {count, incrementCount} = useContext(BooksContext);

	const renderedBooks = books.map((book) => {
		return <BookShow onEdit={onEdit} onDelete={onDelete} key={book.id} book={book} />;
	});

	return (
		<div className="book-list">
			context value - {count}
			<button onClick={incrementCount}>Increment</button>
			{renderedBooks}
		</div>
	);
}

export default BookList; 
```

