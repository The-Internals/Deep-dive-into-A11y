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

  // get all focusable elements inside modal
  const focusableElementsInDialog = this.modalRef.querySelectorAll(
    FOCUSABLE_ELEMENTS
  );

  // get first and last focusable element
  if (focusableElementsInDialog && focusableElementsInDialog.length) {
    firstFocusableElement = focusableElementsInDialog[0];
    lastFocusableElement =
      focusableElementsInDialog[focusableElementsInDialog.length - 1];
  }

  // cycle on focusable elements within modal.
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
