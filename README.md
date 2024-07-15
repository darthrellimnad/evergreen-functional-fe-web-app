# evergreen-functional-fe-web-app

**This is a living document. 🌱**

___

Front End (FE) coding for web applications that manage state, interact with remote data and render UI updates on a client device with javascript (JS) can be deceptively difficult, especially if quality is a concern. Doing so with just the plain web standard technologies (HTML, CSS and JS) can be harder, but we've proven it doable.

Anyone can do this and learn it with minimal technological or capital investment. The only limiting factors are our abilities to learn and educate others (along with unhealthy social practices like non-compete/non-disclosure agreements and corporate gatekeeping).

We can match or exceed the quality of many proprietary, non-web solutions this way and avoid building multiple versions of the same app just to support multiple commercial platforms. And unlike commercial platforms, web applications can work forever as long as the web standards exist and browser manufacturers abide. As a result, they can be more energy efficient and better for the environment 🌲✌️. You just need a basic computer, text editor, and browser to get started, whether you need a Back End (BE) server or not. No app store required.

This document describes one generic way to do it, presented as an abstract idea... no software patents should hamper the accessible web.

## Basic Recipe

*Note: This method generally requires javascript (JS) to be enabled by user settings for client-side rendering and state management, with a fallback message when disabled. Serverside rendering can also be used as a fallback, but that's a BE concern, not relevant to the runtime FE system described here aside for page initialization. While many of the ideas here can prove useful for any web project, you should also read up on "progressive enhancement" techniques if you're looking to build a more traditional, server-rendered website with JS-enabled features.*

*Also wik: There are many other considerations you may need to make while working on your application, such as security, live ops, UX & content design, internationalization, change management, analytics, etc. These are also important, but not relevant to this general-use design. This doc only describes the most basic social and technical things that most evergreen FE web app projects of reasonable complexity must consider for an accessible and high quality end-user and development experience. Think of this as a brief, plain-language checklist for web developers and designers, not a comprehensive "how-to" guide.*

