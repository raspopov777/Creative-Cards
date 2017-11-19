<template>
  <div class="row">
    <div class="col-sm-12">
      <div class="form-group">
        <h4>Edit Text</h4>
        <textarea
          class="form-control" cols="50" rows="4" placeholder="Add text here!"
          v-model="textBoxInput" @keyup="textChanged"> <!--v-model двунаправленно связывает данные. работает с input, select, textarea-->
        </textarea>                                          <!--@keyup при каждом нажатии вызывает метод "textChanged"-->
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data: function () {
      return {
        textBoxInput: ''
      }
    },
    methods: {
      textChanged: function () {
        this.$emit('displayTextChanged', this.textBoxInput)
      }
    }
  }
</script>

<style>

</style>
