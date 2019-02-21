## TeleportHQ Code Generators 0.3 - Alpha!

[![npm]()]()
[![Build Status]()]()
[![Codecov]()]()
[![Codacy Badge]()]()
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg)](https://github.com/prettier/prettier)

This is a **WIP prototype** containing all our project and component generators, as well as the UIDL schemas and validators. While we have some working examples, it should not be considered production ready by any means! Do not hesitate to give us feedback and contribute back!

## What is this?
The **code generators** are a part of the **TeleportHQ** ecosystem, which we are actively building, in an effort to streamline website and design generation. You can read more about our inception in [this article](https://teleporthq.io/blog/we-believe-in-AI-powered-code-generation/).

The code generators are used by our online visual editor (coming soon), a tool which lets you build websites via a familiar design tool interface. The glue between our different tools and systems and the code generators is the [UIDL Standard](todo: blog link). The **UIDL** allows us to define **user interfaces** in an **abstract** way, independent of any framework or even the web platform itself, which then allows us to convert that abstraction into different flavors of coding (ex: React, Vue, etc.)

Our philosophy behind the code generators is:
* User interfaces are decomposed into **components**, hence our focus on component generation
* What can be built with `React`, can also be built with `Vue` or on top of the `Web Components` standard, we support multiple targets
* A project built with the visual editor should have a **high standard of quality** (performance, security, accessibility included)
* Generated **code quality** should be as good as possible, so that any developer can pick up the work from there and enhance the project
* The code generation architecture is open and extendable, we invite everyone to contribute!

You can also read more about our [decision to open source our code generators](todo: blog link).

Read more about the [UIDL Standard](todo: link).

## Instalation and Basic Usage
While this will probably remain a [monorepo](https://danluu.com/monorepo/), we will publish different **npm** packages for various parts of our code generation ecosystem. For now, there's a single package published under `@teleporthq/teleport-generators`. So, let's integrate that into your project:

```bash
npm install @teleporthq/teleport-generators
```

```javascript
import { createReactComponentGenerator } from "teleport-generators"

const reactGenerator = createReactComponentGenerator()

const componentUIDL = {
    "name": "MyComponent",
    "content": {
        "type": "text",
        "key": "text",
        "children": ["Teleport World!"]
    }
}

const result = reactGenerator.generateComponent(componentUIDL)
```

The code output from this snippet would be
```
import React from "react"

const MyComponent = props => {
  return <span>Teleport World!</span>
}

export default MyComponent
```

### Component Generators

We have **official** component generators for `React` and `Vue`, but we plan on supporting other frameworks and standards as soon as possible. Also, `React Native` is definitely on our minds, because we designed the UIDL in such a way that it is agnostic of the web platform.

There are two **factory functions** exported from our main module, for the React and Vue generators.

#### React

```javascript
import { createReactComponentGenerator } from "teleport-generators"

// Instantiate a generator, selecting the styled-jsx plugin for handling styles (other options: CSSModules, JSS, InlineStyles)
const reactGenerator = createReactComponentGenerator({ variation: ReactComponentFlavors.StyledJSX })

// Calling the generate function will return the code as a string
const result = reactGenerator.generateComponent(uidl)

console.log(result.code)
```

Read more about [the API of the component generator](todo: doc link).

Read more about [mappings and resolvers](todo: doc link).

TODO: More complex examples

#### Vue

```javascript
import { createVueComponentGenerator } from "teleport-generators"

// Instantiate a vue generator
const vueGenerator = createVueComponentGenerator()

// Calling the generate function will return the code as a string
const result = vueGenerator.generateComponent(uidl)

console.log(result.code)
```

TODO: More complex examples

#### Current capabilities
Here's a list of functionalities that the UIDL and the component generators support at the moment, besides the obvious presentational layer:
*  Dynamic values (props, state) inside html nodes or at attribute level
*  Type definitions for component props (PropTypes in React, props in Vue)
*  Simple component state (Hooks in React)
*  Event Handlers (related to state changes)
*  Repeat structures (.map in React, v-for in Vue)

### Project Generators

We have **official** project generators for the two different frameworks we support so far. For `React`, we can generate a project based on a `React` and `React-Router` template, or we can generate a project with `Next.js`. For `Vue`, we have a standard `Vue` app, build with the `vue-cli` and a generator for `Nuxt`.

Project generators rely on the component generators and on the structure of the `ProjectUIDL` to figure out how many files to create and where. Each project generator has its own strategy, based on the particularities of that specific framework/tool.

#### React + React-Router

Coming soon

#### Next

Coming soon

#### Vue

Coming soon

#### Nuxt

Coming soon

### UIDL Validators

The package also exports a module that performs UIDL validations for any given JSON structure, based on the [JSON Schema](todo: link documentation).

```javascript
import { UIDLValidators } from "@teleporthq/teleport-generators"

const componentUIDL = { ... }
const projectUIDL = { ... }

UIDLValidators.validateComponent(componentUIDL) // true / error object
UIDLValidators.validateProject(projectUIDL) // true / error object
```

When the validation fails, an **error** object is returned. Validation is performed using [https://github.com/epoberezkin/ajv](a standard JSON schema validator).


### Further Reading
A few useful links to get you up to speed with the **teleport** ecosystem:
*  [Component](todo: link) and [Project](todo: link) JSON Schemas
*  [Full Documentation](https://teleporthq.io/docs)
*  [Introducing the new Generators](todo: link)

## Development

This project is writen with **TypeScript**. The project setup is pretty standard. In order to give it a spin locally, you have to do:

```
npm install
npm run create-react-basic
```

Project generators are running locally in the `/examples` folder, where you will find a number of UIDL samples as well as the code that write the files and folders to disk.

todo: Write about tests

## Planning
todo: write about next steps

## Contributions
We would be super happy to have community involvment around this project. We strongly believe in the power of open source, so we want to build the best possible code generators together with the entire development community.

todo: Contact links
