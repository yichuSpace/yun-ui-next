<template>
  <div class="yun-color-alpha-slider" :class="{ 'is-vertical': vertical }">
    <div
      ref="bar"
      class="yun-color-alpha-slider__bar"
      :style="{
        background,
      }"
      @click="handleClick"
    ></div>
    <div
      ref="thumb"
      class="yun-color-alpha-slider__thumb"
      :style="{
        left: thumbLeft + 'px',
        top: thumbTop + 'px',
      }"
    ></div>
  </div>
</template>

<script>
import { watch, ref, onMounted, getCurrentInstance } from 'vue'
import draggable from './draggable'

export default {
  name: 'YunColorAlphaSlider',
  props: {
    color: {
      type: Object,
      required: true,
    },
    vertical: {
      type: Boolean,
      default: false,
    },
  },
  setup(props) {
    const instance = getCurrentInstance()
    // ref
    const thumb = ref(null)
    const bar = ref(null)

    // data
    const thumbLeft = ref(0)
    const thumbTop = ref(0)
    const background = ref(null)

    watch(
      () => props.color.get('alpha'),
      () => {
        update()
      },
    )
    watch(
      () => props.color.value,
      () => {
        update()
      },
    )

    //methods
    function getThumbLeft() {
      if (props.vertical) return 0
      const el = instance.vnode.el
      const alpha = props.color.get('alpha')

      if (!el) return 0
      return Math.round((alpha * (el.offsetWidth - thumb.value.offsetWidth / 2)) / 100)
    }

    function getThumbTop() {
      const el = instance.vnode.el
      if (!props.vertical) return 0
      const alpha = props.color.get('alpha')

      if (!el) return 0
      return Math.round((alpha * (el.offsetHeight - thumb.value.offsetHeight / 2)) / 100)
    }

    function getBackground() {
      if (props.color && props.color.value) {
        const { r, g, b } = props.color.toRgb()
        return `linear-gradient(to right, rgba(${r}, ${g}, ${b}, 0) 0%, rgba(${r}, ${g}, ${b}, 1) 100%)`
      }
      return null
    }

    function handleClick(event) {
      const target = event.target

      if (target !== thumb.value) {
        handleDrag(event)
      }
    }

    function handleDrag(event) {
      const el = instance.vnode.el
      const rect = el.getBoundingClientRect()

      if (!props.vertical) {
        let left = event.clientX - rect.left
        left = Math.max(thumb.value.offsetWidth / 2, left)
        left = Math.min(left, rect.width - thumb.value.offsetWidth / 2)

        props.color.set(
          'alpha',
          Math.round(((left - thumb.value.offsetWidth / 2) / (rect.width - thumb.value.offsetWidth)) * 100),
        )
      } else {
        let top = event.clientY - rect.top
        top = Math.max(thumb.value.offsetHeight / 2, top)
        top = Math.min(top, rect.height - thumb.value.offsetHeight / 2)

        props.color.set(
          'alpha',
          Math.round(((top - thumb.value.offsetHeight / 2) / (rect.height - thumb.value.offsetHeight)) * 100),
        )
      }
    }

    function update() {
      thumbLeft.value = getThumbLeft()
      thumbTop.value = getThumbTop()
      background.value = getBackground()
    }

    // mounded
    onMounted(() => {
      const dragConfig = {
        drag: event => {
          handleDrag(event)
        },
        end: event => {
          handleDrag(event)
        },
      }

      draggable(bar.value, dragConfig)
      draggable(thumb.value, dragConfig)
      update()
    })

    return {
      thumb,
      bar,
      thumbLeft,
      thumbTop,
      background,
      handleClick,
      update,
    }
  },
}
</script>
