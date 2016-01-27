# Data fetching

## Experiment #1

```js
const usersQuery = Store.createUsersQuery({ company_id: 15})
usersQuery.subscribe(result => {
  setState({ users: { isLoading: result.isLoading, users: result.items, error: result.error } })
})

// How to handle pesimistic update if it failed?
const newUserMutation = Store.createNewUserMutation()
newUserMutation.subscribe(result => {
  setState({ userMutation: { isLoading: result.isLoading, user: result.item, error: result.error } })
})

usersQuery.fetch(3)
// { users: { isLoadig: true, items: [], error: undefined } } 
// .... 
// { users: { isLoadig: false, items: [User, User, User], error: undefined } }

newUserMutation.dispatch({ name: 'Viktor' })
// { userMutation: { isLoadig: true, item: undefined, error: undefined } }
// { users: { isLoadig: false, items: [newUser, User, User, User], error: undefined } }
// ....
// { userMutation: { isLoadig: false, item: NewUser, error: undefined } }
// { users: { isLoadig: false, items: [User, User, User, User], error: undefined } }

usersQuery.fetch(8)
// Uses flatMap in backend which makes it sequential
// { users: { isLoadig: true, items: [newUser, User, User, User], error: undefined } }
// ....
// { users: { isLoadig: false, items: [newUser, User, User, User, User, User, User, User], error: undefined } }
```