1. Mental model of the web FE is a simple system, which is linear, single threaded control flow.  [Our diagram is an SVG](https://raw.githubusercontent.com/darthrellimnad/generic-fe-system/main/Generic-FE-System.drawio.svg), which is evergreen. "Web Workers" can achieve multi-threaded behavior on a client device when high-performance or heavy computation is critical, but these remain orchestrated by the main page thread and are often unnecessary.
2. FE system can be managed in JS using something like Redux or any similar evergreen JS code for event processing, state management, and UI notification. This design is highly reusable, even if the application's UI code changes or is rebuilt using different technology.
3. Design System UI patterns can be created using plain HTML templates or JS functions that return an HTML template string.  Higher order JS functions can also be used to promote code reuse. Unlike components, patterns are primarily used to document and test static HTML and styles representing possible UI states. These are intended for designers, component authors, application developers, QA professionals and community testers. Automated & manual unit testing, visual regression testing, and static accessibility/compatibility testing happen here. Patterns will always be reusable and trustworthy, even if component or app implementations change. Building static patterns (in addition to dynamic components) can help teams spread UI design and development work more effectively among people with diverse skillsets and experience levels.
4. Web components or framework components can reference (or “copy paste”) HTML from the pattern library for implementation.  Components are concrete implementations of patterns that allow for encapsulation and reuse of UI code within the application. Not all patterns need be, or should be, implemented as web components (and sometimes vice versa). Automated and manual component integration tests happen here.
5. Design system patterns and components can be manually tested with plain HTML files, or with tools like Pattern Lab and Storybook. Global or organizational community can participate in unit & integration testing if these tests are made publicly or organizationally accessible. Spread the work.
6. Styles can be implemented with global or modularized CSS, which can be used for both the pattern library and web components. Remember to design responsively for supported viewport sizes and browser settings.
7. The standard ["History API"](https://html.spec.whatwg.org/dev/nav-history-apis.html#the-history-interface)" can be used for client-side "page" navigation, scroll restoration and deep linking.
8. Static data can be imported with json modules. Configurations, "API schemas" or even a "signed asset manifest" can be loaded this way.
9. Remote and dynamic data can be fetched with the web standard "fetch API". Interceptor or middleware patterns can be used to apply global or regional settings and behavior to all or some fetch calls.  See #10 for one option to simplify and encapsulate async behavior.
10. The [Observer pattern](https://github.com/tc39/proposal-observable), or an implementation of the pattern like RxJS, can be used to abstract and simulate async behavior (e.g. fetch calls, web socket messages and user input) in prototypes, integration tests and/or the real app.  This can help to normalize and compose event streams and allows us to cancel/pause/resume event processing in the application. Other patterns and libraries are similarly capable, although perhaps not as simple or *generally* useful for web FE. Pick your poison based on project and team requirements.
11. HTML, JS, & CSS files can all be hosted as static content and cached (both locally and by CDN).
12. Static types for JS are not evergreen on the web (WebAssembly is a different story), so dynamic types can be used alongside an evergreen library like JSverify inside of unit and integration tests (similar to QuickCheck in Haskell). This can approach the same limit of quality as can be achieved with static types in a decoupled FE/BE system when accounting for complexity and desynchronization with BE. This method can also be used for testing other stuff, like HTML generated by functional UI patterns. Statically typed languages that compile to JS can be great too, just not relevant to this document.
13. Desynchronization errors happen when the BE is updated before an active user's FE cache is clear, or FE is updated on a client device before the BE on server.  This can happen when using either static or dynamic types, and can be addressed with versioning (semantic or hash) and "dynamic handshakes" between FE and BE. Design error handling and a recovery experience for desync errors as needed.
14. UI Prototypes can be created and shared with plain HTML files or tools like Codepen or Storybook. Prototypes are a great way to learn and gather human feedback before committing to an idea in the application. Pattern library styles or components can be used here to mimic the live application.
15. Basic terminal or browser can be used to make curl or fetch calls for testing BE endpoints and designing API integration logic for the FE. Demand good documentation from API developers.
16. At minimum, we just need a browser and text editor to make quality stuff.  Unit and integration tests for JS and UI code can be made to run in browser, but often it's more practical to use other tools depending on the type of test.
17. Make quality controls and a test plan based on your application's requirements. Evolve your plans as you grow and adapt. Test as you go and test end-to-end holistically. Use a performance budget. Remember to watch out for external links and cross site scripting.
18. Learn as much as you can about the needs and desires of the real humans who may use the app. Don't discriminate.
19. Remember to use a "cache busting" strategy when changing static FE files and the design of other locally cached data (e.g. cookies or "Web Storage API").
20. Learn about [web standards and the "web content accessibility guidelines" (WCAG)](https://www.w3.org/WAI/standards-guidelines/). Accessible design improves experiences for all. Accessibility is quality.
21. Start simple. It's easier to make a simple thing more complicated, than a complicated thing more simple.
22. Work smart (sometimes working smart means working hard) and work together. Be kind. Listen and learn. Choose your mentors and teachers wisely.

## What is this good for?

*... absolutely nothing! (jk)*

The application design described here won't be for everyone or every web project.  This is primarily intended for projects that will require javascript (JS) and some moderately advanced software development techniques.  The purpose is to promote system accessibility, testability, stability and resilience over time while managing application behavior with JS. Here are some possible use cases I've come across where this might be helpful:

- Incrementally improving the design and quality of legacy JS-rendered or "JS framework" web applications.
- Single page or progressive web apps.
- Isomorphic web applications.
- Accessible web games that don't require much graphical power.
- Audio games.
- Integration orchestrator between Web Assembly, Web Worker, Frame or Plugin processes and the DOM.
- Non-traditional "web tools" that are only really feasible with JS.
- Web apps that require lots of async data communication, user interaction and correctness on the FE.
- Accessible digital art projects.
- A cheap way for folks to learn useful software development techniques and share creations on the web.
- Sharable application prototypes.
- Offline web applications.

## Notes

Many coders (including plenty of dyslexic, autistic, adhd, disabled and/or mathematical coders) prefer functional, declarative, visual and/or UI programming, but industry has tended to favor statically typed, Object Oriented design and imperative coding while minimizing the importance of web standards, UI, human experience and QA.

If you want it, grit your teeth and learn it. Accessible FE web app development is challenging, but it is rewarding work that can help anyone and everyone on the web.

...and if you just need a basic website or webpage, just use HTML/CSS and as little JS as possible!  HTML and CSS are pretty powerful on their own these days and only getting better. The mental model, a design system, pattern library, a11y testing and quality assurance will be helpful regardless.

## Additional Resources

This book should be accessible for many, and is a good place to start learning about functional coding: [Mostly adequate guide to Functional Programming (in javascript)](https://github.com/MostlyAdequate/mostly-adequate-guide)

For more general wisdom about software design and development, the following web page is a fun and insightful read: [The Grug Brained Developer](https://grugbrain.dev/)

If you're interested in learning more about accessibility testing, I highly recommend the following course.  Worth the price of admission imo:
[Testing Accessibility](https://testingaccessibility.com/)

## Contributors
Too many to name... you know who you are. Thank you all. 🤘💥❤️

### Special Thanks
Aaron Swartz for markdown and teaching us all a thing or two about courage.

Patrick Cyr for helping me through a tough time early in my career and reminding me to find my own inspiration. Shine bright pal. 🌌

Sarah Douglas for the encouragement and opening my mind to the world of web accessibility.

## ASCII Art Triforce
...just for fun. Three triangles combined.

```
     /\
    /  \
   /____\  
  /\::::/\
 /  \::/  \
/____\/____\
```
