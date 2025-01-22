# smh-expo-persist-secure-store

smh-expo-persist-secure-store

This Package only helpful with the [redux-persist](https://www.npmjs.com/package/redux-persist) package only.

## Installation
```sh
npx expo install smh-expo-persist-secure-store
```

## Usage
Use as a `redux-persist` global storage engine

```js
import {createSecureStore} from "smh-expo-persist-secure-store";

import { createStore } from "redux";
import { persistStore, persistCombineReducers } from "redux-persist";
import reducers from "./reducers";

// Secure storage
const storage = createSecureStore();

const config = {
  key: "root",
  storage
};

const reducer = persistCombineReducers(config, reducers);

function configureStore() {
  // ...
  const store = createStore(reducer);
  const persistor = persistStore(store);

  return { persistor, store };
}

```

Use as an engine for only a reducer

```js
import {createSecureStore} from "smh-expo-persist-secure-store";

import { combineReducers } from "redux";
import { persistReducer } from "redux-persist";
import AsyncStorage from "redux-persist/lib/storage";

import { mainReducer, secureReducer } from "./reducers";

// Secure storage
const secureStorage = createSecureStore();

const securePersistConfig = {
  key: "secure",
  storage: secureStorage
};

// Non-secure (AsyncStorage) storage
const mainPersistConfig = {
  key: "main",
  storage: AsyncStorage
};

// Combine them together
const rootReducer = combineReducers({
  main: persistReducer(mainPersistConfig, mainReducer),
  secure: persistReducer(securePersistConfig, secureReducer)
});

function configureStore() {
  // ...
  let store = createStore(rootReducer);
  let persistor = persistStore(store);

  return { persistor, store };
}

```

And we're done 🎉
## Contributing

Contribution are always welcome, no matter how large or small !

We want this community to be friendly and respectful to each other.Please follow it in all your interactions with the project.

Please feel free to drop me a mail [S MUNI HARISH](mailto:samamuniharish@gmail.com?subject=[GitHub])

## Acknowledgements

Thanks to the authors of these libraries for inspiration

## Note

Inspired by [redux-persist-expo-securestore](https://github.com/Cretezy/redux-persist-expo-securestore#readme)

## Sponsor & Support

To keep this library maintained and up-to-date please consider [sponsoring it on GitHub](https://github.com/sponsors/smuniharish). Or if you are looking for a private support or help in customizing the experience, then reach out to me on Linkedin [@smuniharish](https://www.linkedin.com/in/smuniharish).

## License

[MIT](./LICENSE)

---

Made with ❤️
