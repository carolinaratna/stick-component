<template>
  <div>
    <h4 class="font-medium-lg">
      Table selection:
    </h4>
    <hr class="mb-8">

    <fieldset>
      <legend class="font-medium-md">
        Checkbox:
      </legend>

      <SCTable :row-selection="rowSelection" :columns="columns" :data-source="data">
        <a slot="name" slot-scope="{ text }">{{ text }}</a>
      </SCTable>
    </fieldset>

    <fieldset class="mt-10">
      <legend class="font-medium-md">
        Radio:
      </legend>

      <SCTable :row-selection="rowRadioSelection" :columns="columns" :data-source="data">
        <a slot="name" slot-scope="{ text }">{{ text }}</a>
      </SCTable>
    </fieldset>
  </div>
</template>

<script>
import SCTable from '../index.vue'

const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
    key: 'name',
    scopedSlots: { customRender: 'name' }
  },
  {
    title: 'Age',
    dataIndex: 'age',
    key: 'age'
  },
  {
    title: 'Address',
    dataIndex: 'address',
    key: 'address 1'
  }
]

const data = [
  {
    key: '1',
    name: 'John Brown',
    age: 32,
    address: 'New York No. 1 Lake Park'
  },
  {
    key: '2',
    name: 'Jim Green',
    age: 42,
    address: 'London No. 1 Lake Park'
  },
  {
    key: '3',
    name: 'Joe Black',
    age: 32,
    address: 'Sidney No. 1 Lake Park'
  },
  {
    key: '4',
    name: 'Disabled User',
    age: 99,
    address: 'Sidney No. 1 Lake Park'
  }
]

export default {
  components: {
    SCTable
  },
  data() {
    return {
      data,
      columns
    }
  },
  computed: {
    rowSelection() {
      return {
        onChange: (selectedRowKeys, selectedRows) => {
          console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows)
        },
        getCheckboxProps: (record) => ({
          props: {
            disabled: record.name === 'Disabled User', // Column configuration not to be checked
            name: record.name
          }
        })
      }
    },
    rowRadioSelection() {
      return {
        type: 'radio',
        onChange: (selectedRowKeys, selectedRows) => {
          console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows)
        },
        getCheckboxProps: (record) => ({
          props: {
            disabled: record.name === 'Disabled User', // Column configuration not to be checked
            name: record.name
          }
        })
      }
    }
  }
}
</script>
