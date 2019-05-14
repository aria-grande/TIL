# Copy to clipboard via js

```js
navigator.clipboard.writeText(window.location.href)
.then(() => {
   alert("Copied the text!");
})
.catch(err => {
  // This can happen if the user denies clipboard permissions:
  console.error('Could not copy text: ', err);
});
```
