<template>
  <div>
    <BRow class="justify-content-center">
      <h1 class="text-center">РЕЗЮМЕ на вакантную должность:</h1>
    </BRow>
    <BRow class="justify-content-center">
      <h2 class="text-warning text-center" style="max-width: 80rem">
        Главный специалист управления техническо-программной поддержки и
        развития информационных систем
      </h2>
    </BRow>

    <BRow class="d-flex justify-content-between mt-3" cols="12" xl="12">
      <BCol cols="12" md="12" xl="3" class="d-flex justify-content-center mt-2">
        <BRow><PhotoUpload /></BRow>
      </BCol>

      <BCol xl="9">
        <BRow class="align-items-start">
          <BCol md="4">
            <BFormGroup label="Фамилия:">
              <ValidationProvider
                #default="{ errors }"
                name='"Фамилия"'
                rules="required"
              >
                <BFormInput placeholder="Фамилия" v-model="formData.lastName" />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol>

          <BCol md="4">
            <BFormGroup label="Адрес проживания:">
              <ValidationProvider
                #default="{ errors }"
                name='"Адрес проживания"'
                rules="required"
              >
                <BFormInput
                  placeholder="Адрес проживания"
                  v-model="formData.addressLive"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol>
          <BCol md="4">
            <BFormGroup label="Семейное положение:">
              <BFormSelect v-model="selected" :options="options" />
            </BFormGroup>
          </BCol>
        </BRow>
        <BRow>
          <BCol md="4">
            <BFormGroup label="Имя:">
              <ValidationProvider
                #default="{ errors }"
                name='"Имя"'
                rules="required"
              >
                <BFormInput placeholder="Имя" v-model="formData.firstName" />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol>

          <BCol md="4">
            <BFormGroup label="Адрес прописки:">
              <ValidationProvider
                #default="{ errors }"
                name='"Адрес прописки"'
                rules="required"
              >
                <BFormInput
                  placeholder="Адрес прописки"
                  v-model="formData.addressPass"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol>
          <BCol md="4">
            <BFormGroup label="Номер телефона:">
              <ValidationProvider
                #default="{ errors }"
                name='"Номер телефона"'
                rules="required"
              >
                <!-- <BFormInput
                  v-model="formData.phoneNumber"
                  placeholder="+998"
                  oninput="this.value =
            this.value.replace(/[^0-9+]/g, '')"
                /> -->
                <cleave
                  ref="cleave"
                  v-model="formData.phoneNumber"
                  :options="mask_options.phoneNumber"
                  class="form-control"
                  placeholder="+998-xx-xxx-xx-xx"
                  tabindex="5"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol>
        </BRow>

        <BRow>
          <BCol md="4"
            ><BFormGroup label="Отчество:">
              <ValidationProvider
                #default="{ errors }"
                name='"Отчество"'
                rules="required"
              >
                <BFormInput
                  placeholder="Отчество"
                  v-model="formData.middleName"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol>
          <BCol md="4"
            ><BFormGroup label="Национальность:">
              <ValidationProvider
                #default="{ errors }"
                name='"Национальность"'
                rules="required"
              >
                <BFormInput
                  v-model="formData.nationality"
                  placeholder="Национальность"
                  oninput="this.value = this.value.replace(/[^а-яА-Я]/g, '')"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol>
          <BCol md="4"
            ><BFormGroup label="E-mail:">
              <ValidationProvider
                #default="{ errors }"
                name='"E-mail"'
                rules="required|email"
              >
                <BFormInput
                  type="email"
                  placeholder="E-mail"
                  v-model="formData.email"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCol></BRow
        >
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
  BFormSelect,
  BButton,
  BForm,
  BContainer
} from 'bootstrap-vue';
import PhotoUpload from './PhotoUpload.vue';
import Cleave from 'vue-cleave-component';
import 'cleave.js/dist/addons/cleave-phone.uz';
import { required, email } from '@validations';

export default {
  components: {
    BRow,
    BCol,
    BCard,
    BFormGroup,
    BFormInput,
    BTabs,
    BTab,
    BFormSelect,
    BButton,
    BForm,
    BContainer,
    PhotoUpload,
    Cleave,
  },
  data() {
    return {
      required,
      email,
      selected: null,
      options: [
        { value: 'b', text: 'Женат (Замужем)' },
        { value: null, text: 'Не женат (Замужем)' },
      ],
      formData: {
        lastName: '',
        firstName: '',
        middleName: '',
        addressLive: '',
        addressPass: '',
        nationality: '',
        phoneNumber: '',
        email: '',
      },
      mask_options: {
        phoneNumber: {
          phone: true,
          phoneRegionCode: 'UZ',
          delimiter: '-',
          prefix: '+998',
          noImmediatePrefix: true,
          signBeforePrefix: true,
        },
      },
    };
  },
};
</script>

<style></style>
