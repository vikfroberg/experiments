# Data fetching

## Experiment #1

```js
const usersQuery = Store.createUsersQuery({ company_id: 15})
usersQuery.subscribe(result => {
  setState({ isLoading: result.isLoading, users: result.items, error: result.error })
})

// How to handle pesimistic update if it failed?
const newUserMutation = Store.createNewUserMutation()
newUserMutation.subscribe(result => {
  setState({ isLoading: result.isLoading, user: result.item, error: result.error })
})

usersQuery.fetch(3)
// { isLoadig: true, items: [], error: undefined } 
// .... 
// { isLoadig: false, items: [User, User, User], error: undefined }

newUserMutation.dispatch({ name: 'Viktor' })
// { isLoadig: false, items: [newUser, User, User, User], error: undefined }

usersQuery.fetch(8)
// Uses flatMap in backend which makes it sequential
// { isLoadig: true, items: [newUser, User, User, User], error: undefined }
// ....
// { isLoadig: false, items: [newUser, User, User, User, User, User, User, User], error: undefined }
```
