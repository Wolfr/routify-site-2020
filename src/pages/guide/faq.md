---
layout: default
---

### How do I use Routify with Electron?

Electron doesn't detect changes in node_modules. To get around that, we can export the generated files to a folder in the project. ``routify --routify-dir routify``. Remember to import your ``routes.js`` from this folder.
@kevmodrome might have more info

### Why does my app disappear when I refresh?

Your server isn't forwarding requests to Routify. Make sure that you redirect 404s to your entry point. Usually ``/index.html`` or ``/__app.html``.

### Can I use Routify without SSR, dynamic imports, static exports, etc.?

Yes. If you're using the starter template, these features are enabled by default but can be disabled. Please note that these features are not mutually exclusive and you still get a fullfledged SPA when they're enabled.

### What's the difference between SSR and prerender/static export?

SSR (Server-Side Rendering) is done in realtime and is useful for pages with dynamic content, like a news feed. Prerendering/static export is done when building the app. Prerendered pages are great for pages that don't rely on APIs.

### Why do prerendered/SSR pages not contain data from my API?

Pages are written to HTML when a page and its layouts have rendered. To wait for dynamic data, insert a `$ready()` at the end of your API request. For more information refer to our [$ready() helper](/docs/helpers#ready)

### What's the difference between prerendering and SSR?

Prerendering happens when the site is built. SSR, or server-side rendering, is performed in realtime.

### Can prerendered pages have dynamic content?

Yes and no. The saved HTML remains static, but once the app has loaded on the client, the dynamic content will be seamlessly updated.

### Can I have SSR without a server?

Yes. SSR can be performed in serverless functions. Please refer to the script folder of the starter template for serverless functions.

### What is Roxi?

Roxi is a framework, still in development. It will leverage Routify for routing as well as provide the same features as the starter template.

### How is Roxi different from Routify?

Roxi handles the responsibilities which are currently assigned to the Routify Starter Template. This provides a much smoother upgrade path since the logic will be contained within Roxi and not the starter template.

### Can I join the team?

Yes. We welcome all contributions and would appreciate additional core members. Especially documentation, examples, guides, art, templates, etc. can use an extra hand.

### Does Routify provide error handling

Routify offers decorators. These are excellent for handling errors. Decorators are components which wrap around each individual descendant layout/page.
```html
<script> import {Boundary} from "@crownframework/svelte-error-boundary" </script>

<slot decorator={Boundary} />
```

<!-- routify:options index=90 -->
<!-- routify:options title="FAQ" -->

### Case insensitive routing
Case insensitive routing is not currently baked into Routify, however it is easily achievable! There are two ways to do this:

- Config
  ```html
  <script>
    import { Router } from '@roxi/routify'
    import { routes } from '../.routify/routes'
    
    const config = {
      urlTransform: {
        remove: url => url.toLowerCase()
      }
    }
  </script>

  <Router {config} {routes} />
  ```
  
- Map
  ```js
  routes.forEach(r => r.regex = new RegExp(r.regex, 'i'))
  ```
