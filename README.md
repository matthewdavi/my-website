# My website

I made a website for myself, no javascript on the client. Used astro.

Cool thing about it is the ThemeToggle that only uses css, no javascript. It's kinda like the [CSS Zen Garden](https://csszengarden.com/). 

If you want to see how the ThemeToggle works, check out the [Theme Selector Astro Component](https://github.com/matthewdavi/my-website/blob/main/src/components/ThemeSelector.astro). I do a bunch of tricks with the css variables and set them dynamically based on the state of the theme selector, which is actually just a radio button. This runs some JavaScript (at BUILD TIME ONLY) to generate the markup, but if you disable JavaScript in your browser you'll see the site doesn't actually use any to run. I like Astro because JSX is a great templating language, maybe even the best we have. I would like to see people clinging to Handlebars try to recreate this in a way that's as reusable as what Astro gives you.

Here's an AI generated summary of how this thing works:

## CSS Tricks Used in the Theme Selector

* **CSS Variables**: Using CSS custom properties to define theme values that can be changed dynamically
* **:has() Selector**: Using this powerful selector to detect when a specific radio button is checked and apply styles accordingly
* **:focus-within**: Opening the dropdown menu when the container receives focus
* **tabindex Attribute**: Making non-interactive elements focusable to control the dropdown state
* **Hidden Radio Buttons**: Using visually hidden radio inputs to store the selected theme state
* **Overlay Technique**: Creating an invisible overlay that captures clicks outside the dropdown to close it
* **CSS-only Animations**: Animating the dropdown arrow and gradient background without JavaScript
* **Dynamic Style Generation**: Using Astro's server-side rendering to generate theme-specific CSS at build time
* **Mobile-friendly Interactions**: Making the dropdown work on touch devices without any JavaScript handlers

## How Radio Buttons Control Theme Variables

The magic behind the theme switching happens through a clever combination of hidden radio inputs and the CSS `:has()` selector. Here's how it works:

1. Each theme option has a hidden radio input with a unique ID (like `theme-serif` or `theme-hacker`)
2. At build time, Astro generates CSS rules for each theme using the `generateThemeSelectionCSS()` function
3. These rules use the pattern `:root:has(#theme-X:checked)` to detect when a specific theme's radio button is checked
4. When a radio button becomes checked (by clicking its label), the matching CSS rule applies that theme's variables to the `:root` element
5. For example, when the "Hacker" theme is selected, rules like this activate:
   ```css
   :root:has(#theme-hacker:checked) {
     --color-background: #0d0d0d;
     --color-text-primary: #33ff33;
     /* other variables */
   }
   ```
6. The site's components are styled using these variables (like `color: var(--color-text-primary)`)
7. When the variables change, all styled elements instantly update to reflect the new theme
8. No JavaScript events or handlers are needed - it's all handled by the CSS cascade

This approach leverages the global nature of CSS custom properties and the power of the `:has()` selector to create a complete theming system without any client-side JavaScript.
