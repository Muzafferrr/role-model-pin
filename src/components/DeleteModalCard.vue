<template>
  <div>
    <b-modal @hidden="hideModal()" ref="my-modal" hide-footer :title="modelName + ' -- Role Modal Card'">
      <b-button class="mt-2" variant="outline-warning" block @click="toggleModal">Delete Role Modal</b-button>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    index: Number,
    modelName: String,
  },
  methods: {
    showModal() {
      this.$refs['my-modal'].show()
    },
    hideModal() {
      this.$refs['my-modal'].hide();
      this.$emit('deleteModalHide')

    },
    toggleModal() {
      this.$refs['my-modal'].toggle('#toggle-btn')
      this.$emit('deleteModal')
    }
  },
  mounted() {
    this.showModal();
  }
}
</script>