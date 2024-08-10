# evergreen-functional-fe-web-app

**This is a living document. 🌱**

___

## Introduction

Front End (FE) coding for web applications that manage state, interact with remote data and handle UI updates on a client device with javascript (JS) can be deceptively difficult, especially if quality is a concern. Doing so with just the evergreen web standard technologies (HTML, CSS and JS) can be harder, but we've proven it doable... even if not always wise or necessary for most web projects.

Anyone can do this and learn it with minimal technological or capital investment. The only limiting factors are our abilities to learn and educate others.

We can match or exceed the quality of many proprietary, non-web solutions this way and avoid building multiple versions of the same app just to support multiple commercial platforms. And unlike commercial platforms and proprietary technologies, web applications can work forever on most hardware as long as the web standards exist and browser and OS manufacturers abide. As a result, they can be more energy efficient and better for the environment 🌲☮️. You just need a basic computer, text editor, and browser to get started, whether you need a Back End (BE) server or not. No app store required.

This document describes one generic way to do it, presented as an abstract idea... no software patents should hamper the accessible web.

## Generic Recipe

*Wik: This method generally requires javascript (JS) to be enabled by user settings for client-side rendering and state management, with a fallback message when disabled. Server-side rendering can also be used as a fallback, but that's a BE concern, not relevant to the runtime FE system described here aside for page initialization. While many of the ideas here can prove useful for any web project, you should also read up on "[progressive enhancement](https://www.w3.org/wiki/Graceful_degradation_versus_progressive_enhancement)" techniques if you're building a more traditional, server-rendered website with enhanced JS features.*

*Also wik: There are many other considerations you may need to make while working on your application, such as security, CI/CD, Dev/Design Ops, UX & content design, internationalization, change management, analytics, etc. These are also important, but not relevant to this general-use design. This doc only describes the most basic social and technical things that most evergreen FE web app projects of reasonable complexity must consider for accessible and high quality end-user and development experiences. Think of this as a brief, plain-language checklist (or at least as "plain" as I can manage so far) for web developers and designers, not a comprehensive "how-to" guide.*

### Technical Bits

