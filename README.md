# About
This project was intended to learn about programming in the Svelte 
framework, and demonstrate my current skills.

It is a to-do demonstration knowledge of transitions, components 
and data-flow.


# What I learned
- Information about 2 way bindings (`bind:`)
  - I ran into a bug with 2 way bindings while to flip a
  boolean value in a component. 
  I later learned how to fix the issue, but decided it was 
  simpler to store the end value in the parent

- Functions are defined differently inside objects
  - Specifically, they can be defined without the `function`
  keyword
  - I learned this through researching the `fallback()` 
  method for the crossfade transition

- How to use `{#each}` blocks, and how it functions 
differently when a key is provided
  - There was an issue with transitions not working correctly, 
  which was later fixed by providing the `{#each}` block with 
  a key

- How to use svelte transitions


# Quickstart
`git clone` this repository, `cd` into it then `npm install`
dependencies.


# Known bugs

