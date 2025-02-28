# Steps

### Intro

Split and display the steps of a process, guide users to complete tasks according to the process, or show users the current status.

### Install

```js
import { createApp } from 'vue';
import { Steps, Step } from '@nutui/nutui';

const app = createApp();
app.use(Steps);
app.use(Step);
```

### Basic Usage

:::demo

```vue
<template>
  <nut-steps :current="current1" @click-step="handleClickStep">
    <nut-step title="Step One">
      1
      <template #title>Step One</template>
    </nut-step>
    <nut-step title="Not started">2</nut-step>
    <nut-step title="Not started">3</nut-step>
  </nut-steps>
</template>
<script setup>
import { ref } from 'vue';
const current1 = ref(1);
const handleClickStep = (index) => {
  console.log(index);
};
</script>
```

:::

### Basic Usage(Dot)

:::demo

```vue
<template>
  <nut-steps :current="current2" progress-dot>
    <nut-step></nut-step>
    <nut-step></nut-step>
    <nut-step></nut-step>
  </nut-steps>
  <div class="steps-button">
    <nut-button size="mini" type="primary" @click="handleStep('current2')">{{ translate('next') }}</nut-button>
  </div>
</template>
<script setup>
import { ref } from 'vue';
const curren2 = ref(1);
const handleClickStep = (index) => {
  console.log(index);
};
</script>
```

:::

### Title and description information

:::demo

```vue
<template>
  <nut-steps :current="current2">
    <nut-step title="Completed" content="Step description">1</nut-step>
    <nut-step title="In progress" content="Step description">2</nut-step>
    <nut-step title="Not started" content="Step description">3</nut-step>
  </nut-steps>
</template>
<script setup>
import { ref } from 'vue';
const curren2 = ref(1);
</script>
```

:::

### Custom icon

:::demo

```vue
<template>
  <nut-steps current="1">
    <nut-step title="Completed">
      <template #icon><Service /></template>
    </nut-step>
    <nut-step title="In progress">
      <template #icon><People /></template>
    </nut-step>
    <nut-step title="Not started">
      <template #icon><Location2 /></template>
    </nut-step>
  </nut-steps>
</template>
<script setup>
import { Service, People, Location2 } from '@nutui/icons-vue';
</script>
```

:::

### Vertical step bar

:::demo

```vue
<template>
  <nut-steps direction="vertical" current="2">
    <nut-step title="Completed" content="Your order has been packaged and the goods have been delivered">1</nut-step>
    <nut-step title="In progress" content="Your order is in transit">2</nut-step>
    <nut-step
      title="Not started"
      content="The receiving address is Jingdong building, yard 18, Kechuang 11th Street, Beijing Economic and Technological Development Zone"
      >3</nut-step
    >
  </nut-steps>
</template>
```

:::

### Point step and vertical direction

:::demo

```vue
<template>
  <nut-steps direction="vertical" progress-dot current="2">
    <nut-step title="Completed" content="Your order has been packaged and the goods have been delivered">1</nut-step>
    <nut-step title="In progress" content="Your order is in transit">2</nut-step>
    <nut-step title="Not started">
      3
      <template #content>
        <p>The receiving address is：</p>
        <p>Jingdong building, yard 18, Kechuang 11th Street, Beijing Economic and Technological Development Zone</p>
      </template>
    </nut-step>
  </nut-steps>
</template>
```

:::

## API

### Steps Props

| Attribute    | Description                             | Type             | Default      |
| ------------ | --------------------------------------- | ---------------- | ------------ |
| direction    | Show direction，`horizontal`,`vertical` | string           | `horizontal` |
| current      | Current step                            | number \| string | `0`          |
| progress-dot | Dot step bar                            | boolean          | `false`      |

### Steps Events

| Event      | Description                                             | Arguments     |
| ---------- | ------------------------------------------------------- | ------------- |
| click-step | Triggered when the title or icon of the step is clicked | index: number |

### Step Props

| Attribute | Description                                                   | Type   | Default            |
| --------- | ------------------------------------------------------------- | ------ | ------------------ |
| title     | Title of the process step                                     | string | `Step`             |
| content   | Descriptive text of process steps (supporting HTML structure) | String | `Step description` |

### Step Slots

| Name    | Description  |
| ------- | ------------ |
| title   | Step title   |
| content | Step content |
| icon    | Step icon    |

## Theming

### CSS Variables

The component provides the following CSS variables, which can be used to customize styles. Please refer to [ConfigProvider component](#/en-US/component/configprovider).

| Name                                  | Default Value              |
| ------------------------------------- | -------------------------- |
| --nut-steps-base-icon-width           | _25px_                     |
| --nut-steps-base-icon-height          | _25px_                     |
| --nut-steps-base-icon-line-height     | _25px_                     |
| --nut-steps-base-icon-font-size       | _13px_                     |
| --nut-steps-base-title-font-size      | _14px_                     |
| --nut-steps-base-line-color           | _#909ca4_                  |
| --nut-steps-base-title-color          | _#909ca4_                  |
| --nut-steps-base-title-margin-bottom  | _10px_                     |
| --nut-steps-base-content-font-size    | _14px_                     |
| --nut-steps-base-content-color        | _#666_                     |
| --nut-steps-wait-icon-bg-color        | _#959fb1_                  |
| --nut-steps-wait-icon-text-color      | _var(--nut-white)_         |
| --nut-steps-wait-icon-color           | _var(--nut-white)_         |
| --nut-steps-wait-head-color           | _#909ca4_                  |
| --nut-steps-wait-head-border-color    | _#909ca4_                  |
| --nut-steps-wait-content-color        | _#909ca4_                  |
| --nut-steps-finish-head-color         | _var(--nut-primary-color)_ |
| --nut-steps-finish-head-border-color  | _var(--nut-primary-color)_ |
| --nut-steps-finish-title-color        | _var(--nut-primary-color)_ |
| --nut-steps-finish-line-background    | _var(--nut-primary-color)_ |
| --nut-steps-finish-icon-text-color    | _var(--nut-white)_         |
| --nut-steps-process-head-color        | _var(--nut-white)_         |
| --nut-steps-process-head-border-color | _var(--nut-primary-color)_ |
| --nut-steps-process-title-color       | _var(--nut-primary-color)_ |
| --nut-steps-process-icon-text-color   | _var(--nut-primary-color)_ |
