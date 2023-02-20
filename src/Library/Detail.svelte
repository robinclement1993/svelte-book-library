<script>
  import { onMount } from "svelte";

  import BackButtonRow from "../common/BackButtonRow/BackButtonRow.svelte";
  import Header from "../common/Header/Header.svelte";
  import BookCover from "../common/BookCover/BookCover.svelte";
  import Button from "../common/Button/Button.svelte";
  import { httpGet, httpPut } from "../common/api/api";

  export let id;

  let book = {};

  onMount(async (_) => {
    const { data } = await httpGet("/" + id);
    book = data;
  });

  const handleFavoriteClick = async () => {
    const toggledBook = { ...book, favorite: !book.favorite };
    const { ok } = await httpPut("/" + book.id, toggledBook);
    if (ok) {
      book = toggledBook;
    }
  };
</script>

<BackButtonRow />

<Header element="h1" size="large">Discover</Header>

<div class="detail">
  <div class="cover">
    <BookCover {book} />
    <div class="favorite">
      <Button on:click={handleFavoriteClick}
        >{book.favorite ? "Unfavorite" : "Favorite"}</Button
      >
    </div>
  </div>
  <div>
    <Header>About</Header>
    <p>{book.about}</p>
  </div>
</div>

<style>
  .detail {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(40vw, 20rem));
    grid-template-rows: minmax(64vw, 32rem) auto;
    gap: var(--spacingXLarge);
  }
  .cover {
    position: relative;
    display: flex;
    margin-bottom: var(--spacingXLarge);
  }
  .favorite {
    position: absolute;
    width: 90%;
    left: calc(10% + var(--spacingSmall));
    bottom: var(--spacingLarge);
  }
</style>
