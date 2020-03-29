# Focus trapping in Dialog

```html
<dialog onOpen="{this.onOpen}" ... />
```

```js
onOpen = () => {
  keyShortcuts.bind(['tab'], this.onTab);
}

onTab(event) {
  if (!this.modalRef) { //or querySelector
    return;
  }

  const modal = this.modalRef;

  let firstFocusableElement = modal,
    lastFocusableElement = modal;

  const focusableElementsInDialog = this.modalRef.querySelectorAll(
    FOCUSABLE_ELEMENTS
  );

  if (focusableElementsInDialog && focusableElementsInDialog.length) {
    firstFocusableElement = focusableElementsInDialog[0];
    lastFocusableElement =
      focusableElementsInDialog[focusableElementsInDialog.length - 1];
  }

  let toFocusElement = null;
  if (event.shiftKey && document.activeElement === firstFocusableElement) {
    toFocusElement = lastFocusableElement;
  } else if (document.activeElement === lastFocusableElement) {
    toFocusElement = firstFocusableElement;
  }

  if (toFocusElement) {
    event.preventDefault();
    toFocusElement.focus();
  }
}
```
