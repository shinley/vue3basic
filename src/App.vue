<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <column-list :list="list"></column-list>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from '@/components/ColumnList.vue'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader.vue'

const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: '这是test1专栏， 有一段非常有意思的简介, 可以更新一下',
    avatar: require('@/assets/logo.png'),
  },
  {
    id: 2,
    title: 'test1的专栏',
    description: '这是test1专栏， 有一段非常有意思的简介, 可以更新一下',
    // avatar: require('./assets/logo.png'),
  },
  {
    id: 3,
    title: 'test1的专栏',
    description: '这是test1专栏， 有一段非常有意思的简介, 可以更新一下',
    avatar: require('./assets/logo.png'),
  },
  {
    id: 4,
    title: 'test1的专栏',
    description: '这是test1专栏， 有一段非常有意思的简介, 可以更新一下',
    avatar: require('./assets/logo.png'),
  },
]

const currentUser: UserProps = {
  id: 1,
  name: 'shinley',
  isLogin: true,
}
export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader,
  },
  setup() {
    return {
      list: testData,
      currentUser,
    }
  },
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
