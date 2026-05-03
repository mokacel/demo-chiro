<script setup lang="ts">
// TODO: migrate variants to CVA (class-variance-authority) for typed, composable styling
// See: https://cva.style — same pattern shadcn-vue uses

defineProps<{
  variant?: 'primary' | 'ghost' | 'outline'
  size?: 'sm' | 'md' | 'lg'
  type?: 'button' | 'submit'
  to?: string
  loading?: boolean
  disabled?: boolean
}>()

const variantClass = {
  primary: 'bg-primary-500 text-white hover:bg-primary-600 focus-visible:ring-primary-500',
  ghost: 'bg-transparent text-(--color-foreground) hover:bg-(--color-muted)',
  outline: 'border border-(--color-border) bg-transparent hover:bg-(--color-muted)'
}

const sizeClass = {
  sm: 'px-3 py-1.5 text-sm rounded-md gap-1.5',
  md: 'px-4 py-2 text-sm rounded-lg gap-2',
  lg: 'px-5 py-2.5 text-base rounded-lg gap-2'
}
</script>

<template>
  <component
    :is="to ? resolveComponent('NuxtLink') : 'button'"
    :to="to"
    :type="to ? undefined : (type ?? 'button')"
    :disabled="disabled || loading"
    :class="[
      'inline-flex items-center justify-center font-medium transition-colors cursor-pointer focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 disabled:opacity-50 disabled:pointer-events-none',
      variantClass[variant ?? 'primary'],
      sizeClass[size ?? 'md']
    ]"
  >
    <slot />
  </component>
</template>
