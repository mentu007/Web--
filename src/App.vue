<script setup>
import Edit from './components/Edit.vue'
import axios from 'axios'
import { ref } from 'vue'
import { onMounted } from 'vue';
// TODO: 列表渲染
const list = ref([]);
const getList = async () => {
  const res = await axios.get('/list')
  list.value = res.data
}

onMounted(() => getList())


// TODO: 删除功能
/* 
删除功能开发思路：
1. 拿到当前行的ID
2. 通过ID去掉删除接口
3. 跟新最新列表
*/
const onDelete = async (id) =>{
  await axios.delete(`/del/${id}`)
  getList()
}

// TODO: 编辑功能

</script>

<template>
  <div class="app">
    <el-table :data="list">
      <el-table-column label="ID" prop="id"></el-table-column>
      <el-table-column label="姓名" prop="name" width="150"></el-table-column>
      <el-table-column label="籍贯" prop="place"></el-table-column>
      <el-table-column label="操作" width="150">
        <template #default="{row}">
          <el-button type="primary" link>编辑</el-button>
          <el-button type="danger" @click="onDelete(row.id)" link>删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
  <Edit />
</template>

<style scoped>
.app {
  width: 980px;
  margin: 100px auto 0;
}
</style>
