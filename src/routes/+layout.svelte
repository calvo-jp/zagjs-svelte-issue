<script lang="ts">
  import "@fontsource/inter/400.css";
  import "@fontsource/inter/500.css";
  import "@fontsource/inter/600.css";
  import "@fontsource/inter/700.css";

  let { children } = $props();
</script>

<main style="padding:2rem;">
  {@render children()}
</main>

<style>
  :global(*),
  :global(*::before),
  :global(*::after) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(ul),
  :global(ol) {
    list-style: none;
  }

  :global(a) {
    text-decoration: none;
    color: inherit;
  }

  :global(html) {
    font-size: 16px;
    line-height: 1.25;
    color-scheme: light;
  }

  :global(body) {
    font-family:
      "Inter",
      system-ui,
      -apple-system,
      BlinkMacSystemFont,
      "Segoe UI",
      Roboto,
      Oxygen,
      Ubuntu,
      Cantarell,
      "Open Sans",
      "Helvetica Neue",
      sans-serif;
    font-size: 100%;
    color: var(--color-default);
    background: white;
  }

  :global(input),
  :global(select),
  :global(textarea),
  :global(button) {
    font: inherit;
    color: inherit;
    background: transparent;
    display: inline-block;
    border: none;
  }

  :global(button) {
    cursor: pointer;
  }

  :global(button:disabled),
  :global(button[data-disabled]) {
    cursor: not-allowed;
    opacity: 0.5;
  }

  :global(label) {
    display: inline-block;
  }

  :global(table) {
    border-collapse: collapse;
  }

  :global(image) {
    display: block;
    max-width: 100%;
    height: auto;
  }

  :global(label) {
    display: inline-block;
  }

  :global([hidden]) {
    display: none !important;
  }

  :global(h1),
  :global(h2),
  :global(h3),
  :global(h4),
  :global(h5),
  :global(h6) {
    font-weight: 600;
  }

  :global(h1) {
    font-size: 2.25rem;
  }

  :global(h2) {
    font-size: 1.875rem;
  }

  :global(h3) {
    font-size: 1.5rem;
  }

  :global(h4) {
    font-size: 1.25rem;
  }

  :global(h5) {
    font-size: 1.125rem;
  }

  :global(h6) {
    font-size: 1rem;
  }
</style>
