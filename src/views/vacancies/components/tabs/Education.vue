<template>
  <div>
    <BRow
      
      v-for="(item, index) in items"
      :key="index"
      class="d-flex justify-content-between align-items-end mb-3"
    >
      <BCol col md="3" xl>
        <BFormGroup label="Период обучения: ">
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
      <BCol col md="3" xl>
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
        <BFormGroup label="Название учебного заведения и факультета:" >
          <BFormInput
            v-model="item.institution"
            placeholder="Название учебного заведения и факультета"
          >
          </BFormInput>
        </BFormGroup>
      </BCol>
      <BCol cols="12" md xl>
        <BFormGroup label="Специальность:">
          <BFormInput v-model="item.specialty" placeholder="Специальность" />
        </BFormGroup>
      </BCol>
      <BCol col md xl>
        <BFormGroup label="Степень:">
          <BFormInput v-model="item.degree" placeholder="Степень" />
        </BFormGroup>
      </BCol>
      

      <BCol class="d-flex justify-content-center align-items-end" style="max-width: 100px;" col xl>
        <BButton
          v-if="items.length === index + 1"
          variant="outline-primary"
          class="p-75 mr-1 mb-1 btn_hover "
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
  BFormGroup,
  BRow,
  BCol,
  BFormDatepicker,
  BForm,
  BFormInput,
  BButton,
} from 'bootstrap-vue';

export default {
  components: {
    BFormGroup,
    BRow,
    BCol,
    BFormDatepicker,
    BForm,
    BFormInput,
    BButton,
  },

  data() {
    return {
      items: [
        {
          start_date: '',
          end_date: '',
          institution: '',
          specialty: '',
        },
      ],
    };
  },
  methods: {
    addRow() {
      let item = {
        start_date: '',
        end_date: '',
        institution: '',
        specialty: '',
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
