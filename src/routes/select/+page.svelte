<script lang="ts">
  import * as select from "@zag-js/select";
  import { normalizeProps, reflect, useMachine } from "@zag-js/svelte";
  import { uid } from "uid";

  let id = uid();

  let items = $state([
    { label: "Item 1", value: "1" },
    { label: "Item 2", value: "2" },
    { label: "Item 3", value: "3" },
    { label: "Item 4", value: "4" },
    { label: "Item 5", value: "5" },
  ]);

  let value: string[] = $state([]);

  let collection = $derived(select.collection({ items }));

  let context: select.Context = reflect(() => ({
    id,
    value,
    onValueChange(detail) {
      value = detail.value;
    },
    multiple: true,
    collection,
  }));

  let [snapshot, send] = useMachine(select.machine(context), {
    // Adding this causes an issue
    // context,
  });

  let api = reflect(() => select.connect(snapshot, send, normalizeProps));

  $effect(() => {
    // doesn't work because context is not controlled
    setTimeout(() => {
      value = ["1", "2", "3"];
    }, 250);
  });

  $inspect({ value });
</script>

<div {...api.getRootProps()}>
  <div {...api.getControlProps()}>
    <label for="" {...api.getLabelProps()}>Label</label>
    <button {...api.getTriggerProps()}>
      <span {...api.getValueTextProps()}>
        {#if api.valueAsString}
          {api.valueAsString}
        {:else}
          Please Select
        {/if}
      </span>
      <span {...api.getIndicatorProps()}>▼</span>
    </button>
  </div>

  <div {...api.getPositionerProps()}>
    <ul {...api.getContentProps()}>
      {#each items as item}
        <li {...api.getItemProps({ item })}>
          <span>{item.label}</span>
          <span {...api.getItemIndicatorProps({ item })}>✓</span>
        </li>
      {/each}
    </ul>
  </div>

  <select {...api.getHiddenSelectProps()}></select>
</div>