1. Mental model of the web FE is a simple system, which is linear, single threaded control flow.  Our [FE system diagram](https://raw.githubusercontent.com/darthrellimnad/generic-fe-system/main/Generic-FE-System.drawio.svg) is an SVG (which is evergreen). "Web Workers" can achieve multi-threaded behavior on a client device when high-performance or heavy computation is critical, but these remain orchestrated by the main page thread and are often unnecessary.
2. FE system can be managed in JS using something like Redux or any similar evergreen JS code for event processing, state management, and UI notification. This design is highly reusable, even if the application's UI code changes or is rebuilt using different technology.
3. Design System (DS) UI patterns can be created using plain HTML templates or JS functions that return an HTML template string.  Higher order JS functions can also be used to promote code reuse. Unlike components, patterns are primarily used to document and test static HTML and styles representing possible UI states. These are intended for designers, component authors, application developers, QA professionals and community testers. Automated & manual unit testing, regression testing, and static accessibility/compatibility testing happen here. It's much quicker and more efficient to test (and re-test) a large number of test cases with static patterns as opposed to dynamic components. Patterns will always be reusable and trustworthy, even if component or app implementations change.
4. DS web components or framework components can reference (or copy-paste, export, etc) HTML from the pattern library for implementation.  Components are dynamic implementations of patterns that allow for encapsulation and reuse of UI code within the application. Not all patterns need be, or should be, implemented as web components (and sometimes vice versa). Automated and manual dynamic component tests happen here. It's best to only include reusable components with no external or remote dependencies for your DS; integrated app testing should happen separately.
5. DS patterns and components can be manually tested with plain HTML files, or with tools like Pattern Lab and Storybook. Global or organizational community can participate in unit & integration testing if these tests are made publicly or organizationally accessible. Spread the work... the more human senses and diverse perspectives on these the better.
6. Styles can be implemented with global or modularized CSS (or a build system than can produce both). The same styles can be used for both the pattern library and web components. CSS variables can be used for theme and design token management.  Remember to design responsively for supported viewport sizes and browser settings.
7. The standard ["History API"](https://html.spec.whatwg.org/dev/nav-history-apis.html#the-history-interface)" can be used for client-side "page" navigation, scroll restoration and deep linking.
8. Static data can be imported with json modules. Configurations, API schemas or even a "signed asset manifest" can be loaded this way. Data and scripts can also be loaded async after page-load with dynamic import statements.
9. Remote and dynamic data can be fetched with the web standard "fetch API". Interceptor or middleware patterns can be used to apply global or regional settings and behavior to all or some fetch calls. Remember to appropriately communicate loading and error states with the UI. See #10 for one option to simplify and encapsulate async behavior if needed.
10. The [Observer pattern](https://github.com/tc39/proposal-observable), or an implementation of the pattern like RxJS, can be used to abstract and simulate async behavior (e.g. fetch calls, web socket messages, user input, etc.) in prototypes, integration tests and/or the real app.  This can help to normalize and compose event streams and allows us to buffer, cancel, pause and resume event processing in the application. While not strictly functional, it can be used alongside functional state management (i.e. redux) to great effect in a multiparadigm language like JS.  Other patterns, libraries and techniques are similarly helpful or capable (e.g. vanilla Redux with middleware, functional-reactive methods, pub-sub, state machine, various frameworks, etc) although perhaps not as simple or *generally* useful for web FE. Pick your poison based on project and team requirements.
11. HTML, JS, & CSS files can all be hosted as static content and cached (both locally and by CDN).
12. Make sure you understand [CORS](https://fetch.spec.whatwg.org/#cors-protocol) (Cross-Origin Resource Sharing) when hosting your FE on a different domain than the BE(s).
13. Static types for JS are not evergreen on the web (WebAssembly is a different story), so dynamic types can be used alongside an evergreen library like JSverify inside of unit and integration tests (similar to QuickCheck in Haskell). This can approach the same limit of quality as can be achieved with static types in a decoupled FE/BE system when accounting for complexity and desynchronization with BE. This method can also be used for testing other stuff, like HTML generated by functional UI patterns. Statically typed languages that compile to JS can be great too, just not relevant to this document.
14. Desynchronization errors (silent or otherwise) happen when the BE is updated before an active user's FE cache is clear, or FE is updated on a client device before the BE on server.  This can happen when using static or dynamic types and can cause errors on the server and client (including violations of WCAG SC [3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data) and [3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification)). One way to address this is to version the API or individual endpoints (semantic or hash) and use "dynamic handshakes" between FE and BE by including the expected version identifier along with each request to the BE. Design error handling and a recovery experience as needed. This [visual desynchronization example](https://raw.githubusercontent.com/darthrellimnad/evergreen-functional-fe-web-app/main/Decoupled-desync-example.drawio.svg) shows one way this could work using semantic version strings.
15. Basic terminal or browser can be used to make curl or fetch calls for testing BE endpoints and designing API integration logic for the FE. Demand good documentation from API developers.
16. At minimum, we just need a browser and text editor to make quality stuff.  Unit and integration tests for JS and UI code can be made to run in browser, but often it's more practical to use other tools depending on the type of test.
17. Remember to use a "cache busting" strategy when changing static FE files. Use cache busting or a migration strategy when changing the design of other locally cached data like cookies or "Web Storage API" data.
18. Make quality controls and a test plan based on your application's requirements. Evolve your plans as you grow and adapt. Test as you go and test end-to-end holistically. Here's some basic things to remember when considering quality:
    - Use a performance budget.
    - Progressively enhance or gracefully degrade functionality as needed.
    - Watch out for external links and cross site scripting.

### Social Bits

1. Building static patterns in addition to dynamic components for your DS can help teams spread work and collaborate more effectively among people with diverse skillsets and experience levels while minimizing context switching. It also allows us to perform a lot more UI testing earlier in the development cycle before failures get much more expensive. For example, designers and qualified A11y/HTML/CSS coders can own the patterns and static unit tests, while App/JS coders can test against them while implementing or updating components and pages... you don't need unicorns to do it all.
2. Document intended usage constraints for DS patterns & components, particularly for things that aren't encoded or apparent by the implementation and test cases. Try to make these docs as simple and easy to understand as possible.
3. Learn as much as you can about the needs and desires of the real humans who may use the app. Don't discriminate.
4. UI Prototypes can be created and shared with plain HTML files (or tools like Codepen or Storybook). Prototypes are a great way to learn and gather human feedback before committing to an idea in the application. DS styles, patterns and components (experimental or otherwise) can be used here to mimic the live application.
5. Learn about [web standards and the "web content accessibility guidelines" (WCAG)](https://www.w3.org/WAI/standards-guidelines/). Accessible design improves experiences for all. Accessibility is quality. If you know nothing else, remember to "**POUR** some love on it" (accessible features are **P**erceivable, **O**perable, **U**nderstandable, and **R**obust).
6. Start simple. It's easier to make a simple thing more complicated, than a complicated thing more simple.
7. *"When faced with two or more alternatives that deliver roughly the same value, take the path that makes future change easier."* -- Dave Thomas
8. Mind your tech and design debt. Don't allow a stench to linger long, but make sure you understand where it's really coming from before trying to clean up.
9. When needed, don't be afraid to try things and find better operations.
10. Care about those you work with and those who your work may affect.
11. Work smart (working smart also means knowing when to work hard) and work together.
12. Be kind.
13. Listen and learn.
14. Build trust.
15. Choose your mentors and teachers wisely.
16. When you have spoons to spare, help others and share what you know.

## What is this good for?

*... absolutely nothing! (jk)*

The application design described here won't be for everyone or every web project.  This is primarily intended for accessible web projects that will require javascript and some moderately advanced software development techniques (as well as proving it possible with just the evergreen web technologies and reminding myself of stuff). There are many great tools and frameworks out there that can help as well, but I'm trying to keep this doc as simple and generic as possible.

The purpose of this is to promote system accessibility, testability, stability and resilience over time while managing application behavior with JS. Here are some possible use cases I've come across where this (or parts of this) might be helpful:

- Incrementally improving the design and quality of legacy JS-rendered or "JS framework" web applications.
- Single page, isomorphic and progressive web apps.
- FE systems that can be entirely created and hosted as static files.
- Decoupled FE/BE systems and codebases that allow for simpler & faster local development environments with fewer cross-discipline or cross-team dependencies.
- A family of web apps/sites that share a design system but must support multiple component frameworks, rendering modes or themes.
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

Many coders and designers (including plenty of dyslexic, autistic, adhd, disabled, mathematical and/or creative coders) prefer functional, declarative, visual and/or UI programming, but industry has historically favored statically typed Object Oriented design, imperative coding and BE systems while neglecting the importance of web standards, UI, accessibility, human experience and QA. Having "engineers" and "buisness/policy people" in charge of UI and UX has created much of the global web accessibility and usability mess we're still dealing with today.

Keep in mind: decoupling the FE and BE this way can increase the complexity of the entire system, even if each system can better separate concerns, simplify mental models, result in improved UX/DX and reduce overall network traffic in many situations. You'll need to keep an eye on that pesky "complexity demon" so it doesn't get out of control. If you're careful and brave (like good JS and FE devs are), it can be crushed into submission. Honestly, it's often not as bad as the other demons you'll face with many server rendered websites.

When we were forced to build these things at the dawn of the "Web 2.0" era, we really didn't understand what we were doing so well, and things got awful real fast for a real long time 💩. This "checklist" is basically my attempt to provide others with what I would have liked to have had back then. Things are a bit better these days, but make sure your project requirements actually call for this before traveling down this road... remember, it's dangerous to go alone!

That said, if you want it grit your teeth and learn it 🤘. Accessible FE web app development is challenging, but it is rewarding work that can help anyone and everyone on the web.

...and to reiterate, if you just need a basic website or webpage, just use HTML/CSS and as little JS as possible!  HTML and CSS are pretty powerful on their own these days and only getting better. The mental model, a design system, pattern library, a11y testing and quality assurance will be helpful regardless.

## Additional Resources

This book should be accessible for many, and is a good place to start learning about functional coding: [Mostly adequate guide to Functional Programming (in javascript)](https://github.com/MostlyAdequate/mostly-adequate-guide)

For more general wisdom about software design and development, the following web page is a fun and insightful read: [The Grug Brained Developer](https://grugbrain.dev/)

If you're interested in learning more about accessibility testing, I highly recommend the following course:
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
