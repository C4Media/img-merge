<template>
  <div>
    <myheader></myheader>
    <div>
      <img v-show="uploadedImage" :src="uploadedImage">
      <label >画像を選ぶ
        <input type="file" v-on:change="onFileChange">
      </label>
    </div>
    <myfooter></myfooter>
  </div>
</template>

<style lang="scss">
label > input {
  display: none;
}

label {
  padding: 0 1em;
  border: solid 1px #888;
}
</style>

<script>
import myheader from './components/myheader'
import myfooter from './components/myfooter'

export default {
  components: {
    myheader,myfooter
  },
  data () {
    return {
      uploadedImage: '',
    }
  },
  methods: {
    onFileChange(e) {
      let files = e.target.files || e.dataTransfer.files;
      this.createImage(files[0]);
    },
    // アップロードした画像を表示
    createImage(file) {
      let reader = new FileReader();
      reader.onload = (e) => {
        this.uploadedImage = e.target.result;
      };
      reader.readAsDataURL(file);
    },
  },
}
</script>