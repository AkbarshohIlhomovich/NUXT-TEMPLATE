<template>
  <UApp>
    <NuxtPage />
  </UApp>
</template>

<script setup>
const router = useRouter()

function checkMobile() {
  return window.innerWidth <= 768
}

onMounted(() => {
  if (!checkMobile()) {
    router.push('/not-available')
  }
  // agar foydalanuvchi oynani qayta o'lchasa ham tekshiradi
  window.addEventListener('resize', () => {
    if (!checkMobile()) {
      router.push('/not-available')
    }
  })
})
</script>