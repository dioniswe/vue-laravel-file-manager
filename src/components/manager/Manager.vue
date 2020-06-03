<template>
    <div class="fm-content d-flex flex-column">
        <disk-list v-if="multipleDisksMode" v-bind:manager="manager"></disk-list>
        <breadcrumb v-if="nonCompactMode"  v-bind:manager="manager"></breadcrumb>
        <div class="fm-content-body">
            <table-view v-if="viewType === 'table'" v-bind:manager="manager"></table-view>
            <grid-view v-else v-bind:manager="manager"></grid-view>
        </div>
    </div>
</template>

<script>
// Components
import DiskList from './DiskList.vue';
import Breadcrumb from './Breadcrumb.vue';
import TableView from './TableView.vue';
import GridView from './GridView.vue';

export default {
  name: 'Manager',
  components: {
    DiskList,
    Breadcrumb,
    TableView,
    GridView,
  },
  props: {
    manager: { type: String, required: true },
  },
  computed: {
    /**
     * view type - grid or table
     * @returns {default.computed.viewType|(function())|string}
     */
    viewType() {
      return this.$store.state.fm[this.manager].viewType;
    },
    nonCompactMode() {
      //console.log(this.$store.state);
      return this.$store.state.fm.settings.compactMode !== true;
    },
    multipleDisksMode() {
      //console.log(this.$store.state);
      return this.$store.state.fm.settings.singleDiskMode !== true;
    },
  },
};
</script>

<style lang="scss">
    .fm-content {
        height: 100%;
        padding-left: 1rem;

        .fm-content-body {
            overflow: auto;
        }
    }
</style>
