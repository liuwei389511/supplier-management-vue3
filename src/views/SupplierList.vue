<template>
  <div class="supplier-container">
    <!-- 顶部标签页 -->
    <el-tabs v-model="activeTab" class="supplier-tabs">
      <el-tab-pane name="viewCount">
        <template #label>
          <span class="tab-label">
            <el-icon><View /></el-icon>
            浏览量
          </span>
        </template>
      </el-tab-pane>
      <el-tab-pane name="likes">
        <template #label>
          <span class="tab-label">
            <el-icon><Pointer /></el-icon>
            点赞
          </span>
        </template>
      </el-tab-pane>
      <el-tab-pane name="favorites">
        <template #label>
          <span class="tab-label">
            <el-icon><Star /></el-icon>
            收藏
          </span>
        </template>
      </el-tab-pane>
    </el-tabs>

    <!-- 表格内容 -->
    <div class="table-wrapper">
      <el-table
        :data="tableData"
        style="width: 100%"
        :header-cell-style="headerCellStyle"
        :cell-style="cellStyle"
        border
      >
        <!-- 分类列 -->
        <el-table-column
          prop="category"
          label="分类"
          width="100"
          fixed="left"
        >
          <template #default="scope">
            <div class="category-cell">{{ scope.row.category }}</div>
          </template>
        </el-table-column>

        <!-- 标题列 -->
        <el-table-column
          prop="title"
          label="标题"
          min-width="400"
          fixed="left"
        >
          <template #default="scope">
            <div class="title-cell">
              {{ scope.row.title }}
              <span v-if="scope.row.isImportant" class="important-tag">重要通知</span>
            </div>
          </template>
        </el-table-column>

        <!-- 供应商列 -->
        <el-table-column
          v-for="supplier in suppliers"
          :key="supplier"
          :label="supplier"
          :prop="supplier"
          width="120"
          align="center"
        >
          <template #default="scope">
            <span v-if="scope.row[supplier]" class="supplier-tag">
              {{ scope.row[supplier] }}
            </span>
          </template>
        </el-table-column>

        <!-- 操作列 -->
        <el-table-column
          label="操作"
          width="120"
          fixed="right"
          align="center"
        >
          <template #default="scope">
            <el-dropdown v-if="scope.$index < 2">
              <el-button link type="primary">
                <el-icon><More /></el-icon>
              </el-button>
              <template #dropdown>
                <el-dropdown-menu>
                  <el-dropdown-item>查看详情</el-dropdown-item>
                  <el-dropdown-item>编辑</el-dropdown-item>
                  <el-dropdown-item>删除</el-dropdown-item>
                </el-dropdown-menu>
              </template>
            </el-dropdown>
            <el-button 
              v-else-if="scope.row.isImportant" 
              type="success" 
              size="small"
              @click="handleExport(scope.row)"
            >
              <el-icon><Upload /></el-icon>
              导出
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { ElMessage } from 'element-plus'
import { View, Pointer, Star, More, Upload } from '@element-plus/icons-vue'

// 当前激活的标签
const activeTab = ref('viewCount')

// 供应商列表
const suppliers = [
  'xxxx企业', 'xxxx企业', 'xxxx企业', 'xxxx企业', 
  'xxxx企业', 'xxxx企业', 'xxxx企业', 'xxxx企业', 'xxxx企业'
]

// 表格数据
const tableData = ref([
  {
    category: 'NEWS',
    title: 'FY23第二回合作伙伴会议通知 (7月14日)',
    isImportant: false,
    'xxxx企业': 'xxxx企业',
    // 为每个供应商添加数据
    ...suppliers.reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  },
  {
    category: '重要通知',
    title: 'FY23上海大金纳凉节通知 (8月26日)',
    isImportant: true,
    'xxxx企业': 'xxxx企业',
    ...suppliers.slice(0, 3).reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  },
  {
    category: 'NEWS',
    title: 'FY23第二回合作伙伴会议通知 (7月14日)',
    isImportant: false,
    ...suppliers.reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  },
  {
    category: '重要通知',
    title: 'FY23上海大金纳凉节通知 (8月26日)',
    isImportant: true,
    ...suppliers.reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  },
  {
    category: 'NEWS',
    title: 'FY23第二回合作伙伴会议通知 (7月14日)',
    isImportant: false,
    ...suppliers.reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  },
  {
    category: '重要通知',
    title: 'FY23上海大金纳凉节通知 (8月26日)',
    isImportant: true,
    ...suppliers.reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  },
  {
    category: 'NEWS',
    title: 'FY23第二回合作伙伴会议通知 (7月14日)',
    isImportant: false,
    ...suppliers.reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  },
  {
    category: '重要通知',
    title: 'FY23上海大金纳凉节通知 (8月26日)',
    isImportant: true,
    ...suppliers.reduce((acc, supplier) => {
      acc[supplier] = supplier
      return acc
    }, {})
  }
])

// 表头样式
const headerCellStyle = {
  backgroundColor: '#5B8FF9',
  color: '#ffffff',
  fontWeight: 'bold',
  fontSize: '14px',
  padding: '12px 0'
}

// 单元格样式
const cellStyle = ({ row, columnIndex }) => {
  const baseStyle = {
    padding: '8px 0',
    fontSize: '13px'
  }
  
  // 重要通知行的背景色
  if (row.isImportant) {
    baseStyle.backgroundColor = '#f0f9ff'
  }
  
  return baseStyle
}

// 导出处理
const handleExport = (row) => {
  ElMessage.success('正在导出数据...')
}
</script>

<style scoped>
.supplier-container {
  min-height: 100vh;
  background-color: #f5f5f5;
  padding: 20px;
}

.supplier-tabs {
  background-color: white;
  padding: 0 20px;
  border-radius: 8px 8px 0 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.tab-label {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: 14px;
}

.table-wrapper {
  background-color: white;
  border-radius: 0 0 8px 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.category-cell {
  font-weight: 500;
  color: #333;
}

.title-cell {
  display: flex;
  align-items: center;
  gap: 8px;
}

.important-tag {
  background-color: #52c41a;
  color: white;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 12px;
  white-space: nowrap;
}

.supplier-tag {
  color: #1890ff;
  font-size: 12px;
}

:deep(.el-table__header-wrapper) {
  border-radius: 0;
}

:deep(.el-table__body-wrapper) {
  font-size: 13px;
}

:deep(.el-table__row) {
  transition: all 0.3s;
}

:deep(.el-table__row:hover) {
  background-color: #f5f7fa !important;
}

:deep(.el-tabs__item) {
  font-size: 14px;
  height: 48px;
  line-height: 48px;
}

:deep(.el-tabs__nav-wrap::after) {
  height: 1px;
  background-color: #e4e7ed;
}

:deep(.el-tabs__active-bar) {
  height: 3px;
  background-color: #409eff;
}

:deep(.el-dropdown) {
  font-size: 20px;
}
</style>