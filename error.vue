<script setup lang="ts">
import type { NuxtError } from '#app';
import { headerLinks } from './header-links';

useSeoMeta({
  title: 'Page not found',
  description: 'We are sorry but this page could not be found.',
});

defineProps({
  error: {
    type: Object as PropType<NuxtError>,
    required: true,
  },
});

useHead({
  htmlAttrs: {
    lang: 'en',
  },
});

const { data: navigation } = await useAsyncData('navigation', () => fetchContentNavigation());

provide('navigation', navigation);
</script>

<template>
  <div>
    <HeaderComponent :links="unref(computed(() => headerLinks()))" />

    <UMain>
      <UContainer>
        <UPage>
          <UPageError :error="error" />
        </UPage>
      </UContainer>
    </UMain>

    <FooterComponent />

    <UNotifications />
  </div>
</template>
