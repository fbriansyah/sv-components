<script>
  import { createEventDispatcher } from "svelte";

  export let name = "checkbox-name";
  export let label = "Checkbox Label";
  export let hint = "";
  export let options = [
    {
      value: "item-1",
      label: "Item 1",
      description: "lorem ipsum dolor sit amet",
    },
    {
      value: "item-2",
      label: "Item 2",
      description: "lorem ipsum dolor sit amet",
    },
  ];
  export let checked = [];

  let values = [...checked]

  const dispatch = createEventDispatcher();

  function changeHandler(e, option) {
    if(e.target.checked) {
      // console.log("add", option.value);
      values.push(option.value)
    } else {
      // console.log("remove", option.value);
      values = values.filter(item => item !== option.value)
    }
    dispatch("change", { name, value: values });
  }
</script>

<div>
  <legend for="id">{label}</legend>
  {#if hint !== ""}
    <p class="hint">{hint}</p>
  {/if}

  <fieldset>
    {#each options as opt}
      <div class="relative flex items-start">
        <div class="flex h-5 items-center">
          <input
            id={opt.value}
            on:click={(e) => changeHandler(e, opt)}
            aria-describedby="{name}-description"
            {name}
            type="checkbox"
            checked={checked.includes(opt.value)}
          />
        </div>
        <div class="ml-3 text-sm">
          <label for={opt.value}>{opt.label}</label>
          <p id="{opt.value}-description">{opt.description}</p>
        </div>
      </div>
    {/each}
  </fieldset>
</div>

<style lang="postcss">
  legend {
    @apply text-base text-gray-900 font-medium;
  }
  .hint {
    @apply text-sm leading-5 text-gray-500;
  }
  p {
    @apply text-gray-500;
  }
  fieldset {
    @apply mt-2 space-y-3;
  }
  input {
    @apply h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500;
  }
  label {
    @apply font-medium text-gray-700;
  }
</style>
