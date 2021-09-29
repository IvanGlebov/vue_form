<template>
  <div>
    <div class="slider-component">
      <div v-show="errorI !== undefined && errorI !== ''" class="text-mainPink text-pt12">Это поле необходимо заполнить</div>
      <div class="slidecontainer">
        <input
            ref="input"
            v-model="currentValue"
            type="range"
            :min="min"
            :max="max"
            class="slider"
            :style="{background: `linear-gradient(to right, #0CE2F4 0%, #0CE2F4 ${currentValue}%, black ${currentValue}%, black 100%)`}"
            @input="$emit('input', currentValue)"
        >
        <span v-bind:style="{
          'margin-left': `${currentValue < 3 ? '0%' : ( currentValue > 94 ? 'calc(100% - 45px)' : 0.98 * currentValue + '%')}`,
          'margin-right': `${currentValue > 94 ? 0 : 'auto'}%`
        }"
          class="text-left text-mainBlue text-pt16 h-0 block transition duration-500"
        >{{currentValue}}%</span>
        <div class="flex justify-between">
          <div class="text-pt16 transition duration-300" :class="[currentValue < 4 ? 'opacity-0' : '']">
            {{min}}%
          </div>
          <div class="text-pt16 transition duration-300" :class="[currentValue > 90 ? 'opacity-0' : '']">
            {{max}}%
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      // type: Number,
      required: true
    },
    min: {
      type: Number,
      required: true
    },
    max: {
      type: Number,
      required: true
    },
    error: String
  },
  emits: ['input'],
  data() {
    return {
      errorI: '',
      currentValue: this.value,
    };
  },
  methods: {
    onInput() {
      this.$emit('input', parseInt(this.currentValue));
    },
    setError: function(error) {
      this.errorI = error
    }
  },
  created() {
    // this.width = this.$refs.input.clientWidth
  }
};
</script>

<style scoped>
.slider-component .slidecontainer {
  width: 100%;
}

.slider-component .slidecontainer .slider {
  -webkit-appearance: none;
  appearance: none;
  width: 100%;
  height: 2px;
  border-radius: 2px;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

.slider-component .slidecontainer .slider:hover {
  opacity: 1;
}

.slider-component .slidecontainer .slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 16px;
  height: 16px;
  @apply bg-mainBlue;
  border: 1px solid black;
  /*background: #D8A22E;*/
  cursor: pointer;
  border-radius: 50%;
}

.slider-component .slidecontainer .slider::-moz-range-thumb {
  width: 18px;
  height: 18px;
  background: #D8A22E;
  cursor: pointer;
  border-radius: 50%;
}
</style>