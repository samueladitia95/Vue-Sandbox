<template>
  <div class="row">
    <div class="col-12">
      <div class="card f-border">
        <div class="card-body page-setting">
          <h4 class="card-title mb-1">Foto Produk</h4>
          <div class="data-form-setting">
            <form class="form-horizontal" role="form">
              <div class="row mb-4">
                <div class="col-lg-3">
                  <span class="form-title">Kriteria Foto</span> <br />
                  <span class="form-title">
                    <span class="form-desc form-desc-absolute"
                      >Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                      sed do eiusmod tempor incididunt ut labore et dolore
                      magna.</span
                    >
                  </span>
                </div>
                <div class="col-lg-9 pr-0">
                  <image-box
                    v-for="(position, i) in imagePosition"
                    :key="i"
                    :position="position"
                    :image="currentImages[i]"
                    @imageSuccess="handleImages"
                  />
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ImageBox from "./subComponents/ImageBox.vue";
export default {
  name: "UploadImages",
  components: {
    ImageBox,
  },
  data: function () {
    return {
      imagePosition: [1, 2, 3, 4, 5, 6],
      images: [],
    };
  },
  methods: {
    handleImages: function ({ imageUrl, position }) {
      const isDuplicate = this.images.findIndex(
        (el) => el.position === position,
      );

      if (isDuplicate < 0) {
        this.images.push({
          imageUrl,
          position,
        });
      } else {
        const replaceImages = this.images.filter((_, i) => i !== isDuplicate);
        replaceImages.push({
          imageUrl,
          position,
        });
        this.images = replaceImages;
      }
    },
  },
  computed: {
    currentImages: function () {
      return this.imagePosition.map((el) => {
        const isExist = this.images.findIndex((image) => image.position === el);
        return isExist < 0 ? null : this.images[isExist];
      });
    },
  },
  // created: function () {
    // this.images = [{
    // imageUrl: "",
    // position: 1
    // }]
  // },
};
</script>

<style></style>
