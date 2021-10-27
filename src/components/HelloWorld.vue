<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ count }}</h1>
    <h1>{{ double }}</h1>
    <h1>{{ person.name }}</h1>
    <ul>
      <li>试试一</li>
      <li>试试二</li>
    </ul>
    <button @click="increase">+</button>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, reactive, ref, watch } from 'vue'
interface Person {
  name: string
  sex: string
}
export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  setup() {
    const count = ref(0)
    const person = reactive({ name: 'chen', sex: '男' })
    const increase = () => {
      count.value++
    }
    const double = computed(() => {
      return count.value * 2
    })
    person.name = 'wc'
    watch(double, (newV, oldV) => {
      console.log(newV, oldV)
    })
    return {
      count,
      increase,
      person,
      double,
    }
  },
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
