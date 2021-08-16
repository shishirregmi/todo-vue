<template>
  <div>
    <h1>Filters</h1>
    <h2>{{ name | Ucase }}</h2>
    <h2>{{ amount | convertCurrency }}</h2>
  </div>
</template>
<script>
export default {
  name: "Filters",
  data() {
    return {
      name: "Shishir Regmi",
      amount: 160,
    };
  },
  created() {
    console.warn("created");
  },
  beforeCreate() {
    console.warn("beforeCreate");
  },
};
</script>