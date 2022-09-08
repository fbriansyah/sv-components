<script>
  import "remixicon/fonts/remixicon.css";
  import Select from "./lib/Form/Select.svelte";

  const listOfPets = [
    { value: "cat", label: "Cat" },
    { value: "dragon", label: "Dragon" },
    { value: "penguin", label: "Penguin" },
  ];
  const listOfFruits = [
    { value: "apple", label: "Apple" },
    { value: "orange", label: "Orange" },

  ]

  let state = {
    pet: { value: "cat", label: "Cat" },
    fruit: { value: "orange", label: "Orange" },
  };

  const changeHandler = (event) => {
    const {detail} = event;
    const {name, value} = detail;
    state = {
      ...state,
      [name]: value
    }
    console.log(state);
  }
</script>

<main>
  <h1>Svelte Components</h1>
  <form class="mt-6 space-y-3">
    <Select
      label="Favorite Pet"
      name="pet"
      options={listOfPets}
      selected={state.pet}
      on:change={changeHandler}
    />
    <Select
      label="Favorite Fruit"
      name="fruit"
      options={listOfFruits}
      selected={state.fruit}
      on:change={changeHandler}
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
