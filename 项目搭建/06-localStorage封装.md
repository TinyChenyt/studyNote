# localStorage

```js
const set = (key, value, expirationTime) => {
  if (!key) {
    return;
  }

  if (value === undefined) {
    return;
  }

  if (value === null) {
    localStorage.removeItem(key);
    return;
  }

  if (expirationTime) {
    const expirationTimeStamp = new Date().getTime() + expirationTime;
    localStorage.setItem(key, JSON.stringify({ value, expirationTimeStamp }));
  } else {
    localStorage.setItem(key, JSON.stringify({ value, expirationTimeStamp: null }));
  }
};

const get = (key) => {
  if (!key) {
    return;
  }

  const item = localStorage.getItem(key);
  if (!item) {
    return;
  }

  const parsedItem = JSON.parse(item);
  if (parsedItem.expirationTimeStamp && parsedItem.expirationTimeStamp < new Date().getTime()) {
    localStorage.removeItem(key);
  }

  return parsedItem.value;
};

const del = (key) => {
  if (!key) {
    return;
  }

  localStorage.removeItem(key);
};

const delAll = () => {
  localStorage.clear();
};

export default { set, get, del, delAll };
```

