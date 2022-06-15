<template>
  <div fluid class="container">
    <ValidationObserver v-slot="{ handleSubmit }">
      <BForm @submit.prevent="handleSubmit(onSubmit)">
        <BRow>
          <BCol>
            <GenInfo />
          </BCol>
        </BRow>
        <BRow class="d-flex justify-content-center mt-4">
          <BTabs align="center" style="width: 100%">
            <BTab title="Образование">
              <BCard><Education /> </BCard>
            </BTab>
            <BTab title="Предыдущий опыт работы"
              ><BCard><PreviousExperience /></BCard>
            </BTab>
            <BTab title="Черты характера">
              <BCard><Character /> </BCard>
            </BTab>
            <BTab title="Дополнительные навыки"
              ><BCard>
                <ExtraSkills />
              </BCard>
            </BTab>
            <BTab title="Владение языками"
              ><BCard>
                <Languages />
              </BCard>
            </BTab>
            <BTab title="Ваши ожидания"
              ><BCard>
                <Expectations />
              </BCard>
            </BTab>
          </BTabs>
        </BRow>
        <BRow>
          <BCol class="d-flex justify-content-end">
            <b-button type="submit" variant="outline-primary" class="btn_hover"
              >Отправить
            </b-button>
          </BCol>
        </BRow>
      </BForm>
    </ValidationObserver>
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
  BFormSelect,
  BButton,
  BForm,
} from 'bootstrap-vue';

import GenInfo from './components/GenInfo.vue';
import Education from './components/tabs/Education.vue';
import PreviousExperience from './components/tabs/PreviousExperience.vue';
import Character from './components/tabs/Character.vue';
import ExtraSkills from './components/tabs/ExtraSkills.vue';
import Languages from './components/tabs/Languages.vue';
import Expectations from './components/tabs/Expectations.vue';

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
    BFormSelect,
    BButton,
    BForm,

    GenInfo,
    Education,
    PreviousExperience,
    Character,
    ExtraSkills,
    Languages,
    Expectations,
  },
  methods: {
    onSubmit() {
      console.log('Submit');
    },
  },
};
</script>

<style>
.nav-tabs .nav-link.active {
  color: #fea54f;
}
.nav-tabs .nav-link:after {
  left: 0;
  background: linear-gradient(30deg, #ff9634, #fea54f) !important;
}
.btn_hover {
  transition: all 0.3s linear;
  -webkit-transition: all 0.3s linear;
  -moz-transition: all 0.3s linear;
}
.btn_hover:hover {
  background: #93a7e8 !important;
  color: white !important;
}
</style>

#93a7e8 фиолетовый
