<template>
  <div>
    <div v-show="errorI !== undefined && errorI !== ''" class="text-mainPink text-pt12">{{errorI}}</div>
    <div
        v-bind:class="[!inputField ? clearClass : textClass]"
        class="text-mainBlue -z-10 text-left transition-all w-full pointer-events-none duration-300 outline-none"
    >{{title}}</div>
    <input
        v-bind:class="[errorI ? 'border-mainPink' : 'border-mainGray']"
        class="z-50 text-pt16 outline-none w-full border-t-0 border-l-0 border-r-0 border-b-2"
        id="input" v-model="inputField" @input="onInput"/>
  </div>
</template>

<script>
export default {
  name: "Input",
  props: {
    value: String,
    error: String,
    onChange: Function,
    title: String
    },
  emits: ['input'],
  data() {
    return {
      errorI: this.error,
      clearClass: 'text-pt16 transform translate-y-8',
      textClass: 'text-pt12 transform translate-y-0',
      inputField: this.value
    }
  },
  methods: {
    setError: function(error) {
      this.errorI = error
    },
    onInput() {
      this.$emit('input', this.inputField)
    }
  },
}
</script>

<style scoped>

</style>