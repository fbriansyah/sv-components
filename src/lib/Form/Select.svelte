<script>
  import { createEventDispatcher } from "svelte";
  import ListOptions from "./ListOptions.svelte";

  export let label = "Field Label";
  export let name = "field-name";
  export let options = [{ value: "", label: "Choose one" }];
  export let selected = options[0];

  let isMenuShow = false;
  const dispatch = createEventDispatcher();
  const toggleMenu = () => (isMenuShow = !isMenuShow);
  const changeHandler = (event) => {
    isMenuShow = false;
    dispatch("change", { ...event.detail });
  };
</script>

<div>
  <label for={name}>{label}</label>
  <div class="relative mt-1">
    <button type="button" on:click={toggleMenu}>
      <span class="label">{selected.label}</span>
      <span class="icon">
        <i class="ri-arrow-right-s-fill" class:show={isMenuShow} />
      </span>
    </button>
    <ListOptions on:change={changeHandler} {name} {options} {selected} {isMenuShow} />
  </div>
</div>

<style lang="postcss">
  label {
    @apply block text-base font-medium text-gray-900;
  }
  button {
    @apply relative w-full border border-gray-300 rounded-md;
    @apply text-left text-sm shadow-sm bg-white py-2 pl-3 pr-9;
    @apply cursor-default focus:outline-none focus:border-indigo-500;
    @apply focus:ring-1 focus:ring-indigo-500;
  }
  .label {
    @apply block truncate;
  }
  .icon {
    @apply absolute inset-y-0 right-0 flex items-center pr-2;
  }
  i {
    @apply text-xl text-gray-400;
  }
  i.show {
    @apply rotate-90;
  }
</style>
