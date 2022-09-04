<script>
  import "remixicon/fonts/remixicon.css";
  import TextInput from "./lib/Form/TextInput.svelte";
</script>

<main>
  <h1>Svelte Components</h1>
  <form class="mt-6 space-y-3">
    <TextInput label="Username" name="username" value="admin" />
    <TextInput
      label="Password"
      name="pass"
      type="password"
      isError
      hint="wrong password !!!"
    />
  </form>
</main>

<style lang="postcss">
  main {
    @apply p-2;
  }
  h1 {
    @apply text-xl font-semibold text-gray-700;
  }
</style>
