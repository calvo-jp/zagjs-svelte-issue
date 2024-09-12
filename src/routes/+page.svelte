<script lang="ts">
  import * as collapsible from "@zag-js/collapsible";
  import { normalizeProps, reflect, useMachine } from "@zag-js/svelte";
  import { uid } from "uid";

  let id = uid();

  let open = $state(false);

  let context: collapsible.Context = reflect(() => ({
    id,
    open,
    "open.controlled": true,
    onOpenChange(detail) {
      open = detail.open;
    },
  }));

  let [snapshot, send] = useMachine(collapsible.machine(context), { context });

  let api = reflect(() => collapsible.connect(snapshot, send, normalizeProps));
</script>

<div {...api.getRootProps()}>
  <button type="button" {...api.getTriggerProps()}>
    {#if open}
      Close
    {:else}
      Open
    {/if}
  </button>

  <p {...api.getContentProps()}>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Sint fugiat
    dolorum, modi consectetur aspernatur magni cumque adipisci inventore labore
    doloremque magnam error iure! Blanditiis, culpa porro? Pariatur nam unde
    exercitationem. Amet minima dolorem perspiciatis voluptates harum magnam
    culpa? Eaque possimus voluptatem pariatur! Animi sit quisquam nostrum ad
    vitae eum deleniti!
  </p>
</div>
