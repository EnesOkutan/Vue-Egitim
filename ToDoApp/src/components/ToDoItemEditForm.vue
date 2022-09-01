<template>
  <form class="stack-small" @submit.prevent="onSubmit">
    <div>
      <label class="edit-label"
        >{{ label }} görevi için değiştirilecek isim</label
      >
      <input ref="labelInput" type="text" v-model="newLabel" />
    </div>
    <div class="btn-group">
      <button type="button" class="btn" @click="onCancel">
        İptal
        <span class="visually-hidden">{{ label }} görevi değiştiriliyor</span>
      </button>
      <button type="submit" class="btn btn__primary">
        Kaydet
        <span class="visually-hidden">{{ label }} görevi değiştirilecek</span>
      </button>
    </div>
  </form>
</template>

<script>
export default {
  props: ["label", "id"],
  data() {
    return {
      newLabel: this.label,
    };
  },
  methods: {
    onCancel() {
      this.$emit("edit-cancelled");
    },
    onSubmit() {
      if (this.newLabel && this.newLabel !== this.label) {
        this.$emit("item-edited", this.newLabel);
      }
    },
  },
  mounted() {
    const labelInputRef = this.$refs.labelInput;
    labelInputRef.focus();
  },
};
</script>

<style scoped>
.edit-label {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialised;
  -moz-osx-font-smoothing: grayscale;
  color: #0b0c0c;
  display: block;
  margin-bottom: 5px;
}

input {
  display: inline-block;
  margin-top: 0.4rem;
  width: 100%;
  min-height: 4.4rem;
  padding: 0.4rem 0.8rem;
  border: 2px solid #565656;
}

form {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

form > * {
  flex: 0 0 100%;
}
</style>