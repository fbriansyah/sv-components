<script>
  import { createEventDispatcher } from "svelte";

  export let isMenuShow = false;
  export let options = [];
  export let selected = {};
  export let name = "";

  const dispatch = createEventDispatcher();

  const selectItemHandler = (option) => {
    dispatch("change", { name: name, value: option });
  };
</script>

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

<style lang="postcss">
  .label {
    @apply block truncate;
  }
  .icon {
    @apply absolute inset-y-0 right-0 flex items-center pr-3;
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
