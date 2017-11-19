<template>
  <div class="row">
    <div class="form-check form-check-inline">
      <div class="form-check-label">
        <input class="form-check-input" type="checkbox"
               v-model="checked" @click="sectionCompleted">Mark Section
      </div>
    </div>
  </div>
</template>

<script>

  /*Для обеспечения информацией между компонентами, которые не состоят в отношениях родитель-потомок
  можно использовать пустой экземпляр Vue в качестве централизованной шины событий*/

  import { EventBus }  from '../../main.js'

  export default {
    data: function () {
      return {
        checked: false
      }
    },
    methods: {
      sectionCompleted: function () {
        EventBus.$emit('mark-as-completed', this.checked)
      }
    }
  }
</script>
