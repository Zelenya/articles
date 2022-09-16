# PureScript in Production

Two simplified stories and a couple of anecdotes about using PureScript in production.

Over the past 2-3 years I had an opportunity to work with PureScript in production in two different companies. I want to document and share our experiences: introducing the language, onboarding people, challenges and feedbacks.

## **First journey (**How we used PureScript to sell shoes**)**

Back in the day the team was working on developing normal little backend services. As long as a service could communicate with other little services via REST all the the teams in the company were free to choose any language. At some point team’s services were written either in Scala or Haskell. But then during the internal hackathon, the team developed a prototype for a new backend service in PureScript. 

> Developer insight: Nothing is more permanent than the temporary

Because in our industry you have to think big and act fast: the service found its way to production. And thanks to the rapid microservice architecture, the number of PureScript services grew. At some later point majority of team’s (backend) services were written in PureScript. They were talking among themselves and with others in all sorts of synchronous and asynchronous ways (REST/GraphQL/different queues), they were shuffling massive JSONs around, and exchanging data with ElasticSearch. 

Later we’ve implemented a frontend app written in PureScript using React.

### Our experience

**What was your prior experience?**

*(What was your functional programming and frontend experience when you started using PureScript?)*

> **Filippo:** some ****frontend experience, professional Haskell experience.

> **Jay:** barely any frontend experience, years of professional Scala FP, pet Haskell experience.

> **Mark:** barely any frontend experience, years of professional Scala FP.

**How did you first learn PureScript?**

> **Filippo:** With Haskell knowledge, reading [PureScript documentation](https://github.com/purescript/documentation) was enough.

> **Jay:**  I read [the PureScript book](https://book.purescript.org) while waiting for my visa.

> **Mark:** I read the beginning of [the PureScript book](https://book.purescript.org) on holiday.

**Where would you go when you have questions?**

> **Filippo:** Ask colleagues, stack-overflow, [PureScript Discourse](https://discourse.purescript.org/).

> **Jay:** to Mark.

> **Mark:** Back then it [was Slack](https://discourse.purescript.org/t/migrating-to-discord/2493), today definitely [Discord](https://purescript.org/chat).

 ****

**What were the biggest challenges?**

While other teams were getting company and industry support, free tooling, and templates for their mainstream languages, our team had to reimplement everything ourselves (e.g. authentication between services, company-standardised http response pagination). On top of that we were the only ones testing and using these, as a result lots of exceptional cases wouldn’t be handled and blow up time to time.

> **Filippo:** 
> - Annoying-to-debug errors (e.g. errors involving do notation display desugared expressions composed of `>>=` calls, errors with non-matching record types).
> - Colleagues using unnecessarily fancy constructs.
> - The tooling mess (Were we supposed to use bower or spago? Do you specify PureScript as a *package.json* dependency? or do you use a system-wide one?)
> - Lack of best-practices and guidance for newcomers (e.g. How to deal with JSON data: Simple.JSON vs/and Data.Argonaut?)
> - Poor operational knowledge on the team’s side / Inability to reuse templates with best practices (For example, an app was running for a long time with the default NodeJS settings - missing even basic memory limits to reflect the k8s pod resource adjustments. Not really a language issue, but other teams using mainstream tech don’t tend to have such issues, because they can reuse existing Docker images provided by the company).

> **Jay:** 
> - Dealing with all the bundlers and packagers and pre-post-über-processors.
> - Dealing with JavaScript world.

> **Mark:** 
> - Sneaking it into the company.

## Second **journey (**How we used PureScript to build bot builders**)**

An early version of the graph editor was implemented in TypeScript. The team looked into PureScript because the developers were already using Haskell on the backend and were familiar with the functional programming. 

PureScript-JavaScript interoperability allows migration of one React component at a time. Which empowers gradual upgrades to PureScript without a complete rewrite and without a feature development halt. In our case, the project was completely converted to PureScript within two to three weeks.

A functional approach of working with state plus prior [Elm](https://guide.elm-lang.org/architecture/) and Redux experience made the move simple. Roughly speaking, PureScript just differs in syntax, while [FFI](https://book.purescript.org/chapter10.html) allows interfacing with the JavaScript environment without starting from scratch, as well as accessing the abundance of JavaScript libraries and tools.

### Our experience

**What was your prior experience?**

> **Andy:** started with Java and JavaScript, then moved on to TypeScript, then Scala and Elm, later Haskell. 

> **Giovanni:** some ****frontend experience (AngularJS and Elm), professional Elixir and Haskell experience.

> **Igor:** quite versed in Haskell.

**How did you first learn PureScript?**

> **Giovanni:** I read [the PureScript book](https://book.purescript.org) focusing specifically on the differences between Haskell and PS. Then I solved some simple exercises in PureScript.

> **Igor:** I started learning it using [the PureScript book](https://book.purescript.org), and trying to re-implement some personal projects frontend in it. 

**Where would you go when you have questions?**

> **Andy:** I would start with the documentation or a search across all of GitHub repositories, when looking for an example of how to implement something or use a library. Apart from that, [Discord](https://purescript.org/chat) is quite active, [PureScript cookbook](https://github.com/JordanMartinez/purescript-cookbook) is improving.

> **Giovanni:** I'm a big believer in reading the docs and the source code, failing that I would ask my colleagues.

> **Igor:** I could always count on the community (slack, [Discord](https://purescript.org/chat)) to help, and after, my colleagues at work.

**What were the biggest challenges?**

> **Andy:** 
> - It was hard(er) to find documentation and tutorials. There wasn't a lot of information available on how to start using PureScript, aside from a few brief examples scattered around.

> **Giovanni:** 
> - Getting to grips with React using a non-standard language (The general flow of data was clear, but then I had to translate between React classes and PureScript types, or trying to understand if a binding is an `Eff` or an `Aff`. I would say most of my nightmares were Integrating JavaScript components, especially when the TypeScript file says they're of type `any`)
> - Records and Row types.

> **Igor:**
> - Type signatures in documentation tended to be somewhat "de-sugared" and harder to parse because of that. Some function signatures are quite verbose.
> - Context switching with Haskell, especially because of records, strictness and missing features, but also the small syntax differences.
> - Dealing with frontend issues unrelated to the language itself.
> - JavaScript.

> **Jay:**
> - (In the context of working on a larger frontend app for the first time.) Getting used to the architecture, finding a right place to deal with a new side effect or deal with state.

**Bonus (useful resources from Andy)**

- [Thomas Honeyman Articles](https://thomashoneyman.com/articles/)
- [PureScript: Cookbook](https://github.com/JordanMartinez/purescript-cookbook)
- [PureScript: Jordan’s Reference](https://jordanmartinez.github.io/purescript-jordans-reference-site/)

*Thank you to [Andy](https://github.com/andys8), [Filippo](https://github.com/fghibellini), [Giovanni](https://github.com/sphaso), [Igor](https://github.com/elland), [Mark](https://github.com/i-am-the-slime) for your time and answers.*

*However I’m the one to blame for all the typos and errors, because the answers were heavily edited and censored ;)*
