<template>
  <div>
    <input
      type="file"
      ref="image"
      style="display: none"
      @change="handleImage"
    />
    <button
      class="f-img-add-produk photo active"
      type="button"
      @click="$refs.image.click()"
    >
      <img
        v-if="currentImage"
        :src="currentImage"
        style="height: 100px; width: 100px"
      />
      <span v-else> Foto {{ position }} </span>
    </button>
  </div>
</template>

<script>
export default {
  name: "ImageBox",
  props: ["position", "image"],
  methods: {
    handleImage: function (files) {
      const image = files.target.files[0];
      console.log(image);

      //! PURA2 UPLOAD DI SINI
      //! INI RANDOM IMAGE AJA
      const randomimage = Math.floor(Math.random() * 100);
      this.$emit("imageSuccess", {
        imageUrl: `https://picsum.photos/10${randomimage}/10${randomimage}`,
        position: this.position,
      });
    },
  },
  computed: {
    currentImage: function () {
      return this.image ? this.image.imageUrl : null;
    },
  },
};
</script>

<style>
.f-img-add-produk {
  width: 150px;
  height: 150px;
  border-radius: 8px;
  margin-bottom: 20px;
  background-color: transparent;
  border: 2px solid #ced4da;
  border-style: dashed;
  background-repeat: no-repeat;
  background-size: cover;
  color: #505d69;
}
</style>
