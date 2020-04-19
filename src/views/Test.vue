<template>
  <div class="test">
    <h1>test page</h1>
    <h1>test count: {{count}}</h1>
    <h1>count * 2 = {{doubleCount}}</h1>
    <h1>state from vuex {{a}}</h1>

    <button @click="add">add</button>
    <button @click="update">update a</button>
  </div>
</template>

<script>
import { ref, computed, watch, getCurrentInstance } from "vue";

export default {
  setup() {
    const { ctx } = getCurrentInstance();
    console.log(ctx.$router.currentRoute.value);
    const count = ref(0);
    const add = () => {
      count.value++;
    };
    watch(
      () => count.value,
      val => {
        console.log(`count is ${val}`);
      }
    );
    const doubleCount = computed(() => count.value * 2);
    const a = computed(() => ctx.$store.state.test.a);
    const update = () => {
      ctx.$store.commit("setTestA", count);
    };
    return { count, doubleCount, add, a ,update};
  }
};
</script>

<style scoped>
.test {
  color: red;
}
</style>


