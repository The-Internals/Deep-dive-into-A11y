# Focus only on keyboard navigation

```js
componentDidMount() {
  //set state to `true` on TAB key press events
  keyShortcuts.bind(['tab'], () => {
    this.setState({ keyBoardActive: true });
  });

  //set state to `false` on mousedown events
  document.addEventListener('mousedown', () => {
    this.setState({ keyBoardActive: false });
  });



  //root level
  <body className={this.state.keyBoardActive ? 'keyboard-active': ''}>
    ...
  </body>
```

```css
a:focus {
  outline: none;
}
.keyboard-active a:focus {
  outline: 3px solid blue;
}
```
