<script lang="ts" setup name="FDialog">
  import { Props, Emits } from './dialog'
  import { FIcon } from '@fighting-design/fighting-components'
  import type {
    transitionEventInterface,
    closeDialogInterface
  } from './interface'

  defineProps(Props)
  const emit = defineEmits(Emits)

  const closeDialog: closeDialogInterface = (): void => {
    emit('update:visible', false)
  }

  const open: transitionEventInterface = (evt: MouseEvent): void => {
    emit('open', evt)
  }

  const openEnd: transitionEventInterface = (evt: MouseEvent): void => {
    emit('open-end', evt)
  }

  const close: transitionEventInterface = (evt: MouseEvent): void => {
    emit('close', evt)
  }

  const closeEnd: transitionEventInterface = (evt: MouseEvent): void => {
    emit('close-end', evt)
  }
</script>

<template>
  <teleport to="body" :disabled="!appendToBody">
    <transition
      name="f-dialog-fade"
      @before-enter="open"
      @after-enter="openEnd"
      @before-leave="close"
      @after-leave="closeEnd"
    >
      <div
        v-show="visible"
        :class="[
          'f-dialog-mask',
          {
            'f-dialog-mask-modal': modal
          }
        ]"
        :style="{ zIndex }"
        @click.self="modalClose && closeDialog()"
      >
        <div
          :class="[
            'f-dialog',
            {
              'f-dialog-shadow': !modal
            }
          ]"
          :style="{
            width,
            height,
            marginTop: top
          }"
        >
          <header class="f-dialog-header">
            <slot name="title">{{ title }}</slot>
            <f-icon :icon="closeIcon || 'f-icon-close'" @click="closeDialog" />
          </header>

          <section v-if="$slots.default" class="f-dialog-body">
            <slot />
          </section>

          <footer v-if="$slots.footer" class="f-dialog-footer">
            <slot name="footer" />
          </footer>
        </div>
      </div>
    </transition>
  </teleport>
</template>
