<script>
import { mapState } from 'vuex';
import BadgeListRow from './badge_list_row.vue';
import { GROUP_BADGE } from '../constants';

export default {
  name: 'BadgeList',
  components: {
    BadgeListRow,
  },
  computed: {
    ...mapState(['badges', 'isLoading', 'kind']),
    hasNoBadges() {
      return !this.isLoading && (!this.badges || !this.badges.length);
    },
    isGroupBadge() {
      return this.kind === GROUP_BADGE;
    },
  },
};
</script>

<template>
  <div class="card">
    <div class="card-header">
      {{ s__('Badges|Your badges') }}
      <span
        v-show="!isLoading"
        class="badge badge-pill"
      >{{ badges.length }}</span>
    </div>
    <gl-loading-icon
      v-show="isLoading"
      :size="2"
      class="card-body"
    />
    <div
      v-if="hasNoBadges"
      class="card-body"
    >
      <span v-if="isGroupBadge">{{ s__('Badges|This group has no badges') }}</span>
      <span v-else>{{ s__('Badges|This project has no badges') }}</span>
    </div>
    <div
      v-else
      class="card-body"
    >
      <badge-list-row
        v-for="badge in badges"
        :key="badge.id"
        :badge="badge"
      />
    </div>
  </div>
</template>
