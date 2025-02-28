<template src="./template.html"></template>
<script lang="ts">
import { computed, Ref, ref } from 'vue';
import { StarFillN } from '@nutui/icons-vue';
import { createComponent, renderIcon } from '@/packages/utils/create';
import { pxCheck } from '@/packages/utils/pxCheck';
import { useTouch } from '@/packages/utils/useTouch';
const { create, componentName } = createComponent('rate');
export default create({
  props: {
    count: {
      type: [String, Number],
      default: 5
    },
    modelValue: {
      type: [String, Number],
      default: 0
    },
    customIcon: {
      type: Object,
      default: () => {
        return StarFillN;
      }
    },
    size: {
      type: [String, Number],
      default: undefined
    },
    activeColor: {
      type: String,
      default: ''
    },
    voidColor: {
      type: String,
      default: ''
    },
    readonly: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    allowHalf: {
      type: Boolean,
      default: false
    },
    touchable: {
      type: Boolean,
      default: true
    },
    spacing: {
      type: [String, Number],
      default: undefined
    }
  },
  components: { StarFillN },
  emits: ['update:modelValue', 'change'],
  setup(props: any, { emit, slots }: any) {
    const rateRefs = ref<HTMLElement[]>([]);
    const classes = computed(() => {
      const prefixCls = componentName;
      return {
        [prefixCls]: true
      };
    });
    const updateVal = (value: number) => {
      emit('update:modelValue', value);
      emit('change', value);
    };
    const onClick = (e: number, index: number) => {
      if (props.disabled || props.readonly) return;
      let value = 0;
      if (index === 1 && props.modelValue === index) {
        value = 0;
      } else {
        value = index;
        if (props.allowHalf && e == 2) {
          value -= 0.5;
        }
      }
      updateVal(value);
    };
    const getScoreByPosition = (x: number, rateRefs: Ref<HTMLElement[]>, allowHalf: boolean) => {
      let v = 0;
      for (let index = rateRefs.value.length - 1; index >= 0; index--) {
        const item = rateRefs.value[index];
        if (x > item.offsetLeft) {
          if (allowHalf) {
            v = index + (x > item.offsetLeft + item.clientWidth / 2 ? 1 : 0.5);
          } else {
            v = index + 1;
          }
          break;
        }
      }
      return v;
    };
    const touch = useTouch();
    const touchMethods = {
      onTouchStart(event: TouchEvent) {
        if (!props.touchable || props.readonly) return;
        touch.start(event);
      },
      onTouchMove(event: TouchEvent) {
        if (!props.touchable) return;
        touch.move(event);
        if (touch.isHorizontal()) {
          if (rateRefs.value) {
            event.preventDefault();
            updateVal(getScoreByPosition(touch.moveX.value, rateRefs, props.allowHalf));
          }
        }
      }
    };
    const refRandomId = Math.random().toString(36).slice(-8);
    return {
      classes,
      ...touchMethods,
      onClick,
      pxCheck,
      rateRefs,
      refRandomId,
      renderIcon,
      slots
    };
  }
});
</script>
