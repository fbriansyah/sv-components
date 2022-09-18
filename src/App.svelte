<script>
  import "remixicon/fonts/remixicon.css";
  import CheckBox from "./lib/Form/CheckBox.svelte";
  import ComboBox from "./lib/Form/ComboBox.svelte";
  import RadioBox from "./lib/Form/RadioBox.svelte";
  import Select from "./lib/Form/Select.svelte";

  const listOfPets = [
    { value: "cat", label: "Cat" },
    { value: "dragon", label: "Dragon" },
    { value: "penguin", label: "Penguin" },
  ];
  const listOfFruits = [
    { value: "apple", label: "Apple" },
    { value: "orange", label: "Orange" },
    { value: "melon", label: "Melon" },
    { value: "water-melon", label: "Water Melon" },
    { value: "pineapple", label: "Pineapple" },
  ];
  const listItems = [
    { value: "item-1", label: "Item 1" },
    { value: "item-2", label: "Item 2" },
    { value: "item-3", label: "Item 3" },
  ];

  let state = {
    pet: { value: "cat", label: "Cat" },
    fruit: { value: "orange", label: "Orange" },
    radio: { value: "item-2", label: "Item 2" },
    ckbx: [],
  };

  const changeHandler = (event) => {
    const { detail } = event;
    const { name, value } = detail;
    state = {
      ...state,
      [name]: value,
    };
  };
</script>

<main>
  <h1>Svelte Components</h1>
  <form class="mt-6 space-y-3">
    <CheckBox
      label="Checkbox Field"
      name="ckbx"
      checked={state.ckbx}
      on:change={changeHandler}
    />
    <RadioBox
      label="Radio Button"
      hint="Lorem ipsum dolor sit amet"
      checked={state.radio}
      name="radio"
      options={listItems}
      on:change={changeHandler}
    />
    <Select
      label="Favorite Pet"
      name="pet"
      options={listOfPets}
      selected={state.pet}
      on:change={changeHandler}
    />
    <ComboBox
      label="Favorite Fruit"
      name="fruit"
      options={listOfFruits}
      selected={state.fruit}
      on:change={changeHandler}
    />
    <button type="button" on:click="{() => console.dir(state)}">Save</button>
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
