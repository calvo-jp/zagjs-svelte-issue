<script lang="ts">
  import * as collapsible from "@zag-js/collapsible";
  import { normalizeProps, useMachine } from "@zag-js/svelte";

  const id = $props.id();
  const service = useMachine(collapsible.machine, { id });
  const api = $derived(collapsible.connect(service, normalizeProps));
</script>

<div {...api.getRootProps()}>
  <button {...api.getTriggerProps()}>Collapse Trigger</button>
  <div {...api.getContentProps()}>Collape Content</div>
</div>

<style>
  :global([data-scope="collapsible"][data-part="root"]) {
    max-width: 400px;
  }

  :global([data-scope="collapsible"][data-part="trigger"]) {
    padding-left: 14px;
    padding-right: 14px;
    height: 40px;
    border: 1px solid oklch(87.2% 0.01 258.338);
  }

  :global([data-scope="collapsible"][data-part="content"]) {
    margin-top: 8px;
    color: var(--color-muted);
    overflow: hidden;
  }

  :global([data-scope="collapsible"][data-part="content"][data-state="open"]) {
    animation: fade-collapse-in 250ms;
  }

  :global(
    [data-scope="collapsible"][data-part="content"][data-state="closed"]
  ) {
    animation: fade-collapse-out 150ms;
  }

  @keyframes fade-collapse-in {
    from {
      opacity: 0;
      height: 0;
    }
    to {
      opacity: 1;
      height: var(--height);
    }
  }

  @keyframes fade-collapse-out {
    from {
      opacity: 1;
      height: var(--height);
    }
    to {
      opacity: 0;
      height: 0;
    }
  }
</style>
