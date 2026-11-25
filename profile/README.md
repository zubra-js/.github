<p align="center"><img src="zubra-tile.svg" width="96" height="96" alt="Zubra"></p>

<h1 align="center">Zubra</h1>

<p align="center"><b>Write components like HTML. Ship them as the platform's own.</b></p>

<p align="center">
  <a href="https://zubra-js.github.io/zubra/">Website</a> ·
  <a href="https://zubra-js.github.io/zubra/docs/">Docs</a> ·
  <a href="https://zubra-js.github.io/zubra/playground/">Playground</a> ·
  <a href="https://zubra-js.github.io/zubra-ui/">Zubra UI</a> ·
  <a href="https://marketplace.visualstudio.com/items?itemName=JourneytoCode.zubra">VS Code</a>
</p>

---

Zubra is a compiler for Web Components. You write a component as one `.zb` file: a `<script>`, scoped styles and an HTML template with `{expr}` bindings. Zubra compiles it to a standard custom element, the HTML a server sends, and TypeScript typings. The element works in plain HTML, React, Vue, Svelte, Angular and on the server, with no integration code.

**Nothing is hidden.** `zubra compile` prints every line it generates, and each part of that output follows a rule of the platform.

## Projects

<table>
<tr>
<td width="50%" valign="top">

### [Zubra](https://github.com/zubra-js/zubra)

The compiler, runtime and server packages. `.zb` in; elements, server HTML and typings out.

```sh
npm create zubra@latest
```

[Website](https://zubra-js.github.io/zubra/) · [Guide](https://zubra-js.github.io/zubra/docs/guide/01-first-component/) · [Reference](https://zubra-js.github.io/zubra/docs/reference/) · [Changelog](https://zubra-js.github.io/zubra/docs/changelog/)

</td>
<td width="50%" valign="top">

### [Zubra UI](https://github.com/zubra-js/zubra-ui)

96 web components you copy in and own: switches, date pickers, dialogs, data tables and more. Built on native elements and themed with shadcn/ui variables.

```sh
npx shadcn@latest add https://zubra-js.github.io/zubra-ui/r/toggle-switch.json
```

[Components](https://zubra-js.github.io/zubra-ui/) · [Themes](https://zubra-js.github.io/zubra-ui/themes/) · [Theme studio](https://zubra-js.github.io/zubra-ui/studio/) · [Showcase](https://zubra-js.github.io/zubra-ui/showcase/)

</td>
</tr>
</table>

## A component

```html
<!-- copy-button.zb -->
<script>
  let copied = false                               // state: assigning it updates the DOM

  async function copy() {
    await navigator.clipboard.writeText(text)      // `text` is a prop, by name
    copied = true
    setTimeout(() => (copied = false), 1500)
  }
</script>
<style>
  button.done { color: green; }                    /* scoped to this component, in light DOM */
</style>
<copy-button text label="Copy">
  <button type="button" onclick={copy} class:done={copied}>
    {copied ? "Copied!" : label}
  </button>
</copy-button>
```

Use it anywhere:

```html
<copy-button text="npm create zubra"></copy-button>   <!-- plain HTML -->
```

```tsx
<CopyButton text="npm create zubra" />                // React or Vue, through @zubra/unplugin, typed
```

## Packages

| Package | What it adds | Needed when |
|---|---|---|
| `@zubra/compiler` | The compiler as WebAssembly, with the `zubra` command; no Rust needed | Always |
| `@zubra/runtime` | The browser runtime that compiled components import | Always, except with `--emit element` |
| `@zubra/unplugin` | `.zb` imports in Vite, Rollup, webpack, esbuild and Rspack; React and Vue wrappers; Astro | Your app has a bundler |
| `@zubra/server` | Components in Express, Fastify, Hono, Eleventy or any template engine | A JavaScript server renders pages |
| `@zubra/actions` | `'use server'` functions over a plain form POST | A form should work with JavaScript off |
| `@zubra/sync` | `'use collection'`: state in IndexedDB, synced across tabs and devices | State must survive reloads or work offline |
| `@zubra/router` | `'use route'`: a component served as a page, with a server-only `load` | An app with no host framework needs pages |
| `create-zubra` | The starter app | Starting a project |

## Built on the platform

The runtime follows what the web is standardizing: template parts in the shape of DOM Parts, the Context Protocol, form-associated custom elements and declarative shadow DOM. As browsers ship these, the runtime shrinks. Reactivity runs on Zubra's own engine, modelled on the TC39 Signals proposal. The proposal's API itself is available as an experimental mode (`engine: 'signals'`).

Coming from a framework? Read the guide for [React](https://zubra-js.github.io/zubra/docs/guide/for-react-developers/), [Vue](https://zubra-js.github.io/zubra/docs/guide/for-vue-developers/), [Svelte](https://zubra-js.github.io/zubra/docs/guide/for-svelte-developers/) or [Angular](https://zubra-js.github.io/zubra/docs/guide/for-angular-developers/) developers.

## Get involved

- Report bugs and ask questions in each repository's issue tracker.
- Read [CONTRIBUTING.md](https://github.com/zubra-js/zubra/blob/main/CONTRIBUTING.md) before opening a pull request.
- Report vulnerabilities as described in [SECURITY.md](https://github.com/zubra-js/zubra/blob/main/SECURITY.md).

Zubra is open source under the ISC license.
