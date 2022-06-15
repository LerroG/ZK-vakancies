<template>
  <div>
    <BRow cols="12">
      <BCol cols="12" md="6">
        <BRow v-for="(item, index) in positive" :key="index" class="mb-2">
          <BCol cols="12">
            <BFormGroup label="Положительные:">
              <BFormInput placeholder="Положительные" v-model="item.positive">
              </BFormInput>
            </BFormGroup>
          </BCol>
          <BCol
            class="d-flex justify-content-center align-items-center ml-50"
            
          >
            <BButton
              v-if="positive.length === index + 1"
              variant="outline-primary"
              class="p-75 mr-1 mb-25 btn_hover"
              @click="addRowPositive"
            >
              <FeatherIcon icon="PlusIcon"></FeatherIcon>
            </BButton>
            <BButton
              v-if="positive.length > 1"
              variant="outline-danger"
              class="p-75 mb-25 btn_hover_delete"
              @click="deleteRowPositive(item)"
            >
              <FeatherIcon icon="XIcon"></FeatherIcon>
            </BButton>
          </BCol>
        </BRow>
      </BCol>
      <BCol cols="12" md="6">
        <BRow v-for="(item, index) in negative" :key="index" class="mb-2">
          <BCol cols="12">
            <BFormGroup label="Отрицательные:">
              <BFormInput placeholder="Отрицательные" v-model="item.negative">
              </BFormInput>
            </BFormGroup>
          </BCol>
          <BCol
            class="d-flex justify-content-center align-items-center ml-50"
            
          >
            <BButton
              v-if="negative.length === index + 1"
              variant="outline-primary"
              class="p-75 mr-1 mb-25 btn_hover"
              @click="addRowNegative"
            >
              <FeatherIcon icon="PlusIcon"></FeatherIcon>
            </BButton>
            <BButton
              v-if="negative.length > 1"
              variant="outline-danger"
              class="p-75 mb-25 btn_hover_delete"
              @click="deleteRowNegative(item)"
            >
              <FeatherIcon icon="XIcon"></FeatherIcon>
            </BButton>
          </BCol>
        </BRow>
      </BCol>
    </BRow>
  </div>
</template>

<script>
import {
  BRow,
  BCol,
  BFormGroup,
  BFormInput,
  BFormDatepicker,
  BForm,
  BButton,
} from 'bootstrap-vue';

export default {
  components: {
    BRow,
    BCol,
    BFormGroup,
    BFormInput,
    BFormDatepicker,
    BForm,
    BButton,
  },
  data() {
    return {
      positive: [
        {
          positive: '',
        },
      ],
      negative: [
        {
          negative: '',
        },
      ],
    };
  },
  methods: {
    addRowPositive() {
      let item = {
        positive: '',
      };
      this.positive.push(item);
    },

    deleteRowPositive(item) {
      //  нужно исправить потом
      this.positive.splice(this.positive.indexOf(item), 1);
    },
    addRowNegative() {
      let item = {
        negative: '',
      };
      this.negative.push(item);
    },

    deleteRowNegative(item) {
      //  нужно исправить потом
      this.negative.splice(this.negative.indexOf(item), 1);
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
