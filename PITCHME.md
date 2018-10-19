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
  dispatch(fetchMyData(params));
}
```

@[1-4]
@[6-7]
@[9-14](In our app, we often map to `dispatch` in `connect` from `react-redux`)

---

### `cRA`: The Good

- Dispatches request action types for a given constant:
  - `DATA` => `DATA_REQUEST`, `DATA_SUCCESS`, `DATA_FAILURE`
- Updates related slices of state:
  - `isFetching`
  - `errors`
- Both of these patterns do not need to vary across different calls to `createRequestAction`.
