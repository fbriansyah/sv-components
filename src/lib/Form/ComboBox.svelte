<script>
  import { createEventDispatcher } from "svelte";

  import ListOptions from "./ListOptions.svelte";

  export let label = "Field Label";
  export let name = "field-name";
  export let options = [{ value: "", label: "Choose one" }];
  export let selected = options[0];

  $: filteredOptions = filter(options, searchedText);

  let isMenuShow = false;
  let searchedText = "";
  const dispatch = createEventDispatcher();

  const toggleMenu = () => (isMenuShow = !isMenuShow);
  const changeHandler = (event) => {
    isMenuShow = false;
    searchedText = "";
    dispatch("change", { ...event.detail });
  };
  function filter(list, text) {
    if (text !== "") {
      return list.filter((item) => {
        return item.label
          .toLowerCase()
          .includes(text.toLowerCase());
      });
    } else {
      return list;
    }
  }
  const inputHandler = (e) => {
    searchedText = e.target.value;
  };
</script>

<div>
  <label for="search-{name}">{label}</label>
  <div class="relative mt-1">
    <input
      on:focus={() => (isMenuShow = true)}
      on:input={inputHandler}
      id="search-{name}"
      type="text"
      value={selected.label}
    />
    <button type="button" class:show={isMenuShow} on:click={toggleMenu}>
      <i class="ri-arrow-right-s-fill" />
    </button>
    <ListOptions
      on:change={changeHandler}
      {name}
      options={filteredOptions}
      {selected}
      {isMenuShow}
    />
  </div>
</div>

<style lang="postcss">
  label {
    @apply block text-base font-medium text-gray-900;
  }
  input {
    @apply w-full rounded-md border border-gray-300 bg-white;
    @apply py-2 pl-3 pr-12 shadow-sm text-sm focus:border-indigo-500;
    @apply focus:outline-none focus:ring-1 focus:ring-indigo-500;
  }
  button {
    @apply absolute inset-y-0 right-0 flex items-center px-2;
  }
  i {
    @apply text-xl text-gray-400;
  }
  .show {
    @apply rotate-90;
  }
</style>
