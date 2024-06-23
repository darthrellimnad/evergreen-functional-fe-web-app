# evergreen-functional-web-app

Front End (FE) coding for web applications that interact with remote data and render UI updates on a client device (e.g. "single page app" or "progressive web app") is deceptively difficult, especially if quality is a concern. Doing so with just the plain web standard technologies (HTML, CSS and JS) can be harder, but we've proven it doable.

Anyone can do this and learn it with minimal technological or capital investment.  We can match or exceed the quality of many proprietary, non-web solutions this way and avoid building multiple versions of the same app just to support multiple commercial platforms. And unlike commercial platforms, these web applications will work forever as long as the web standards exist and browser manufacturers adhere to them.  You just need a basic computer, text editor, and browser to get started, whether you need a Back End (BE) server or not.

Here's one generic way to do it, presented as an abstract idea... no software patents should hamper the accessible web.

## Basic Recipe

*Note: This method generally requires javascript (JS) to be enabled by user settings for client-side rendering, with a fallback message when disabled. Serverside rendering can also be used as a fallback, but that wouldn't be evergreen.*

1. Mental model of the FE is a simple system, which is linear, single threaded control flow.  [Our diagram is an SVG](https://raw.githubusercontent.com/darthrellimnad/generic-fe-system/main/Generic-FE-System.drawio.svg), which is evergreen.
2. Mental model can be achieved using something like Redux or any similar evergreen JS library for event processing, state management, and UI updates.
3. Design System patterns can be created using JS functions (or higher order functions) that return an html string.  Unlike components, these patterns are primarily used to document static html and styles representing different UI states, intedended for standard library developers, unit testing, a11y testing and documentation.  Visual regression and manual/automated unit testing happens here. Patterns will always be reusable, even if component implementations change.
4. Design system patterns and/or components can be tested w/ simple html files, or a tool like storybook. Global community can participate in testing if these tests are made publicly accessible.
5. Styles can be implemented with global css or modularized css, which can be used for both the pattern library and web components.
6. Web components or framework components can reference (or “copy paste”) html from pattern libraries and use the same css as patterns.  JS implementation of patterns and integration tests happen here.
7. Static data can be imported with json modules.
8. Remote data can be fetched with standard fetch.
9. HTML, JS, & CSS can all be hosted as static content.
10. Static types for JS are not evergreen on the web (WebAssembly is a different story), so dynamic types can be used, along with a tool like jsverify (similar to QuickCheck) inside of unit tests.  This can approach the same limit of quality as can be achieved w/ static types in a decoupled FE/BE system, when accounting for desynchronization of BE api.
11. Desynchronization errors happen when BE is updated before FE cache is clear, or FE is updated before BE.  This can happen when using either static or dynamic types, and can be addressed with versioning and "dynamic handshakes" between FE and BE.
12. UI Prototypes can be created and shared with plain html files or a tool like codepen.
13. Basic terminal or browser can be used to make curl or fetch calls for testing BE endpoints and designing api integration logic for the FE.
14. The Observer pattern, or an implementation of the pattern like RxJS, can be used to simulate or mock async behavior (like fetch calls) in prototypes, or wrap actual network calls and other async behavior to normalize async event stream.
15. We just need a browser and text editor (and maybe terminal) to make quality stuff.  Unit and integration tests can be made to run in browser, but often it's more practical to use other tools.
16. Make quality controls and a test plan based on your application's requirements. And remember to watch out for external links.
17. Learn as much as you can about the needs and desires of the real humans who may use the app. Don't discriminate.
18. Make sure to use a "cache busting" strategy when updating static files for the FE.
19. Learn about [web standards](https://www.w3.org/WAI/standards-guidelines/).
20. Work smart (sometimes working smart means working hard) and work together. Be kind. Listen and learn. Choose your mentors and teachers wisely.

Many coders (including plenty of dyslexic, autistic, adhd, disabled and/or mathematical coders) prefer functional and/or UI programming, but industry has tended to favor Object Oriented design while minimizing the importance of human experience.

If you want it, grit your teeth and learn it. Accessible FE web application development is challenging, but it is rewarding work that can help anyone and everyone on the web.

This book should be accessible for many, and is a good place to start: [Mostly adequate guide to Functional Programming (in javascript)](https://github.com/MostlyAdequate/mostly-adequate-guide)

...and if you just need a simple website or webpage, just use HTML/CSS and as little JS as possible!  A design system, pattern library, a11y testing and quality assurance will be helpful regardless.

## Contributors
Too many to name... you know who you are.  Thank you all ❤️

### ASCII art triforce... just for fun. Three triangles combined.
```
     /\
    /  \
   /____\  
  /\    /\
 /  \  /  \
/____\/____\
```
