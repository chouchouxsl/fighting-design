<template>
  <v-t-social-links
    v-if="config.socialLinks"
    class="VPNavScreenSocialLinks"
    size="medium"
    :links="config.socialLinks"
  />
</template>

<script lang="ts" setup>
  import { VTSocialLinks } from '../../core'
  import { useConfig } from '../composables/config'

  const { config } = useConfig()
</script>
