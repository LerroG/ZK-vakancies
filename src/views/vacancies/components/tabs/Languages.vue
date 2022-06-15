<template>
  <div>
    <BRow v-for="(item, index) in items" :key="index" class="mb-2 d-flex justify-content-center">
      <BCol cols="12" md xl>
        <BFormGroup label="Язык:">
          <BFormInput placeholder="Язык" v-model="item.language"> </BFormInput>
        </BFormGroup>
      </BCol>
      <BCol cols="12" md xl>
        <BFormGroup label="Разговор:">
          <BFormSelect
            title="Разговор"
            v-model="item.talk"
            :options="options"
          />
        </BFormGroup>
      </BCol>
      <BCol cols="12" md xl>
        <BFormGroup label="Написание:">
          <BFormSelect v-model="item.write" :options="options" />
        </BFormGroup>
      </BCol>
      <BCol cols="12" md xl>
        <BFormGroup label="Чтение:">
          <BFormSelect v-model="item.read" :options="options" />
        </BFormGroup>
      </BCol>
      <BCol class="d-flex justify-content-center align-items-end" style="max-width: 90px;" md xl>
        <BButton
          v-if="items.length === index + 1"
          variant="outline-primary"
          class="p-75 mr-1 mb-1 btn_hover"
          @click="addRow"
        >
          <FeatherIcon icon="PlusIcon"></FeatherIcon>
        </BButton>
        <BButton
          v-if="items.length > 1"
          variant="outline-danger"
          class="p-75 mb-1 btn_hover_delete"
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
  BRow,
  BCol,
  BCard,
  BFormGroup,
  BFormInput,
  BTabs,
  BTab,
  BContainer,
  BForm,
  BButton,
  BFormSelect,
} from 'bootstrap-vue';

export default {
  components: {
    BRow,
    BCol,
    BCard,
    BFormGroup,
    BFormInput,
    BTabs,
    BTab,
    BContainer,
    BForm,
    BButton,
    BFormSelect,
  },
  data() {
    return {
      options: [
        { value: '', text: 'Начальный' },
        { value: 'a', text: 'Средний' },
        { value: 'b', text: 'Продвинутый' },
      ],
      // optionsW: [
      //   { value: null, text: 'Начальный' },
      //   { value: 'a', text: 'Средний' },
      //   { value: 'b', text: 'Продвинутый' },

      // ],
      // optionsR: [
      //   { value: null, text: 'Начальный' },
      //   { value: 'a', text: 'Средний' },
      //   { value: 'b', text: 'Продвинутый' },

      // ],
      items: [
        {
          language: '',
          talk: '',
          write: '',
          read: '',
        },
      ],
    };
  },
  methods: {
    addRow() {
      let item = {
        language: '',
        talk: '',
        write: '',
        read: '',
      };
      this.items.push(item);
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
