---
title: "Query Variables"
---

What is a variable in GraphQL context?
-------------------------------------
GraphQL has a first-class way to factor dynamic values out of the query, and pass them as a separate dictionary. These values are called variables. In our case, we are defining the object to be inserted as a mutation.

So let's define the graphql mutation to be used.

Open `src/components/Todo/TodoInput.js` and add the following code:

```javascript
import React from 'react';
+ import gql from 'graphql-tag';

+ const ADD_TODO = gql `
+  mutation ($todo: String!, $isPublic: Boolean!) {
+    insert_todos(objects: {title: $todo, is_public: $isPublic}) {
+      affected_rows
+      returning {
+        id
+        title
+        created_at
+        is_completed
+      }
+    }
+  }
+ `;

const TodoInput = ({isPublic=false}) => {
  return (
    <form className="formInput" onSubmit={(e) => {
      e.preventDefault();
    }}>
      <input
        className="input"
        placeholder="What needs to be done?"
      />
      <i className="inputMarker fa fa-angle-right" />
    </form>
  );
};

export default TodoInput;
```

What does this mutation do?
---------------------------
The mutation inserts into `todos` table with the $objects variable being passed as one todo type.

Awesome! We have defined our first graphql mutation.