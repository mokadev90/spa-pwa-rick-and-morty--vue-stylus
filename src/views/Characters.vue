<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue';
import Character from '../types/Character';

const API_URL: string = 'https://rickandmortyapi.com/api/character?page=';
const reqN = ref<number>(1);

const fetchData = async () => {
  //console.log(reqN.value);
  const url: string = `${API_URL}${reqN.value}`;
  //console.log(url);
  let dataArray: Array<Character> = [];
  dataArray = (await (await fetch(url)).json()).results;
  //console.log(dataArray);
  reqN.value = reqN.value + 1;
  //console.log(reqN.value);
  return dataArray;
};

const data = ref<Character[]>([]);
const scrollComponent = ref(null);

const loadMoreCharacters = async () => {
  let newCharacters: Array<Character> = await fetchData();
  data.value.push(...newCharacters);
};

onMounted(() => {
  loadMoreCharacters();
});

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});

const handleScroll = () => {
  let element: any = scrollComponent.value;
  if (element.getBoundingClientRect().bottom < window.innerHeight) {
    loadMoreCharacters();
  }
};
</script>

<template>
  <div class="visor" ref="scrollComponent">
    <div v-for="d in data" :key="d.id" class="card">
      <div class="top">
        <img :src="d.image" alt="" />
        <div class="card-info">
          <div class="name">{{ d.name }} ({{ d.gender }})</div>
          <div class="species">Especies: {{ d.species }}</div>
        </div>
      </div>
      <div class="bottom">
        <div class="origin">{{ d.origin?.name }} - {{ d.location?.name }}</div>
        <div class="status">{{ d.status }}</div>
      </div>
    </div>
  </div>
</template>

<style lang="stylus">
.visor
    display grid
    grid-template-columns repeat(auto-fit, minmax(400px, 1fr))

.card
    width 100%
    max-width 400px
    height auto
    background-color #88d684
    margin 1.5rem
    border-radius 10px

    img
        width 150px
        height 150px
        margin 1rem
        border-radius  30px 0 30px 0

.top
    display flex

.card-info
    display flex
    flex-direction column
    justify-content space-around
    margin 1rem

.bottom
    display flex
    margin 1rem
    justify-content space-between
</style>
