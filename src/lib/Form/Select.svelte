<script>
  import {createEventDispatcher} from 'svelte';

  export let label = "Field Label";
  export let name = "field-name";
  export let options = [
    { value: "", label: "Choose one" },
  ];
  export let selected = options[0];

  let isMenuShow = false;
  const dispatch = createEventDispatcher();

  const selectItemHandler = (option) => {
    dispatch('change', {name:name, value: option})
    isMenuShow = false;
  };
  const toggleMenu = () => (isMenuShow = !isMenuShow);
</script>

<div>
  <label for="{name}">{label}</label>
  <div class="relative mt-1">
    <button type="button" on:click={toggleMenu}>
      <span class="label">{selected.label}</span>
      <span class="icon">
        <i class="ri-arrow-right-s-fill" class:show={isMenuShow} />
      </span>
    </button>
    <ul class:hide={!isMenuShow}>
      {#each options as opt}
        <li
          on:click={() => selectItemHandler(opt)}
          class:active={selected.value === opt.value}
        >
          <span class="label">{opt.label}</span>
          {#if selected.value === opt.value}
          <span class="icon">
            <i class="ri-check-line" />
          </span>
          {/if}
        </li>
      {/each}
    </ul>
  </div>
</div>

<style lang="postcss">
  label {
    @apply block text-sm font-medium text-gray-700;
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
    @apply absolute inset-y-0 right-0 flex items-center pr-3;
  }
  button > .icon {
    @apply pr-2;
  }
  button > .icon > i {
    @apply text-xl text-gray-400;
  }
  button > .icon > i.show {
    @apply rotate-90;
  }
  ul {
    @apply absolute z-10 mt-1 py-1 w-full bg-white shadow-lg rounded-md;
    @apply ring-1 ring-black ring-opacity-10 text-sm;
    @apply max-h-60 overflow-auto focus:outline-none;
  }
  ul.hide {
    @apply transition ease-in duration-100 opacity-0;
    @apply w-0 h-0;
  }
  li {
    @apply py-2 pl-3 pr-9 relative select-none;
    @apply text-gray-900 hover:text-white hover:bg-indigo-500;
  }
  li.active {
    @apply text-indigo-600 hover:text-white;
  }
</style>
