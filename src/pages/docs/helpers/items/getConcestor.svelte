<script>
  import FunctionDoc from "@/components/FunctionDoc.svelte";
  import Code from "@/components/Code.svelte";
  import Note from "@/components/Note.svelte";

  const params = [
    {
      type: "Layout | Page",
      name: "path1",
      description: "First Page/Layout"
    },
    {
      type: "Layout | Page",
      name: "path2",
      description: "Second Page/Layout."
    }
  ];
</script>

<!-- routify:options index=1400 -->

<FunctionDoc name="getConcestor" {params}>
  <p>
    Takes two components and returns their closest shared layout and their
    sibling ancestors.
  </p>

  <Code language="svelte">
    {`
      <`}{`script>
        import { route, getConcestor } from '@roxi/routify'
        $: lastRoute = $route.last
        $: ([concestor, ancestor, oldAncestor] = getConcestor($route, lastRoute))
        $: direction = ancestor.meta.$index - oldAncestor.meta.$index
      </script>
    `}
  </Code>

  <Note type="info">
      <code>getConcestor</code>
      is used by
      <code>getDirection</code>
      to determine the direction when navigating.
  </Note>

</FunctionDoc>
