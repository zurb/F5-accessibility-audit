# JavaScript Overrides

# General
- Toggle  aria-values such as `aria-expanded` and `aria-show` through a general
  helper method (`toggleAriaValue`) to keep if/else clauses to a minimum
  toggled with the opening and instantiation of the core functionality of all
  components.

## Reveal
- If an element has [data-reveal] and isn't a dialog, create a dialog element
  from its contents, attach the new dialog to the DOM, and remove the faux
  dialog
- `showModal` used instead of `open()` to reveal the component since dialog has
  that built in to show the dialog and address accessibility concerns with dialog-like elements to meet WCAG 2.0 standards (i.e, nothing but the dialog shouldbe focusable when the dialog element is active))
  - Ideally with `showModal?` (Coffee)—or the native equivalent through
    condition checking-we could fallback to the original custom `open` event)
- on `keypress.escape`(jQuery) or the respective keycode equivalent, the modal
  should be close

- <del>Shift combined with Escape Should Combined</del> Escape key should used to close the dialog

  ```javascript
  let dialog  = document.querySelector("[data-reveal]");
  // Function should **NOT** be passed in anonymously for testing and callback purposes.
  window.addEventListener('keyup', function(e){
    // keyCode 27 is escape
    if (e.keyCode == 27){
      dialog.close();
    }
  });
  ```
## Clearing
- The generated modal Clearing creates should be a dialog; for caching, an
  if/else condition and/or a flag can be used to not have to reflow and repaint
    continously for later instantiations of the Clearing.
- The aria values outlined in the document that are toggleable should be in fact
  alternating true and false when an activated modal happens
- The wrapper with the main image of an activated modal, should have
  `aria-live="assertive"` & `role="status"`

## Tabs
- `aria-selected`, `aria-hidden`, and other toggle aria-values outlined in the
annotated components HTML file should be activated and accounted for throughout
this component's use by the user.
- left and right arrow keys should be used to alternate between the next and
  previous tabs.
- `tabindex=0` should be used on the active tab and `tabindex=-1` should be used for adjacent tabs; `focus()` should be used to go to the next and previous tabs for an element.
- <kbd>Shift</kbd>+<kbd>Tab</kbd> should be used to switch back to a tab after
  tabbing or navigating through its inner content.

  ```javascript
  let tab  = document.querySelector(".test");
  // Function should **NOT** be passed in anonymously for testing and callback purposes.
  window.addEventListener('keyup', function(e){
    // keyCode 27 is escape
    if (e.keyCode == 27){
      if (e.shiftKey){
        console.log("The tab currently active should be focused w/ `focus()` and previous initialization of the elements get them working");
        // tab.focus()
      }
    } else {
      console.log("e.keyCode not correct");
    }
    });
  ```
