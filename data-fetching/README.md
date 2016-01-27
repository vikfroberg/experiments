# Data fetching

## Experiment #1

- [x] Sequential appending fetch with argument
- [x] Sequential replacing fetch with argument
- [x] Sequential mutations with argument
- [x] Optimistic pesimistic updates
- [ ] Latest replacing fetch with argument

```js
const usersQuery = User.createSequentialQuery({ company_id: 15})
usersQuery.subscribe(result => {
  setState({ users: { isLoading: result.isLoading, users: result.items, error: result.error } })
})

const addUserMutation = User.createSequentialMutation('add')
addUserMutation.subscribe(result => {
  setState({ userMutation: { isLoading: result.isLoading, user: result.item, error: result.error } })
})

usersQuery.append(3)
// { users: { isLoadig: true, items: [], error: undefined } } 
// .... 
// { users: { isLoadig: false, items: [User, User, User], error: undefined } }

addUserMutation.dispatch({ name: 'Viktor', company_id: 15 })
// { userMutation: { isLoadig: true, item: undefined, error: undefined } }
// { users: { isLoadig: false, items: [OptimisticUser, User, User, User], error: undefined } }
// ....
// { userMutation: { isLoadig: false, item: User, error: undefined } }
// { users: { isLoadig: false, items: [User, User, User, User], error: undefined } }

usersQuery.append(8)
// { users: { isLoadig: true, items: [User, User, User, User], error: undefined } }
// ....
// { users: { isLoadig: false, items: [User, User, User, User, User, User, User, User], error: undefined } }

usersQuery.replace(8)
// { users: { isLoadig: true, items: [User, User, User, User, User, User, User, User], error: undefined } }
// ....
// { users: { isLoadig: false, items: [User, User, User, User, User, User, User, User], error: undefined } }
```
