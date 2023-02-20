<script>
  import { onMount } from "svelte";
  import Button from "../common/Button/Button.svelte";
  import BookGrid from "./BookGrid.svelte";
  import { httpGet } from "../common/api/api";

  let books;
  onMount(async function () {
    const { data } = await httpGet("/?_sort=id&_order=desc");
    books = data;
  });
</script>

<div />

<header>
  <span class="preamble">Welcome to the</span>
  <h1>Library</h1>
</header>

<p class="greeting">This is a library for the people. Welcome. Be inspired.</p>

<Button to="/create">+ Add Book</Button>
<BookGrid {books} />

<style>
  header {
    margin: var(--spacingMedium) 0 var(--spacingLarge) 0;
    text-transform: uppercase;
  }
  .preamble {
    display: block;
  }
  h1 {
    font-size: var(--typeSizeXXLarge);
    font-weight: var(--typeWeightBold);
    line-height: var(--typeLineHeightTight);
  }

  .greeting {
    font-size: var(--typeSizeSmall);
  }
</style>
