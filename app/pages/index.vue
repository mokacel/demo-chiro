<script setup lang="ts">
import { brand } from '~/utils/brand'

const { data: posts } = await useAsyncData('home-blog',
  () => queryCollection('blog').where('published', '=', true).order('date', 'DESC').limit(3).all()
)

useSeoMeta({ title: brand.name, description: brand.description })

const services = [
  {
    title: 'Chiropractic Adjustments',
    description: 'Manual spinal adjustments to restore alignment, reduce pain, and improve your nervous system function.'
  },
  {
    title: 'Deep Tissue Massage',
    description: 'Targeted massage therapy for chronic tension, sports recovery, and stress relief. 60 and 90 minute sessions.'
  },
  {
    title: 'Postural Assessment',
    description: 'A full-body analysis of how you sit, stand, and move — and a correction plan built around your lifestyle.'
  },
  {
    title: 'Sports Injury Rehab',
    description: 'Treatment and rehab for acute and chronic sports injuries. We work with athletes at every level.'
  },
  {
    title: 'Dry Needling',
    description: 'Trigger point therapy using fine needles to release stubborn muscle tension and improve range of motion.'
  },
  {
    title: 'Prenatal Care',
    description: 'Gentle, safe chiropractic support throughout pregnancy to manage discomfort and prepare your body for birth.'
  }
]

const testimonials = [
  {
    quote: "I came in barely able to turn my neck. After three sessions I was back training. The difference was immediate.",
    name: 'Marcus T.',
    role: 'Marathon runner'
  },
  {
    quote: "I've been to chiropractors before but this felt different. They actually listened and explained everything.",
    name: 'Sarah K.',
    role: 'Graphic designer, desk worker'
  },
  {
    quote: "The prenatal sessions got me through the last trimester. I cannot recommend Align enough.",
    name: 'Jess M.',
    role: 'First-time mum'
  },
  {
    quote: "Six months of lower back pain, gone in four weeks. I wish I'd come sooner.",
    name: 'David R.',
    role: 'Construction manager'
  }
]
</script>

<template>
  <div>
    <SectionHero :title="brand.tagline" :subtitle="brand.description" />

    <SectionServices id="services" title="How we can help" :items="services" />

    <SectionTestimonials title="What our patients say" :items="testimonials" />

    <section v-if="posts?.length" class="py-20 border-t border-(--color-border)">
      <div class="max-w-5xl mx-auto px-6">
        <div class="flex items-end justify-between mb-10">
          <h2 class="font-serif text-3xl md:text-4xl font-semibold">From the blog</h2>
          <BaseButton to="/blog" variant="ghost" size="sm">All posts →</BaseButton>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <CardBlog
            v-for="post in posts"
            :key="post.path"
            :title="post.title"
            :description="post.description"
            :date="post.date"
            :tags="post.tags"
            :image="post.image"
            :to="post.path"
            :min-read="post.minRead"
          />
        </div>
      </div>
    </section>

    <SectionContact />
  </div>
</template>
