<template>
  <div>
    <BRow class="d-flex">
      <BCol cols="12" md="6">
        <BFormGroup label="Заработная плата минимум:">
          <BFormInput
            placeholder="Минимум"
            oninput="this.value = this.value.replace(/[^0-9]/g, '')"
          >
          </BFormInput>
        </BFormGroup>
      </BCol>
      <BCol cols="12" md="6">
        <BFormGroup label="Заработная плата максимум:">
          <BFormInput
            placeholder="Максимум"
            oninput="this.value = this.value.replace(/[^0-9+]/g, '')"
          >
          </BFormInput>
        </BFormGroup>
      </BCol>

      <BCol cols="12" class="mt-2">
        <BFormGroup label="Напишите ваши ожидания о будущей работе:">
          <BFormTextarea rows="6"> </BFormTextarea>
        </BFormGroup>
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
  BFormTextarea,
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
    BFormTextarea,
  },
};
</script>

<style></style>
