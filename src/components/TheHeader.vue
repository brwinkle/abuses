<template>
  <header>
    <center-wrapper :top="true">
      <div class="leadin">A video archive of</div>
      <h1>Police Abuses</h1>
      <div class="leadout">{{ total }} Videos</div>
      <incident-filter v-if="showFilter" :value="city" />
    </center-wrapper>
  </header>
</template>

<script>
import CenterWrapper from '@/components/CenterWrapper.vue'
import IncidentFilter from '@/components/IncidentFilter.vue'
import useIncidents from '@/use/incidents'

export default {
  setup() {
    const { total } = useIncidents()

    return { total }
  },
  components: {
    CenterWrapper,
    IncidentFilter,
  },

  props: {
    city: {
      type: String,
      default: '',
    },
  },

  computed: {
    showFilter() {
      return this.$route.name === 'City' || this.$route.name === 'Root'
    },
  },
}
</script>

<style scoped lang="postcss">
header {
  @mixin color-negative;

  position: sticky;
  top: 0;
  padding: 0.5em 0 2em;
  z-index: var(--z-header);
  border-bottom: 1px solid var(--color-white);
}

h1 {
  line-height: var(--line-height-header);
  font-weight: var(--font-weight-bold);
  font-family: var(--font-family-header);
  font-size: 2rem;

  @media (--viewport-xs) {
    font-size: 2.25rem;
  }

  @media (--viewport-sm) {
    font-size: 3rem;
  }
}

.leadin {
  font-size: 1.125em;
  line-height: 1;
}

.leadout {
  font-size: 0.875em;
  line-height: 1;
  text-transform: uppercase;
}
</style>
