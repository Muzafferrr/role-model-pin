<template>
  <div>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="4" class="mb-5">
          <AddRoleModel @fromAddRoleModel="updateCard($event)"></AddRoleModel>
        </b-col>
        <b-col sm="8" class="cardContainer">
          <ModelCard v-for="(item,index) in card"
                     :key="index"
                     :index="index"
                     :modelName="item[0]"
                     :modelJob="item[1]"
                     :modelNationality="item[2]"
                     :modelBirthday="item[3]"
                     :modelAbout="item[4]"
                     :modelPicture="item[5]"
                     :tags="item[6]"
                     @updateEmitIndex="activeIndex($event)"
                     @deleteModalOpen="deleteModalOpen($event)"
          ></ModelCard>
          <UpdateModalCard v-if="showModal"
                           @closeModal="updateOkay($event)"
                           @hideUpdateModal="hideUpdateModal()"
                           :modelName="card[activeNumber][0]"
                           :modelJob="card[activeNumber][1]"
                           :modelNationality="card[activeNumber][2]"
                           :modelBirthday="card[activeNumber][3]"
                           :modelAbout="card[activeNumber][4]"
                           :modelPicture="card[activeNumber][5]"
                           :tags="card[activeNumber][6]"
          ></UpdateModalCard>
          <DeleteModalCard v-if="showModalDelete"
                           :index="activeNumber"
                           :modelName="card[activeNumber][0]"
                           @deleteModal="deleteModal()"
                           @deleteModalHide="deleteModalHide()"
          ></DeleteModalCard>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import globalComponents from "@/globalComponents";

export default {
  name: 'App',
  data() {
    return {
      card: [],
      showModal: false,
      showModalDelete: false,
      activeNumber: -1
    }
  },
  methods: {
    updateCard(e) {
      this.card.push(e);
    },
    activeIndex(e) {
      this.showModal = true;
      this.activeNumber = e;
    },
    updateOkay(e) {
      this.card.splice(this.activeNumber, 1, e)
      this.showModal = false;
      this.activeNumber = -1;
    },
    deleteModalOpen(e) {
      this.showModalDelete = true;
      this.activeNumber = e;
    },
    deleteModal() {
      this.card.splice(this.activeNumber, 1);
      this.showModalDelete = false;
      this.activeNumber = -1;
    },
    deleteModalHide() {
      this.showModalDelete = false;
    },
    hideUpdateModal() {
      this.showModal = false;
    }
  },
  components: {
    ...globalComponents
  }
}
</script>
<style>
.cardContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
  margin-top: 20px;
}
</style>
