<script setup>
import { defineProps } from 'vue'

const props = defineProps({ pokemon: Object })
</script>

<template>
  <a :href="pokemon.species.url" class="card">
    <div class="card__header">
      <div class="card__name">{{ pokemon.species.name }}</div>
    </div>
    <div class="card__body">
      <img :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name" class="card__img">
    </div>
    <div class="card__footer">
      <div class="card__total">experience: {{ pokemon.base_experience }}</div>
    </div>
  </a>
</template>


<style lang='scss' scoped>
  .card {
    display: flex;
    flex-direction: column;
    border-radius: 10px;
    color: #fff;
    height: 300px;
    padding: 20px;
    transition: all 0.3s ease-in-out;
    background-color: #2d4d5d;
    box-shadow: 0px 0px 10px 1px #274ca4;
    border: 1px solid #3b7b9b;
    &:hover {
      box-shadow: 0px 0px 10px 1px #d6d6d6;
      transform: scale(1.02);
    }
    &__name {
      text-transform: capitalize;
      font-size: 20px;
    }
    &__body {
      display: flex;
      align-items: center;
      justify-content: center;
      flex: 1 1 auto;
    }
    &__img { height: 150px; }
    &__total { text-align: right; }
    &__footer {
      margin-top: auto;
    }
  }
</style>