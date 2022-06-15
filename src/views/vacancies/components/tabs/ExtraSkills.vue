<template>
  <div >
    <BRow v-for="(item, index) in items" :key="index" class="mb-2 d-flex justify-content-center">
      <BCol cols="12" md xl>
        <BFormGroup label="Какими другими полезными навыками обладаете?">
          <BFormTextarea rows="4" v-model="item.skill">
          </BFormTextarea>
        </BFormGroup>
      </BCol>
      <BCol  class="d-flex justify-content-end align-items-center mt-25" style="max-width: 100px;"  md xl>
        <BButton
          v-if="items.length === index + 1"
          variant="outline-primary"
          class="p-75 mr-1 btn_hover"
          @click="addRow"
        >
          <FeatherIcon icon="PlusIcon"></FeatherIcon>
        </BButton>
        <BButton
          v-if="items.length > 1"
          variant="outline-danger"
          class="p-75 btn_hover_delete"
          @click="deleteRow(item)"
        >
          <FeatherIcon icon="XIcon"></FeatherIcon>
        </BButton>
      </BCol>
    </BRow>
  </div>
</template>

<script>
import {
  BFormGroup,
  BFormInput,
  BRow,
  BCol,
  BButton,
  BFormTextarea,
} from 'bootstrap-vue';

export default {
  components: {
    BFormGroup,
    BFormInput,
    BRow,
    BCol,
    BButton,
    BFormTextarea,
  },
  data() {
    return {
      items: [
        {
          skill: '',
        },
      ],
    };
  },
  methods: {
    addRow() {
      this.items.push({
        skill: '',
      });
    },
    deleteRow(item) {
      this.items.splice(this.items.indexOf(item), 1);
    },
  },
};
</script>

<style>
.btn_hover{
    	transition: all .3s linear;
    	-webkit-transition: all .3s linear;
    	-moz-transition: all .3s linear; 	
    }
.btn_hover:hover {
    background: #93a7e8!important;
    color: white!important;
}
.btn_hover_delete{
    	transition: all .3s linear;
    	-webkit-transition: all .3s linear;
    	-moz-transition: all .3s linear; 	
    }
.btn_hover_delete:hover {
    background: rgb(255, 85, 85)!important;
    color: white!important;
}
</style>
