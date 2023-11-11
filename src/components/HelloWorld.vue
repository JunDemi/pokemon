<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input v-model="message" placeholder="여기를 수정해보세요" @change="Calc">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    Calc() {
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
