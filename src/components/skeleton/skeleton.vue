<template>
  <template v-if="uiLoading">
    <div :class="['yun-skeleton', animation ? 'is-animated' : '']" v-bind="$attrs">
      <template v-for="i in count" :key="i">
        <slot v-if="loading" name="template">
          <yun-skeleton-item class="is-first" variant="p" />
          <yun-skeleton-item
            v-for="item in rows"
            :key="item"
            :class="{
              'yun-skeleton__paragraph': true,
              'is-last': item === rows && rows > 1,
            }"
            variant="p"
          />
        </slot>
      </template>
    </div>
  </template>
  <template v-else>
    <slot v-bind="$attrs"></slot>
  </template>
</template>

<script>
import { computed } from 'vue'
import YunSkeletonItem from '../skeleton-item'
import useThrottleRender from './use-throttle'

export default {
  name: 'YunSkeleton',
  components: { YunSkeletonItem },
  props: {
    animation: {
      type: Boolean,
      default: false,
    },
    count: {
      type: Number,
      default: 1,
    },
    rows: {
      type: Number,
      default: 3,
    },
    loading: {
      type: Boolean,
      default: true,
    },
    throttle: {
      type: Number,
    },
  },
  setup(props) {
    const innerLoading = computed(() => props.loading)

    const uiLoading = useThrottleRender(innerLoading, props.throttle)

    return {
      uiLoading,
    }
  },
}
</script>
