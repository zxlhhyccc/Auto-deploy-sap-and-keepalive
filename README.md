# Auto-SAP应用部署说明文档

## 概述

本项目是自动部署argo节点到SAP Cloud Foundry平台，自动保活的方案

### 前置要求
* GitHub 账户：需要有一个 GitHub 账户来创建仓库和设置工作流
* SAP Cloud Foundry 账户：需要有 SAP Cloud Foundry 的有效账户

## 部署步骤

1. Fork本仓库

2. 在Actions菜单允许 `I understand my workflows, go ahead and enable them` 按钮

3. 在 GitHub 仓库中设置以下 secrets（Settings → Secrets and variables → Actions → New repository secret）：
- `EMAIL`: Cloud Foundry账户邮箱
- `PASSWORD`: Cloud Foundry账户密码
- `SG_ORG`: 新加坡组织名称
- `US_ORG`: 美国组织名称
- `SPACE`: Cloud Foundry空间名称

4. **设置Docker容器环境变量**
   - 使用固定隧道token部署，请在cloudflare里设置端口为8001：
   - 设置基础环境变量：
     - UUID(节点uuid)
     - ARGO_DOMAIN(固定隧道域名,未设置将使用临时隧道)
     - ARGO_AUTH(固定隧道json或token,未设置将使用临时隧道)
     - SUB_PATH(订阅token,未设置默认是sub)
   - 可选环境变量
     - NEZHA_SERVER(v1形式: nezha.xxx.com:8008  v0形式：nezha.xxx.com)
     - NEZHA_PORT(V1哪吒没有这个)
     - NEZHA_KEY(v1的NZ_CLIENT_SECRET或v0的agent密钥)
     - CFIP(优选域名或优选ip)
     - CFPORT(优选域名或优选ip对应端口)

5. **开始部署**
   1: 在GitHub仓库的Actions页面找到"Deploy to SAP Cloud"工作流
   2: 点击"Run workflow"按钮
   3: 根据需要选择或填写以下参数：
      - environment: 选择部署环境（staging/production）
      - region: 选择部署区域（ap21/us10/eu10）
      - app_name: （可选）指定应用名称
   4: 点击绿色的"Run workflow"按钮开始部署

## 注意事项

1. 确保所有必需的GitHub Secrets已正确配置
2. Docker镜像必须可访问且包含正确的应用代码
4. 部署完成后会显示应用状态信息
