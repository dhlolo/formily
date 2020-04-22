# 理解表单布局

`MegaLayout` 是下一代的 **Formily** 表单布局，基于表单组件维度，到整体维度都有相应的设计标准指导。
查看这些设计了解更多：[单字段布局能力](https://img.alicdn.com/tfs/TB1N2xIC8r0gK0jSZFnXXbRRXXa-1090-876.png)，[静态布局场景](https://img.alicdn.com/tfs/TB1vwlFCYj1gK0jSZFuXXcrHpXa-1090-1231.png)，[响应式布局场景](https://img.alicdn.com/tfs/TB1qjRyC.H1gK0jSZSyXXXtlpXa-1090-1231.png)

下面会通过一些实际例子来理解有哪些能力：

## 单字段布局能力

### label 对齐方式

| 字段名     | 描述           | 类型                   | 默认值  |
| :--------- | :------------- | :--------------------- | :------ |
| labelAlign | label 对齐方式 | `left`, `right`, `top` | `right` |

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
    <Form>
      <h5>label右对齐（默认）</h5>
      <MegaLayout labelCol={4}>
        <FormItem name="alignLeft" title="标题" component={Select} />
      </MegaLayout>

      <h5>label左对齐</h5>
      <MegaLayout labelCol={4} labelAlign="left">
        <FormItem name="alignRight" title="标题" component={Select} />
      </MegaLayout>

      <h5>label在顶部</h5>
      <MegaLayout labelAlign="top">
        <FormItem name="alignTop" title="标题" component={Select} />
      </MegaLayout>
    </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

### full 表单组件是否撑满

| 字段名 | 描述             | 类型    | 默认值 |
| :----- | :--------------- | :------ | :----- |
| full   | 表单组件是否撑满 | boolean | false  |

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form >
        <h5>不撑满（默认）</h5>

        <MegaLayout labelCol={4}>
          <FormItem name="defaultFull" title="标题" component={Select} />
        </MegaLayout>

        <h5>撑满</h5>

        <MegaLayout labelCol={4} full>
          <FormItem name="full" title="标题" component={Select} />
        </MegaLayout>

        <h5>label在顶部，撑满</h5>

        <MegaLayout labelAlign="top" full>
          <FormItem name="fullTop" title="标题" component={Select} />
        </MegaLayout>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

### labelCol/wrapperCol 经典布局

| 字段名     | 描述             | 类型         | 默认值 |
| :--------- | :--------------- | :----------- | :----- |
| labelCol   | label 所占列数   | number(0-24) |        |
| wrapperCol | wrapper 所占列数 | number(0-24) |        |

`labelCol/wrapperCol` 布局与经典的栅格布局完全一致，一行总共 24 列，`label/wrapper` 按照比例分配。

> 为了更好的说明例子，下面所有例子都声明 `full=true`

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'
import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form >
        <h5>labelCol: undefined / wrapperCol: undefined </h5>

        <MegaLayout full>
          <FormItem name="lc1" title="标题" component={Select} />
        </MegaLayout>

        <h5>labelCol: 4 / wrapperCol: undefined </h5>

        <MegaLayout labelCol={4} full>
          <FormItem name="lc2" title="标题" component={Select} />
        </MegaLayout>

        <h5>labelCol: undefined / wrapperCol: 20 </h5>

        <MegaLayout wrapperCol={20} full>
          <FormItem name="lc3" title="标题" component={Select} />
        </MegaLayout>

        <h5>labelCol: 4 / wrapperCol: 20</h5>

        <MegaLayout labelCol={4} wrapperCol={20} full>
          <FormItem name="lc4" title="标题" component={Select} />
        </MegaLayout>

        <h5>labelCol: 12 / wrapperCol: 12</h5>

        <MegaLayout labelCol={12} wrapperCol={12} full>
          <FormItem name="lc5" title="标题" component={Select} />
        </MegaLayout>

        <h5>labelCol: 20 / wrapperCol: 4</h5>

        <MegaLayout labelCol={20} wrapperCol={4} full>
          <FormItem name="lc6" title="标题" component={Select} />
        </MegaLayout>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

### labelWidth/wrapperWidth 定宽布局

| 字段名       | 描述         | 类型   | 默认值 |
| :----------- | :----------- | :----- | :----- |
| labelWidth   | label 宽度   | number |        |
| wrapperWidth | wrapper 宽度 | number |        |

`labelWidth/wrapperWidth` 是经典的栅格比例布局的补充，`label/wrapper` 按照指定的宽度来渲染。

> 为了更好的说明例子，下面所有例子都声明 `full=true`

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'
import Printer from '@formily/printer'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form >
        <h5>labelWidth: undefined / wrapperWidth: undefined </h5>

        <MegaLayout full>
          <FormItem name="lw1" title="lw1" component={Select} />
        </MegaLayout>

        <h5>labelWidth: 200px / wrapperWidth: undefined </h5>

        <MegaLayout labelWidth={200} full>
          <FormItem name="lw2" title="lw2" component={Select} />
        </MegaLayout>

        <h5>labelWidth: undefined / wrapperWidth: 200px </h5>

        <MegaLayout wrapperWidth={200} full>
          <FormItem name="lw3" title="lw3" component={Select} />
        </MegaLayout>

        <h5>labelWidth: 200px / wrapperWidth: 400px</h5>

        <MegaLayout labelWidth={200} wrapperWidth={400} full>
          <FormItem name="lw4" title="lw4" component={Select} />
        </MegaLayout>

        <h5>labelWidth: 300px / wrapperWidth: 300px</h5>

        <MegaLayout labelWidth={300} wrapperWidth={300} full>
          <FormItem name="lw5" title="lw5" component={Select} />
        </MegaLayout>

        <h5>labelWidth: 400px / wrapperWidth: 200px</h5>

        <MegaLayout labelWidth={400} wrapperWidth={200} full>
          <FormItem name="lw6" title="lw6" component={Select} />
        </MegaLayout>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

### addonBefore/addonAfter/description 辅助文案

以下属性适用于 **MegaLayout**

| 字段名      | 描述                        | 类型 | 默认值 |
| :---------- | :-------------------------- | :--- | :----- |
| addonBefore  | MegaLayout 前辅助文案   | any  |        |
| addonAfter   | MegaLayout 后辅助文案   | any  |        |
| description | MegaLayout 底部辅助文案 | any  |        |

以下属性适用于 **MegaLayout 下的 FormItem**

| 字段名                      | 描述               | 类型 | 默认值 |
| :-------------------------- | :----------------- | :--- | :----- |
| ['mega-props'].addonBefore | 表单组件前辅助文案 | any  |        |
| ['mega-props'].addonAfter  | 表单组件后辅助文案 | any  |        |

`MegaLayout` 通过`addonBefore/addonAfter/description`，实现在各种位置需要插入辅助文案。

> 为了更好的说明例子，下面所有例子都声明 `full=true`

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  SchemaMarkupField as Field,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form >
        <h5>无label + 辅助文案</h5>

        <MegaLayout
          addonBefore="容器before"
          addonAfter="容器after"
          description="容器description"
          full
        >
          <FormItem name="addon1" title="组件标题" component={Select} />
        </MegaLayout>

        <h5>label + 辅助文案</h5>

        <MegaLayout
          label="容器标题"
          addonBefore="容器before"
          addonAfter="容器after"
          description="容器description"
          full
        >
          <FormItem name="addon2" title="组件标题" component={Select} />
        </MegaLayout>

        <h5>单纯表单字段（label + 辅助文案）</h5>

        <MegaLayout full>
          <FormItem
            name="itemAddon"
            title="组件标题"
            component={Select}
            mega-props={{
              addonBefore: '组件before',
              addonAfter: '组件after'
            }}
            description="组件description"
          />
        </MegaLayout>

        <h5>label + 辅助文案 + 表单字段（label + 辅助文案）</h5>

        <MegaLayout
          label="容器标题"
          addonBefore="容器before"
          addonAfter="容器after"
          description="容器description"
          full
        >
          <FormItem
            name="itemAddon"
            title="组件标题"
            component={Select}
            mega-props={{
              addonBefore: '组件before',
              addonAfter: '组件after'
            }}
            description="组件description"
          />
        </MegaLayout>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

# inline 行内布局

| 字段名 | 描述             | 类型    | 默认值 |
| :----- | :--------------- | :------ | :----- |
| inline | 是否启用行内布局 | boolean | false  |

> 为了更好的说明例子，下面所有例子都声明 `full=true`

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form >
        <h5>最简单的inline布局</h5>

        <MegaLayout inline>
          <FormItem name="is1" title="标题" component={Select} />
          <FormItem name="is2" title="标题" component={Select} />
          <FormItem name="is3" title="标题" component={Select} />
        </MegaLayout>

        <h5>inline + labelWidth: 120 + wrapperWidth: 200</h5>

        <MegaLayout inline labelWidth={120} wrapperWidth={200} full>
          <FormItem name="il2w2f1" title="标题" component={Select} />
          <FormItem name="il2w2f2" title="标题" component={Select} />
          <FormItem name="il2w2f3" title="标题" component={Select} />
        </MegaLayout>

        <h5>inline + labelAlign: top</h5>

        <MegaLayout inline labelAlign="top">
          <FormItem name="ilt1" title="标题" component={Select} />
          <FormItem name="ilt2" title="标题" component={Select} />
          <FormItem name="ilt3" title="标题" component={Select} />
        </MegaLayout>

        <h5>inline + labelAlign: top + labelWidth: 120 + wrapperWidth: 200</h5>

        <MegaLayout
          inline
          labelAlign="top"
          labelWidth={120}
          wrapperWidth={200}
          full
        >
          <FormItem name="iltl2w21" title="标题" component={Select} />
          <FormItem name="iltl2w22" title="标题" component={Select} />
          <FormItem name="iltl2w23" title="标题" component={Select} />
        </MegaLayout>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

# grid 栅格布局

### MegaLayout 属性

| 字段名  | 描述             | 类型    | 默认值 |
| :------ | :--------------- | :------ | :----- |
| grid    | 是否启用栅格布局 | boolean | false  |
| columns | 栅格布局总共列数 | number  | 3      |
| autoRow | 是否自动换行     | boolean | false  |

### MegaLayout 下 FormItem 的属性

| 字段名                | 描述     | 类型   | 默认值 |
| :-------------------- | :------- | :----- | :----- |
| ['mega-props'].span | 所占列数 | number | 1      |

通过 `CSS Grid Layout` 实现栅格布局，功能更加强大。

> 为了更好的说明例子，下面所有例子都声明 `full=true`

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form >
        <h5>最简单的grid栅格布局</h5>

        <MegaLayout grid full>
          <FormItem name="g1" title="标题1" component={Select} />
          <FormItem
            mega-props={{ span: 2 }}
            name="g2"
            title="标题2"
            component={Select}
          />
        </MegaLayout>

        <h5>grid + autoRow 自动换行</h5>

        <MegaLayout grid full autoRow>
          <FormItem
            mega-props={{ span: 2 }}
            name="ga1"
            title="标题1"
            component={Select}
          />
          <FormItem name="ga2" title="标题2" component={Select} />
          <FormItem name="ga3" title="标题3" component={Select} />
        </MegaLayout>

        <h5>grid + autoRow 自动换行 + labelWidth: 100</h5>

        <MegaLayout grid full autoRow labelWidth={100}>
          <FormItem
            mega-props={{ span: 2 }}
            name="gal1"
            title="标题1"
            component={Select}
          />
          <FormItem name="gal2" title="标题2" component={Select} />
          <FormItem name="gal3" title="标题3" component={Select} />
        </MegaLayout>

        <h5>grid + autoRow 自动换行 + label在顶部</h5>

        <MegaLayout grid full autoRow labelAlign="top">
          <FormItem
            mega-props={{ span: 2 }}
            name="galt1"
            title="标题1"
            component={Select}
          />
          <FormItem name="galt2" title="标题2" component={Select} />
          <FormItem name="galt3" title="标题3" component={Select} />
        </MegaLayout>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

# 响应式布局

`MegaLayout` 提供响应式栅格布局。默认使用 3 栏栅格布局，你只需要将子元素按顺序排布，指定子元素所占的比例（默认为 1，即 1/3），并且配合屏幕大小改变子元素占比，页面内容就可以根据自适应。

| 字段名                         | 描述                                                   | 类型   | 默认值    |
| :----------------------------- | :----------------------------------------------------- | :----- | :-------- |
| ['mega-props'].responsive.s  | 媒体查询断点，视口宽度 <=720px，响应式栅格             | Number | Column 值 |
| ['mega-props'].responsive.m  | 媒体查询断点，720px <= 视口宽度 <= 1200px ，响应式栅格 | Number | Column 值 |
| ['mega-props'].responsive.lg | 媒体查询断点，视口宽度 >=1200px，响应式栅格            | Number | Column 值 |

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form >
        <h5>嵌套栅格布局</h5>

        <MegaLayout
          labelAlign="top"
          grid
          full
          autoRow
          responsive={{ lg: 3, m: 2, s: 1 }}
        >
          <FormItem name="flngt1" title="字段1" component={Select} />
          <FormItem
            name="flngt2"
            mega-props={{ span: 2 }}
            title="字段2"
            component={Select}
          />
          <FormItem
            name="flngt3"
            mega-props={{ span: 2 }}
            title="字段3"
            component={Select}
          />
          <FormItem name="flngt4" title="字段4" component={Select} />
          <FormItem name="flngt5" title="字段5" component={Select} />

          <MegaLayout columns={3} span={2}>
            <FormItem name="flngtc6" title="字段6" component={Select} />
            <FormItem name="flngtc7" title="字段7" component={Select} />
            <FormItem name="flngtc8" title="字段8" component={Select} />
          </MegaLayout>

          <MegaLayout columns={2} span={3} id="xx">
            <FormItem name="flngtc9" title="字段9" component={Select} />
            <FormItem name="flngtc10" title="字段10" component={Select} />
            <MegaLayout columns={2} span={2}>
              <FormItem
                name="flngtc11"
                title="字段11"
                component={Select}
                mega-props={{ span: 2 }}
              />
              <MegaLayout columns={3} span={2}>
                <FormItem name="flngtc12" title="字段12" component={Select} />
                <FormItem
                  name="flngtc13"
                  title="字段13"
                  component={Select}
                  mega-props={{ span: 2 }}
                />
                <FormItem name="flngtc14" title="字段14" component={Select} />
                <FormItem name="flngtc15" title="字段15" component={Select} />
              </MegaLayout>
            </MegaLayout>
          </MegaLayout>
        </MegaLayout>

        <FormButtonGroup align="right">
          <Submit>提交</Submit>
          <Reset>重置</Reset>
        </FormButtonGroup>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

# 嵌套布局

`MegaLayout` 的属性会传递到下面的 **表单组件** 或 嵌套的 **MegaLayout**。

由于部分属性如 **labelCol** 等属性是父子组件共用的，约定只能影响子组件。因此需要更改 `MegaLayout` 自身时需要通过 **layoutProps** 来实现。

| 字段名      | 描述                                 | 类型                                                                                                   | 默认值 |
| :---------- | :----------------------------------- | :----------------------------------------------------------------------------------------------------- | :----- |
| layoutProps.labelCol | 改变自身布局属性, wrapper 比例 | number(0-24) |        |
| layoutProps.wrapperCol | 改变自身布局属性, label 比例 | number(0-24) |        |
| layoutProps.labelWidth | 改变自身布局属性, label 宽度 | number |        |
| layoutProps.wrapperWidth | 改变自身布局属性, wrapper 宽度 | number |        |



```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
    <Form>
      <MegaLayout labelCol={4}>
        <FormItem name="ndomain1" title="col4" component={Select} />
        <MegaLayout label="独立作用域" labelCol={6}>
          <FormItem name="ndomain2" title="col6" component={Select} />
        </MegaLayout>

        <MegaLayout
          label="修改MegaLayout本身"
          layoutProps={{ labelCol: 6 }}
        >
          <FormItem name="ndomain3" title="col4" component={Select} />
        </MegaLayout>
      </MegaLayout>
    </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

# 复杂嵌套布局

`MegaLayout` 强大之处在于能够处理复杂的嵌套，使得上述原子化的能力能够通过各种组合实现极其复杂的布局。

```jsx
import React, { useEffect } from 'react'
import ReactDOM from 'react-dom'
import {
  Form,
  FormItem,
  FormButtonGroup,
  createFormActions,
  Submit,
  Reset
} from '@formily/next' // 或者 @formily/next
import styled, { css } from 'styled-components'
import { MegaLayout, Input, Select } from '@formily/next-components'

import '@alifd/next/dist/next.css'

const App = () => {
  return (
      <Form>
        <MegaLayout labelCol={4}>
          <FormItem name="ff1" title="普通字段" component={Select} />

          <MegaLayout label="以下字段会撑满" full>
            <FormItem name="flf1" component={Select} />
            <FormItem name="flf2" component={Select} />
          </MegaLayout>

          <MegaLayout label="行内布局" inline>
            <FormItem name="fi1" component={Select} />
            <FormItem name="fi2" component={Select} />
          </MegaLayout>

          <MegaLayout label="栅格布局" grid>
            <FormItem name="fg1" component={Select} />
            <FormItem name="fg2" component={Select} />
            <FormItem name="fg3" component={Select} />
          </MegaLayout>

          <MegaLayout label="栅格布局 + 撑满(3列默认)" grid full>
            <FormItem name="ffg1" component={Select} />
            <FormItem name="ffg2" component={Select} />
            <FormItem name="ffg3" component={Select} />
          </MegaLayout>

          <MegaLayout label="栅格布局 + 撑满(2列)" grid columns={2} full>
            <FormItem name="ffcg1" component={Select} />
            <FormItem name="ffcg2" component={Select} />
          </MegaLayout>

          <MegaLayout
            label="栅格 + 自动换行 + 自定义比例"
            autoRow
            grid
            full
          >
            <FormItem name="fag1" component={Select} />
            <FormItem
              name="fag2"
              mega-props={{ span: 2 }}
              component={Select}
            />
            <FormItem name="fag3" component={Select} />
          </MegaLayout>

          <FormItem
            title="辅助文案"
            mega-props={{
              addonBefore: 'before',
              addonAfter: 'after'
            }}
            description="description"
            name="fad1"
            component={Select}
          />

          <FormItem
            full
            title="辅助文案 + full"
            mega-props={{
              addonBefore: 'before',
              addonAfter: 'after'
            }}
            description="description"
            name="fad2"
            component={Select}
          />

          <MegaLayout label="行内布局 + 辅助文案" inline>
            <FormItem
              title="辅助文案"
              mega-props={{
                addonBefore: 'before',
                addonAfter: 'after'
              }}
              description="description"
              name="fiad1"
              component={Select}
            />
            <FormItem
              title="辅助文案"
              mega-props={{
                addonBefore: 'before',
                addonAfter: 'after'
              }}
              description="description"
              name="fiad2"
              component={Select}
            />
          </MegaLayout>

          <MegaLayout
            label="栅格 + 辅助文案(3列默认)"
            grid
            full
            labelCol={null}
          >
            <FormItem
              title="辅助文案"
              mega-props={{
                addonBefore: 'before',
                addonAfter: 'after'
              }}
              description="description"
              name="fgiad1"
              component={Select}
            />
            <FormItem
              title="辅助文案"
              mega-props={{
                addonBefore: 'before',
                addonAfter: 'after'
              }}
              description="description"
              name="fgiad2"
              component={Select}
            />
            <FormItem
              title="辅助文案"
              mega-props={{
                addonBefore: 'before',
                addonAfter: 'after'
              }}
              description="description"
              name="fgiad3"
              component={Select}
            />
          </MegaLayout>

          <MegaLayout
            label="栅格 + 辅助文案(2列)"
            grid
            full
            columns={2}
            labelCol={null}
          >
            <FormItem
              title="辅助文案"
              mega-props={{
                addonBefore: 'before',
                addonAfter: 'after'
              }}
              description="description"
              name="fcgiad1"
              component={Select}
            />
            <FormItem
              title="辅助文案"
              mega-props={{
                addonBefore: 'before',
                addonAfter: 'after'
              }}
              description="description"
              name="fcgiad2"
              component={Select}
            />
          </MegaLayout>

          <MegaLayout
            label="嵌套栅格布局"
            autoRow
            grid
            full
            labelCol={null}
          >
            <FormItem name="fnestg1" title="字段1" component={Select} />
            <FormItem
              name="fnestg2"
              mega-props={{ span: 2 }}
              title="字段2"
              component={Select}
            />
            <FormItem
              name="fnestg3"
              mega-props={{ span: 2 }}
              title="字段3"
              component={Select}
            />
            <FormItem name="fnestg4" title="字段4" component={Select} />
            <FormItem name="fnestg5" title="字段5" component={Select} />

            <MegaLayout columns={3} span={2}>
              <FormItem name="fnestg6" title="字段1" component={Select} />
              <FormItem name="fnestg7" title="字段2" component={Select} />
              <FormItem name="fnestg8" title="字段3" component={Select} />
            </MegaLayout>
          </MegaLayout>

          <MegaLayout label="连续嵌套布局" labelCol={null}>
            <FormItem name="confns1" title="字段1" component={Select} />

            <MegaLayout inline label="嵌套行内">
              <FormItem name="confns2" title="字段2" component={Select} />
              <FormItem name="confns3" title="字段3" component={Select} />
              <FormItem name="confns4" title="字段4" component={Select} />
            </MegaLayout>

            <MegaLayout grid label="嵌套栅格" full autoRow>
              <FormItem name="confngt1" title="字段1" component={Select} />
              <FormItem
                name="confngt2"
                mega-props={{ span: 2 }}
                title="字段2"
                component={Select}
              />
              <FormItem
                name="confngt3"
                mega-props={{ span: 2 }}
                title="字段3"
                component={Select}
              />
              <FormItem name="confngt4" title="字段4" component={Select} />
              <FormItem name="confngt5" title="字段5" component={Select} />

              <MegaLayout columns={3} span={2}>
                <FormItem name="confngtc1" title="字段1" component={Select} />
                <FormItem name="confngtc2" title="字段2" component={Select} />
                <FormItem name="confngtc3" title="字段3" component={Select} />
              </MegaLayout>
            </MegaLayout>
          </MegaLayout>
        </MegaLayout>

        <FormButtonGroup offset={6}>
          <Submit>提交</Submit>
          <Reset>重置</Reset>
        </FormButtonGroup>
      </Form>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```