# Data fetching

## Experiment #1

```js
const usersQuery = Store.createUsersQuery({ initialCount: 3, company_id: 15})
usersQuery.subscribe(result => {
  setState({ isLoading: result.isLoading, users: result.items, error: result.error })
})
// { isLoadig: true, items: [], error: undefined } 
// .... 
// { isLoadig: false, items: [User, User, User], error: undefined }

Store.dispatch(newUserMutation)
// { isLoadig: false, items: [newUser, User, User, User], error: undefined }


usersQuery.setCount(8)
// { isLoadig: true, items: [newUser, User, User, User], error: undefined }
// ....
// { isLoadig: false, items: [newUser, User, User, User, User, User, User, User], error: undefined }
```
