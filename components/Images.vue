<!-- eslint-disable array-callback-return -->
<script setup lang="ts">
import type { Image } from '~/types/Image'

const props = defineProps<{
  title: string
  type: string
  images: any
}>()

const thumb = ref<any>()

const imagesCount = computed(() => `${props.images.length} ${props.images.length > 1 ? 'Images' : 'Image'}`)

if (props.type === 'poster')
  thumb.value = `https://image.tmdb.org/t/p/w370_and_h556_bestv2`
else
  thumb.value = `https://image.tmdb.org/t/p/w533_and_h300_bestv2`

props.images.map((image: Image) => {
  image.thumb = `${thumb.value}${image.file_path}`
  image.src = `original${image.file_path}`
})
</script>

<template>
  <div>
    <div flex items-baseline gap-4>
      <h2 text-2xl text-white>
        {{ title }}
      </h2>
      <strong text-sm text-zinc-400>{{ imagesCount }}</strong>
    </div>
    <div flex flex-wrap gap-2>
      <ImagesItem v-for="(image, index) in images" :key="index" :image="image" :index="index" :type="type" />
    </div>
  </div>
</template>
