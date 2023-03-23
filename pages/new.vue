<script setup>
const router = useRouter();
const config = useRuntimeConfig();
const trainerName = ref("");
const safeTrainerName = computed(() => trimAvoidCharacters(trainerName.value));
const valid = computed(() => safeTrainerName.value.length > 0);
const onSubmit = async () => {
  const response = await fetch(`${config.backendOrigin}/api/trainer`, {
    method: "POST",
    headers: {
      "Content-Type": "applicaton/json",
    },
    body: JSON.stringify({
      name: safeTrainerName.value,
    }),
  });
  if (!response.ok) return;
  router.push(`/trainer/${safeTrainerName.value}`);
};
const { dialog, onOpen, onClose } = useDialog();
</script>

<template>
  <div>
    <h1>あたらしくはじめる</h1>
    <p>では　はじめに　きみの　なまえを　おしえて　もらおう！</p>
    <form @submit.prevent>
      <div class="item">
        <label for="name">なまえ</label>
        <span id="name-description"
          >とくていの　もじは　とりのぞかれるぞ！</span
        >
        <input
          id="name"
          v-model="trainerName"
          aria-describedby="name-description"
          @keydown.enter="valid && onOpen(true)"
        />
        <GamifyDialog v-if="dialog" id="confirm-submit" title="かくにん">
          :description="`ふむきみは ${safeTrainerName} というのだな｀"
          @close="onClose"
          <GamifyList :border="false" direction="horizon">
            <GamifyItem>
              <GamifyButton @click="onClose">いいえ</GamifyButton>
            </GamifyItem>
            <GamifyItem>
              <GamifyButton @click="onSubmit">はい</GamifyButton>
            </GamifyItem>
          </GamifyList>
        </GamifyDialog>
      </div>
    </form>
  </div>
</template>

<style scoped>
h1,
p {
  text-align: center;
}
form {
  border-radius: 0.5rem;
  border: solid 4px red;
  padding: 1.5rem 3rem;
  margin: 1rem 20rem;
}

form > :not(:last-child) {
  display: block;
  margin-bottom: 1rem;
}

.item > label,
.item > span {
  display: block;
  margin-bottom: 0.25rem;
}
.item > span {
  font-size: 0.875rem;
}
</style>
