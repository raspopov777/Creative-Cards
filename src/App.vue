<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12">
        <nav-header @pageWasChanged="currentPage = $event"></nav-header>
        <keep-alive> <!--кэширует экземпляры интерактивных компонентов-->
          <component :is="currentPage"></component> <!--динамически изменяет компонент.
        если в currentPage будет cardFront, то это равносильно <card-front></card-front>-->
        </keep-alive>
        <cc-footer>
          <p class="text-center" slot="app-name">&copy;Creative Cards</p>
          <nav>
            <ul class="nav justify-content-center">
              <li class="nav-item"><a class="nav-link" >Home</a></li>
              <li class="nav-item"><a class="nav-link" >About Us</a></li>
              <li class="nav-item"><a class="nav-link" >Contact Us</a></li>
            </ul>
          </nav>
        </cc-footer>
      </div>
    </div>
  </div>
</template>

<script>
  import FirebaseConfig from './firebaseConfig.js'

  import Header from './components/Header.vue'
  import CardFront from './components/card/CardFront.vue'
  import CarrInsideLeft from './components/card/CardInsideLeft.vue'
  import CarrInsideRight from './components/card/CardInsideRight.vue'
  import CardBack from './components/card/CardBack.vue'
  import Footer from './components/Footer.vue'


  export default {
    data: function () {
      return {
        currentPage: 'cardFront'
      }
    },
    components: {
      navHeader: Header,
      cardFront: CardFront,
      cardInsideLeft: CarrInsideLeft,
      cardInsideRight: CarrInsideRight,
      cardBack: CardBack,
      ccFooter: Footer
    }
  }
</script>

<style>
  .body {
    font-family: Verdana, Gevena, sans-serif;
    color: #333;
  }
  a {
    cursor: pointer;
  }
</style>
