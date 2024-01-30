<script setup lang="ts">
import { cva } from 'class-variance-authority'
import { RouterLink, type RouteLocationRaw } from 'vue-router'
import { computed } from 'vue'

const buttonVariants = cva('button', {
  variants: {
    variant: {
      filled: '--variant-filled',
      outlined: '--variant-outlined'
    },
    size: {
      small: '--size-sm',
      regular: '--size-md',
      large: '--size-lg'
    },
    color: {
      default: '--color-default',
      yellow: '--color-yellow'
    }
  },
  defaultVariants: {
    variant: 'filled',
    size: 'regular',
    color: 'default'
  }
})

interface Props {
  variant?: NonNullable<Parameters<typeof buttonVariants>[0]>['variant']
  size?: NonNullable<Parameters<typeof buttonVariants>[0]>['size']
  color?: NonNullable<Parameters<typeof buttonVariants>[0]>['color']
  as?: 'button' | 'router-link' | 'a'
  block?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  as: 'button'
})

const isRouterLink = computed(() => {
  return props.as === 'router-link'
})
</script>

<script lang="ts">
export default {
  inheritAttrs: false
}
</script>

<template>
  <router-link
    v-if="isRouterLink"
    :tabindex="$attrs.disabled && 0"
    :to="$attrs.to as RouteLocationRaw"
    custom
    v-bind="$props"
    v-slot="{ href, navigate }"
  >
    <a
      v-bind="$attrs"
      :class="[buttonVariants({ variant, size, color }), { '--block': block }, $attrs.class]"
      @click="navigate"
      :href="href"
    >
      <slot name="prepend" />
      <div>
        <slot />
      </div>
      <slot name="append" />
    </a>
  </router-link>
  <component
    v-else
    v-bind="$attrs"
    :tabindex="$attrs.disabled && 0"
    :is="as"
    :class="[buttonVariants({ variant, size, color }), { '--block': block }, $attrs.class]"
  >
    <slot name="prepend" />
    <div>
      <slot />
    </div>
    <slot name="append" />
  </component>
</template>

<style scoped>
.button {
  all: unset;
  box-sizing: border-box;
  cursor: pointer;
  font-family: Poppins, Arial, Helvetica, sans-serif;
  font-style: normal;
  transition-property: color, background-color, border-color, text-decoration-color, fill, stroke;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
  border-radius: 1.75rem;
  margin-top: auto;
  margin-bottom: auto;
  text-align: center;
  color: var(--color-text);
  display: inline-flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  vertical-align: middle;
  gap: 0.5rem;
}

.button div {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
}

.button:disabled {
  cursor: not-allowed;
  opacity: 0.4;
}

.--variant-filled {
  background: var(--color-0);
}
.--variant-filled:not([disabled]):focus,
.--variant-filled:not([disabled]):hover {
  background: var(--color-1);
}

.--variant-outlined {
  border: 1px solid var(--color-text);
  background: white;
}
.--variant-outlined:not([disabled]):focus,
.--variant-outlined:not([disabled]):hover {
  background: var(--color-1);
}

.--size-lg {
  padding: 1rem 1.5rem;
  font-size: 1.125rem;
  font-weight: 600;
  line-height: 1.35;
  letter-spacing: -0.54px;
}

.--size-md {
  padding: 0.875rem 1.5rem;
  font-size: 1rem;
  font-weight: 600;
  line-height: 1.25;
  letter-spacing: -0.48px;
}

.--size-sm {
  padding: 0.625rem 1rem;
  font-size: 0.875rem;
  font-weight: 500;
  line-height: 1.4;
  letter-spacing: -0.42px;
}

.--color-default {
  --color-0: #a5a5a5;
  --color-1: #e6e6e6;
  --color-text: #171717;
}

.--color-yellow {
  --color-0: #ffbf52;
  --color-1: #ffd788;
  --color-text: #171717;
}

.--block {
  width: 100%;
}
</style>
