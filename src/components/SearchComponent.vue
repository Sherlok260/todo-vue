<template>
  <div>
      <input class="form-control" type="search" placeholder="Search" v-model="search_text" v-on:keyup="keyboard" v-on:keydown="keyboard">
  </div>
</template>

<script>
export default {
    name: "SearchComponent",
    data() {
        return {
            search_text: ''
        }
    },
    methods: {
        keyboard() {
            // if(this.search_text.length != 0) {
                this.$emit("search_text", this.search_text)
            // }
        },
    }
}
</script>

<style scoped>
  /*input {*/
  /*    */
  /*    padding: 5px;*/
  /*    border-radius: 10px;*/
  /*    border: 1px solid black;*/
  /*    width: 100%;*/
  /*}*/
</style>