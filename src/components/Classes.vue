<template>
  <div>
    <h1 class="vueStyle">Static Class and Style Bindings</h1>
    <h1 v-bind:style="{ color: colorName }">
      Dynamic Class and Style Bindings
    </h1>
    <h1 v-bind:class="['display', 'vueStyleObj']">Class with Array</h1>
    <h1 v-bind:class="[show ? 'vueStyle' : 'display']">Class with Array</h1>
    <h1 v-bind:class="{ display: show, vueStyleObj: show, hide: hide }">
      Class with Object
    </h1>
    <button v-on:click="showClass">Toggle</button>
    <button v-on:click="showValue">Toggle hide/show</button>
  </div>
</template>
<script>
export default {
  name: "Classes",
  data() {
    return {
      show: false,
      colorName: "blue",
      hide: false,
    };
  },
  methods: {
    showValue() {
      this.hide = !this.hide;
    },
    showClass() {
      this.show = !this.show;
    },
  },
};
</script>

<style scoped>
.vueStyle {
  color: orange;
}
.vueStyleObj {
  color: white;
}

.display {
  background-color: coral;
}

.hide {
  display: none;
}
</style>