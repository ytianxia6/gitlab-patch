<script>
import CiIcon from '~/vue_shared/components/ci_icon.vue';
import Popover from '~/vue_shared/components/help_popover.vue';

/**
 * Renders the summary row for each report
 *
 * Used both in MR widget and Pipeline's view for:
 * - Unit tests reports
 * - Security reports
 */

export default {
  name: 'ReportSummaryRow',
  components: {
    CiIcon,
    Popover,
  },
  props: {
    summary: {
      type: String,
      required: true,
    },
    statusIcon: {
      type: String,
      required: true,
    },
    popoverOptions: {
      type: Object,
      required: false,
      default: null,
    },
  },
  computed: {
    iconStatus() {
      return {
        group: this.statusIcon,
        icon: `status_${this.statusIcon}`,
      };
    },
  },
};
</script>
<template>
  <div class="report-block-list-issue report-block-list-issue-parent">
    <div class="report-block-list-icon append-right-10 prepend-left-5">
      <gl-loading-icon
        v-if="statusIcon === 'loading'"
        css-class="report-block-list-loading-icon"
      />
      <ci-icon
        v-else
        :status="iconStatus"
      />
    </div>

    <div class="report-block-list-issue-description">
      <div class="report-block-list-issue-description-text">
        {{ summary }}
      </div>

      <popover
        v-if="popoverOptions"
        :options="popoverOptions"
      />

    </div>
  </div>
</template>
