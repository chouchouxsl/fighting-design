<script setup lang="ts" name="FLoading">
  import { computed } from 'vue'
  import { Props, Emits } from './loading'
  import { FIcon } from '@fighting-design/fighting-components'
  import type { handleClickInterface } from './interface'
  import type { ComputedRef, CSSProperties } from 'vue'

  const prop = defineProps(Props)
  const emit = defineEmits(Emits)

  const handleClick: handleClickInterface = (evt: MouseEvent): void => {
    prop.close && emit('close', evt)
  }

  const loadingStyleList: ComputedRef<CSSProperties> = computed(
    (): CSSProperties => {
      const { background, opacity, textColor } = prop

      return {
        background,
        opacity,
        color: textColor
      } as const
    }
  )
</script>

<template>
  <div
    v-if="show"
    class="f-loading"
    :style="loadingStyleList"
    @click="handleClick"
  >
    <f-icon :icon="icon || 'f-icon-loading'" class="f-loading-animation" />
    <span class="f-loading-title" :style="{ fontSize: textSize }">
      {{ text || '加载中' }}
    </span>
  </div>
</template>
