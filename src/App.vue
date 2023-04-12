<script setup lang="ts">
import { ref, reactive, computed } from 'vue';

  const red = ref(0);
  const green = ref(0);
  const blue = ref(0);

  let paletteColor = computed(() => {
    return `rgb(${red.value}, ${green.value}, ${blue.value})`
  });

</script>

<template>
  <div class="container mt-5">
    <div class="palette" :style="{backgroundColor:paletteColor}"></div>
    <p class="mt-2">background-color: {{ paletteColor }};</p>
    <div class="row mt-5">
      <dl class="col-md-4 col-12">
        <dt>
          <label for="red" class="form-label label label--red">red</label>
        </dt>
        <dd>
          <input type="range" class="form-range" min="0" max="255" id="red" v-model="red">
        </dd>
        <dd>
          <input type="text" class="form-control" id="red" v-model="red">
        </dd>
      </dl>
      <dl class="col-md-4 col-12">
        <dt>
          <label for="green" class="form-label label label--green">green</label>
        </dt>
          <input type="range" class="form-range" min="0" max="255" id="green" v-model="green">
        <dd>
        </dd>
        <dd>
          <input type="text" class="form-control" id="green" v-model="green">
        </dd>
      </dl>
      <dl class="col-md-4 col-12">
        <dt>
          <label for="blue" class="form-label label label--blue">blue</label>
        </dt>
        <dd>
          <input type="range" class="form-range" min="0" max="255" id="blue" v-model="blue">
        </dd>
        <dd>
          <input type="text" class="form-control" id="blue" v-model="blue">
        </dd>
      </dl>
    </div>
  </div>
</template>

<style scoped>
.palette {
  height: 200px;
  border: 1px solid #ccc;
}
.palette-text {

}
.label {
  font-weight: 700;
  text-transform: capitalize;
}
.label::first-letter {
  font-size: 1.5em;
}
.label--red {
  color: red;
}
.label--green {
  color: green;
}
.label--blue {
  color: blue;
}
input[type='range'] {
  width: 100%;
}
</style>
