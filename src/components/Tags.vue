<template>
  <div class="tags-container">
    <div
      v-if="tags.length"
      class="tags-container__content"
    >
      <span
        v-for="tag in tags"
        :key="tag.label"
        :class="{ 'tags-container__tag--active': tag.isActive }"
        class="tags-container__tag"
      >
        {{ tag.label }}
      </span>
    </div>
    <span
      v-else
      class="no-content"
    >
      {{ $t(`no-content.${noContent}`) }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'Tag',
  props: {
    tags: {
      type: Array,
      required: true
    },
    noContent: {
      type: String,
      default: 'no-data'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/styles/variables/colors.scss';

.tags-container {
  .tags-container__content {
    display: flex;

    .tags-container__tag {
      font-size: 0.83em;
      color: $--color-text-placeholder;
      border: 1px solid $--color-text-placeholder;
      border-radius: 6px;
      padding: 4px 6px;
      margin-left: 6px;

      &:first-child { margin-left: 0; }

      &--active {
        background-color: $--color-success;
        border: 1px solid $--color-success;
        color: $--color-white;
      }
    }
  }
}
</style>
