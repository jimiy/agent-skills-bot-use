# 🎯 Agent Skills 实战示例集

> 从入门到精通的完整案例

---

## 目录

1. [入门级：个人代码规范Skill](#1-入门级个人代码规范skill)
2. [进阶级：Flutter项目Skill](#2-进阶级flutter项目skill)
3. [高级：自动化工作流Skill](#3-高级自动化工作流skill)
4. [专家级：带脚本的DevOps Skill](#4-专家级带脚本的devops-skill)
5. [组合案例：Skill + MCP](#5-组合案例skill--mcp)

---

## 1. 入门级：个人代码规范Skill

### 目标
创建一个TypeScript/React代码规范Skill，让AI按你的风格写代码

### 步骤

#### 1.1 创建目录结构

```bash
mkdir -p ~/.cursor/skills/my-react-style
touch ~/.cursor/skills/my-react-style/SKILL.md
```

#### 1.2 编写SKILL.md

```markdown
---
name: my-react-style
description: 个人React/TypeScript代码规范，包含组件结构、样式、状态管理
---

# 我的React代码规范

## 技术栈
- React 18+
- TypeScript
- Tailwind CSS
- Zustand（状态管理）

## 组件规范

### 1. 文件结构
```
src/
├── components/          # 公共组件
│   ├── ui/             # 基础UI组件
│   └── business/       # 业务组件
├── hooks/              # 自定义Hooks
├── stores/             # Zustand状态
├── types/              # TypeScript类型
└── utils/              # 工具函数
```

### 2. 组件模板
```tsx
// 函数式组件 + TypeScript + 默认导出
import React from 'react';

interface Props {
  title: string;
  onClick?: () => void;
}

export const MyComponent: React.FC<Props> = ({ title, onClick }) => {
  return (
    <div className="p-4 bg-white rounded-lg shadow">
      <h2 className="text-xl font-bold">{title}</h2>
      {onClick && (
        <button 
          onClick={onClick}
          className="mt-2 px-4 py-2 bg-blue-500 text-white rounded"
        >
          点击
        </button>
      )}
    </div>
  );
};
```

### 3. 样式规范
- 使用Tailwind CSS
- 禁止内联样式
- 响应式前缀：sm: md: lg:
- 颜色使用Tailwind预设

### 4. 状态管理
```tsx
// 使用Zustand
import { create } from 'zustand';

interface Store {
  count: number;
  increment: () => void;
}

export const useStore = create<Store>((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
}));
```

### 5. 命名规范
- 组件：PascalCase（MyComponent）
- 函数：camelCase（handleClick）
- 常量：UPPER_SNAKE_CASE（API_URL）
- 文件：PascalCase.tsx（组件）/ camelCase.ts（工具）

## 创建新组件步骤
1. 在components/下创建组件文件
2. 定义Props接口
3. 编写函数式组件
4. 添加样式类名
5. 导出组件

## 示例
用户："创建一个用户卡片组件"
AI输出：
```tsx
import React from 'react';

interface UserCardProps {
  name: string;
  email: string;
  avatar?: string;
  onViewProfile?: () => void;
}

export const UserCard: React.FC<UserCardProps> = ({
  name,
  email,
  avatar,
  onViewProfile,
}) => {
  return (
    <div className="p-4 bg-white rounded-lg shadow-md flex items-center space-x-4">
      {avatar ? (
        <img 
          src={avatar} 
          alt={name}
          className="w-12 h-12 rounded-full object-cover"
        />
      ) : (
        <div className="w-12 h-12 rounded-full bg-gray-300 flex items-center justify-center">
          <span className="text-xl text-gray-600">{name[0]}</span>
        </div>
      )}
      <div className="flex-1">
        <h3 className="text-lg font-semibold">{name}</h3>
        <p className="text-gray-500 text-sm">{email}</p>
      </div>
      {onViewProfile && (
        <button
          onClick={onViewProfile}
          className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
        >
          查看资料
        </button>
      )}
    </div>
  );
};
```
```

#### 1.3 测试Skill

1. **重启Cursor**
2. **在Chat中输入**：
   ```
   使用my-react-style skill创建一个商品卡片组件，
   包含商品图片、名称、价格、加入购物车按钮
   ```
3. **检查结果**：
   - ✅ 使用TypeScript
   - ✅ 使用Tailwind CSS
   - ✅ Props接口定义
   - ✅ 函数式组件
   - ✅ 样式符合规范

---

## 2. 进阶级：Flutter项目Skill

### 目标
创建完整的Flutter项目开发规范Skill

### 完整代码

```markdown
---
name: flutter-project-standard
description: 公司Flutter项目开发规范，包含架构、状态管理、UI组件、代码风格
---

# Flutter项目开发规范

## 技术栈
- Flutter 3.16+
- Dart 3.0+
- GetX（状态管理 + 路由）
- Dio（网络请求）
- GetStorage（本地存储）
- logger（日志）

## 项目结构
```
lib/
├── app/
│   ├── bindings/          # 依赖注入
│   ├── middleware/        # 中间件
│   ├── routes/           # 路由配置
│   └── theme/            # 主题配置
├── core/
│   ├── constants/        # 常量
│   ├── services/         # 服务层
│   ├── utils/            # 工具类
│   └── network/          # 网络层
├── data/
│   ├── models/           # 数据模型
│   ├── providers/        # 数据提供者
│   └── repositories/     # 仓库层
├── modules/              # 业务模块
│   └── [module_name]/
│       ├── pages/        # 页面
│       ├── controllers/  # 控制器
│       ├── widgets/      # 组件
│       └── bindings/     # 模块绑定
└── main.dart
```

## 代码规范

### 1. 控制器规范
```dart
import 'package:get/get.dart';

class HomeController extends GetxController {
  // 状态变量
  final RxInt counter = 0.obs;
  final RxList<Item> items = <Item>[].obs;
  final RxBool isLoading = false.obs;
  
  @override
  void onInit() {
    super.onInit();
    loadData();
  }
  
  Future<void> loadData() async {
    try {
      isLoading.value = true;
      // 加载数据
    } catch (e) {
      logger.e('加载数据失败', error: e);
    } finally {
      isLoading.value = false;
    }
  }
  
  void increment() {
    counter.value++;
  }
}
```

### 2. 页面规范
```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

class HomePage extends GetView<HomeController> {
  const HomePage({Key? key}) : super(key: key);
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('首页'),
        centerTitle: true,
      ),
      body: Obx(() {
        if (controller.isLoading.value) {
          return const Center(child: CircularProgressIndicator());
        }
        return ListView.builder(
          itemCount: controller.items.length,
          itemBuilder: (context, index) {
            final item = controller.items[index];
            return _buildItemCard(item);
          },
        );
      }),
      floatingActionButton: FloatingActionButton(
        onPressed: controller.increment,
        child: const Icon(Icons.add),
      ),
    );
  }
  
  Widget _buildItemCard(Item item) {
    return Card(
      margin: const EdgeInsets.all(8),
      child: ListTile(
        title: Text(item.title),
        subtitle: Text(item.description),
        leading: const Icon(Icons.item),
      ),
    );
  }
}
```

### 3. 模型规范
```dart
import 'package:json_annotation/json_annotation.dart';

part 'user_model.g.dart';

@JsonSerializable()
class UserModel {
  final String id;
  final String name;
  final String email;
  @JsonKey(name: 'avatar_url')
  final String? avatarUrl;
  
  const UserModel({
    required this.id,
    required this.name,
    required this.email,
    this.avatarUrl,
  });
  
  factory UserModel.fromJson(Map<String, dynamic> json) =>
      _$UserModelFromJson(json);
  
  Map<String, dynamic> toJson() => _$UserModelToJson(this);
}
```

### 4. UI规范
- 所有颜色使用Theme
- 间距使用8的倍数（8, 16, 24, 32）
- 圆角使用8或16
- 字体大小：12, 14, 16, 18, 20, 24

### 5. 路由配置
```dart
// app/routes/app_pages.dart
part of 'app_routes.dart';

class AppPages {
  static final routes = [
    GetPage(
      name: Routes.HOME,
      page: () => const HomePage(),
      binding: HomeBinding(),
    ),
    GetPage(
      name: Routes.PROFILE,
      page: () => const ProfilePage(),
      binding: ProfileBinding(),
    ),
  ];
}

// app/routes/app_routes.dart
abstract class Routes {
  static const HOME = '/';
  static const PROFILE = '/profile';
}
```

## 创建新模块步骤
1. 在modules/下创建模块目录
2. 创建pages、controllers、widgets、bindings子目录
3. 编写controller（继承GetxController）
4. 编写page（继承GetView）
5. 编写binding（继承Bindings）
6. 在routes中添加路由
7. 在bindings中添加依赖注入

## 依赖注入示例
```dart
class HomeBinding extends Bindings {
  @override
  void dependencies() {
    Get.lazyPut<HomeController>(() => HomeController());
    Get.lazyPut<HomeRepository>(() => HomeRepository());
  }
}
```

## 网络请求示例
```dart
class UserRepository {
  final Dio _dio = Get.find<Dio>();
  
  Future<UserModel> getUser(String id) async {
    final response = await _dio.get('/users/$id');
    return UserModel.fromJson(response.data);
  }
  
  Future<List<UserModel>> getUsers() async {
    final response = await _dio.get('/users');
    return (response.data as List)
        .map((json) => UserModel.fromJson(json))
        .toList();
  }
}
```

## 完整页面示例
用户："创建一个用户列表页面"
AI应该生成：
1. UserListController
2. UserListPage
3. UserListBinding
4. 更新路由
```

### 安装与使用

```bash
# 1. 创建目录
mkdir -p ~/.cursor/skills/flutter-project-standard

# 2. 复制上述内容到SKILL.md

# 3. 测试
# 在Cursor Chat中输入：
"使用flutter-project-standard skill创建用户资料页面"
```

---

## 3. 高级：自动化工作流Skill

### 目标
创建一个"新功能开发"工作流Skill，规范从需求到代码的完整流程

### SKILL.md

```markdown
---
name: feature-development-workflow
description: 新功能开发完整工作流，包含需求分析、技术方案、代码实现、测试
---

# 新功能开发工作流

## 触发条件
当需要开发新功能时

## 工作流程

### Phase 1: 需求分析
1. **理解需求**
   - 功能目标是什么？
   - 用户是谁？
   - 核心场景有哪些？
   - 验收标准是什么？

2. **输出文档**
   - 创建 `docs/features/功能名称.md`
   - 包含：背景、目标、用户故事、验收标准

### Phase 2: 技术方案
1. **架构设计**
   - 需要哪些数据模型？
   - 需要哪些API接口？
   - 页面结构如何？
   - 状态如何管理？

2. **输出文档**
   - 创建 `docs/tech/功能名称-技术方案.md`
   - 包含：架构图、数据流、接口定义、组件设计

### Phase 3: 代码实现
按以下顺序实现：
1. 数据模型（Model）
2. API接口（Service/Repository）
3. 状态管理（Controller/Store）
4. UI组件（Widgets）
5. 页面（Pages）
6. 路由配置

### Phase 4: 测试
1. 单元测试（关键逻辑）
2. 集成测试（API调用）
3. 手动测试（UI交互）
4. 更新测试文档

### Phase 5: 代码审查
1. 自测清单：
   - [ ] 代码符合团队规范
   - [ ] 有必要的注释
   - [ ] 无console.log
   - [ ] 错误处理完善
   - [ ] 性能考虑

2. 提交PR
   - 标题格式：`[Feature] 功能名称`
   - 描述包含：变更内容、测试方法、截图

## 文档模板

### 需求文档模板
```markdown
# 功能名称

## 背景
为什么需要这个功能

## 目标
- 目标1
- 目标2

## 用户故事
作为[用户角色]，我希望[功能]，以便[价值]

## 验收标准
- [ ] 标准1
- [ ] 标准2

## 界面原型
[截图或链接]
```

### 技术方案模板
```markdown
# 功能名称 - 技术方案

## 架构设计
[架构图]

## 数据模型
```typescript
interface Model {
  id: string;
  name: string;
}
```

## API接口
- GET /api/resource - 获取列表
- POST /api/resource - 创建

## 组件设计
- ComponentA: 负责xxx
- ComponentB: 负责xxx

## 状态管理
使用Zustand，结构：
```typescript
interface Store {
  items: Item[];
  fetchItems: () => Promise<void>;
}
```
```

## 示例
用户："开发一个购物车功能"

AI执行：
1. 创建需求文档 `docs/features/shopping-cart.md`
2. 创建技术方案 `docs/tech/shopping-cart-tech.md`
3. 实现代码：
   - `models/cart_item.ts`
   - `services/cart_service.ts`
   - `stores/cart_store.ts`
   - `components/CartItem.tsx`
   - `components/CartSummary.tsx`
   - `pages/CartPage.tsx`
4. 创建测试文件
5. 生成PR描述
```

---

## 4. 专家级：带脚本的DevOps Skill

### 目标
创建一个完整的CI/CD自动化部署Skill，包含可执行脚本

### 目录结构

```
auto-cicd/
├── SKILL.md
└── scripts/
    ├── setup.sh
    ├── build.sh
    ├── test.sh
    ├── deploy-staging.sh
    └── deploy-production.sh
```

### SKILL.md

```markdown
---
name: auto-cicd
description: 自动化CI/CD流程，包含构建、测试、部署到staging/production
---

# 自动化CI/CD流程

## 前置条件
- Node.js 18+
- Docker
- kubectl（K8s部署）
- 配置好kubeconfig

## 环境变量
```bash
export DOCKER_REGISTRY=your-registry.com
export IMAGE_NAME=your-app
export K8S_NAMESPACE=your-namespace
export SLACK_WEBHOOK_URL=your-slack-webhook
```

## 工作流程

### 1. 环境设置
```bash
./scripts/setup.sh
```
检查并安装必要依赖

### 2. 构建
```bash
./scripts/build.sh [version]
```
- 安装依赖
- 运行构建
- 构建Docker镜像
- 推送到镜像仓库

### 3. 测试
```bash
./scripts/test.sh
```
- 运行单元测试
- 运行集成测试
- 生成测试报告

### 4. 部署到Staging
```bash
./scripts/deploy-staging.sh [version]
```
- 更新K8s deployment
- 等待滚动更新完成
- 发送通知

### 5. 部署到Production
```bash
./scripts/deploy-production.sh [version]
```
- 确认当前staging正常
- 蓝绿部署
- 健康检查
- 发送通知

## 使用示例

### 完整流程
```bash
# 1. 设置环境
./scripts/setup.sh

# 2. 构建（版本号v1.2.3）
./scripts/build.sh v1.2.3

# 3. 测试
./scripts/test.sh

# 4. 部署到staging
./scripts/deploy-staging.sh v1.2.3

# 5. 验证staging
# ... 手动验证 ...

# 6. 部署到production
./scripts/deploy-production.sh v1.2.3
```

### 一键部署
```bash
# staging
./scripts/build.sh v1.2.3 && ./scripts/test.sh && ./scripts/deploy-staging.sh v1.2.3

# production（需要确认）
read -p "Deploy to production? (y/n) " confirm
if [ $confirm == "y" ]; then
  ./scripts/deploy-production.sh v1.2.3
fi
```
```

### scripts/setup.sh

```bash
#!/bin/bash
set -e

echo "🔧 检查环境..."

# 检查Node.js
if ! command -v node &> /dev/null; then
    echo "❌ Node.js未安装"
    exit 1
fi

# 检查Docker
if ! command -v docker &> /dev/null; then
    echo "❌ Docker未安装"
    exit 1
fi

# 检查kubectl
if ! command -v kubectl &> /dev/null; then
    echo "❌ kubectl未安装"
    exit 1
fi

# 检查kubeconfig
if [ ! -f ~/.kube/config ]; then
    echo "❌ kubeconfig未配置"
    exit 1
fi

echo "✅ 环境检查通过"

# 安装依赖
echo "📦 安装依赖..."
npm ci

echo "✅ 设置完成"
```

### scripts/build.sh

```bash
#!/bin/bash
set -e

VERSION=${1:-latest}

echo "🚀 开始构建版本: $VERSION"

# 运行测试
echo "🧪 运行测试..."
npm test

# 构建应用
echo "📦 构建应用..."
npm run build

# 构建Docker镜像
echo "🐳 构建Docker镜像..."
docker build -t $DOCKER_REGISTRY/$IMAGE_NAME:$VERSION .
docker tag $DOCKER_REGISTRY/$IMAGE_NAME:$VERSION $DOCKER_REGISTRY/$IMAGE_NAME:latest

# 推送到镜像仓库
echo "📤 推送到镜像仓库..."
docker push $DOCKER_REGISTRY/$IMAGE_NAME:$VERSION
docker push $DOCKER_REGISTRY/$IMAGE_NAME:latest

echo "✅ 构建完成: $DOCKER_REGISTRY/$IMAGE_NAME:$VERSION"
```

### scripts/test.sh

```bash
#!/bin/bash
set -e

echo "🧪 运行测试..."

# 单元测试
echo "Running unit tests..."
npm run test:unit

# 集成测试
echo "Running integration tests..."
npm run test:integration

# E2E测试（可选）
# npm run test:e2e

# 代码检查
echo "Running lint..."
npm run lint

# 类型检查
echo "Running type check..."
npm run type-check

echo "✅ 所有测试通过"
```

### scripts/deploy-staging.sh

```bash
#!/bin/bash
set -e

VERSION=${1:-latest}
ENVIRONMENT=staging

echo "🚀 部署到Staging环境"
echo "版本: $VERSION"

# 更新镜像
kubectl set image deployment/$IMAGE_NAME \
  $IMAGE_NAME=$DOCKER_REGISTRY/$IMAGE_NAME:$VERSION \
  -n $K8S_NAMESPACE

# 等待部署完成
echo "⏳ 等待部署完成..."
kubectl rollout status deployment/$IMAGE_NAME -n $K8S_NAMESPACE

# 发送通知
curl -X POST $SLACK_WEBHOOK_URL \
  -H 'Content-type: application/json' \
  --data "{
    \"text\": \"✅ Staging部署成功\",
    \"attachments\": [{
      \"color\": \"good\",
      \"fields\": [
        {\"title\": \"环境\", \"value\": \"$ENVIRONMENT\", \"short\": true},
        {\"title\": \"版本\", \"value\": \"$VERSION\", \"short\": true}
      ]
    }]
  }"

echo "✅ Staging部署完成"
```

### scripts/deploy-production.sh

```bash
#!/bin/bash
set -e

VERSION=${1:-latest}
ENVIRONMENT=production

echo "🚀 部署到Production环境"
echo "版本: $VERSION"

# 确认部署
read -p "⚠️  确认部署到Production? (yes/no): " confirm
if [ "$confirm" != "yes" ]; then
    echo "❌ 取消部署"
    exit 1
fi

# 蓝绿部署
echo "🔵 开始蓝绿部署..."

# 1. 部署新版本（绿色环境）
kubectl apply -f k8s/production-green.yaml
kubectl set image deployment/$IMAGE_NAME-green \
  $IMAGE_NAME=$DOCKER_REGISTRY/$IMAGE_NAME:$VERSION \
  -n $K8S_NAMESPACE

# 2. 等待绿色环境就绪
echo "⏳ 等待绿色环境就绪..."
kubectl rollout status deployment/$IMAGE_NAME-green -n $K8S_NAMESPACE

# 3. 健康检查
echo "🏥 健康检查..."
GREEN_URL=$(kubectl get svc $IMAGE_NAME-green -n $K8S_NAMESPACE -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
if ! curl -f http://$GREEN_URL/health; then
    echo "❌ 健康检查失败，回滚..."
    kubectl rollout undo deployment/$IMAGE_NAME-green -n $K8S_NAMESPACE
    exit 1
fi

# 4. 切换流量（蓝→绿）
echo "🔄 切换流量..."
kubectl patch service $IMAGE_NAME -n $K8S_NAMESPACE -p '{"spec":{"selector":{"version":"green"}}}'

# 5. 观察一段时间
sleep 30

# 6. 如果正常，删除旧版本（蓝色）
echo "🗑️  清理旧版本..."
kubectl delete deployment $IMAGE_NAME-blue -n $K8S_NAMESPACE || true

# 7. 将新版本标记为蓝色（为下次部署做准备）
kubectl label deployment $IMAGE_NAME-green version=blue --overwrite

# 发送通知
curl -X POST $SLACK_WEBHOOK_URL \
  -H 'Content-type: application/json' \
  --data "{
    \"text\": \"✅ Production部署成功\",
    \"attachments\": [{
      \"color\": \"good\",
      \"fields\": [
        {\"title\": \"环境\", \"value\": \"$ENVIRONMENT\", \"short\": true},
        {\"title\": \"版本\", \"value\": \"$VERSION\", \"short\": true}
      ]
    }]
  }"

echo "✅ Production部署完成"
```

### Dockerfile（配套）

```dockerfile
# 构建阶段
FROM node:18-alpine AS builder

WORKDIR /app

# 复制依赖文件
COPY package*.json ./
RUN npm ci

# 复制源码
COPY . .

# 构建
RUN npm run build

# 运行阶段
FROM node:18-alpine

WORKDIR /app

# 复制构建产物
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./

# 健康检查
HEALTHCHECK --interval=30s --timeout=3s --start=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1

EXPOSE 3000

CMD ["node", "dist/main.js"]
```

### 使用方法

```bash
# 1. 创建目录结构
mkdir -p ~/.cursor/skills/auto-cicd/scripts

# 2. 复制所有文件

# 3. 添加执行权限
chmod +x ~/.cursor/skills/auto-cicd/scripts/*.sh

# 4. 在项目中使用
# 在Cursor Chat中输入：
"使用auto-cicd skill部署版本v1.2.3到staging"
```

---

## 5. 组合案例：Skill + MCP

### 目标
创建一个"智能代码审查"系统，结合Skill和MCP

### 架构

```
用户请求审查PR
        ↓
Code Review Skill（定义流程）
        ↓
AI Agent决定调用哪些工具
        ↓
├─ GitHub MCP（获取PR信息）
├─ FileSystem MCP（读取代码）
└─ Browser MCP（预览效果）
        ↓
生成审查报告
```

### 配置MCP

```json
// .cursor/mcp.json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/project"]
    },
    "browser": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-browser"]
    }
  }
}
```

### SKILL.md

```markdown
---
name: smart-code-review
description: 智能代码审查，结合GitHub MCP自动获取PR信息并生成审查报告
---

# 智能代码审查流程

## 触发条件
当用户要求审查代码或PR时

## 审查流程

### 步骤1: 获取PR信息
使用GitHub MCP：
- 获取PR详情（标题、描述、作者）
- 获取变更文件列表
- 获取diff内容
- 获取评论历史

### 步骤2: 代码分析
- 读取变更文件
- 分析代码质量
- 检查潜在问题
- 对比最佳实践

### 步骤3: 功能验证（可选）
如果涉及UI变更：
- 检出分支
- 启动开发服务器
- 使用Browser MCP截图对比

### 步骤4: 生成报告
包含：
- 变更概述
- 发现的问题（按严重程度分类）
- 改进建议
- 正面评价
- 总体结论

## 审查检查清单

### 代码质量
- [ ] 代码符合团队规范
- [ ] 命名清晰有意义
- [ ] 函数/组件粒度合适
- [ ] 无重复代码

### 安全性
- [ ] 无SQL注入风险
- [ ] 无XSS漏洞
- [ ] 敏感信息未泄露
- [ ] 输入验证完善

### 性能
- [ ] 无明显的性能问题
- [ ] 避免不必要的重渲染
- [ ] 图片/资源优化

### 测试
- [ ] 有对应的单元测试
- [ ] 测试覆盖关键路径
- [ ] 测试用例有意义

### 文档
- [ ] 必要的注释
- [ ] 复杂逻辑有说明
- [ ] API文档更新

## 报告模板

```markdown
# PR审查报告

## 基本信息
- PR: #123
- 标题: [PR标题]
- 作者: @username
- 分支: feature/xxx → main

## 变更概述
[总结这次PR的主要变更]

## 详细审查

### 文件1: [文件路径]
**状态**: ✅ 通过 / ⚠️ 需修改 / ❌ 严重问题

**问题**:
1. [问题描述] - [建议]
2. [问题描述] - [建议]

**优点**:
- [正面评价]

### 文件2: [文件路径]
...

## 发现的问题汇总

### 🔴 严重（必须修复）
1. [问题描述]

### 🟡 中等（建议修复）
1. [问题描述]

### 🟢 轻微（可选）
1. [问题描述]

## 总体评价
- 代码质量: ⭐⭐⭐⭐☆
- 安全性: ⭐⭐⭐⭐⭐
- 测试覆盖: ⭐⭐⭐☆☆

**结论**: ✅ 通过 / ⚠️ 需修改后重新审查 / ❌ 拒绝

## 建议
1. [具体建议]
2. [具体建议]
```

## 使用示例

### 审查GitHub PR
```
"使用smart-code-review skill审查PR #123"
```

AI执行：
1. 调用GitHub MCP获取PR信息
2. 分析代码变更
3. 生成审查报告

### 审查本地代码
```
"使用smart-code-review skill审查src/components/Button.tsx的变更"
```

AI执行：
1. 使用FileSystem MCP读取文件
2. 对比git历史
3. 生成审查意见
```

### 配套脚本（可选）

```bash
# scripts/post-review-comment.sh
#!/bin/bash

PR_NUMBER=$1
REPORT_FILE=$2

# 将审查报告发布为PR评论
curl -X POST \
  -H "Authorization: token $GITHUB_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/$REPO/issues/$PR_NUMBER/comments \
  -d "{\"body\": \"$(cat $REPORT_FILE | sed 's/"/\\"/g')\"}"
```

---

## 总结

这些示例展示了Agent Skills的多种用法：

1. **入门级**：简单的代码规范Skill
2. **进阶级**：完整的项目开发规范
3. **高级**：自动化工作流
4. **专家级**：带可执行脚本的DevOps
5. **组合级**：Skill + MCP协同工作

**关键要点**：
- ✅ Skill定义"做什么"和"怎么做"
- ✅ MCP提供"工具能力"
- ✅ 两者结合 = 强大的AI自动化
- ✅ 从简单开始，逐步复杂化

---

**Happy Coding!** 🚀
