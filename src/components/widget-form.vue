<template>
  <div class="widget-form-wrapper">
    <div
      class="widget-form-container"
      :style="{backgroundColor:pageData.config.backgroundColor,backgroundImage:`url(${pageData.config.backgroundImage})`}"
    >
      <img v-if="theme" :src="themeBanner" alt="banner" width="100%" @click="setConfigTab()" />
      <widget-form-list
        list="formList"
        v-if="theme"
        :class="theme.value"
        :style="{width:theme.contentWidth,margin:theme.margin,borderRadius:theme.borderRadius?'10px':'0'}"
      />
      <widget-form-list list="list" />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import WidgetFormList from './widget-form-list'

export default {
  components: {
    WidgetFormList
  },
  data() {
    return {
    }
  },
  computed: {
    themeBanner() {
      if (this.theme.banner.includes("http://") || this.theme.banner.includes("https://")) {
        return this.theme.banner;
      }
      return this.BASE_URL + this.theme.banner;
    },
    ...mapState({
      selectWg: state => state.common.selectWg,
      pageData: state => state.common.pageData,
      theme: state => state.common.pageData.config.theme,
    })
  },
  methods: {
    setConfigTab() {
      this.$store.commit("setConfigTab", "page");
    }
  }
}
</script>
