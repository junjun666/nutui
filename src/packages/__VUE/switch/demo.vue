<template>
  <div class="demo">
    <h2>{{ translate('basic') }}</h2>
    <nut-cell>
      <nut-switch v-model="data.checked1" />
    </nut-cell>

    <h2>{{ translate('title1') }}</h2>
    <nut-cell>
      <nut-switch
        :v-model="translate('text1')"
        :active-value="translate('text1')"
        :inactive-value="translate('text2')"
      />
    </nut-cell>

    <h2>{{ translate('title2') }}</h2>
    <nut-cell>
      <nut-switch v-model="data.checked2" disable />
    </nut-cell>

    <h2>{{ translate('title3') }}</h2>
    <nut-cell>
      <nut-switch v-model="data.checked3" loading active-color="red" />
    </nut-cell>

    <h2>{{ translate('title4') }}</h2>
    <nut-cell>
      <nut-switch v-model="data.checked4" @change="change" />
    </nut-cell>

    <h2>{{ translate('title5') }}</h2>
    <nut-cell>
      <nut-switch :model-value="checkedAsync" :loading="loadingAsync" @change="changeAsync" />
    </nut-cell>

    <h2>{{ translate('title6') }}</h2>
    <nut-cell>
      <nut-switch v-model="data.checked6" active-color="blue" />
    </nut-cell>

    <h2>{{ translate('title7') }}</h2>
    <nut-cell>
      <nut-switch
        v-model="data.checked7"
        :active-text="translate('text1')"
        :inactive-text="translate('text2')"
        class="switch-demo1"
      />
    </nut-cell>

    <h2>{{ translate('title8') }}</h2>
    <nut-cell>
      <nut-switch v-model="data.checked8" loading>
        <template #icon>
          <Loading name="loading" />
        </template>
      </nut-switch>
    </nut-cell>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';
import NutSwitch from './index.vue';
import NutCell from '../cell/index.vue';
import { createComponent } from '@/packages/utils/create';
import { Loading } from '@nutui/icons-vue';
import { showToast } from '@/packages/nutui.vue';
const { translate } = createComponent('switch');
import { useTranslate } from '@/sites/assets/util/useTranslate';
const initTranslate = () =>
  useTranslate({
    'zh-CN': {
      basic: '基础用法',
      title1: '值为字符串',
      title2: '禁用状态',
      title3: '加载状态',
      title4: 'change 事件',
      title5: '异步控制',
      title6: '自定义颜色',
      title7: '支持文字',
      title8: '自定义加载图标',
      text1: '开',
      text2: '关'
    },
    'en-US': {
      basic: 'Basic Usage',
      title1: 'Value Is String',
      title2: 'Disabled',
      title3: 'Loading',
      title4: 'Change Event',
      title5: 'Async Control',
      title6: 'Custom Color',
      title7: 'Support Text',
      title8: 'Custom loading icon',
      text1: 'Open',
      text2: 'Closed'
    }
  });
initTranslate();
const data = reactive({
  checked1: true,
  checked2: true,
  checked3: true,
  checked4: true,
  checked6: true,
  checked7: true,
  checked8: true
});
const checkedAsync = ref(true);
const loadingAsync = ref(false);

// const checkedStr = ref('开');

const change = (value: boolean) => {
  showToast.text(`value：${value}`);
};

const changeAsync = (value: boolean) => {
  showToast.text(`after 2 second： ${value}`);
  loadingAsync.value = true;
  setTimeout(() => {
    checkedAsync.value = value;
    loadingAsync.value = false;
  }, 2000);
};
</script>
