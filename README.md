# evergreen-functional-web-site

Here's one way to do it.

1. Mental model of the FE is a simple system, which is linear, single threaded control flow.  Our diagram is an SVG, which is evergreen.
2. Mental model can be achieved using redux (evergreen) or any similar “Just JavaScript” library for event processing, state management, and UI updates.
3. Design System patterns can be created using JavaScript functions (or higher order functions) that return an html string, or they could be rendered by a server.  Unlike components, these patterns are primarily used to document static html and styles representing different UI states, intedended for standard library developers, unit testing, and documentation.  Visual regression and manual unit testing happens here.
4. Design system patterns and/or components can be tested w/ simple html files, or a tool like storybook. Global community can participate in testing.
5. Styles can be implemented w/ global css or modularized css, which can be used for the pattern library, as well as for web components.  Build systems and compilation may vary.
6. Web components or framework components can reference (or “copy paste”) default html from pattern libraries and use the same css modules as patterns.  JS implementation and integration tests happen here. It's often easier to use a functional reactive method for rendering html this way.
7. Static data can be imported with json modules 
8. Remote data can be fetched w/ standard fetch.
9. Html, JS, & CSS can all be hosted as static content or served via BE templates.
10. Static types are not evergreen on the web, so dynamic types can be used, along with jsverify (similar to quick check) inside of unit tests when using just javascript.  This can approach the same limit of quality as can be achieved w/ static types in a decoupled FE/BE system, when accounting for desynchronization of BE api. Static types can also be provided as needed.
11. Desyncs happen when BE is updated before FE cache is clear.  This can happen while using either static types or dynamics types.  See our canvas on VA slack channel for details about versioning.
12. UI Prototypes can be created and shared with plain html or a tool like code pen.
13. Basic terminal or browser can be used to make curl or fetch calls for testing a BE API and designing integration logic for the FE.
14. Observable pattern can be used to simulate or mock async behavior (like fetch calls). This can work real well with redux.
15. We just need a browser and text editor (and maybe terminal) to make real stuff.  Hosting may vary.
16. Make a test plan.
17. Learn your rudiments.

Many dyslexic, autistic and/or mathematical coders preffer functional and/or UI programming, but industry has tended to favor OO design.

If you want it, grit your teeth and learn it. Accessible website development is challenging, but it's rewarding work that can help anyone and everyone on the web.

This book should be accessible for many: https://github.com/MostlyAdequate/mostly-adequate-guide
