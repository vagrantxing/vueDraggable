<template>
  <div>
    <el-card>
      <el-row :gutter="20">
        <el-col :span="10">
          <el-table :data="tableData"
            border
            id="table1"
            row-key="id"
            align="left">
          <el-table-column v-for="(item, index) in col"
              :key="`col_${index}`"
              :prop="dropCol[index].prop"
              :label="item.label"> 
            </el-table-column>
          </el-table>
        </el-col>
        <el-col :span="10">
          <el-table
            :data="tableData1"
            border
            id="table2"
            row-key="id"
            stripe
            style="width: 100%">
            <el-table-column v-for="(item, index) in col"
              :key="`col_${index}`"
              :prop="dropCol[index].prop"
              :label="item.label"> 
            </el-table-column>
          </el-table>
        </el-col>
      </el-row>
    </el-card>
    <div>{{tableData}}</div>
    <div>{{tableData1}}</div>
  </div>
</template>
<script>
import Sortable from 'sortablejs'
export default {
  data() {
    return {
      col: [
        {
          label: '日期',
          prop: 'id'
        },
        {
          label: '姓名',
          prop: 'name'
        }
      ],
      dropCol: [
        {
          label: '日期',
          prop: 'id'
        },
        {
          label: '姓名',
          prop: 'name'
        }
      ],
      tableData: [
        {
          id: '1',
          name: '王小虎1'
        },
        {
          id: '2',
          name: '王小虎2'
        },
        {
          id: '3',
          name: '王小虎3'
        },
        {
          id: '4',
          name: '王小虎4'
        }
      ],
      tableData1: [{
          id: '1',
          name: 'xingtao'
        }, {
          id: '2',
          name: 'dye'
        }, {
          id: '3',
          name: 'mike'
        }, {
          id: '4',
          name: 'sumu'
        }],
        
        newIndex:null,
        oldIndex:null
    }
  },
  mounted() {
    // 阻止默认行为
	  document.body.ondrop = function (event) {
            event.preventDefault();
            event.stopPropagation();
    };
    this.rowDrop1()
    this.rowDrop2()
  },
  methods: {
    //行拖拽
    rowDrop1() {
      // const tbody = document.querySelector('.el-table__body-wrapper tbody')
      const tbody = document.querySelector('#table1 tbody')
      this.dataDraggable(tbody);
    },
    rowDrop2() {
      // const tbody = document.querySelector('.el-table__body-wrapper tbody')
      const tbody2 = document.querySelector('#table2 tbody')
      this.dataDraggable(tbody2);
    },
    dataDraggable(tbody){
      const _this = this ;
      Sortable.create(tbody, {
        onEnd({ newIndex, oldIndex }) {
          const currRow = _this.tableData.splice(oldIndex, 1)[0]
          _this.tableData.splice(newIndex, 0, currRow)
          
          const currRow2 = _this.tableData1.splice(oldIndex, 1)[0]
          _this.tableData1.splice(newIndex, 0, currRow2)
        }
      })
    }
    //列拖拽
    // columnDrop() {
    //   const wrapperTr = document.querySelector('.el-table__header-wrapper tr')
    //   this.sortable = Sortable.create(wrapperTr, {
    //     animation: 180,
    //     delay: 0,
    //     onEnd: evt => {
    //       const oldItem = this.dropCol[evt.oldIndex]
    //       this.dropCol.splice(evt.oldIndex, 1)
    //       this.dropCol.splice(evt.newIndex, 0, oldItem)
    //     }
    //   })
    // }
  }
}
</script>
