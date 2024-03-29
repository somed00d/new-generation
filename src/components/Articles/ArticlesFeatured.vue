<script setup lang="ts">
import { Articles } from '~/ghostTypes'
const { t } = useI18n()
const props = defineProps<{
  articles: Articles
}>()
</script>

<template>
  <section class="articles-featured">
    <div class="articles-featured__header-wrapper">
      <h1 class="articles-featured__header">{{ t('articles.featured') }}</h1>
    </div>
    <div class="articles-featured__articles-wrapper">
      <article
        v-for="article in props.articles"
        :key="article.slug"
        class="articles-featured__article"
      >
        <articles-featured-article :article="article" />
      </article>
    </div>
  </section>
</template>

<style lang="postcss" scoped>
.articles-featured {
  padding: 1rem;
  padding-bottom: 2rem;
  background-color: var(--slate-300);
  @media (min-width: 1100px) {
    margin: 0 0rem 1rem 0rem;
    padding: 1rem 2rem;
    border-radius: 6px;
  }
  .articles-featured__header-wrapper {
    display: flex;
    justify-content: space-between;
    position: sticky;
    position: -webkit-sticky;
    top: 0;
    z-index: 200;
    background-color: none;
    margin: 2rem 0rem;
    border-bottom: 3px solid var(--slate-700);
    background-color: var(--slate-300);
    letter-spacing: 1.2px;
    .articles-featured__header {
      font-family: var(--font-normal);
      font-size: var(--step-1);
      letter-spacing: 0.5px;
      text-transform: uppercase;
      color: var(--slate-700);
      margin: 0;
      padding: 1rem 0.5rem;
      padding-right: 1rem;
    }
  }
  .articles-featured__articles-wrapper {
    margin: 1rem 0;
    --min: 45ch;
    --gap: 2rem;

    @media (max-width: 768px) {
      --gap: 0rem;
    }
    display: grid;
    grid-gap: var(--gap);
    /* min() with 100% prevents overflow
    in extra narrow spaces */
    grid-template-columns: repeat(auto-fit, minmax(min(100%, var(--min)), 1fr));
    .articles-featured__article {
      background-color: var(--slate-300);
      @media (max-width: 994px) {
        padding-bottom: 1rem;
      }
      &:last-child {
        ::v-deep(.featured-article__wrapper) {
          @media (max-width: 768px) {
            /* border-bottom: 3px solid var(--green);
            padding-bottom: 3rem; */
            border-bottom: none;
          }
        }
      }
    }
  }
}

@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}

html.dark {
  .articles-featured {
    background-color: #161618;
    .articles-featured__header-wrapper {
      background-color: #161618;
      border-color: var(--slate-200);
      .articles-featured__header {
        color: var(--slate-200);
      }
    }
    .articles-featured__article {
      background-color: #161618;
    }
  }
}
</style>
