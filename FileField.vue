<template>
  <div class="projectService">
    <div class="projectService-label long">{{ label }}:</div>
    <div class="file">
      <div class="file__item">
        <input
          class="file__input"
          type="file"
          accept=".jpg, .png, gif"
          @change="onFileSelected"
        />
        <button style="padding: 5px 9px 5px 9px; min-width: 0">
          Выберите файл
        </button>
        <span class="file__span">{{fileSpan}}</span>
      </div>
      <div class="file__preview">
        <img v-if="url" :src="url" alt="">
      </div>
      <!-- <div class="file__preview" ref="fileInput">gh</div> -->
    </div>
    
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true,
    },
  },
  data: () => ({
    selectedFile: null,
    fileSpan: 'Файл не выбран',
    url: null
  }),

  methods: {
    onFileSelected(e) {
      this.selectedFile = e.target.files[0];
      this.fileSpan = this.selectedFile.name;
      this.url = URL.createObjectURL(this.selectedFile);
    },
  },
};
</script>
<style lang="scss" scoped>
.file {
  &__item {
    position: relative;
  }
  &__input {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
    font-size: 0;
    cursor: pointer;
  }
  &__span {
    font-size: 12px;
    line-height: 14px;
    padding-left: 13px;
  }
  &__preview{
    margin-top: 10px;
    margin-left: -225px;
    display: inline-block;
    width: 220px;
    img {
      max-width: 100%;
    }
  }
}
</style>
