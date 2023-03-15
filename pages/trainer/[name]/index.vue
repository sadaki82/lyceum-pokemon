<script setup>
const route = useRoute();
const config = useRuntimeConfig();
const { data: trainer } = await useFetch(
  () => `${config.backendOrigin}/api/trainer/${route.params.name}`
);
</script>

<template>
  <div>
    <h1>トレーナー情報</h1>
    <div class="trainer-info">
      <img src="/avatar.png" />
      <span>{{ trainer.name }}</span>
    </div>
  </div>
  <h2>てもちポケモン</h2>
  <CatchButton :to="`/trainer/${trainer.name}/catch`"
    >ポケモンをつかまえる</CatchButton
  >
  <GamifyList>
    <GamifyItem v-for="pokemon in trainer.pokemons" :key="pokemon.id">
      <img :src="pokemon.sprites.front_default" />
      <span class="pokemon-name">{{ pokemon.nickname || pokemon.name }}</span>
      <GamifyButton @click="onOpenNickname(pokemon)"
        >ニックネームをつける</GamifyButton
      >
      <GamifyButton @click="onOpenRelease(pokemon)"
        >はかせにおくる</GamifyButton
      >
    </GamifyItem>
  </GamifyList>
</template>

<style scoped>
.item > label {
  display: block;
  margin-bottom: 0.25rem;
}

.gamify-item:hover img {
  animation: bounce;
  animation-duration: 0.8s;
  animation-iteration-count: infinite;
}

.trainer-info {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.trainer-info > img {
  width: 3rem;
  height: 3rem;
}
</style>
