<template>
  <div>
    <BRow class="d-flex justify-content-center">
    <BAvatar :src="dataAvatar" rounded  style="height: 250px; width: 200px;"/>
    </BRow>

    <div>
      <div class="d-flex mt-1 flex-wrap mb-1">
        <BFormFile
        style="width: 200px;"
          v-model="profile_picture"
          placeholder="Имя файла"
          browseText="Выбрать"
          @input="fileInput"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { BFormGroup, BImg, BAvatar, BFormFile, BCol,BRow } from 'bootstrap-vue';

export default {
  components: {
    BFormGroup,
    BImg,
    BAvatar,
    BFormFile,
    BCol,
    BRow,
  },
  data() {
    return {
      dataAvatar: '',
      profile_picture: null,
    };
  },
  methods: {
    fileInput(file) {
      let reader = new FileReader();
      reader.readAsDataURL(file);
      reader.onload = () => (this.dataAvatar = reader.result);
    },
  },
};
</script>

<style></style>
