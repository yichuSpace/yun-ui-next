<template>
  <span
    :class="[
      'yun-tag',
      type ? `is-${type}` : '',
      dark ? 'is-dark' : '',
      dot ? 'is-dot' : '',
      checkable ? 'is-checkable' : '',
      checkable && checked ? 'is-checked' : '',
      { 'no-border': noBorder },
    ]"
    :style="tagStyleBind"
    @click="handleClick"
  >
    <span v-if="dot" class="yun-dot"></span>
    <slot></slot>
    <i
      class="yun-iconfont yun-icon-close"
      v-if="closable"
      :style="dot ? { backgroundColor: '#fff', color } : {}"
      @click="handleClose"
    ></i>
  </span>
</template>

<script>
import { computed, ref, watch } from 'vue'
import { UPDATE_MODEL_EVENT, CHANGE_EVENT } from '../../utils/constants'
import { typeColor } from '../../utils/log'

export default {
  name: 'YunTag',
  props: {
    name: String,
    closable: Boolean,
    type: String,
    dot: Boolean,
    noBorder: Boolean,
    color: String,
    tagStyle: {},
    fontSize: String,
    dark: Boolean,
    checkable: Boolean,
    modelValue: {
      type: Boolean,
      default: true,
    },
  },
  emits: [UPDATE_MODEL_EVENT, CHANGE_EVENT, 'click', 'close'],
  setup(props, { emit }) {
    const checked = ref(props.modelValue)

    const handleClose = e => {
      e.stopPropagation()
      emit('close', e)
    }
    const handleClick = e => {
      e.stopPropagation()
      if (props.checkable) {
        checked.value = !checked.value
        emit(UPDATE_MODEL_EVENT, checked.value)
        emit(CHANGE_EVENT, checked.value, props.name)
      }
      emit('click', e)
    }
    const dotColor = computed(() => (props.type ? typeColor(props.type) : props.color))
    const tagStyleBind = computed(() => {
      return props.dot
        ? {
            backgroundColor: 'transparent',
            color: props.color || 'rgba(0,0,0,.65)',
            fontSize: props.fontSize,
            ...props.tagStyle,
          }
        : {
            backgroundColor: props.color,
            color: props.color ? '#fff' : '',
            fontSize: props.fontSize,
            ...props.tagStyle,
          }
    })
    watch(
      () => props.modelValue,
      val => {
        checked.value = val
      },
    )
    return {
      checked,
      dotColor,
      tagStyleBind,
      handleClose,
      handleClick,
    }
  },
}
</script>
