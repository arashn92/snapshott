<script setup lang="ts">
import { sanitizeUrl } from '@braintree/sanitize-url';

const props = defineProps<{ space?: Record<string, any> }>();

type SocialItem = { icon: string; link: string };

const socials = computed<SocialItem[]>(() => {
  const socialsArray: SocialItem[] = [];

  if (props.space?.twitter) {
    socialsArray.push({
      icon: 'twitter',
      link: `https://twitter.com/${props.space?.twitter}`
    });
  }

  if (props.space?.github) {
    socialsArray.push({
      icon: 'github',
      link: `https://github.com/${props.space?.github}`
    });
  }

  if (props.space?.website) {
    socialsArray.push({
      icon: 'earth',
      link: sanitizeUrl(props.space?.website)
    });
  }

  if (props.space?.coingecko) {
    socialsArray.push({
      icon: 'coingecko',
      link: `https://www.coingecko.com/coins/${props.space?.coingecko}`
    });
  }

  return socialsArray;
});
</script>

<template>
  <div v-if="socials.length" class="my-4 flex items-center space-x-2 px-4">
    <BaseLink
      v-for="social in socials"
      :key="social.icon"
      :link="social.link"
      class="text-sm text-skin-text hover:text-skin-link"
      hide-external-icon
    >
      <i-s-twitter v-if="social.icon === 'twitter'" class="text-[18px]" />
      <i-s-github v-if="social.icon === 'github'" />
      <i-ho-globe-alt v-if="social.icon === 'earth'" class="text-[19px]" />
      <i-s-coingecko v-if="social.icon === 'coingecko'" />
    </BaseLink>
  </div>
</template>
