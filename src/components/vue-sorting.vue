<template>
    <div class="container">
      <div class="controls">
        <label class="control_delay">Delay (ms) </label><input type="number" placeholder="Delay" step="100" v-model="delay"/>
        <button class="btn btn-sort" type="button" v-on:click="mergeSort()">Merge Sort</button>
        <button class="btn btn-sort" type="button" v-on:click="quickSort()">Quick Sort</button>
        <button class="btn btn-sort" type="button" v-on:click="bubbleSort()">Bubble Sort</button>
        <button class="btn btn-sort" type="button" v-on:click="generateNodes()">Randomize</button>


      </div>
      <vue-item v-for="(node, i) in nodes"
                :key="node.key"
                :height="node.value"
                :index="i"
                :range="[lowerRange, upperRange]"/>
    </div>

</template>

<script>
import vueitem from './vue-item';
const nodeWidth = 10;


export default {
      data: () => ({
    nodes: [],
    delay: 200,
    lowerRange: 0,
    upperRange: 0,
  }),
  mounted() {
    this.generateNodes();
    // this.quickSort();

  },
  components:{
      'vue-item': vueitem
  },
  methods: {
    comparer: (a, b) => a.value > b.value,
    generateNodes() {
      this.nodes = [];
      this.$nextTick(() => {
        const numberOfNodes = Math.floor(window.innerWidth/nodeWidth);
        this.nodes = [...Array(numberOfNodes)].map((x, key) => ({ key , value: Math.floor(Math.random()*100)}));
      });
    },
    bubbleSort: function(){
        const len = this.nodes.length;
        for(let i = len-1; i>=0; i--){
          for(let j = 1; j<=i; j++){
            setTimeout(()=>{
                if(this.comparer(this.nodes[j-1],this.nodes[j])){
                this.swap(j-1, j);
            }
          },this.delay);
        }
      }
    },
    

    merge(arr,L = null, R = null){
      let i = 0;
      let j = 0;
      let k = 0;
      while(i<L.length && j < R.length){
        // setTimeout(() => {
        if(this.comparer(L[i],R[j])){
          // this.nodes[k] = L[i];
          // this.swap(this.nodes[k],L[i]);
          this.$set(arr, k, L[i]);
          i++;
        }
        else{
          // this.nodes[k] = R[j];
          this.$set(arr, k, R[j]);
          // this.swap(this.nodes[k],R[j]);
          j++
        }
        k++
      // },this.delay);
      }
      while(i < L.length){
        // setTimeout(() => {
        // this.nodes[k] = L[i];
        this.$set(arr, k, L[i]);
        // this.swap(this.nodes[k],L[i]);
        i++;
        k++;
        // },this.delay);
      }
      while(j < R.length){
        // setTimeout(() => {

        // this.nodes[k] = R[j];
        this.$set(arr, k, R[j]);
          // this.swap(k,R[j]);
        j++;
        k++;
        // },this.delay);
      }
      
    },

    mergeSort(arr = null){
        if(arr === null){
          arr = this.nodes;
        }
        if(arr.length <= 1){
          return arr;
        }
        if (arr.length > 1){

            // let mid = (arr.length/2).floor;
            let mid = Math.floor(arr.length/2);
            let L = arr.slice(0,mid);
            let R = arr.slice(mid, );
            this.mergeSort(L);
            this.mergeSort(R);
            setTimeout(() => {
              return this.merge(arr,L,R)
            },this.delay);
        }
    },

    quickSort(i = null, j = null) {
      setTimeout(() => {
        if (i === null) i = 0;
        if (j === null) j = this.nodes.length - 1;
        // this.lowerRange = i;
        // this.upperRange = j;
        if (i >= j) {
          return;
        }
        const pivot = this.partition(i, j);
        this.quickSort(i, pivot - 1);
        this.quickSort(pivot + 1, j);
      }, this.delay);
    },

    partition(min, max) {
      const pivot = max;
      let wall = min;
      for (let i = wall; i <= max; i++) {
        if(this.comparer(this.nodes[i], this.nodes[pivot])) {
          this.swap(i, wall)
          wall++;
        }
      }
      this.swap(wall, pivot);
        return wall;
    },

    swap(from, to) {
      const tmp = this.nodes[from];
      this.$set(this.nodes, from, this.nodes[to]);
      this.$set(this.nodes, to, tmp);
    }
  },
}
</script>

<style>

</style>