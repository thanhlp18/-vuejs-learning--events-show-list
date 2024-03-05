<script setup>
import router from '@/router'
import { inject } from 'vue'

defineProps(['event'])
const GStore = inject('GStore')
router.beforeEach((to, from) => {
  const notAuthorized = true
  if (to.meta.requireAuth && notAuthorized) {
    GStore.flashMessage = 'Sorry, you are not authorized to view this page'

    setTimeout(() => {
      GStore.flashMessage = ''
    }, 3000)

    if (from.href) {
      console.log(from.href)
      // <--- If this navigation came from a previous page.
      return false
    } else {
      // <--- Must be navigating directly
      return { path: '/' } // <--- Push navigation to the root route.
    }
  }
})
</script>
<template>
  <p>Edit the event here</p>
</template>
