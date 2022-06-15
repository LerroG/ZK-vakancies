<template>
  <div>
    <BRow
      v-for="(item, index) in items"
      :key="index"
      class="d-flex justify-content-center align-items-center mb-3"
    >
      <BCol col md="3" xl="2">
        <BFormGroup label="Период работы: ">
          <BFormDatepicker
            class="mr-1"
            placeholder="С"
            v-model="item.start_date"
            :date-format-options="{
              year: 'numeric',
              month: 'numeric',
              day: 'numeric',
            }"
          />
        </BFormGroup>
      </BCol>
      <BCol col md="3" xl="2" align-self="end">
        <BFormGroup label="По:">
          <BFormDatepicker
          
            placeholder="По"
            v-model="item.end_date"
            :date-format-options="{
              year: 'numeric',
              month: 'numeric',
              day: 'numeric',
            }"
          />
        </BFormGroup>
      </BCol>
      <BCol cols="12" md="6" xl="4">
        <BFormGroup label="Должность:">
          <BFormInput v-model="item.job" placeholder="Должность"> </BFormInput>
        </BFormGroup>
      </BCol>
      <BCol cols="12" xl="4">
        <BFormGroup label="Название компании и сфера ее деятельности:">
          <BFormInput
            v-model="item.сompany"
            placeholder="Название компании и сфера ее деятельности"
          >
          </BFormInput>
        </BFormGroup>
      </BCol>
      <BCol cols="12" md xl>
        <BFormGroup
          label="Опишите Ваши функциональные обязанности в каждом месте работы, а также Ваши успехи и достижения:"
        >
        
          <BFormTextarea v-model="item.responsibilities" rows="4">
          </BFormTextarea>
        </BFormGroup>
      </BCol>
      <BCol class="d-flex justify-content-center align-items-center" style="max-width: 100px;" md xl>
        <BButton
          v-if="items.length === index + 1"
          variant="outline-primary"
          class="p-75 mr-1  btn_hover"
          @click="addRow"
        >
          <FeatherIcon icon="PlusIcon"></FeatherIcon>
        </BButton>
        <BButton
          v-if="items.length > 1"
          variant="outline-danger"
          class="p-75  btn_hover_delete"
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
  BFormGroup,
  BFormDatepicker,
  BFormInput,
  BButton,
  BFormTextarea,
} from 'bootstrap-vue';

export default {
  components: {
    BRow,
    BCol,
    BFormGroup,
    BFormDatepicker,
    BFormInput,
    BButton,
    BFormTextarea,
  },
  data() {
    return {
      items: [
        {
          start_date: '',
          end_date: '',
          job: '',
          сompany: '',
          responsibilities: '',
        },
      ],
    };
  },
  methods: {
    addRow() {
      let item = {
        start_date: '',
        end_date: '',
        job: '',
        сompany: '',
        responsibilities: '',
      };
      this.items.push(item);
    },

    deleteRow(item) {
      //  нужно исправить потом
      this.items.splice(this.items.indexOf(item), 1);
    },
  },
};
</script>

<style>
.btn_hover {
  transition: all 0.3s linear;
  -webkit-transition: all 0.3s linear;
  -moz-transition: all 0.3s linear;
}
.btn_hover:hover {
  background: #93a7e8 !important;
  color: white !important;
}
.btn_hover_delete {
  transition: all 0.3s linear;
  -webkit-transition: all 0.3s linear;
  -moz-transition: all 0.3s linear;
}
.btn_hover_delete:hover {
  background: rgb(255, 85, 85) !important;
  color: white !important;
}
</style>

