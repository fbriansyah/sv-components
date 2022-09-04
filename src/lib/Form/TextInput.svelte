<script>
  export let isError = false;
  export let label = "Field Label";
  export let name = "field-name";
  export let type = "text";
  export let value = "";
  export let hint = "";
</script>

<div>
  <label for={name}>{label}</label>
  <div class="mt-1 relative">
    <input {type} {value} class:error={isError} id={name} {name} />
    <div class="icon">
      <i class="ri-error-warning-fill" />
    </div>
  </div>
  {#if hint !== ""}
    <p class:error={isError}>{hint}</p>
  {/if}
</div>

<style lang="postcss">
  label {
    @apply block text-sm text-gray-700 font-semibold;
  }
  input {
    @apply block w-full border-gray-300 rounded-md;
    @apply focus:border-indigo-600 focus:ring-indigo-600;
  }
  input.error {
    @apply border-red-300;
    @apply focus:border-red-600 focus:ring-red-600;
  }
  .icon {
    @apply absolute inset-y-0 right-0 pr-3;
    @apply hidden items-center text-red-600;
  }
  input.error + .icon {
    @apply flex;
  }
  p {
    @apply mt-1 text-sm text-gray-500;
  }
  p.error {
    @apply text-red-500;
  }
</style>
