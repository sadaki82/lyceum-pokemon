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
</template>

<style scoped>
.item > label {
  display: black;
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

.trainer-info {
  width: 3rem;
  height: 3rem;
}
</style>
