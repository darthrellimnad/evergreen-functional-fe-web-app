# evergreen-functional-web-site

Heres one way to do it.

1. Mental model of the FE is a simple system, which is linear, single threaded control flow.  Our diagram is an SVG, which is evergreen.
2. Mental model can be achieved using redux (evergreen) or any similar “Just JavaScript” evergreen library for event processing, state management, and UI updates 
3. Design System patterns can be created using JavaScript functions (or higher order functions) that return an html string.  Unlike React, these functions are primarily used to document static patterns and styles representing different states, intedended by standard library developers, unit testing, and documentation.  Visual regression and manual unit testing happens here.
4. Design system patterns or components can be tested w/ simple html files, or a tool like storybook. Global community can participate in testing.
5. Styles for patterns can be implemented w/ global css or modularized css, which can be used for the pattern library, as well as for web components.  Build systems and compilation may vary.
6. Web components or React components can reference (or “copy paste”) default html from pattern libraries and use the same css modules as patterns.  JS implementation and integration tests happen here. it's generally easier to use a functional reactive method for rendering html this way.
7. Static data can be imported with json modules 
8. Remote data can be fetched w/ standard fetch.
9. Html, JS, & CSS can all be hosted as static content or served via BE templates.
10. Static types are not evergreen on the web, so dynamic types can be used, along with jsverify (similar to quick check) inside of unit tests.  This approaches the same limit of quality as can be achieved w/ static types in a decoupled coupled system, accounting for desynchronization of BE apis are called. static types could also be provided as needed.
11. Desyncs happen when BE is updated before FE cache is clear.  This can happen while using either static types or dynamics c types.  See our canvas on VA slack channel for details about versioning.
12. UI Prototypes can created and shared with plain html or a tool like code pen.
13. Basic terminal can be used to make curl (or similar) calls in order to be used for testing API calls and designs integration logic on frontend.
14. Observable pattern can be used to simulate or mock async behavior (like fetch calls). Works real well with redux.
15. Just need a browser and text editor (and maybe terminal) to make real stuff.  Hosting may vary.
16. Make a test plan.
17. Learn your rudiments.

Many dyslexic and autistic programmers (or coders really) preffer functional and UI programming, but industry tends to discriminate.

If you want it, grit your teeth and learn it.

This book should be accessible for most: https://github.com/MostlyAdequate/mostly-adequate-guide
