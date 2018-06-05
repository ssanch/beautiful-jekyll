---

layout: post
title: Accessibility checklist
subtitle: I came up with a checklist of accessibility features that should be helpful in order to build accessible sites
gh-badge: [star, fork, follow]

## tags: [accessibility, html, checklist]

## WAI-ARIA Authoring Practices 1.1

If you are using/creating a custom element this is the first place to go in order to make sure the element will be accessible.

This is a document that describes considerations and recommends approaches to make widgets, navigation and behaviors accessible using roles, states and properties.

**Sticking to native HMTL tags as much as possible you will get accessible features for free.**

[WAI-ARIA Authoring Practices 1.1](https://www.w3.org/TR/wai-aria-practices-1.1/)

# Accessibility checklist

The list below outlines the development effort needed in order to make sure our code will result in accessible pages.

## General Checks

- [ ] Content has good color contrast


- [ ] Focus is properly managed and visible


- [ ] Controls have accessible labels

## Color Contrast

[WCAG 2.0](https://www.w3.org/TR/WCAG20/) **level AA** requires a contrast ratio of at least **4.5:1 for normal text** and **3:1 for large text**. **Level AAA** requires a contrast ratio of at least **7:1 for normal text** and **4.5:1 for large text**.

**Tools**

- [Webaim Color Contrast Checker](https://webaim.org/resources/contrastchecker/)

## Focus is properly managed and visible

To validate

- Tab order should follow the order of the visual layout from the top to the bottom of the screen

- Hidden elements should not be part of the accessibility tree. Find the `inert` section to see how to achieve this

- Focus cannot escape from widgets, dialogs or any other element where the user is supposed to choose an option before leaving (User must be able escape out of the web content area for security reasons)

**Tools**

- [ChromeLens](http://chromelens.xyz/) - Tracker feature
- Use your keyboard :)

## Acccessible Labels

All interactive controls should have labels associated. These labels describe the purpose of the control to screen readers. 

Considerations

- Descriptions must be brief

- Typically action verbs

- The `label` tag only works with form HTML native elements

- `arial-label``aria-labelledby``aria-describedby` are great options for elements where the label tag does not work

- Consider compound labels for interactive controls that by themselves do not offer a good descriptions of its purpose. See [Compound Labels](#compound-labels) section

Brief descriptions of controls. **Typically action verbs**.

**Tools**

- [Axe Core](https://axe-core.org/)
- [Google Chrome](https://developers.google.com/web/fundamentals/accessibility/) has a built-in feature that allows you to audit this

## `inert` attribute/property

## <a id="compound-labels">Compound Labels</a>

#### Screen Readers Software

- VoiceOver - Mac, IOS

- NVDA - Windows

- GTalk - Android
