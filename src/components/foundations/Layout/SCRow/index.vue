<template>
  <a-row
    :id="id"
    :align="align"
    :justify="justify"
    :type="type"
    :gutter="gutter"
  >
    <slot />
  </a-row>
</template>

<script>
import { Row } from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css'

export default {
  name: 'SCRow',
  components: {
    'a-row': Row
  },
  props: {
    id: {
      type: String,
      default: null
    },
    align: {
      type: String,
      default: 'top',
      validator(value) {
        return ['top', 'middle', 'bottom'].indexOf(value) !== -1
      }
    },
    justify: {
      type: String,
      default: 'start',
      validator(value) {
        return ['start', 'end', 'center', 'space-around', 'space-between'].indexOf(value) !== -1
      }
    },
    type: {
      type: String,
      default: null,
      validator(value) {
        return ['flex'].indexOf(value) !== -1
      }
    },
    gutter: {
      type: [Number, Object, Array],
      default: 0
    }
  }
}
</script>
