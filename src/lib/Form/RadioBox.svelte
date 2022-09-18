<script>
  import { createEventDispatcher } from "svelte";

  export let name = 'radio-name';
  export let label = 'Radio Label';
  export let hint = '';
  export let options = [
    { value: "item-1", label: "Item 1" },
    { value: "item-2", label: "Item 2" },
  ]
  export let checked = options[0];

  const dispatch = createEventDispatcher();

  function changeHandler(option) {
    dispatch('change', {name, value:option})
  }
</script>

<div>
  <legend for="id">{label}</legend>
  {#if hint !== ''}
    <p>{hint}</p>
  {/if}
  <fieldset>
    {#each options as opt}
      <div class="flex items-center" on:click="{() => changeHandler(opt)}">
        <input type="radio" id="{opt.value}" name="{name}" checked={checked.value === opt.value} />
        <label for="{opt.value}">{opt.label}</label>
      </div>
    {/each}
  </fieldset>
</div>

<style lang="postcss">
  legend {
    @apply text-base text-gray-900 font-medium;
  }
  p {
    @apply text-sm leading-5 text-gray-500;
  }
  fieldset {
    @apply mt-2 space-y-3;
  }
  input {
    @apply border-gray-300 text-indigo-600 focus:ring-indigo-500;
  }
  label {
    @apply block ml-3 text-sm text-gray-700 font-medium;
  }
</style>
