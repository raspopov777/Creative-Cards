<template>
  <div>
    <h1 class="text-center">Creative Cards</h1>
    <ul class="nav justify-content-center">
      <li class="nav-item"><a class="nav-link" @click="pageSelected='cardFront'">Font</a></li>  <!--когда надали на ссылку, запишет 'cardFront' в pageSelected-->
      <li class="nav-item"><a class="nav-link" @click="pageSelected='cardInsideLeft'">Inside Left</a></li>
      <li class="nav-item"><a class="nav-link" @click="pageSelected='cardInsideRight'">Inside Right</a></li>
      <li class="nav-item"><a class="nav-link" @click="pageSelected='cardBack'">Back</a></li>
    </ul>
    <hr>
    <cc-card-progress></cc-card-progress>
  </div>
</template>

<script>
  import CardProgress from './card/CardProgress.vue'

  export default {
    data: function () {
      return {
        pageSelected: ''
      }
    },
    watch: {
      pageSelected: function () {  //вызовется при изменении pageSelected
        this.$emit('pageWasChanged', this.pageSelected) //порождает событие pageWasChanged с аргументом this.pageSelected
      }
    },
    components: {
      ccCardProgress: CardProgress
    }
  }
</script>

<style>
  h1 {
    margin-top: 10px;
  }
</style>
