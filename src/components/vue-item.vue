<template>
    <div class="item" :class="inRange ? 'in-range' : ''" :style="style">

    </div>
</template>

<script>
const nodeWidth = 10;
export default {
    data: () => ({ 
        style: '',
    
    }),
  props: {
    index: Number,
    height: Number,
    range: Array
  },
  mounted() {
    this.style = `height: ${this.height}vh; width: ${nodeWidth}px`;
  },
  computed: {
    inRange() {
      const [ lower, upper ] = this.range
      return this.index >= lower && this.index < upper;
    }
  }
}
</script>

<style>

</style>