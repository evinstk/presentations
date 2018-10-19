# Async Action Creators in Redux

Considerations for `createRequestAction`

---

### `cRA`: What does it do?

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
