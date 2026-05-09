# 课程管理后台系统

一个基于 Node.js + Express + HTML/Vanilla JS 的课程管理后台系统，支持对课程信息的增删改查操作。

## 项目结构

```
Course management backend development/
├── backend/                    # 后端服务
│   ├── app.js                  # 后端入口文件
│   ├── package.json            # 后端依赖配置
│   ├── src/
│   │   ├── controllers/        # 控制器层
│   │   │   └── courseController.js
│   │   ├── models/             # 数据模型层
│   │   │   └── Course.js
│   │   └── routes/             # 路由层
│   │       └── courseRoutes.js
│   └── public/                 # 静态资源目录
└── frontend/                   # 前端页面
    └── index.html              # 课程管理主页面
```

## 技术栈

- **后端**: Node.js + Express.js
- **前端**: HTML5 + Tailwind CSS + Vanilla JavaScript
- **数据存储**: 内存存储（可扩展为数据库存储）
- **跨域处理**: CORS

## 功能特性

### 后端API

| 方法 | 路径 | 描述 |
|------|------|------|
| GET | /api/courses | 获取所有课程列表 |
| GET | /api/courses/:id | 根据ID获取单个课程 |
| POST | /api/courses | 创建新课程 |
| PUT | /api/courses/:id | 更新课程信息 |
| DELETE | /api/courses/:id | 删除课程 |

### 前端功能

- 课程列表展示（支持查看名称、描述、讲师、学分、分类、状态）
- 添加新课程
- 编辑课程信息
- 删除课程
- 课程状态管理（启用/禁用）

## 运行环境要求

- Node.js >= 14.0.0
- npm >= 6.0.0

## 安装与运行

### 1. 克隆或解压项目

将项目文件放置到本地目录。

### 2. 安装后端依赖

```bash
cd backend
npm install
```

### 3. 启动后端服务

```bash
npm start
```

后端服务将启动在 **http://localhost:3000**

启动成功后，控制台会显示：`Server running on port 3000`

### 4. 访问前端页面

使用浏览器直接打开 `frontend/index.html` 文件，或者将文件部署到Web服务器中访问。

**方式一：直接打开文件**
- 双击 `frontend/index.html` 文件
- 或使用浏览器打开文件路径

**方式二：使用Live Server（推荐开发时使用）**
- 在VS Code中安装 Live Server 插件
- 右键点击 `index.html` 选择 "Open with Live Server"

## 使用说明

### 添加课程

1. 点击页面右上角 "添加课程" 按钮
2. 填写课程信息（课程名称、讲师、学分、分类为必填项）
3. 点击 "保存" 按钮

### 编辑课程

1. 在课程列表中找到目标课程
2. 点击该行右侧的编辑按钮（铅笔图标）
3. 修改课程信息
4. 点击 "保存" 按钮

### 删除课程

1. 在课程列表中找到目标课程
2. 点击该行右侧的删除按钮（垃圾桶图标）
3. 在弹出的确认对话框中点击 "确定"

## 预置数据

系统启动时自动加载3门示例课程：

| 课程名称 | 讲师 | 学分 | 分类 |
|---------|------|------|------|
| 高等数学 | 张教授 | 4 | 数学 |
| 计算机科学导论 | 李老师 | 3 | 计算机 |
| 英语听说 | 王老师 | 2 | 语言 |

## API测试

可以使用以下方式测试API：

### PowerShell
```powershell
# 获取所有课程
Invoke-RestMethod -Uri 'http://localhost:3000/api/courses' -Method Get

# 添加新课程
Invoke-RestMethod -Uri 'http://localhost:3000/api/courses' -Method Post -ContentType 'application/json' -Body '{"name":"物理基础","description":"大学物理基础课程","instructor":"赵老师","credit":3,"category":"物理","status":"active"}'
```

### curl
```bash
# 获取所有课程
curl http://localhost:3000/api/courses

# 添加新课程
curl -X POST http://localhost:3000/api/courses \
  -H "Content-Type: application/json" \
  -d '{"name":"物理基础","description":"大学物理基础课程","instructor":"赵老师","credit":3,"category":"物理","status":"active"}'
```

## 课程字段说明

| 字段名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| name | string | 是 | 课程名称 |
| description | string | 否 | 课程描述 |
| instructor | string | 是 | 讲师姓名 |
| credit | number | 是 | 学分（1-10） |
| category | string | 是 | 课程分类 |
| status | string | 否 | 状态（active/inactive，默认active） |

## 常见问题

**Q: 前端页面无法获取数据？**  
A: 请确认后端服务已启动，且端口3000未被其他程序占用。

**Q: 如何修改后端端口？**  
A: 修改 `backend/app.js` 文件中的 `PORT` 变量，或在启动时设置环境变量：`PORT=8080 npm start`

**Q: 如何持久化数据？**  
A: 当前使用内存存储，数据会在服务重启后丢失。如需持久化，可修改 `backend/src/models/Course.js` 使用 MongoDB、MySQL 等数据库。

## 许可证

MIT License
