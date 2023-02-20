<script>
  import BackButtonRow from "../common/BackButtonRow/BackButtonRow.svelte";
  import BookCover from "../common/BookCover/BookCover.svelte";
  import Button from "../common/Button/Button.svelte";
  import Header from "../common/Header/Header.svelte";
  import { httpPost } from "../common/api/api.js";
  import TextInput from "../common/TextInput/TextInput.svelte";
  import { navigate } from "svelte-routing";

  let title = "";
  let author = "";
  let cover = "";
  let about = "";

  $: book = { title, author, cover, about };

  const handleSubmit = async () => {
    const newBook = { ...book, variation: 0, favorite: false };
    const { ok } = await httpPost("/", newBook);
    if (ok) {
      navigate("/");
    }
  };
</script>

<BackButtonRow />

<Header element="h1" size="large">Create</Header>

<form on:submit|preventDefault={handleSubmit}>
  <div class="fields">
    <TextInput label="Title" bind:value={title} />
    <TextInput label="Author" bind:value={author} />
    <TextInput label="Cover URL" bind:value={cover} />
    <TextInput label="About" multiline bind:value={about} />
    <div>
      <Button>Save</Button>
    </div>
  </div>

  <div>
    <Header>Preview</Header>
    <div class="preview">
      <BookCover {book} />
    </div>
  </div>
</form>

<style>
  form {
    display: grid;
    grid-auto-rows: auto;
    grid-template-columns: 1fr;
    gap: var(--spacingXLarge);
  }
  .fields {
    display: grid;
    grid-auto-rows: auto;
    gap: var(--spacingMedium);
  }
  .preview {
    display: grid;
    grid-template-columns: minmax(20vw, 10rem);
    grid-template-rows: minmax(32vw, 16rem);
  }
  @media (min-width: 48rem) {
    form {
      grid-template-columns: 60vw 20vw;
    }
  }
</style>
