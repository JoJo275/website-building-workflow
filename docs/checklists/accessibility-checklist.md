# Accessibility Checklist

Baseline accessibility checks every page should pass before launch.

- [ ] Page has semantic landmarks (`header`, `main`, `nav`, `footer`)
- [ ] Headings are ordered logically (no skipping levels)
- [ ] All interactive elements are keyboard accessible
- [ ] [Focus states](../glossary.md#focus-ring) are visible on all interactive elements
- [ ] Buttons use `<button>` elements
- [ ] Links use `<a>` elements
- [ ] Form labels are present and associated with inputs
- [ ] Error messages are programmatically associated with their inputs
- [ ] Colour contrast meets [WCAG](../glossary.md#wcag) AA (4.5:1 for text, 3:1 for large text)
- [ ] Images have useful `alt` text or are marked as decorative (`alt=""`)
- [ ] Modals trap focus when open and return focus on close
- [ ] Page is usable at 200% zoom

!!! info "Beyond the floor"
    This list is the minimum. For deeper coverage, run an automated audit
    with axe DevTools or Lighthouse and test with a screen reader on at
    least one critical flow.
