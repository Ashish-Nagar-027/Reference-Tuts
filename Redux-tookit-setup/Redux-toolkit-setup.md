# Redux toolkit setup in react in few steps

## step 1 : Installations

![alt](./redux-toolkit/redux%20step%201%20and%202.png)

```
npm install @reduxjs/toolkit react-redux
```

<br>

## Step 2 : Create a Redux Store in new file.

The path can be :- src/app/store.js

```

import { configureStore } from '@reduxjs/toolkit';


export default configureStore({
  reducer: {},
});

```

## step 3 : include the store in app.js parent

![alt](./redux-toolkit/include%20store%20in%20app.png)

```

//...

import { Provider } from 'react-redux';
import store from './app/store';


  <Provider store={store}>
    <App />
  </Provider>

// ...
```

## step 4 : create a Redux state slice

path can be : src/features/pathFolder/slicenameSlice.js
set name , initialState, and reducers like below code
![alt](./redux-toolkit/create%20slice.png)

```
import { createSlice } from '@reduxjs/toolkit';


export const todoSlice = createSlice({
  name: 'addTodo',
  initialState: [],
  reducers: {
    addTodo: (state, action) => {
      const todo = {
        id: uuid(),
        text: action.payload,
      };

      state.push(todo);
  },
}});


// this is for dispatch
export const { addTodo } = todoSlice.actions;

// this is for selecting or subscribing
export const selectTodos = (state) => state.addTodo.value;


// this is for configureStore
export default todoSlice.reducer;

```

## step 5 : Add this slice to store

![alt](./redux-toolkit/add%20slice%20to%20store.png)

```

import { configureStore } from '@reduxjs/toolkit';
import todoReducer from '../features/todo/todoSlice';


export default configureStore({
  reducer: {
    todos: todoReducer,
    //give key name same as you have given name in slice file
  },

})

```

## step 6 : Now we can use useSelector and useDispatch Hooks for getting and setting values in any file of app .

### useSelector

![alt](./redux-toolkit/implement%20useselector.png)

```
import { useSelector } from 'react-redux';

// for selecting values of store slice
const todos = useSelector((state) => state.todos);

           or

// if you have already given selected values in  slice  just like i did there use . you have to import it like first
import selectTodos from '../ slice path  here'

const todos = useSelector(selectTodos);


```

### usedispatch

![alt](./redux-toolkit/useDispathc%20implement.png)

```
import { useDispatch } from 'react-redux';
import { addTodo } from '../features/todos/todosSlice';

// now you can use dispatch function

   dispatch(addTodo(text));


// dispatch is a function make sure you invoke it
```
