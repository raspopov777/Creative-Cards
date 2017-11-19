<template>
  <div class="row">
    <div class="col-sm-12">
      <h4>Upload Image:</h4>
      <div class="form-group">
        <input type="file" class="form-control-file" id="fileUpload"
        @change="uploadFile">
      </div>
      <br>
      <progress value="0" max="100" id="progressBar"></progress>
      <img id="image">
      <button type="button" id="setImageButton" style="display:none" @click="setImage">Set Image</button>
    </div>
  </div>
</template>

<script>
  import Firebase from 'firebase'

  export default {
    data: function () {
      return {
        file: ''
      }
    },
    methods: {
      uploadFile: function (event) {
        document.getElementById('setImageButton').style.display = 'none';

        this.file = event.target.files[0];
        let storageRef = Firebase.storage().ref('user_uploads/'+ this.file.name);
        let upload = storageRef.put(this.file);

        //код ниже вставляет прочитанное с диска изображение на страницу
        let reader = new FileReader(); //читает файл и сохраняет в переменной
        reader.readAsDataURL(this.file); //возвращает содержимое файла как data URL
        //data URI содержит все изображения, оно может быть передано непосредственно в атрибут src тега  <img> и отображено на странице
        reader.onload = function (e) { // обработчик загрузки, вызывается когда файл успешно прочитан
          document.getElementById('image').src = e.target.result //e.target.result - результат чтения
        };
        //progress bar
        upload.on('state_changed', function (snapshot) { //вызывается в любое время когда изменится состояние
          let progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100; //количество загруженных байтов / общее количество загружаемых байтов
          document.getElementById('progressBar').value = progress;

          if(progress === 100) {
            document.getElementById('setImageButton').style.display = 'inline-block';
          }

        });
      },

      setImage: function () {
        this.$emit('displayImageChanged', this.file.name);
      }
    }
  }
</script>

<style scoped>
  img {
    max-width: 200px;
  }
</style>
