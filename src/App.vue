<template>
  <div>
    <b-row>
      <b-col sm="4" class="addingModel">
        <AddRoleModel @fromAddRoleModel="updateCard($event)"></AddRoleModel>
      </b-col>
      <transition-group class="role-model" sm="12" name="role-model" tag="b-col">
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
                         :key="randomKey"
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
                         :key="randomKey"
                         @deleteModal="deleteModal()"
                         @deleteModalHide="deleteModalHide()"
        ></DeleteModalCard>
      </transition-group>
    </b-row>
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
      activeNumber: -1,
      randomKey: Math.random()
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
.role-model{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
  margin-top: 40px;
  backface-visibility: hidden;
  transform-origin: 10% 50%;
  z-index: 1;
}
.addingModel{
  margin-left: 30px;
}
.role-model-move{
  transition: all 600ms ease-out;
}
.role-model-enter-active{
  transition: all 300ms ease-out;
}
.role-model-leave-active{
  transition: all 200ms ease-out;
  position: absolute;
  z-index: 1;
}
.role-model-enter,
.role-model-leave-to{
  opacity: 0;
}
</style>
