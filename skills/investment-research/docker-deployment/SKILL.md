# Docker容器化 (Docker Deployment)

## Overview

Docker容器化是将投研Agent系统容器化部署的技能。参考FinSight的Docker配置，实现一键部署。

## 何时使用

- 生产环境部署
- 环境一致性
- 弹性伸缩
- 微服务架构

## 流程

1. **Dockerfile编写**：编写Dockerfile
2. **镜像构建**：构建镜像
3. **docker-compose编写**：编写编排文件
4. **环境配置**：配置环境变量
5. **本地验证**：本地测试
6. **镜像推送**：推送到仓库
7. **集群部署**：K8s部署

## 模板

### Dockerfile模板
```dockerfile
FROM python:3.11-slim

WORKDIR /app

# 安装系统依赖
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    && rm -rf /var/lib/apt/lists/*

# 复制依赖文件
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 复制应用代码
COPY . .

# 环境变量
ENV PYTHONUNBUFFERED=1
ENV API_MODE=production

# 暴露端口
EXPOSE 8000

# 启动命令
CMD ["uvicorn", "src.api.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### docker-compose模板
```yaml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=${DATABASE_URL}
      - REDIS_URL=${REDIS_URL}
    depends_on:
      - database
      - redis

  streamlit:
    build: .
    ports:
      - "8501:8501"
    command: streamlit run src/ui/app.py
    depends_on:
      - api

  database:
    image: postgres:15
    environment:
      - POSTGRES_DB=research
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_PASSWORD=${DB_PASSWORD}

  redis:
    image: redis:7-alpine
```

## 检查清单

- [ ] Dockerfile优化
- [ ] 镜像大小控制
- [ ] 安全性检查
- [ ] 健康检查
- [ ] 日志配置
- [ ] 监控集成

## 红牌警告

- 镜像过大
- 依赖不安全
- 敏感信息泄露
- 端口冲突
- 资源限制缺失
