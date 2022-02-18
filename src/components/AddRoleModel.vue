<template>
  <b-form>
    <b-form-input v-model="text" placeholder="Enter your name"></b-form-input>
  </b-form>
</template>

<script>
export default {
  name: "AddRoleModel",
  data(){
    return{
      text:''
    }
  }
}
</script>

<style scoped>

</style>