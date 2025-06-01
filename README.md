# 供应商管理系统 - Vue3 + Element Plus

这是一个使用 Vue 3 和 Element Plus 构建的企业供应商管理系统界面。

## 功能特点

- 📊 供应商信息展示
- 🏷️ 分类管理（NEWS、重要通知）
- 📈 浏览量、点赞、收藏统计
- 🔍 供应商关联查看
- 📤 数据导出功能
- 📱 响应式设计

## 技术栈

- Vue 3 - 渐进式 JavaScript 框架
- Element Plus - 基于 Vue 3 的组件库
- Vite - 下一代前端构建工具
- Vue Router - Vue.js 官方路由

## 安装运行

```bash
# 克隆项目
git clone https://github.com/liuwei389511/supplier-management-vue3.git

# 进入项目目录
cd supplier-management-vue3

# 安装依赖
npm install

# 运行开发服务器
npm run dev

# 构建生产版本
npm run build
```

## 项目结构

```
supplier-management-vue3/
├── src/
│   ├── views/          # 页面组件
│   ├── router/         # 路由配置
│   ├── App.vue         # 根组件
│   ├── main.js         # 入口文件
│   └── style.css       # 全局样式
├── index.html          # HTML 模板
├── vite.config.js      # Vite 配置
├── package.json        # 项目配置
└── README.md           # 项目说明
```

## 主要功能模块

### 1. 供应商列表
- 显示所有供应商信息
- 支持按分类筛选
- 重要通知标记
- 供应商关联展示

### 2. 数据统计
- 浏览量统计
- 点赞数统计
- 收藏数统计

### 3. 操作功能
- 查看详情
- 编辑信息
- 删除记录
- 导出数据

## 开发说明

### 添加新功能

1. 在 `src/views` 目录下创建新的页面组件
2. 在 `src/router/index.js` 中添加路由配置
3. 使用 Element Plus 组件构建界面

### 自定义主题

可以通过修改 Element Plus 的主题变量来自定义界面样式：

```css
:root {
  --el-color-primary: #5B8FF9;
  --el-color-success: #52c41a;
}
```

## 部署

构建生产版本后，将 `dist` 目录下的文件部署到任何静态文件服务器即可。

```bash
npm run build
```

## License

MIT License