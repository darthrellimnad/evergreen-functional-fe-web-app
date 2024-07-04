# evergreen-functional-web-app

Front End (FE) coding for web applications that interact with remote data and render UI updates on a client device (e.g. "single page app" or "progressive web app") can be deceptively difficult, especially if quality is a concern. Doing so with just the plain web standard technologies (HTML, CSS and JS) can be harder, but we've proven it doable.

Anyone can do this and learn it with minimal technological or capital investment. The only limiting factors are our abilities to learn and educate others (along with unhealthy social practices like non-compete & non-disclosure agreements).

We can match or exceed the quality of many proprietary, non-web solutions this way and avoid building multiple versions of the same app just to support multiple commercial platforms. And unlike commercial platforms, these web applications will work forever as long as the web standards exist and browser manufacturers adhere to them.  You just need a basic computer, text editor, and browser to get started, whether you need a Back End (BE) server or not.

Here's one generic way to do it, presented as an abstract idea... no software patents should hamper the accessible web.

## Basic Recipe

*Note: This method generally requires javascript (JS) to be enabled by user settings for client-side rendering, with a fallback message when disabled. Serverside rendering can also be used as a fallback, but that's a BE concern, not relevant to the runtime FE system described here, aside from page initialization.*

*Also wik: There are many other considerations you will need to make while working on your application, such as security, monetization, UX design, change management etc. These are also important, but not relevant to this general-use design. This doc just describes things that most all decoupled, evergreen FE web apps of reasonable complexity must account for.*

1. Mental model of the web FE is a simple system, which is linear, single threaded control flow.  [Our diagram is an SVG](https://raw.githubusercontent.com/darthrellimnad/generic-fe-system/main/Generic-FE-System.drawio.svg), which is evergreen. Web Workers can achieve multi-threaded behavior on the client device when high-performance or heavy computation is critical, but these remain orchestrated by the main page thread.
2. Mental model can be achieved using something like Redux or any similar evergreen JS library for event processing, state management, and UI updates. This design is highly reusable, even if the application's UI code changes or is rebuilt using different technology.
3. Design System patterns can be created using plain HTML templates or JS functions that return an html template string.  Higher order JS functions can also be used to promote code reuse and reduce duplication. Unlike components, these patterns are primarily used to document static html and styles representing different UI states, intended for standard component library and/or application developers. Automated & manual unit testing, visual regression testing, and static a11y & compatibility testing happen here. Patterns will always be reusable and trustworthy, even if component or app implementations change.
4. Design system patterns and/or components can be tested with plain HTML files, or tools like Pattern Lab or Storybook. Global and/or organizational community can participate in unit & integration testing if these tests are made publicly or organizationally accessible. Spread the work.
5. Styles can be implemented with global css or modularized css, which can be used for both the pattern library and web components.
6. Web components or framework components can reference (or “copy paste”) html from pattern library for implementation.  Components are concrete implementations of patterns that allow for encapsulation and reuse of UI code within the application. Dynamic component integration tests happen here.
7. Static data can be imported with json modules.
8. Remote and dynamic data can be fetched with the web standard "fetch" api (or a polyfill for old browsers). Interceptor or middleware patterns can be used to apply global or regional settings and behavior to all or some fetch calls.  See #9 for one option to simplify and encapsulate async behavior.
9. The [Observer pattern](https://github.com/tc39/proposal-observable), or an implementation of the pattern like RxJS, can be used to simulate async behavior (like fetch calls and web sockets) in prototypes and integration tests.  It can also be used to wrap actual network activity and other async behavior (like user input) to normalize event stream and cancel/pause/resume event processing in the application. Redux provides a basic pattern for us, and it can be extended with middleware or by treating the store as an Observable object itself.  Other patterns and libraries are similarly capable (although perhaps not as simple or *generally* useful for web FE), so pick your poison based on project and team requirements.
10. HTML, JS, & CSS can all be hosted as static content and cached (both locally and by CDN).
11. Static types for JS are not evergreen on the web (WebAssembly is a different story), so dynamic types can be used, along with a tool like JSverify (similar to QuickCheck in Haskell) inside of unit tests.  This can approach the same limit of quality as can be achieved with static types in a decoupled FE/BE system, when accounting for complexity and desynchronization with BE.
12. Desynchronization errors happen when BE is updated before FE cache is clear, or FE is updated on client device before BE.  This can happen when using either static or dynamic types, and can be addressed with versioning and "dynamic handshakes" between FE and BE.
13. UI Prototypes can be created and shared with plain HTML files or tools like Codepen or Storybook. Prototypes are a great way to learn and gather human feedback before committing to an idea in the application.
14. Basic terminal or browser can be used to make curl or fetch calls for testing BE endpoints and designing API integration logic for the FE.
15. We just need a browser and text editor (and maybe terminal) to make quality stuff.  Unit and integration tests for JS and UI code can be made to run in browser, but often it's more practical to use other tools depending on the type of test.
16. Make quality controls and a test plan based on your application's requirements. Evolve your plans as you grow. Remember to watch out for external links.
17. Learn as much as you can about the needs and desires of the real humans who may use the app. Don't discriminate.
18. Make sure to use a "cache busting" strategy when updating static FE files and other locally cached data (e.g. cookies or "Web Storage API").
19. Learn about [web standards and the "web content accessibility guidelines" (WCAG)](https://www.w3.org/WAI/standards-guidelines/). Accessible design improves experiences for all. Accessibility is quality.
20. Work smart (sometimes working smart means working hard) and work together. Be kind. Listen and learn. Choose your mentors and teachers wisely.

## Notes

Many coders (including plenty of dyslexic, autistic, adhd, disabled and/or mathematical coders) prefer functional, visual and UI programming, but industry has tended to favor statically typed, Object Oriented design while minimizing the importance of web standards, human experience and QA.

If you want it, grit your teeth and learn it. Accessible web application and game development is challenging, but it is rewarding work that can help anyone and everyone on the web.

This book should be accessible for many, and is a good place to start: [Mostly adequate guide to Functional Programming (in javascript)](https://github.com/MostlyAdequate/mostly-adequate-guide)

...and if you just need a simple website or webpage, just use HTML/CSS and as little JS as possible!  A design system, pattern library, a11y testing and quality assurance will be helpful regardless.

## Contributors
Too many to name... you know who you are.  Thank you all. 🤘💥❤️

## ASCII Art Triforce
...just for fun. Three triangles combined.

```
     /\
    /  \
   /____\  
  /\    /\
 /  \  /  \
/____\/____\
```
