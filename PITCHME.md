# Async Action Creators in Redux

Considerations for `createRequestAction`

---

##### `cRA`: What does it do?

```js
// Signature
const createRequestAction = config => params => (dispatch, getState) => {
  /* communicates with API, dispatching actions along the way */
};

// Create an action creator
export const fetchMyData = createRequestAction({ /* ... */ });

// Where dispatch is available
componentDidMount() {
  const { dispatch, fetchMyData, ...params } = this.props;
  dispatch(fetchMyData(params)); // in our app, we often map to `dispatch` in `connect`
}
```

@[1-4]
@[6-7]
@[9-14]

---

### `cRA`: The Good

- Handles dispatching the three request-oriented action types for a given constant:
  - Given constant DATA, will dispatch DATA_REQUEST, DATA_SUCCESS, and DATA_FAILURE at appropriate points.
- Updates related slices of state:
  - isFetching: Boolean flag for constant is toggled over the course of the thunk’s execution.
  - errors: In the event of an error, the details are stored in the errors state slice. These details are cleared on the next execution of the thunk.
- Both of these patterns do not need to vary across different calls to createRequestAction, so it’s a good thing they are encapsulated.
