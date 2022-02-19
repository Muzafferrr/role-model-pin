<template>
  <div class="addRoleModel mt-3">
    <b-img :src="imageSource" v-bind="mainProps" rounded></b-img>
    <b-form>
      <b-form-input class="mt-2" v-model="modelName" placeholder="What is your role model name?"></b-form-input>
      <b-form-input class="mt-2" v-model="modelJob" placeholder="What is his job?"></b-form-input>
      <b-form-input class="mt-2" v-model="modelNationality" placeholder="What is his nationality?"></b-form-input>
      <b-form-input class="mt-2" v-model="modelPicture" placeholder="Add his picture link"></b-form-input>
      <b-form-datepicker class="mt-2" v-model="modelBirthday" placeholder="Choose his birthday"></b-form-datepicker>
      <b-form-textarea class="mt-2" v-model="modelAbout" rows="3" max-rows="6"
                       placeholder="Notes about him..."></b-form-textarea>
      <b-form-tags class="mt-2" v-model="tags" input-id="tags-basic"></b-form-tags>
      <b-button class="mt-2" block variant="outline-primary" @click="sendRoleModel()">Add Role Model</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  name: "AddRoleModel",
  data() {
    return {
      imageSource: 'https://us.123rf.com/450wm/kakigori/kakigori1808/kakigori180800024/107433935-cute-funny-man-dad-and-kid-son-wearing-black-mustache-mask.jpg?ver=6',
      modelName: '',
      modelJob: '',
      modelNationality: '',
      modelPicture: '',
      modelBirthday: '',
      modelAbout: '',
      value: '',
      tags: [],
      mainProps: {width: 150, height: 150, class: 'm1'}
    }
  },
  methods: {
    sendRoleModel() {
      const a = [this.modelName, this.modelJob, this.modelNationality, this.modelBirthday,
        this.modelAbout, this.modelPicture, this.tags];
      this.$emit('fromAddRoleModel', a);
    }
  }
}
</script>

<style scoped>
.addRoleModel {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>