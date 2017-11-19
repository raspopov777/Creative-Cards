<template>
  <footer>
    <slot name="app-name">
      <p>Footer text</p> <!--альтернтива, если в родительском элементе ничего не будет-->
    </slot> <!--все содержимое родительского элемента будет помещено вместо slot'а-->
    <slot></slot>
  </footer>
</template>


