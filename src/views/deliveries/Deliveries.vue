<template>
  <main class="home-container">
    <Header
      :title="$t('labels.welcome')"
      :subtitle="$t('labels.select-delivery')"
      class="home-container__header"
    />

    <component
      :is="isLoadingDeliveries ? 'TableSkeleton' : 'Table'"
      :table-data="deliveries"
      class="home-container__table cx-card"
    />
  </main>
</template>

<script>
import { defineAsyncComponent } from 'vue'
import { mapActions, mapGetters } from 'vuex'
import { useToast } from 'vue-toastification'

const Header = defineAsyncComponent(() => import('@/components/Header' /* webpackChunkName: 'Header' */))
const Table = defineAsyncComponent(() => import('./Table' /* webpackChunkName: 'Table' */))
const TableSkeleton = defineAsyncComponent(() => import('./skeleton/TableSkeleton' /* webpackChunkName: 'TableSkeleton' */))

export default {
  name: 'Home',
  components: {
    Header,
    Table,
    TableSkeleton
  },
  computed: {
    ...mapGetters({
      deliveries: 'getDeliveries',
      isLoadingDeliveries: 'getIsLoadingDeliveries'
    })
  },
  async beforeMount () {
    this.clearDelivery()

    await this.getDeliveries()
      .catch(() => {
        useToast().error(`Ops! ${this.$t('errors.somethig-wrong')}.`)
      })
  },
  methods: {
    ...mapActions([
      'getDeliveries',
      'clearDelivery'
    ])
  }
}
</script>

<style lang="scss" scoped>
.home-container {
  display: flex;
  flex-direction: column;
  height: calc(100vh - 20px);

  .home-container__table {
    flex: 1;
    overflow: hidden;
  }
}

@media (max-width: 600px) {
  .home-container {
    height: calc(100vh);

    .home-container__table.cx-card {
      padding: 30px 0;
    }
  }
}
</style>
