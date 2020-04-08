# Vuex fork

> ## Add support for the `meta` field in mutations as stated in the [November 3rd 2017's PR](https://github.com/vuejs/vuex/pull/1043)

# Additions

There may be times when your plugin needs to know more information about a mutation in order to decide what kind of action to take. In order to pass this 'meta' information to the plugin, the user can supply the meta property to the options argument on a commit: commit(TYPE, payload, { meta: { cache: true } }). This meta information is passed along with the type and payload to the subscribe function:

You can commit mutations by passing a `meta` field in its options:

```javascript
commit("myMutation", "value", { meta: { someMetadataField: true } });
```

Then when you subscribe to store mutations in a plugin:

```javascript
const myPlugin = (store) => {
  // called when the store is initialized
  store.subscribe((mutation, state) => {
    // The mutation comes in the format of `{ type, payload, meta }`.
    if (mutation.meta.someMetadataField) {
      // do stuff
    }
  });
};
```

## License

[MIT](http://opensource.org/licenses/MIT)
