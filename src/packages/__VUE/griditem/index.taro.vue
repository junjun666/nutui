<template>
  <view :class="rootClass" :style="rootStyle" @click="handleClick">
    <view :class="contentClass">
      <slot></slot>
      <view class="nut-grid-item__text">
        <template v-if="text">{{ text }}</template>
        <slot v-else name="text"></slot>
      </view>
    </view>
  </view>
</template>

<script lang="ts">
import { computed, CSSProperties } from 'vue';
import { createComponent } from '@/packages/utils/create';
import { pxCheck } from '@/packages/utils/pxCheck';
import { useInject } from '@/packages/utils/useRelation/useInject';
import { GRID_KEY, GridProps } from '../grid/common';
const { create, componentName } = createComponent('grid-item');

export default create({
  props: {
    text: {
      type: String
    }
    // router
    // to: {
    //   type: [String, Object]
    // },
    // url: {
    //   type: String,
    //   default: ''
    // },
    // replace: {
    //   type: Boolean,
    //   default: false
    // }
  },
  emits: ['click'],
  setup(props, { emit }) {
    const Parent = useInject<{ props: Required<GridProps> }>(GRID_KEY);
    if (!Parent.parent) return {} as any;
    const index = Parent.index;
    const parent = Parent.parent.props;

    // root
    const rootClass = computed(() => {
      const prefixCls = componentName;
      return {
        [prefixCls]: true
      };
    });

    const rootStyle = computed(() => {
      const style: CSSProperties = {
        flexBasis: `${100 / +parent.columnNum}%`
      };

      if (parent.square) {
        style.paddingTop = `${100 / +parent.columnNum}%`;
      } else if (parent.gutter) {
        style.paddingRight = pxCheck(parent.gutter);
        if (index.value >= +parent.columnNum) {
          style.marginTop = pxCheck(parent.gutter);
        }
      }

      return style;
    });

    // content
    const contentClass = computed(() => {
      const prefixCls = `${componentName}__content`;
      return {
        [`${prefixCls}`]: true,
        [`${prefixCls}--border`]: parent.border,
        [`${prefixCls}--surround`]: parent.border && parent.gutter,
        [`${prefixCls}--center`]: parent.center,
        [`${prefixCls}--square`]: parent.square,
        [`${prefixCls}--reverse`]: parent.reverse,
        [`${prefixCls}--${parent.direction}`]: !!parent.direction,
        [`${prefixCls}--clickable`]: parent.clickable
      };
    });

    // click
    const handleClick = (event: Event) => {
      emit('click', event);
    };

    return {
      rootClass,
      rootStyle,
      contentClass,
      handleClick
    };
  }
});
</script>
