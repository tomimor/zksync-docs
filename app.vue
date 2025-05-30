<script setup lang="ts">
import { headerLinks } from './header-links';

const { seo } = useAppConfig();

const { data: navigation } = await useAsyncData('navigation', () => fetchContentNavigation());
provide('navigation', navigation);

useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' },
    { name: 'theme-color', content: '#F2F2F2' },
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico', sizes: '48x48' },
    { rel: 'icon', href: '/zksync-icon_150.svg', sizes: 'any', type: 'image/svg+xml' },
    { rel: 'apple-touch-icon', href: '/apple-touch-icon.png' },
  ],
  htmlAttrs: {
    lang: 'en',
  },
});

useSeoMeta({
  titleTemplate: `%s - ${seo?.siteName}`,
  ogSiteName: seo?.siteName,
  ogUrl: 'https://docs.zksync.io',
  ogImageAlt: 'Hyperscaling Ethereum with ZK tech.',
  ogDescription:
    'ZKsync Docs bring you all information you need about our protocol, APIs, SDKs, ZK Stack, and ZK chains. Start with our guides and tutorials, or go deep into our architecture and protocol specification.',
  description:
    'ZKsync Docs bring you all information you need about our protocol, APIs, SDKs, ZK Stack, and ZK chains. Start with our guides and tutorials, or go deep into our architecture and protocol specification.',
  twitterDescription:
    'ZKsync Docs bring you all information you need about our protocol, APIs, SDKs, ZK Stack, and ZK chains. Start with our guides and tutorials, or go deep into our architecture and protocol specification.',
  twitterTitle: `%s`,
  twitterCard: 'summary_large_image',
  twitterSite: '@zksync',
  twitterCreator: '@zkSyncDevs',
  twitterImageAlt: 'Hyperscaling Ethereum with ZK tech.',
});
</script>

<template>
  <div>
    <NuxtPwaManifest />
    <NuxtLoadingIndicator />

    <HeaderComponent :links="unref(computed(() => headerLinks()))" />

    <UMain>
      <NuxtLayout>
        <NuxtPage />
      </NuxtLayout>
    </UMain>

    <FooterComponent />

    <UNotifications />
  </div>
</template>
