<script setup lang="ts">
import ColorList from './ColorList.vue';
import { ref, computed } from 'vue';

const red = ref<string>('0');
const green = ref<string>('0');
const blue = ref<string>('0');
const hexCode = ref<string>('#000');

const paletteColor = computed((): string => {
  const valCheck = (rgb: string): any => {
    if (rgb !== '') {
      rgb = Math.trunc(parseInt(rgb, 10)).toString();

      if (parseInt(rgb, 10) < 0) {
        return '0'
      } else if (parseInt(rgb, 10) > 255) {
        return '255'
      } else {
        return rgb;
      }
    } else {
      return '0';
    }
  };

  red.value = valCheck(red.value);
  green.value = valCheck(green.value);
  blue.value = valCheck(blue.value);

  return `rgb(${red.value}, ${green.value}, ${blue.value})`;
});

const toRgb = (): void => {
  hexCode.value = hexCode.value.replace('#', '');
  let hexValue: string[] = hexCode.value.split('');

  const val = /[0-9a-fA-F]/;
  let result: boolean = true;
  for (const str of hexValue) {
    if (!str.match(val)) {
      result = false;
    }
  }

  if (result) {
    if (hexValue.length === 3) {
      red.value = parseInt(hexValue[0].toString() + hexValue[0].toString(), 16).toString();
      green.value = parseInt(hexValue[1].toString() + hexValue[1].toString(), 16).toString();
      blue.value = parseInt(hexValue[2].toString() + hexValue[2].toString(), 16).toString();
    } else if (hexValue.length === 6) {
      red.value = parseInt(hexValue[0].toString() + hexValue[1].toString(), 16).toString();
      green.value = parseInt(hexValue[2].toString() + hexValue[3].toString(), 16).toString();
      blue.value = parseInt(hexValue[4].toString() + hexValue[5].toString(), 16).toString();
    }
    hexCode.value = `#${hexCode.value}`;
  } else {
    red.value = '255';
    green.value = '255';
    blue.value = '255';
    hexCode.value = '#fff'
  }
};

const toHex = (): void => {
  const generateHex = (rgb: string): string => {
    let hex: string = parseInt(rgb, 10).toString(16);
    if (hex.length === 1) {
      hex = `0${hex}`;
    }
    return hex;
  }

  let hexR: string = generateHex(red.value);
  let hexG: string = generateHex(green.value);
  let hexB: string = generateHex(blue.value);

  if (hexR === hexG && hexG === hexB && hexB === hexR) {
    if (
      hexR.substring(0, 1) === hexR.substring(1, 2) &&
      hexG.substring(0, 1) === hexG.substring(1, 2) &&
      hexB.substring(0, 1) === hexB.substring(1, 2)
    ) {
      hexR = hexR.substring(1, 2);
      hexG = hexG.substring(1, 2);
      hexB = hexB.substring(1, 2);
    }
  }

  hexCode.value = `#${hexR}${hexG}${hexB}`;
};
</script>
<template>
  <div class="container">
	<div class="mt-5">
	  <div class="palette" :style="{ backgroundColor: paletteColor }"></div>
	</div>
	<div class="row mt-5">
	  <div class="col-md-4 md-12">
		<p class="">background-color: {{ hexCode }};</p>
		<input @change="toRgb" class="form-control" placeholder="#000000" v-model="hexCode">
	  </div>
	</div>
    <div class="row mt-5">
      <p class="col-12">background-color: {{ paletteColor }};</p>
      <dl class="col-md-4 col-12">
        <dt>
          <label for="red" class="form-label label label--red">red</label>
        </dt>
        <dd>
          <input @change="toHex()" type="range" class="form-range" min="0" max="255" id="red" v-model="red">
        </dd>
        <dd>
          <input @change="toHex()" type="number" class="form-control" min="0" max="255" id="red" placeholder="0 to 255"
            v-model="red">
        </dd>
      </dl>
      <dl class="col-md-4 col-12">
        <dt>
          <label for="green" class="form-label label label--green">green</label>
        </dt>
        <input @change="toHex()" type="range" class="form-range" min="0" max="255" id="green" v-model="green">
        <dd>
        </dd>
        <dd>
          <input @change="toHex()" type="number" class="form-control" min="0" max="255" id="green" placeholder="0 to 255"
            v-model="green">
        </dd>
      </dl>
      <dl class="col-md-4 col-12">
        <dt>
          <label for="blue" class="form-label label label--blue">blue</label>
        </dt>
        <dd>
          <input @change="toHex()" type="range" class="form-range" min="0" max="255" id="blue" v-model="blue">
        </dd>
        <dd>
          <input @change="toHex()" type="number" class="form-control" min="0" max="255" id="blue" placeholder="0 to 255"
            v-model="blue">
        </dd>
      </dl>
    </div>
  </div>
</template>
<style scoped>
.palette {
  height: 200px;
  border: 1px solid #ccc;
  border-radius: 20px;
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