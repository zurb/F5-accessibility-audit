# Accessibility Audit
The following is guidelines and tips to consider with the pending upheaval of
Foundation to be more accesibile out-of-the-box

## Tips I’m seeing
Follow the three rules of ARIA
Change .button to button and a 
Change disabled to [disabled] , style to use:  [disabled], a:not([href]) 
“ Links without hrefs, like buttons which include disabled, do not and should not receive focus”
Buttons should never be left empty, there’s specific ways to meet this requirement we don’t meet yet (pg. 28) 
Our tooltips should show during hover *and* focus 
alt should read like what the label would read like as standard text; "it express the function, not a description of something someone can’t see" 

## General
- We must follow the three golden rules of ARIA at all times: http://www.w3.org/TR/aria-in-html/#first-rule-of-aria-use
- Everything must be accessible keyboard.
- We must seriously consider augmenting `progress`, `meter`, and `dialog` for
  the relevant components; on top of that we still must use `aria-notations` for
  maximum compatibility

- All components that churn out dynamic content, specifically post-page-load
  interactions should at least have `live-region` set to true for maximum
  compatibility with browsers FFS supports

- Any component that makes sense to be focusable and uses
  semantically-meaningless div containers should use `tab-index=-1`


## Visibility/Disabling
- Visiblity classes need to have or add `aria-hidden=true`
- Disability hidden on links is useless unless you remove the `href` value for
  accessibility; we may consider using a `data` attribute to then use to store
  and unstore an href's value.
- If some of our components need to be "disabled", they need the appropriate
  role value defined *and* which may in fact be role="button" (additional
  research required on my part); **a disabled class is useless outside of
  visually making it appear disabled; you must use the
  [disabled] attribute.

- with our display none calls, we should use aria-hidden as well.

## Tooltips
- We should use alt with tooltips to make it useable for keyboard users as well.
- `aria-describedby` for the tooltips' targets and the toggling of its `aria-hidden`
  value
- `role=tooltip` 

## Off-Canvas
- Must support the use of anchor tags and buttons to trigger offcanvas
- aria-expanded is needed for the button
- `aria-role = navigation` is needed for the navigation area
- `aria-hidden` is needed for the navigation area
- role = button has to be used the navigation anchor tag **and** aria-controls
  with the id passed of the navigation area
- navigation portion must be duplicated and visibiliy hidden at the bottom of
  the page for PE reasons
- We needed an `aria-label` sign for our hamburger sign. Daresay we may need to
  consider for Foundation for Apps or version 6 to add "menu"

## Icon-bar
- All the icons should use aria-label
- If text are needed for the icons, we need to give it an id to then pass into the
  icon bar's `aria-labeledy` attribute.

## Top Bar
- Same feedback as above with nested links having to be `[role=button]`,
  aria-expanded,  **and**
  `aria-controls` values that make sense.

# Reveal
- We must change reveal to listen for anchor tags with role=button and buttons

- If an anchor tag is used, we must annotate it with role=button

- We need to have `aria-hidden=false/`true pattern with the link
  be hidden with aria-hidden

- `aria-controls` have to be added to the link and the corresponding *id* used for
  the modal.

- Support `<dialog>` and the `show()`, `showModal()`, and `close()` methods. This
  includes supporting the open milestone.
  `(HTMLDialogElement)`

- `role=alertdialog` or `role=dialog` *must* be used. NO exception. For warning and
  errors, as well as the benefit of using `aria-live-regions` (`live-regions` get read aloud the moment they change), we should consider
  using by default and then have an accessibility section on the Foundation docs
  (an accessibility branch during the beta of Zurb Foundation 5.4/5.5) that also
  recommend (or a snippet) to use `role="dialog"` for scenarios where the
  `role=alertdialog` declaration would make the dialog box too powerful.

- `aria-describedby` is necessary in order for the dialog text to be respected
  as being associated with the dialog.

- While open, it *must* not be possible for other elements to be in focus. This
  is actually harder than it sounds. Heydon's recommendation from past work
  is aria-hidden & a custom class of visibility:hidden (elements retain their
  layout, so they don't "jump" back into place in an inelegant way after the
  dialog box is close)
  `$('body > *:not(dialog').addClass('mod-hidden'); `*

- We must return focus back to whatever triggered reveal;

## Magellan
- Magellan will be a somewhat hard component to make accessible.
- We must make sure the links
- We must add tabindex="-1" in order to make the things that Magellan transfers
  to focusable.
- Decide whether or not role="toolbar" better describes the behavior of Magellan
  or nav (research on my part)

## Toggler Bars
- Must have `aria-checked` and `aria-checked` if we allow non form element to have
  similar functionality.

- `aria-pressed`

## Range  Sliders
- `aria-valuemax`, `aria-valuemin`, `aria-valuenow` must be used
- `aria-valuetext` must be used if we're going to have visual text show what
  value is the range slider at any moment like some of our examples.

## Alert dialog
- `role=alertdialog` makes sense for these elements since they are important for
  the user to acknowledge before proceding further alone the document.
- Accordingly, this then focuses us to make sure we have JS to make sure other
  things aren't focusable until modals are  closed.

- We must allow escape to close the dialog.

## Panel
- N/A

## Typography
- We should have a section explaining that the "use h1 whereever now due to
  sectioning"" is no longer a recommendation

- A section of `aria-level` WAI-ARIA attribute must be created and accounted
  for.

## Joyride
- # Hardest one to get right; I'll have to think about this overnight.

## Progress bar
- Must get a `tab-index` value of -1 so it can be focused; it must then have a
  ``aria-label` or `aria-valuetext` to represent what what its percentage
  ultimately resolves to (I have to do research what works best for it)
- I have a hunch that `<progress>` has a `role` alternative to use since we're
  for some reason not using native `progress` elements to then style. My guess
    by using such a role + `aria-valuemax`, `aria-valuemin`, `aria-valuenow` can then be used, simplifying making our progress bars accessible.

## Tables
- Must use the role of `grid`

## Tabs
- Our tabs will likely have to slightly reengineed.
- Use `role=tablist`, `role=tabpanel` and  `role=tab` for the contianer of the links, for each tab
  link and indiviudal panels
  tabs.
- `aria-hidden` must be toggled true/false for each tab when they get focus.
- `aria-selected` must be used for the open tab
- Remove the default accessibilty features of `li`, `dl`, and so on to a special
  role dedicated for widgets such as tabs: `presentation`.
