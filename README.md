# vxe-table

[![npm version](https://img.shields.io/npm/v/vxe-table.svg?style=flat-square)](https://www.npmjs.org/package/vxe-table)
[![npm downloads](https://img.shields.io/npm/dm/vxe-table.svg?style=flat-square)](http://npm-stat.com/charts.html?package=vxe-table)
[![gzip size: JS](http://img.badgesize.io/https://unpkg.com/vxe-table/lib/index.umd.min.js?compression=gzip&label=gzip%20size:%20JS)](http://img.badgesize.io/https://unpkg.com/vxe-table/lib/index.umd.min.js?compression=gzip&label=gzip%20size:%20JS)
[![gzip size: CSS](http://img.badgesize.io/https://unpkg.com/vxe-table/lib/index.css?compression=gzip&label=gzip%20size:%20CSS)](http://img.badgesize.io/https://unpkg.com/vxe-table/lib/index.css?compression=gzip&label=gzip%20size:%20CSS)
[![npm license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/xuliangzhan/vxe-table/blob/master/LICENSE)

A very powerful Vue table component.

## Features

* 基础
* 尺寸
* 斑马线条纹
* 带边框
* 单元格样式
* 列宽拖动
* 流体高度
* 固定表头
* 固定列
* 固定表头和列
* 表头分组
* 序号
* 单选
* 多选
* 排序
* 筛选
* 合并行或列
* 表尾合计
* 导出 CVS
* 自定义列
* 加载中
* 格式化内容
* 自定义模板
* 快捷菜单
* 滚动渲染
* 展开行
* 可编辑表格
* Excel 表格

## Docs

[查看文档](https://xuliangzhan.github.io/vxe-table/)

## Installing

```shell
npm install xe-utils vxe-table
```

Get on [unpkg](https://unpkg.com/vxe-table/) and [cdnjs](https://cdn.jsdelivr.net/npm/vxe-table/)

```HTML
<!-- 引入样式 -->
<link rel="stylesheet" href="https://unpkg.com/vxe-table/lib/index.css">
<!-- 引入脚本 -->
<script src="https://unpkg.com/xe-utils"></script>
<script src="https://unpkg.com/vxe-table"></script>
```

```javascript
import Vue from 'vue'
import VXETable from 'vxe-table'
import 'vxe-table/lib/index.css'

Vue.use(VXETable)
```

## Global config

```javascript
import Vue from 'vue'
import VXETable from 'vxe-table'
import 'vxe-table/lib/index.css'

Vue.use(VXETable, {
  // 默认尺寸
  size: 'small',
  // 全局快捷菜单
  contextMenu: null,
  // 优化配置项
  optimized: {
    scroll: {
      gt: 500,
      oSize: 30,
      rSize: 120
    }
  }
})
```

## Theme

```javascript
// Case 1. 引入默认的样式
import 'vxe-table/lib/index.css'

// Case 2. 自定义表格颜色（复制 style/variable.scss 到自己的项目中，修改颜色变量，然后引入）
// @import 'assets/style/vxe-table/variable.scss';
// @import 'vxe-table/style/table.scss';

// Case 3. 重写主题样式（复制 style/table.scss 到项目中自行修改）
// @import 'assets/style/vxe-table/variable.scss';
// @import 'assets/style/vxe-table/table.scss';
```

## I18n

```javascript
import Vue from 'vue'
import VueI18n from 'vxe-i18n'
import VXETable from 'vxe-table'
import zhCNLocat from 'vxe-table/lib/locale/lang/zh_CN'
import enLocat from 'vxe-table/lib/locale/lang/zh_CN'

const messages = {
  zh_CN: {
    ...zhCNLocat
  },
  en: {
    ...enLocat
  }
}

const i18n = new VueI18n({
  locale: 'zh_CN',
  messages,
})

Vue.use(VXETable, {
  i18n: (key, value) => i18n.t(key, value)
})

new Vue({ i18n }).$mount('#app')
```

## API

### Table

```html
<vxe-table :data.sync="tableData">
  <vxe-table-column type="selection" width="60"></vxe-table-column>
  <vxe-table-column prop="name" label="Name"></vxe-table-column>
  <vxe-table-column prop="address" label="Address"></vxe-table-column>
</vxe-table>
```

#### Table Attributes

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|------|-----|------|-----|
| data | 显示的数据 | Array | — | — |
| customs | 初始化绑定动态列 | Array | — | — |
| height | 表格的高度 | Number | — | — |
| maxHeight | 表格的最大高度 | Number | — | — |
| resizable | 是否允许拖动列宽调整大小 | Boolean | — | false |
| stripe | 是否带有斑马纹 | Boolean | — | false |
| border | 是否带有纵向边框 | Boolean | — | false |
| size | 表格的尺寸 | String | medium / small / mini | — |
| fit | 列的宽度是否自撑开 | Boolean | — | true |
| loading | 表格是否加载中 | Boolean | — | false |
| show-header | 是否显示表头 | Boolean | — | true |
| highlight-current-row | 是否要高亮当前选中行 | Boolean | — | false |
| highlight-hover-row | 鼠标移到行是否要高亮显示 | Boolean | — | false |
| row-class-name | 给行附加 className，也可以是函数 Function({row, rowIndex, data}) | String/Function | — | — |
| cell-class-name | 给单元格附加 className，也可以是函数 Function({row, rowIndex, column, columnIndex, data}) | String/Function | — | — |
| header-row-class-name | 给表头的行附加 className，也可以是函数 Function({rowIndex}) | String/Function | — | — |
| header-cell-class-name | 给表头的单元格附加 className，也可以是函数 Function({rowIndex, column, columnIndex}) | String/Function | — | — |
| footer-row-class-name | 给表尾的行附加 className，也可以是函数 Function({rowIndex}) | String/Function | — | — |
| footer-cell-class-name | 给表尾的单元格附加 className，也可以是函数 Function({rowIndex, column, columnIndex}) | String/Function | — | — |
| show-footer | 是否显示表尾合计 | Boolean | — | — |
| footer-method | 表尾合计的计算方法 Function({columns, data}) | Function | — | — |
| span-method | 合并行或列，该函数 Function({row, rowIndex, column, columnIndex, data}) 返回计算后的值 | Object | — | { rowspan: 1, colspan: 1} |
| row-key | 行数据的 Key | String | — | — |
| context-menu | 快捷菜单配置项 | Object | — | [{header, body, footer}](#context-menu-快捷菜单配置项说明配合-context-menu-link-事件使用) |
| mouse-config | 鼠标配置项 | Object | — | [options](#mouse-config-鼠标相关配置项说明) |
| Keyboard-config | 按键配置项 | Object | — | [options](#Keyboard-config-键盘相关配置项说明) |
| edit-config | 可编辑配置项 | Object | — | [options](#edit-config-可编辑配置项说明) |
| edit-rules | 校验规则配置项 | Object | — | [options](#edit-rules-校验规则配置项说明) |
| optimized | 优化配置项 | Object/Boolean | — | [options](#optimized-优化配置项说明) |
| selectEditMethod | 只对 Keyboard-config={isEdit: true} 有效，用于重写选中编辑处理逻辑，该函数 Function({row, rowIndex, column, columnIndex, cell}, event) 可以返回 false 来阻止默认行为 | Function | — | — |

##### context-menu 快捷菜单配置项说明（配合 context-menu-link 事件使用）

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| disabled | 是否禁用表格头部右键 | Boolean | — | — |
| options | 表格头部菜单配置 | Array | — | { code, name, prefixIcon, suffixIcon, disabled } |
| visibleMethod | 该函数 Function({row, rowIndex, column, columnIndex}, event) 的返回值用来决定是否允许显示右键菜单 | Function | — | — |

###### context-menu 快捷键说明

| 属性 | 描述 |
|------|------|
| Arrow Up ↑ | 移动到上一个菜单选项 |
| Arrow Down ↓ | 移动到下一个菜单选项 |
| Arrow Down → | 打开右侧的二级菜单 |
| Enter | 选中当前菜单选项 |
| Spacebar | 选中当前菜单选项 |

##### optimized 优化配置项说明

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| animat | 表格动画效果开关（关闭后视觉效果更快） | Boolean | — | true |
| overflow | 设置所有行不允许换行（设置后对于固定列能大幅提升性能） | String | ellipsis / title / tooltip | — |
| scroll | 滚动渲染配置 | Object | — | {gt: 500, size: 100} |

##### mouse-config 鼠标相关配置项说明

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| selected | 开启左键选中功能 | Boolean | — | false |
| checked | 开启鼠标移动单元格批量选中功能 | Boolean | — | false |

##### keyboard-config 键盘相关配置项说明

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| isArrow | 开启方向键功能 | Boolean | — | false |
| isTab | 开启 Tab 键功能 | Boolean | — | false |
| isCut | 开启复制粘贴功能 | Boolean | — | false |
| isEdit | 开启任意键进入编辑（功能键除外） | Boolean | — | false |

###### keyboard-config 快捷键说明

| 属性 | 描述 |
|------|------|
| Arrow Up ↑ | 移动到当前活动单元格上面的单元格 |
| Arrow Down ↓ | 移动到当前活动单元格下面的单元格 |
| Arrow Left ← | 移动到当前活动单元格左边的单元格 |
| Arrow Right → | 移动到当前活动单元格右边的单元格 |
| Tab | 移动到当前选中或活动单元格的右侧单元格，如果到最后一列且存在下一行，则从下一行开始移动 |
| Enter | 取消编辑并移动到当前活动单元格下面的单元格 |
| Delete | 清空内容 |
| Backspace | 清空内容并激活选中单元格为编辑状态 |
| F2 | 激活单元格编辑 |
| Esc | 取消单元格编辑 |
| Ctrl + C | 复制选中的单元格内容 |
| Ctrl + X | 剪贴选中的单元格内容 |
| Ctrl + V | 粘贴选中的单元格内容 |
| Ctrl + A | 选中所有单元格 |

##### edit-config 可编辑配置项说明

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| trigger | 触发方式 | String | manual（手动触发方式，只能用于 mode=row） / click（点击触发编辑） / dblclick（双击触发编辑） | click |
| mode | 编辑模式 | String | cell（单元格编辑模式） / row（行编辑模式） | cell |
| showIcon | 是否显示列头编辑图标 | Boolean | — | true |
| showStatus | 是否显示单元格值的修改状态 | Boolean | — | false |

##### edit-rules 校验规则配置项说明

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| required | 是否必填 | Boolean | — | — |
| min  | 校验值最小长度（如果 type=number 则比较值大小） | Number | — | — |
| max  | 校验值最大长度（如果 type=number 则比较值大小） | Number | — | — |
| type | 类型校验 | String | number / string | string |
| pattern | 正则校验 | RegExp | — | — |
| validator  | 自定义校验方法 | Function(rule, value, callback) | — | — |
| trigger  | 触发校验方式 | String | blur / change | change |

#### Table Events

| 事件名 | 说明 | 参数 |
|------|------|-----|
| select-all | 只对 type=selection 有效，当手动勾选全选时触发的事件 | {selection,checked},event |
| select-change | 只对 type=selection/radio 有效，当手动勾选时触发的事件 | {selection,checked,row,column},event |
| cell-click | 当某个单元格被点击时会触发该事件 | {row,rowIndex,column,columnIndex,cell},event |
| cell-dblclick | 当某个单元格被双击时会触发该事件 | {row,rowIndex,column,columnIndex,cell},event |
| context-menu-link | 当点击上下文菜单后触发 | menu,event |
| edit-disabled | 当点击后单元格如果是禁用状态时会触发该事件 | {row,rowIndex,column,columnIndex,cell},event |

#### Table Methods

| 方法名 | 描述 | 参数 |
|------|------|-----|
| reload | 初始化数据 | data |
| insert | 从第一行新增一行新数据 | record |
| insertAt | 第二个参数 row 从指定位置新增一条数据； null 从第一行新增一行新数据；-1 从最后新增一条数据 | record,row |
| revert | 还原更改，还原指定行 row 或者整个表格的数据 | row?rows?,prop? |
| remove | 删除指定行数据，指定 row 或 [row, ...] 删除多条数据 | rows |
| getRecords | 获取表格数据 | rowIndex? |
| clearSelectRow | 用于单选表格，清空用户的选择 | — |
| setCurrentRow | 用于单选表格，设置某一行为选中状态，如果第二个参数为空，则会取消目前高亮行的选中状态 | row? |
| clearSelection | 用于多选表格，清空用户的选择 | — |
| toggleRowSelection | 用于多选表格，切换某一行的选中状态，第二个参数则是设置这一行选中与否 | row,checked |
| toggleAllSelection | 用于多选表格，切换所有行的选中状态 | — |
| clearSort | 用于清空排序条件，数据会恢复成未排序的状态 | — |
| clearFilter | 用于清空筛选条件，数据会恢复成未筛选的状态 | — |
| setActiveRow | 只对 mode=cell 有效，激活行编辑 | row |
| setActiveCell | 只对 mode=row 有效，激活单元格编辑 | row,prop |
| setSelectCell | 只对 trigger!=manual 有效，选中单元格 | row,prop |
| computeWidth | 重新计算并更新列宽 | — |
| isScrollLoad | 判断是否启用了滚动渲染 | — |
| exportCsv| 将表格数据导出为 .csv 文件，说明：支持IE9+、Edge、Chrome、Firefox 等常用浏览器。IE11以下可能存在中文乱码问题，部分浏览器需要手动修改后缀名为 .csv | [options](#exportcsv-参数说明) |

##### exportCsv 参数说明

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| filename | 文件名 | String | — | table.csv |
| original | 是否导出源数据 | Boolean | — | false |
| isHeader | 是否显示表头 | Boolean | — | false |
| download | 是否马上下载，如果设置为 false 则通过返回结果为内容的 Promise | Boolean | — | true |
| data | 自定义数据 | Array | — | — |
| columns | 自定义列 | Array | — | — |
| columnFilterMethod | 列过滤方法，该函数 Function(column,columnIndex) 的返回值用来决定该列是否导出 | Function | — | — |
| dataFilterMethod | 数据过滤方法，该函数 Function(row,rowIndex) 的返回值用来决定该数据是否导出 | Function | — | — |

### Table-column

```html
<vxe-table-column prop="name" label="Name"></vxe-table-column>
```

#### Table-column Attributes 参数

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|------|-----|------|-----|
| type | 列的类型 | String | index / selection / radio / expand | — |
| edit-render | 列编辑配置项 | Object/Boolean | — | [options](#edit-render-配置项说明) |
| prop | 列属性 | String | — | — |
| label | 列标题 | String | — | — |
| width | 列宽度 | String | — | — |
| min-width | 最小列宽度，把剩余宽度按比例分配 | String | — | — |
| fixed | 将列固定在左侧或者右侧 | String | — | left |
| align | 列对其方式 | String | — | left |
| header-align | 表头对齐方式 | String | — | — |
| ellipsis | 当内容过长时显示为省略号 | Boolean | — | false |
| show-overflow-title | 当内容过长显示为省略号和原生的 title 显示内容 | Boolean | — | false |
| show-overflow-tooltip | 当内容过长显示为省略号并用 tooltip 显示完整内容 | Boolean | — | false |
| formatter | 格式化显示内容 Function({cellValue, row, rowIndex, column, columnIndex}) | Function | — | — |
| index-method | 只对 type=index 有效，自定义索引方法 Function({row, rowIndex, column, columnIndex}) | Function | — | — |
| sortable | 是否允许列排序，如果是服务端排序需要设置为custom | Boolean | — | — |
| sortBy | 只对 sortable 有效，自定义排序的属性 | String/Array | — | — |
| filters | 配置筛选条件数组 | Array | — | — |
| filter-multiple | 只对 filters 有效，筛选是否允许多选 | Boolean | — | true |
| filter-method | 只对 filters 有效，自定义筛选方法 Function({value, row, column}) | Function | — | — |
| column-key | 列的 key | String/Number | — | — |

##### edit-render 配置项说明

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
|------|------|-----|-----|-----|
| type | 渲染类型 | String | default（组件触发后可视） / visible（组件一直可视） | default |
| name | 渲染的组件名 | String | input / textarea | input |

#### Table-column Scoped Slot

| name | 说明 |
|------|------|
| — | 自定义显示内容，参数为 { row, rowIndex, column, columnIndex, fixed, isHidden } |
| header | 自定义表头的内容，参数为 { column, columnIndex, fixed, isHidden } |
| edit | 自定义可编辑组件模板，参数为 { column, columnIndex, fixed, isHidden } |

## Example

```html
<template>
  <div>
    <button @click="$refs.vTable.exportCsv()">Export.cvs</button>
    <vxe-table ref="vTable" :data.sync="tableData">
      <vxe-table-column type="index" width="60"></vxe-table-column>
      <vxe-table-column prop="name" label="Name"></vxe-table-column>
      <vxe-table-column prop="sex" label="Sex"></vxe-table-column>
      <vxe-table-column prop="address" label="Address"></vxe-table-column>
    </vxe-table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tableData: [
        {
          id: 10001,
          checked: false,
          name: 'test1',
          role: 'developer',
          sex: 'Man',
          date: '2019-05-01',
          time: 1556677810888,
          region: 'ShenZhen',
          address: 'address abc123'
        }
      ]
    }
  }
}
</script>
```

## License

Copyright (c) 2019-present, Xu Liangzhan