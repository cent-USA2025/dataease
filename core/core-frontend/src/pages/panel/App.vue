<script setup lang="ts">
import { shallowRef, defineAsyncComponent, onBeforeMount } from 'vue'
import { propTypes } from '@/utils/propTypes'
import { useAppStoreWithOut } from '@/store/modules/app'
const appStore = useAppStoreWithOut()
onBeforeMount(() => {
  appStore.setIsDataEaseBi(true)
})
const VisualizationEditor = defineAsyncComponent(
  () => import('@/views/data-visualization/index.vue')
)
const DashboardEditor = defineAsyncComponent(() => import('@/views/dashboard/index.vue'))

const Dashboard = defineAsyncComponent(() => import('./DashboardPreview.vue'))
const ViewWrapper = defineAsyncComponent(() => import('./ViewWrapper.vue'))
const Dataset = defineAsyncComponent(() => import('@/views/visualized/data/dataset/index.vue'))
const Datasource = defineAsyncComponent(
  () => import('@/views/visualized/data/datasource/index.vue')
)
const ScreenPanel = defineAsyncComponent(() => import('@/views/data-visualization/PreviewShow.vue'))
const DashboardPanel = defineAsyncComponent(
  () => import('@/views/dashboard/DashboardPreviewShow.vue')
)
const props = defineProps({
  componentName: propTypes.string.def('DashboardEditor')
})
const currentComponent = shallowRef()

const componentMap = {
  DashboardEditor,
  VisualizationEditor,
  ViewWrapper,
  Dashboard,
  Dataset,
  Datasource,
  ScreenPanel,
  DashboardPanel
}

currentComponent.value = componentMap[props.componentName]
</script>
<template>
  <component :is="currentComponent"></component>
</template>
