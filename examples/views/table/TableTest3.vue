<template>
  <div>
    <vxe-toolbar ref="toolbarRef" print export import custom></vxe-toolbar>

    <vxe-table
      border
      stripe
      resizable
      highlight-hover-row
      height="400"
      ref="tableRef"
      id="aaaa"
      :row-config="rowConfig"
      :column-config="{useKey: true}"
      :column-drag-config="{isCrossDrag:true,isToChildDrag:true,isSelfToChildDrag:true}"
      :resizable-config="resizableConfig"
      :print-config="{}"
      :import-config="{}"
      :export-config="{}"
      :custom-config="{mode: 'popup',immediate: false}"
      :loading="demo1.loading"
      :expand-config="{iconOpen: 'vxe-icon-question-circle-fill', iconClose: 'vxe-icon-question-circle-fill'}"
      :checkbox-config="{labelField: 'id', highlight: true, range: true}"
      :data="demo1.tableData">
      <vxe-column field="seq" type="seq" width="60" row-resize></vxe-column>
      <vxe-column field="checkbox" type="checkbox" title="ID" width="140"></vxe-column>
      <vxe-colgroup title="分组1" field="g1">
        <vxe-column type="expand" field="role" title="Role">
          <template #content="{ row }">
            <div>{{ row.name }}</div>
          </template>
        </vxe-column>
        <vxe-column field="name" title="Name" sortable></vxe-column>
      </vxe-colgroup>
      <vxe-column field="Sex222" title="<span style='color:red;'>Sex222</span>" type="html"></vxe-column>
      <vxe-column field="Sex1111" title="<span style='color:red;'>Sex1111</span>" type="html" :visible="false"></vxe-column>
      <vxe-column field="sex" title="Sex" :filters="demo1.sexList" :filter-multiple="false" :formatter="formatterSex"></vxe-column>
      <vxe-column
        field="age"
        title="Age"
        sortable
        :filters="demo1.ageOptions"
        :filter-method="filterAgeMethod"></vxe-column>
      <vxe-column field="address" title="Address" show-overflow></vxe-column>
    </vxe-table>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref, reactive, nextTick } from 'vue'
import { VxeColumnPropTypes, VxeTableInstance, VxeToolbarInstance, VxeTablePropTypes } from '../../../types'

interface RowVO {
  [key: string]: any
}

const tableRef = ref<VxeTableInstance<RowVO>>()
const toolbarRef = ref<VxeToolbarInstance>()

const rowConfig = reactive<VxeTablePropTypes.RowConfig>({
  useKey: true,
  resizable: true
})

const resizableConfig = reactive<VxeTablePropTypes.ResizableConfig>({
  isAllColumnDrag: true,
  isAllRowDrag: true,
  isDblclickAutoHeight: true
})

const demo1 = reactive({
  loading: false,
  tableData: [] as any[],
  sexList: [
    { label: '女', value: '0' },
    { label: '男', value: '1' }
  ],
  ageOptions: [
    { label: '大于16岁', value: 16 },
    { label: '大于26岁', value: 26 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 },
    { label: '大于30岁', value: 30 }
  ]
})

const formatterSex: VxeColumnPropTypes.Formatter = ({ cellValue }) => {
  const item = demo1.sexList.find(item => item.value === cellValue)
  return item ? item.label : ''
}

const filterAgeMethod: VxeColumnPropTypes.FilterMethod = ({ value, row }) => {
  return row.age >= value
}

onMounted(() => {
  demo1.loading = true
  setTimeout(() => {
    demo1.tableData = [
      { id: 10001, name: 'Test1', role: 'Develop', sex: '0', age: 28, address: 'test abc' },
      { id: 10002, name: 'Test2', role: 'Test', sex: '1', age: 22, address: 'Guangzhou' },
      { id: 10003, name: 'Test3', role: 'PM', sex: '0', age: 32, address: 'Shanghai' },
      { id: 10004, name: 'Test4', role: 'Designer', sex: '1', age: 23, address: 'test abc' },
      { id: 10005, name: 'Test5', role: 'Develop', sex: '1', age: 30, address: 'Shanghai' },
      { id: 10006, name: 'Test6', role: 'Designer', sex: '1', age: 21, address: 'test abc' },
      { id: 10007, name: 'Test7', role: 'Test', sex: '0', age: 29, address: 'test abc' },
      { id: 10008, name: 'Test8', role: 'Develop', sex: '0', age: 35, address: 'test abc' },
      { id: 10009, name: 'Test9', role: 'Test', sex: '1', age: 21, address: 'test abc' },
      { id: 10010, name: 'Test10', role: 'Develop', sex: '0', age: 28, address: 'test abc' },
      { id: 10011, name: 'Test11', role: 'Test', sex: '0', age: 29, address: 'test abc' },
      { id: 10012, name: 'Test12', role: 'Develop', sex: '1', age: 27, address: 'test abc' },
      { id: 10013, name: 'Test13', role: 'Test', sex: '0', age: 24, address: 'test abc' },
      { id: 10014, name: 'Test14', role: 'Develop', sex: '1', age: 34, address: 'test abc' },
      { id: 10015, name: 'Test15', role: 'Test', sex: '1', age: 21, address: 'test abc' },
      { id: 10016, name: 'Test16', role: 'Develop', sex: '0', age: 20, address: 'test abc' },
      { id: 10017, name: 'Test17', role: 'Test', sex: '1', age: 31, address: 'test abc' },
      { id: 10018, name: 'Test18', role: 'Develop', sex: '0', age: 32, address: 'test abc' },
      { id: 10019, name: 'Test19', role: 'Test', sex: '1', age: 37, address: 'test abc' },
      { id: 10020, name: 'Test20', role: 'Develop', sex: '1', age: 41, address: 'test abc' }
    ]
    demo1.loading = false
  }, 100)
})

nextTick(() => {
  // 将表格和工具栏进行关联
  const $table = tableRef.value
  const $toolbar = toolbarRef.value
  if ($table && $toolbar) {
    $table.connect($toolbar)
  }
})
</script>
