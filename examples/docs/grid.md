## Grid 栅格

我们采用了 24 栅格系统，将区域进行 24 等分，和大部分组件库类似，我们也引入两个组件，row 和 col，row 表示行，col 在 row 之内使用

### 基础用法

::: demo

```html
<template>
  <yun-row>
    <yun-col span="12">col-12</yun-col>
    <yun-col span="12">col-12</yun-col>
  </yun-row>
  <br />
  <yun-row>
    <yun-col span="8">col-8</yun-col>
    <yun-col span="8">col-8</yun-col>
    <yun-col span="8">col-8</yun-col>
  </yun-row>
  <br />
  <yun-row>
    <yun-col span="6">col-6</yun-col>
    <yun-col span="6">col-6</yun-col>
    <yun-col span="6">col-6</yun-col>
    <yun-col span="6">col-6</yun-col>
  </yun-row>
</template>
```

:::

### 间隔

可以设置 gutter 间隔

::: demo

```html
<template>
  <yun-row :gutter="20" class="gutter">
    <yun-col span="6">
      <div>col-6</div>
    </yun-col>
    <yun-col span="6">
      <div>col-6</div>
    </yun-col>
    <yun-col span="6">
      <div>col-6</div>
    </yun-col>
    <yun-col span="6">
      <div>col-6</div>
    </yun-col>
  </yun-row>
</template>
```

:::

### flex 改变栅格顺序

::: demo

```html
<template>
  <yun-row type="flex">
    <yun-col span="6" order="4">1 | order-4</yun-col>
    <yun-col span="6" order="3">2 | order-3</yun-col>
    <yun-col span="6" order="2">3 | order-2</yun-col>
    <yun-col span="6" order="1">4 | order-1</yun-col>
  </yun-row>
</template>
```

:::

### 栅格顺序

通过设置 push 和 pull 来改变栅格的顺序。

::: demo

```html
<template>
  <yun-row>
    <yun-col span="14" push="10">col-14 | push="10"</yun-col>
    <yun-col span="10" pull="14">col-10 | pull="14"</yun-col>
  </yun-row>
</template>
```

:::

### 左右偏移

offset 可以设置偏移量

::: demo

```html
<template>
  <yun-row>
    <yun-col span="8">col-8</yun-col>
    <yun-col span="8" offset="8">col-8 | offset-8</yun-col>
  </yun-row>
  <br />
  <yun-row>
    <yun-col span="6" offset="8">col-6 | offset-8</yun-col>
    <yun-col span="6" offset="4">col-6 | offset-4</yun-col>
  </yun-row>
  <br />
  <yun-row>
    <yun-col span="12" offset="8">col-12 | offset-8</yun-col>
  </yun-row>
</template>
```

:::

### flex 布局

::: demo

```html
<template>
  <p>子元素向左排列</p>
  <yun-row type="flex" justify="start" class="code-row-bg">
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
  </yun-row>
  <p>子元素向右排列</p>
  <yun-row type="flex" justify="end" class="code-row-bg">
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
  </yun-row>
  <p>子元素居中排列</p>
  <yun-row type="flex" justify="center" class="code-row-bg">
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
  </yun-row>
  <p>子元素等宽排列</p>
  <yun-row type="flex" justify="space-between" class="code-row-bg">
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
  </yun-row>
  <p>子元素分散排列</p>
  <yun-row type="flex" justify="space-around" class="code-row-bg">
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
    <yun-col span="4">col-4</yun-col>
  </yun-row>
  <p>顶部对齐</p>
  <yun-row type="flex" justify="center" align="top" class="code-row-bg">
    <yun-col span="4"><p style="height: 80px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 30px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 100px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 60px">col-4</p></yun-col>
  </yun-row>
  <p>底部对齐</p>
  <yun-row type="flex" justify="center" align="bottom" class="code-row-bg">
    <yun-col span="4"><p style="height: 80px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 30px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 100px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 60px">col-4</p></yun-col>
  </yun-row>
  <p>居中对齐</p>
  <yun-row type="flex" justify="center" align="middle" class="code-row-bg">
    <yun-col span="4"><p style="height: 80px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 30px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 100px">col-4</p></yun-col>
    <yun-col span="4"><p style="height: 60px">col-4</p></yun-col>
  </yun-row>
</template>
```

:::

### 响应式布局

预设六个响应尺寸：xs sm md lg xl xxl，详见 API。

::: demo

```html
<template>
  <yun-row>
    <yun-col :xs="2" :sm="4" :md="6" :lg="8">yun-col</yun-col>
    <yun-col :xs="20" :sm="16" :md="12" :lg="8">yun-col</yun-col>
    <yun-col :xs="2" :sm="4" :md="6" :lg="8">yun-col</yun-col>
  </yun-row>
</template>
```

:::

### Row Props

| 参数       | 说明                         | 类型   | 可选值                                          | 默认值 |
| ---------- | ---------------------------- | ------ | ----------------------------------------------- | ------ |
| gutter     | 栅格间距，单位 px            | Number | —                                               | 0      |
| type       | 布局模式，在现代浏览器下有效 | String | flex 或不选                                     | —      |
| justify    | lex 布局下的水平排列方式     | String | —                                               | —      |
| align      | flex 布局下的垂直对齐方式    | String | start、end、center、space-around、space-between | —      |
| class-name | 自定义的 class 名称          | String | —                                               | —      |

### Col Props

| 参数       | 说明                                         | 类型            | 可选值 | 默认值 |
| ---------- | -------------------------------------------- | --------------- | ------ | ------ |
| span       | 栅格的占位格数 为 0 时，相当于 display:none  | Number/String   | 0~24   | -      |
| order      | 栅格的顺序 在 flex 布局模式下有效            | Number/String   | -      | -      |
| offset     | 栅格左侧偏移                                 | Number/String   | -      | -      |
| push       | 栅格向右移动格数                             | Number/String   | -      | -      |
| pull       | 栅格向左移动格数                             | Number/String   | -      | -      |
| class-name | 自定义的 class                               | String          | -      | -      |
| xs         | <576px 响应式栅格 响应式栅格                 | Number / Object | -      | -      |
| sm         | (≥576px < 768px)≥576px 响应式栅格 响应式栅格 | Number / Object | -      | -      |
| md         | (≥768px < 992px) 响应式栅格 响应式栅格       | Number / Object | -      | -      |
| lg         | (≥992px < 1200px) 响应式栅格 响应式栅格      | Number / Object | -      | -      |
| xl         | (≥1200px < 1600px) 响应式栅格 响应式栅格     | Number / Object | -      | -      |
| xxl        | ≥1600px 响应式栅格 响应式栅格                | Number / Object | -      | -      |