<script setup lang="ts">
import { CheckCircle } from 'lucide-vue-next'
import { brand } from '~/utils/brand'

const form = reactive({ name: '', email: '', message: '' })
const submitted = ref(false)
const loading = ref(false)

async function submit() {
  loading.value = true
  // Replace with your form handler: Resend, Netlify Forms, Formspree, etc.
  await new Promise(r => setTimeout(r, 800))
  submitted.value = true
  loading.value = false
}
</script>

<template>
  <section id="contact" class="py-20 border-t border-(--color-border)">
    <div class="max-w-5xl mx-auto px-6">
      <div class="grid md:grid-cols-2 gap-16 items-start">
        <div>
          <h2 class="font-serif text-4xl md:text-5xl font-semibold mb-4">
            Let's work together.
          </h2>
          <p class="text-(--color-muted-foreground) leading-relaxed mb-8">
            {{ brand.description }}
          </p>
          <a :href="`mailto:${brand.contact.email}`" class="text-primary-500 hover:underline text-sm">
            {{ brand.contact.email }}
          </a>
        </div>

        <form v-if="!submitted" class="flex flex-col gap-4" @submit.prevent="submit">
          <div class="flex flex-col gap-1.5">
            <label class="text-sm font-medium">Name</label>
            <BaseInput v-model="form.name" placeholder="Your name" />
          </div>
          <div class="flex flex-col gap-1.5">
            <label class="text-sm font-medium">Email</label>
            <BaseInput v-model="form.email" type="email" placeholder="you@example.com" />
          </div>
          <div class="flex flex-col gap-1.5">
            <label class="text-sm font-medium">Message</label>
            <BaseTextarea v-model="form.message" placeholder="Tell me about your project…" :rows="5" />
          </div>
          <BaseButton type="submit" size="lg" :disabled="loading" class="self-start">
            {{ loading ? 'Sending…' : 'Send message' }}
          </BaseButton>
        </form>

        <div v-else class="flex flex-col gap-2">
          <CheckCircle class="size-8 text-primary-500" />
          <p class="font-medium">Message sent.</p>
          <p class="text-sm text-(--color-muted-foreground)">I'll get back to you within a couple of days.</p>
        </div>
      </div>
    </div>
  </section>
</template>
