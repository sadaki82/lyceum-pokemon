<script setup>
const { data: trainers } = await useTrainers();
</script>

<template>
  <div>
    <h1>ポケットモンスターアプリ</h1>
    <GamifyList>
      <h2>ポケモンの旅を</h2>
      <GamifyItem v-if="trainers.length > 0">
        <NuxtLink to="/trainer">つづきからはじめる</NuxtLink>
      </GamifyItem>
      <GamifyItem v-else>
        <span>つづきからはじめる</span>
      </GamifyItem>
      <GamifyItem>
        <NuxtLink to="/new">あたらしくはじめる</NuxtLink>
      </GamifyItem>
    </GamifyList>
  </div>
</template>
