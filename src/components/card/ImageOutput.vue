<template>
  <div class="img-container" :style="styleObjects"
       @mouseover = "showOptions = true"
       @mouseleave ="showOptions = false">

    <button type="button" class="btn btn-outline-danger btn-sm"
    v-show="showOptions" @click="clearImageProp">Remove Image</button>

    <img id="outputImage">
  </div>
</template>

<script>
  import Firebase from 'firebase'

  export  default {
    props: {
      displayImage: {
        type: String
      },
      containerHeight: {
        type: Number,
        default: 200
      },
      clearImageProp: function () {
      }
    },
    data: function () {
      return {
        showOptions: false
      }
    },
    watch: {
      displayImage: function () {
        let storageRef = Firebase.storage().ref('user_uploads/'+ this.displayImage);
        storageRef.getDownloadURL().then(function (url) {
          let img = document.getElementById('outputImage');
          img.src = url;
          setDraggable();
        });
      }
    },
    computed: {
      styleObjects: function () {
        return {
          height: this.containerHeight + 'px'
        }
      }
    }
  }

  function setDraggable() {
    $('#outputImage').draggable(); //jQuery функция, которая делает элементы перемещаемыми по странице
  }
</script>

<style>
  .img-container {
    border: 1px dotted grey;
    overflow: hidden;
    margin: 5px 0;
  }
  img {
    width: 130%;
  }
  button {
    position: absolute;
    z-index: 1;
  }
</style>
