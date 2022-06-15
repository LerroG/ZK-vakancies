<template>
  <div>
    <ValidationObserver ref="userValidation">
      <BRow class="d-flex align-items-start">
        <!-- <BOverlay :show="show" rounded="sm"> -->
        <BCol cols="3">
          <BCard>
            <BCol class="d-flex justify-content-between flex-column" cols="21">
              <div
                class="
                  d-flex
                  flex-column
                  align-items-center
                  justify-content-start
                "
              >
                <template>
                  <BAvatar :src="dataAvatar" rounded size="250px" />
                </template>
                <div class="d-flex flex-column ml-1">
                  <div class="d-flex mt-2 flex-wrap">
                    <BFormFile
                      v-model="formData.profile_picture"
                      drop-placeholder="Перетащите файл сюда"
                      placeholder="Выберите файл"
                      browseText="Выбрать"
                      @input="fileInput"
                    />
                    <BButton
                      class="ml-auto mt-1"
                      variant="danger"
                      @click="deletePhoto"
                    >
                      <feather-icon icon="TrashIcon" />
                      Удалить
                    </BButton>
                  </div>
                </div>
              </div>
            </BCol>
          </BCard>
        </BCol>
        <BCol cols="6">
          <BCard>
            <BRow>
              <BCol cols="4">
                <BFormGroup label="Имя пользователя">
                  <ValidationProvider
                    #default="{ errors }"
                    name="Имя пользователя"
                    rules="required"
                  >
                    <BFormInput
                      v-model="formData.username"
                      placeholder="Имя пользователя"
                    />
                    <small class="text-danger">{{ errors[0] }}</small>
                  </ValidationProvider>
                </BFormGroup>
              </BCol>

              <BCol cols="4">
                <!-- <ValidationProvider
                  #default="{ errors }"
                  name="Пароль"
                  rules="required"
                >
                  <BInputGroup :class="errors.length > 0 ? 'is-invalid' : null">
                    <BFormInput
                      v-model="formData.password"
                      :type="passwordToggleType(hidePswd)"
                      :state="errors.length > 0 ? false : null"
                    />
                    <BInputGroupAppend is-text>
                      <feather-icon
                        :icon="passwordToggleIcon(hidePswd)"
                        class="cursor-pointer"
                        @click="hidePswd = !hidePswd"
                      />
                    </BInputGroupAppend>
                  </BInputGroup>
                  <small class="text-danger">{{ errors[0] }}</small>
                </ValidationProvider> -->

                <BFormGroup label="Пароль">
                  <ValidationProvider
                    #default="{ errors }"
                    name="Пароль"
                    rules="required"
                  >
                    <BInputGroup>
                      <BFormInput
                        v-model="formData.password"
                        placeholder="Пароль"
                        :type="passwordToggleType(hidePswd)"
                        :disabled="Boolean($route.params.id)"
                      />
                      <BInputGroupAppend
                        is-text
                        v-if="!Boolean($route.params.id)"
                      >
                        <feather-icon
                          :icon="passwordToggleIcon(hidePswd)"
                          class="cursor-pointer"
                          @click="hidePswd = !hidePswd"
                        />
                      </BInputGroupAppend>
                    </BInputGroup>
                    <small class="text-danger">{{ errors[0] }}</small>
                  </ValidationProvider>
                </BFormGroup>
              </BCol>

              <BCol cols="4">
                <div
                  v-if="Boolean($route.params.id)"
                  class="d-flex align-items-end h-100"
                >
                  <BButton @click="openModal" class="mb-1">
                    Изменить пароль</BButton
                  >
                </div>

                <BFormGroup v-else label="Подтвердите пароль">
                  <ValidationProvider
                    #default="{ errors }"
                    name="Подтвердите пароль"
                    rules="required|confirm:@Пароль"
                  >
                    <BInputGroup>
                      <BFormInput
                        v-model="formData.confirm_password"
                        :type="passwordToggleType(hideConfirm)"
                        placeholder="Подтвердите пароль"
                      />

                      <BInputGroupAppend is-text>
                        <feather-icon
                          :icon="passwordToggleIcon(hideConfirm)"
                          class="cursor-pointer"
                          @click="hideConfirm = !hideConfirm"
                        />
                      </BInputGroupAppend>
                    </BInputGroup>
                    <small class="text-danger">{{ errors[0] }}</small>
                  </ValidationProvider>
                </BFormGroup>
              </BCol>
            </BRow>

            <BRow>
              <BCol cols="8">
                <BFormGroup label="Роли">
                  <VSelect
                    v-model="formData.roles"
                    :options="roles"
                    label="name"
                    multiple
                  />
                </BFormGroup>
              </BCol>

              <BCol>
                <BFormGroup label="Статус">
                  <BFormCheckbox switch v-model="formData.is_active">
                  </BFormCheckbox>
                </BFormGroup>
              </BCol>
            </BRow>
          </BCard>
        </BCol>

        <BCol cols="3">
          <BCard>
            <BFormGroup label="Имя">
              <ValidationProvider
                #default="{ errors }"
                name="Имя"
                rules="required"
              >
                <BFormInput v-model="formData.first_name" placeholder="Имя" />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
            <BFormGroup label="Фамилия">
              <ValidationProvider
                #default="{ errors }"
                name="Фамилия"
                rules="required"
              >
                <BFormInput
                  v-model="formData.last_name"
                  placeholder="Фамилия"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
            <BFormGroup label="E-mail">
              <ValidationProvider
                #default="{ errors }"
                name="E-mail"
                rules="required"
              >
                <BFormInput
                  v-model="formData.email"
                  placeholder="Адрес электронной почты"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>

            <BFormGroup label="Номер телефона">
              <ValidationProvider
                #default="{ errors }"
                name="Номер телефона"
                rules="required"
              >
                <cleave
                  ref="cleave"
                  v-model="formData.phone_number"
                  :options="mask_options.phone_number"
                  class="form-control"
                  placeholder="+998-xx-xxx-xx-xx"
                  tabindex="5"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </ValidationProvider>
            </BFormGroup>
          </BCard>
        </BCol>
      </BRow>

      <div class="d-flex justify-content-end">
        <BButton class="mr-1" @click="$router.push({ name: 'users-home' })"
          >Отменить</BButton
        >
        <BButton variant="primary" @click="submitHandle">Сохранить</BButton>
      </div>
    </ValidationObserver>

    
  </div>
