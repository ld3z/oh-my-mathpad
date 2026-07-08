<script setup lang="ts">
import { computed } from 'vue'
import { withBase } from 'vitepress'

const props = defineProps<{
  /** Page or external URL the card points to */
  link: string
  /** Card title shown below the logo */
  title: string
  /** Path to the logo image (put files in docs/public and use e.g. /chrome.svg) */
  logo?: string
  /** Alt text for the logo image */
  logoAlt?: string
}>()

const isExternal = computed(() => /^https?:\/\//.test(props.link))
const href = computed(() => (isExternal.value ? props.link : withBase(props.link)))
const logoSrc = computed(() =>
  props.logo && props.logo.startsWith('/') ? withBase(props.logo) : props.logo
)
</script>

<template>
  <a
    class="link-card"
    :href="href"
    :target="isExternal ? '_blank' : undefined"
    :rel="isExternal ? 'noreferrer' : undefined"
  >
    <img v-if="logoSrc" class="link-card-logo" :src="logoSrc" :alt="logoAlt ?? title" />
    <span class="link-card-title">{{ title }}</span>
    <span v-if="$slots.default" class="link-card-text">
      <slot />
    </span>
  </a>
</template>

<style scoped>
.link-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 10px;
  padding: 24px 16px;
  border: 1px solid var(--vp-c-divider);
  border-radius: 12px;
  background-color: var(--vp-c-bg-soft);
  text-decoration: none !important;
  color: inherit;
  transition: border-color 0.25s, background-color 0.25s, transform 0.25s;
}

.link-card:hover {
  border-color: var(--vp-c-brand-1);
  background-color: var(--vp-c-bg-elv);
  transform: translateY(-2px);
}

.link-card-logo {
  width: 48px;
  height: 48px;
  object-fit: contain;
}

.link-card-title {
  font-weight: 600;
  font-size: 16px;
  color: var(--vp-c-text-1);
}

.link-card-text {
  font-size: 13px;
  line-height: 1.5;
  color: var(--vp-c-text-2);
}
</style>
