<template>
  <div class="demo">
    <nut-cell-group :title="translate('funUse')">
      <nut-cell :title="translate('basic')" @click="baseClick"></nut-cell>
      <nut-cell :title="translate('transparent')" @click="transparentClick"></nut-cell>
      <nut-cell :title="translate('html')" @click="htmlClick"></nut-cell>
      <nut-cell :title="translate('beforeClose')" @click="beforeCloseClick"></nut-cell>
      <nut-cell :title="translate('noTitle')" @click="noTitleClick"></nut-cell>
      <nut-cell :title="translate('tipDialog')" @click="tipsClick"></nut-cell>
      <nut-cell :title="translate('title')" @click="verticalClick"></nut-cell>
    </nut-cell-group>
    <nut-cell-group :title="translate('title1')">
      <nut-cell :title="translate('title1')" @click="componentClick"></nut-cell>
      <nut-dialog
        v-model:visible="visible"
        teleport="#app"
        :title="translate('title1')"
        :content="translate('content')"
      >
      </nut-dialog>
      <nut-cell :title="translate('title')" @click="componentvVrticalClick"></nut-cell>
      <nut-dialog
        v-model:visible="visible1"
        footer-direction="vertical"
        teleport="#app"
        :title="translate('title1')"
        :content="translate('content')"
      >
      </nut-dialog>
    </nut-cell-group>
    <nut-cell-group :title="translate('title2')">
      <nut-cell title="body element node" @click="teleportClick('body')"></nut-cell>
      <nut-cell title="#app element node" @click="teleportClick('#app')"></nut-cell>
      <nut-cell title="demo class element node" @click="teleportClick('.demo')"></nut-cell>
    </nut-cell-group>
  </div>
</template>
<script setup lang="ts">
import { createVNode, ref } from 'vue';
import NutDialog from './index.vue';
import { showDialog } from './index';
import NutCell from '../cell/index.vue';
import NutCellGroup from '../cellgroup/index.vue';
import { createComponent } from '@/packages/utils/create';
const { translate } = createComponent('dialog');
import { useTranslate } from '@/sites/assets/util/useTranslate';
const initTranslate = () =>
  useTranslate({
    'zh-CN': {
      funUse: '函数式调用',
      basic: '基础弹框',
      transparent: '透明弹框',
      html: '支持富文本 html',
      beforeClose: '异步关闭',
      noTitle: '无标题弹框',
      tipDialog: '提示弹框',
      tips: '提示',
      title: '底部按钮 垂直使用',
      title1: '标签式使用',
      title2: 'Teleport 使用，挂载到指定节点',
      content: '支持函数调用和组件调用两种方式。',
      content1: '支持底部按钮纵向排列。',
      content2: '打开开发者工具看一下 Elements Tab',
      content3: '我可以是一个自定义组件',
      content4: '点击确认后，1秒后关闭'
    },
    'en-US': {
      funUse: 'Function use',
      basic: 'Basic Usage',
      transparent: 'Transparent Dialog',
      html: 'Use html',
      beforeClose: 'Before Close',
      noTitle: 'No Title',
      tipDialog: 'Tips Dialog',
      tips: 'Tips',
      title: 'Bottom button vertical use',
      title1: 'Template use',
      title2: 'Teleport use, mount to the specified element node',
      content: 'Function call and template call are supported.',
      content1: 'Support vertical arrangement of bottom buttons.',
      content2: 'Open the developer tool and take a look at the Elements tab',
      content3: 'I can be a custom component',
      content4: 'Click confirm to close it in 1 second'
    }
  });
initTranslate();
const visible = ref(false);
const visible1 = ref(false);

const onCancel = () => {
  console.log('event cancel');
};
const onOk = () => {
  console.log('event ok');
};

const baseClick = (): void => {
  showDialog({
    title: translate('basic'),
    content: createVNode('span', { style: { color: 'red' } }, translate('content3')),
    onCancel,
    onOk
  });
};

const transparentClick = (): void => {
  showDialog({
    overlayStyle: { background: 'rgba(0,0,0,0)' },
    title: translate('transparent'),
    content: 'Content',
    onCancel,
    onOk
  });
};

const htmlClick = (): void => {
  showDialog({
    title: translate('html'),
    content:
      "<p style='color:red'>html</p><img src='https://m.360buyimg.com/babel/jfs/t1/164410/22/25162/93384/616eac6cE6c711350/0cac53c1b82e1b05.gif' />",
    onCancel,
    onOk
  });
};

const beforeCloseClick = (): void => {
  showDialog({
    title: translate('beforeClose'),
    content: translate('content4'),
    onCancel,
    onOk,
    beforeClose: (action: string) => {
      return new Promise((r) => {
        setTimeout(() => {
          r(action == 'ok');
        }, 1000);
      });
    }
  });
};

const noTitleClick = () => {
  showDialog({
    content: translate('noTitle'),
    onCancel,
    onOk
  });
};
const tipsClick = () => {
  showDialog({
    title: translate('tips'),
    content: translate('content'),
    noCancelBtn: true,
    onCancel,
    onOk
  });
};
const verticalClick = () => {
  showDialog({
    title: translate('tips'),
    content: translate('content1'),
    footerDirection: 'vertical',
    onCancel,
    onOk
  });
};

const componentClick = () => {
  visible.value = true;
};
const componentvVrticalClick = () => {
  visible1.value = true;
};

const teleportClick = (teleport: string) => {
  showDialog({
    teleport,
    title: 'teleport to ' + teleport,
    content: translate('content2'),
    noCancelBtn: true,
    onCancel
  });
};
</script>
