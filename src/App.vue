<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import { RouterLink, RouterView } from 'vue-router';
</script>

<template>
  <header>
    <h1>Rick <span>and</span> Morty</h1>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/characters">Characters</RouterLink>
      <RouterLink to="/locations">Locations</RouterLink>
    </nav>
  </header>
  <div class="container">
    <RouterView />
  </div>
</template>

<style lang="stylus">
@import url('https://fonts.googleapis.com/css2?family=Schoolbell&display=swap');

@font-face
    font-family Schwifty
    src url(assets/get_schwifty.ttf)

$primary = #00b5cc
$secondary =#88d684

html
    font-size 16px
    font-family 'Schoolbell', cursive;
    margin 0
    padding 0

body
    width 100%
    margin 0

h1
    font-family Schwifty
    color $primary
    text-shadow 0 0 3px $secondary
    font-size 4rem
    text-align center

    >span
        font-size 2rem

header
    margin 1rem
    margin-bottom 0

    nav > :first-child
        margin-left 2rem

h2
    color #c1f380
    margin 0
    margin-top 3rem

a
    text-decoration none
    margin-right .5rem
    background-color $primary
    color #fff700
    padding .5rem
    border-radius 10px 10px 0 0
    font-family 'Schoolbell', cursive;

.container
    background-color $primary
    margin 1rem
    margin-top 0
    border-radius 10px
    min-height 400px
    padding 1rem
    grid-template-columns repeat(auto-fit, minmax(400px, 1fr));
</style>
