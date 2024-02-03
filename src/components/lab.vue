<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
    name: 'lab',
    setup() {
        const posts = ref([
      { id: 1, title: 'My journey with Vue' },
      { id: 2, title: 'Blogging with Vue' },
      { id: 3, title: 'Why Vue is so fun' }
    ])
        const items = [1, 2, 3, 4, , 5]
        return {
            populateVoiceList,
            items,
            posts
        }
    }
})
</script>
<template>
    <div v-for="item in posts">{{ item }}</div>
    <!-- <p>{{ populateVoiceList }}</p> -->
    <!-- <p>{{ populateVoiceList.voices }}</p> -->
</template>