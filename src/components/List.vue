<template>
  <div class="list-container">
    <ul
      v-if="list.length"
      class="list-container__list"
    >
      <li
        v-for="item in list"
        :key="item"
        class="list-container__list-item"
      >
        {{ item }}
      </li>
    </ul>
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
  name: 'List',
  props: {
    list: {
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
@import '@/styles/variables/colors';

.list-container {
  .list-container__list {
    margin-left: 18px;

    .list-container__list-item {
      margin-bottom: 6px;
      &:last-child { margin-bottom: 0; }
    }
  }
}
</style>
