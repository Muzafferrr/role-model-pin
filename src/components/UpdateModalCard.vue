<template>
  <div>
    <b-modal @hidden="hideModal()" ref="my-modal" hide-footer :title="modelName + ' -- Role Modal Card'">
      <b-form-input class="mt-2" v-model="modelName" placeholder="What is your role model name?"></b-form-input>
      <b-form-input class="mt-2" v-model="modelJob" placeholder="What is his job?"></b-form-input>
      <b-form-input class="mt-2" v-model="modelNationality" placeholder="What is his nationality?"></b-form-input>
      <b-form-input class="mt-2" v-model="modelPicture" placeholder="Add his picture link"></b-form-input>
      <b-form-datepicker class="mt-2" v-model="modelBirthday" placeholder="Choose his birthday"></b-form-datepicker>
      <b-form-textarea class="mt-2" v-model="modelAbout" rows="3" max-rows="6"
                       placeholder="Notes about him..."></b-form-textarea>
      <b-form-tags class="mt-2" v-model="tags" input-id="tags-basic"></b-form-tags>
      <b-button class="mt-2" variant="outline-warning" block @click="toggleModal">Update Role Modal</b-button>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    modelName: String,
    modelJob: String,
    modelNationality: String,
    modelBirthday: String,
    modelAbout: String,
    modelPicture: String,
    tags: Array,
    index: Number
  },
  methods: {
    showModal() {
      this.$refs['my-modal'].show()
    },
    hideModal() {
      this.$refs['my-modal'].hide();
      this.$emit('hideUpdateModal')

    },
    toggleModal() {
      // We pass the ID of the button that we want to return focus to
      // when the modal has hidden
      const a = [this.modelName, this.modelJob, this.modelNationality, this.modelBirthday,
        this.modelAbout, this.modelPicture, this.tags];
      this.$refs['my-modal'].toggle('#toggle-btn')
      this.$emit('closeModal', a)
    }
  },
  mounted() {
    this.showModal();
  }
}
</script>