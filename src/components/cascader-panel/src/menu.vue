<template>
  <yun-scrollbar
    :id="menuId"
    tag="ul"
    role="menu"
    class="yun-cascader-menu"
    wrap-class="yun-cascader-menu__wrap"
    :view-class="['yun-cascader-menu__list', isEmpty && 'is-empty']"
    @mousemove="handleMouseMove"
    @mouseleave="clearHoverZone"
  >
    <yun-cascader-node v-for="node in nodes" :key="node.uid" :node="node" :menu-id="menuId" @expand="handleExpand" />
    <div v-if="isEmpty" class="yun-cascader-menu__empty-text">
      暂无数据
    </div>
    <svg v-else-if="panel.isHoverMenu" ref="hoverZone" class="yun-cascader-menu__hover-zone" />
  </yun-scrollbar>
</template>

<script>
import { computed, getCurrentInstance, inject, ref } from 'vue'
import YunScrollbar from '../../scrollbar'
import YunCascaderNode from './node.vue'
import { generateId } from '../../../utils/utilsHelper'
import { PANEL_INJECTION_KEY } from '../utils/utils'

export default {
  name: 'YunCascaderMenu',
  components: {
    YunScrollbar,
    YunCascaderNode,
  },
  props: {
    nodes: {
      type: Array,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },

  setup(props) {
    const instance = getCurrentInstance()
    const id = generateId()
    let activeNode = null
    let hoverTimer = null

    const panel = inject(PANEL_INJECTION_KEY)

    const hoverZone = ref(null)

    const isEmpty = computed(() => !props.nodes.length)
    const menuId = computed(() => `cascader-menu-${id}-${props.index}`)

    const handleExpand = e => {
      activeNode = e.target
    }

    const handleMouseMove = e => {
      if (!panel.isHoverMenu || !activeNode || !hoverZone.value) return

      if (activeNode.contains(e.target)) {
        clearHoverTimer()

        const el = instance.vnode.el
        const { left } = el.getBoundingClientRect()
        const { offsetWidth, offsetHeight } = el
        const startX = e.clientX - left
        const top = activeNode.offsetTop
        const bottom = top + activeNode.offsetHeight

        hoverZone.value.innerHTML = `
          <path style="pointer-events: auto;" fill="transparent" d="M${startX} ${top} L${offsetWidth} 0 V${top} Z" />
          <path style="pointer-events: auto;" fill="transparent" d="M${startX} ${bottom} L${offsetWidth} ${offsetHeight} V${bottom} Z" />
        `
      } else if (!hoverTimer) {
        hoverTimer = window.setTimeout(clearHoverZone, panel.config.hoverThreshold)
      }
    }

    const clearHoverTimer = () => {
      if (!hoverTimer) return
      clearTimeout(hoverTimer)
      hoverTimer = null
    }

    const clearHoverZone = () => {
      if (!hoverZone.value) return
      hoverZone.value.innerHTML = ''
      clearHoverTimer()
    }

    return {
      panel,
      hoverZone,
      isEmpty,
      menuId,
      handleExpand,
      handleMouseMove,
      clearHoverZone,
    }
  },
}
</script>
