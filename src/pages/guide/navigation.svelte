<script>
  import { meta, url } from "@roxi/routify";
  import Note from "@/components/Note.svelte";
  import Code from "@/components/Code.svelte";
  meta.title = "Navigation";
</script>

<!-- routify:options index=50 -->

<div class="c-content">
  <div class="c-container-vertical c-container-vertical--small">
    <h1 class="c-h1">Navigation</h1>
    <p>
      There are a million ways to handle navigation. Hopefully, this page can save you some time when creating navigation for your next project.
    </p>
    
    <Note>
      <p>
        Svelte transitions can occasionally prevent a page from dismounting correctly. If you face this issue, you can add <code>|local</code> to the transition (example below) and this should resolve the issue.
      </p>
      <code>
        transition:fade|local
      </code>
    </Note>
  </div>
  <div class="c-container-vertical c-container-vertical--small">
    <h3 class="c-h3">The url helper</h3>
    <p>
      The
      <code>url</code>
      helper creates links from relative, absolute or, named paths.
    </p>
    <p>
      The advantage of using
      <code>url</code>
      is that it allows for your code to be modular. If you rename your
      <code>editor/</code>
      folder to
      <code>admin/</code>,
      all the internal links inside that folder will still work.
    </p>
    <Code language="svelte">
      {`
    <a href={$url('./introduction')}>
      A link to the introduction section on your left
    </a>`}
    </Code>
    <a href={$url('./introduction')}>
      A link to the introduction section on your left
    </a>
    <Note>
      <p>
        Unlike traditional links,
        <code>$url</code>
        is relative to the layout or page it is located in and not the current
        URL in the address bar.
      </p>
      <p>
        You can read more about the
        <code>$url</code>
        helper
        <a href={$url('/docs/helpers#url')}>here</a>
      </p>
    </Note>
  </div>

  <div class="c-container-vertical c-container-vertical--small">
    <h3 class="c-h3">The isActive helper</h3>
    <p>
      The
      <code>isActive</code>
      helper tells you whether a path is active or not. It resolves the provided
      path with the
      <code>$url</code>
      helper.
    </p>
    <Code language="svelte">
      {`
    <sty`}{`le>
      .active {font-weight: bold}
    </sty`}{`le>

    <div class:active={$isActive('./blog')}
      <a href={$url('./blog')}>
        Blog
      </a>
    </div>  `}
    </Code>
    <p>
      You can read more about the
      <code>$isActive</code>
      helper
      <a href={$url('/docs/helpers#is-active')}>here</a>
    </p>
  </div>

  <div class="c-container-vertical c-container-vertical--small">
    <h3 class="c-h3">Handling multiple links</h3>
    <p>
      Links can be handled in an array of different ways. This might be the
      easiest way.
    </p>
    <Code language="svelte">
      {`
    <sc`}{`ript>
      import {isActive, url} from '@roxi/routify'

      const links =
      [
        ['./index', 'Home'], //add index if you don't want siblings to be considered children
        ['./blog', 'Blog'],
        ['./about', 'About'],
        ['./contact', 'Contact']
      ]
    </script>

    <sty`}{`le>
      .active {font-weight: bold}
    </sty`}{`le>

    <ul>
      {#each links as [path, name]}
        <!-- Svelte magic. If isActive is true, the "active" class is applied. -->
        <li class:active={$isActive(path)}>
          <a href={$url(path)}>
            {name}
          </a>
        </li>
      {/each}
    </ul>
      `}
    </Code>
  </div>

  <div class="c-container-vertical c-container-vertical--small">
    <h3 class="c-h3">Automatic navigation generation</h3>
    <p>
      It is also possible to generate navigation from your file structure. In
      fact, all navigation on this site is generated. Even hash links, external
      links, and the previous/next buttons you see below.
    </p>
    <p>
      To create links for files in a folder, create a
      <code>_layout.svelte</code>
      in the folder and import the layout helper.
    </p>
    <Code language="svelte">
      {`
      <!-- _layout.svelte -->
      <sc`}{`ript>
        import { isActive, url, layout } from "@roxi/routify";
      </script>

      <ul>
        {#each $layout.children as { path, title }}
          <li class:active={$isActive(path)}>
              <a href={$url(path)}>{title}</a>
          </li>
        {/each}
      </ul>
      `}
    </Code>
    <p>
      Links are ordered by their file's index, which you can set with metadata.
      <code>{`<!-- rou`}{`tify:options index=3 -->`}</code>
      . To omit a file from navigation, set index to
      <code>false</code>.
    </p>

    <p>
      External links and hash links can be added with the children metadata.
    </p>
    <Code language="svelte">
      {`
      <!-- rou`}{`tify:options children=[
        {title: "Github", icon:"github", path: "//github.com/sveltech/routify"},
        {title: "Discord", icon:"discord", path: "//discord.gg/ntKJD5B"},
        {title: "Twitter", icon:"twitter", path: "//twitter.com/routifyjs"}
      ] -->
    `}
    </Code>
  </div>
  <div class="c-container-vertical c-container-vertical--small">
    <h3 class="c-h3">&lt;a&gt; default Navigation</h3>
    <p>
      If you want to use anchor's default navigation behaviour you can do so by adding the
      <code>target</code> attribute.
    </p>
    <p>Routify will ignore all anchors with <code>target</code> attribute.</p>
    <Code language="svelte">
      {`
      <a href="/non-routify-page" target="_self">Legacy Navigation</a>
      `}
    </Code>
  </div>
</div>