</template>

<script>
import {
  BAvatar,
  BButton,
  BCard,
  BCol,
  BFormGroup,
  BFormInput,
  BInputGroup,
  BInputGroupAppend,
  BFormFile,
  BFormCheckbox,
  BRow,
} from "bootstrap-vue";
import VSelect from "vue-select";
import { min, required, email } from "@validations";
import { extend } from "vee-validate";
import Cleave from "vue-cleave-component";
import "cleave.js/dist/addons/cleave-phone.uz";
import { mapActions, mapState } from "vuex";

extend("confirm", {
  params: ["target"],
  validate(value, { target }) {
    return value === target;
  },
  message: "Пароли не совпадают",
});

export default {
  name: "AddEdit",
  components: {
    BAvatar,
    BButton,
    BCard,
    BCol,
    BRow,
    BFormGroup,
    BFormInput,
    BInputGroup,
    BInputGroupAppend,
    BFormFile,
    BFormCheckbox,
    VSelect,
    
    Cleave,
  },

  data() {
    return {
      hideConfirm: true,
      hidePswd: true,
      dataAvatar: "https://via.placeholder.com/150",
      formData: {
        profile_picture: "",
        username: "",
        password: "",
        confirm_password: "",
        roles: [],
        is_active: false,
        first_name: "",
        last_name: "",
        email: "",
        phone_number: "+998",
      },
      mask_options: {
        phone_number: {
          phone: true,
          phoneRegionCode: "UZ",
          delimiter: "-",
          prefix: "+998",
          noImmediatePrefix: true,
          signBeforePrefix: true,
        },
      },
    };
  },

  computed: {
    ...mapState("users", ["roles", "userDetail"]),
  },
  mounted() {
    this.FETCH_ALL_ROLES();
    if (this.$route.params.id) {
      this.FETCH_ONE_USER({ id: this.$route.params.id }).then(() => {
        this.formData.password = "*********";
        this.formData = {
          ...this.formData,
          ...this.userDetail,
        };
        this.dataAvatar = this.fixUrlPath(this.userDetail.profile_picture);
      });
    }
  },

  methods: {
    ...mapActions("users", [
      "FETCH_ALL_ROLES",
      "CREATE_USER",
      "PATCH_USER",
      "FETCH_ONE_USER",
    ]),
    passwordToggleIcon: (state) => (state ? "EyeIcon" : "EyeOffIcon"),
    passwordToggleType: (state) => (state ? "password" : "text"),

    fileInput(file) {
      let reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = () => (this.dataAvatar = reader.result);
    },
    async submitHandle() {
      let valid = await this.$refs.userValidation.validate();
      if (!valid) return;
      const {
        username,
        password,
        confirm_password,
        is_active,
        first_name,
        last_name,
        phone_number,
        roles,
        profile_picture,
        email,
      } = this.formData;
      let item = {
        username,
        is_active,
        first_name,
        last_name,
        phone_number,
        roles: roles.map((e) => e.id),
        email,
      };

      if (this.$route.params.id) {
        //  при редактировании пользователя только указываем его id
        item.id = this.$route.params.id;
      } else {
        //  указываю пороль при создании пользователя
        item.password = password;
        item.confirm_password = confirm_password;
      }
      if (profile_picture instanceof File) {
        // если пришел файл для загрузки аватара то передаю его в объект item и передаю его в метод для создания или редактирования пользователя
        item.profile_picture = profile_picture;
      }

      let req = this.$_convertToFormdata(item);

      (item.id ? this.PATCH_USER : this.CREATE_USER)(req)
        .then(() => {
          this.$router.push({ name: "users-home" });
          this.$_okToast();
        })
        .catch(this.$_errorToast);
    },
    patchPassword(taget) {
      let items = {
        id: this.$route.params.id,
        password: taget.password,
        confirm_password: taget.confirm_password,
      };
      let req = this.$_convertToFormdata(items);
      this.PATCH_USER(req).then(this.$_okToast).catch(this.$_errorToast);
    },
    fixUrlPath(url) {
      return process.env.VUE_APP_FILE_URL + url;
    },
    openModal() {
      this.$refs.changePassword.open();
    },
    deletePhoto() {
      let items = {
        id: this.$route.params.id,
        profile_picture: null,
      };
      let req = this.$_convertToFormdata(items);
      this.PATCH_USER(req).then(this.$_okToast).catch(this.$_errorToast);
    },
  },
};
</script>

<style lang="scss">
@import "@core/scss/vue/libs/vue-select.scss";
.vs__open-indicator {
  fill: rgba(60, 60, 60, 0.5);
}

.w-20 {
  width: 20%;
}
</style>