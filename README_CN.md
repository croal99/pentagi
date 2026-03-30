# PentAGI

<div align="center" style="font-size: 1.5em; margin: 20px 0;">
    <strong>P</strong>enetration testing <strong>A</strong>rtificial <strong>G</strong>eneral <strong>I</strong>ntelligence
</div>
<br>
<div align="center">

> 🚀 **加入社区！** 与安全研究人员、AI 爱好者和道德黑客建立联系。获取支持、分享见解，并了解 PentAGI 的最新动态。

[![Discord](https://img.shields.io/badge/Discord-7289DA?logo=discord&logoColor=white)](https://discord.gg/2xrMh7qX6m)⠀[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?logo=telegram&logoColor=white)](https://t.me/+Ka9i6CNwe71hMWQy)

<a href="https://trendshift.io/repositories/15161" target="_blank"><img src="https://trendshift.io/api/badge/repositories/15161" alt="vxcontrol%2Fpentagi | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>

</div>

## 📖 目录

- [概述](#-概述)
- [功能特性](#-功能特性)
- [快速开始](#-快速开始)
- [API 访问](#-api-访问)
- [高级配置](#-高级配置)
- [开发](#-开发)
- [测试 LLM 智能体](#-测试-llm-智能体)
- [嵌入配置与测试](#-嵌入配置与测试)
- [使用 ftester 测试功能](#-使用-ftester-测试功能)
- [构建](#-构建)
- [致谢](#-致谢)
- [许可证](#-许可证)

## 🎯 概述

PentAGI 是一个创新的自动化安全测试工具，利用尖端人工智能技术。该项目专为信息安全专业人员、研究人员和爱好者设计，需要强大且灵活的解决方案来进行渗透测试。

您可以观看 **PentAGI 概述**视频：
[![PentAGI 概述视频](https://github.com/user-attachments/assets/0828dc3e-15f1-4a1d-858e-9696a146e478)](https://youtu.be/R70x5Ddzs1o)

## ✨ 功能特性

- 🛡️ 安全与隔离。所有操作都在沙箱化的 Docker 环境中执行，完全隔离。
- 🤖 完全自主。AI 驱动的智能体自动确定并执行渗透测试步骤。
- 🔬 专业渗透测试工具。内置 20+ 专业安全工具套件，包括 nmap、metasploit、sqlmap 等。
- 🧠 智能记忆系统。长期存储研究结果和成功方法以供将来使用。
- 📚 知识图谱集成。基于 Graphiti 的知识图谱，使用 Neo4j 进行语义关系跟踪和高级上下文理解。
- 🔍 网络智能。通过 [scraper](https://hub.docker.com/r/vxcontrol/scraper) 内置浏览器，从网络来源收集最新信息。
- 🔎 外部搜索系统。与高级搜索 API 集成，包括 [Tavily](https://tavily.com)、[Traversaal](https://traversaal.ai)、[Perplexity](https://www.perplexity.ai)、[DuckDuckGo](https://duckduckgo.com/)、[Google 自定义搜索](https://programmablesearchengine.google.com/)、[Sploitus 搜索](https://sploitus.com) 和 [Searxng](https://searxng.org) 以进行全面信息收集。
- 👥 专家团队。具有专门 AI 智能体的委托系统，用于研究、开发和基础设施任务。
- 📊 综合监控。详细日志记录，并与 Grafana/Prometheus 集成以实现实时系统观察。
- 📝 详细报告。生成完整的漏洞报告和利用指南。
- 📦 智能容器管理。根据特定任务需求自动选择 Docker 镜像。
- 📱 现代界面。用于系统管理和监控的简洁直观的 Web UI。
- 🔌 全面的 API。完整的 REST 和 GraphQL API，支持 Bearer 令牌认证，用于自动化和集成。
- 💾 持久化存储。所有命令和输出都存储在带有 [pgvector](https://hub.docker.com/r/vxcontrol/pgvector) 扩展的 PostgreSQL 中。
- 🎯 可扩展架构。支持水平扩展的微服务设计。
- 🏠 自托管解决方案。完全控制您的部署和数据。
- 🔑 灵活认证。支持各种 LLM 提供商（[OpenAI](https://platform.openai.com/)、[Anthropic](https://www.anthropic.com/)、[Ollama](https://ollama.com/)、[AWS Bedrock](https://aws.amazon.com/bedrock/)、[Google AI/Gemini](https://ai.google.dev/)、[Deep Infra](https://deepinfra.com/)、[OpenRouter](https://openrouter.ai/)、[DeepSeek](https://www.deepseek.com/en)、[Moonshot](https://platform.moonshot.ai/)）和自定义配置。
- 🔐 API 令牌认证。安全的 Bearer 令牌系统，用于 REST 和 GraphQL API 的编程访问。
- ⚡ 快速部署。通过 [Docker Compose](https://docs.docker.com/compose/) 轻松设置，具有全面的环境配置。

## 🏗️ 架构

### 系统上下文

```mermaid
flowchart TB
    classDef person fill:#08427B,stroke:#073B6F,color:#fff
    classDef system fill:#1168BD,stroke:#0B4884,color:#fff
    classDef external fill:#666666,stroke:#0B4884,color:#fff

    pentester["👤 安全工程师
    (系统用户)"]

    pentagi["✨ PentAGI
    (自主渗透测试系统)"]

    target["🎯 target-system
    (被测系统)"]
    llm["🧠 llm-provider
    (OpenAI/Anthropic/Ollama/Bedrock/Gemini/自定义)"]
    search["🔍 search-systems
    (Google/DuckDuckGo/Tavily/Traversaal/Perplexity/Sploitus/Searxng)"]
    langfuse["📊 langfuse-ui
    (LLM 可观察性仪表板)"]
    grafana["📈 grafana
    (系统监控仪表板)"]

    pentester --> |使用 HTTPS| pentagi
    pentester --> |监控 AI HTTPS| langfuse
    pentester --> |监控系统 HTTPS| grafana
    pentagi --> |测试 各种协议| target
    pentagi --> |查询 HTTPS| llm
    pentagi --> |搜索 HTTPS| search
    pentagi --> |报告 HTTPS| langfuse
    pentagi --> |报告 HTTPS| grafana

    class pentester person
    class pentagi system
    class target,llm,search,langfuse,grafana external

    linkStyle default stroke:#ffffff,color:#ffffff
```

<details>
<summary><b>🔄 容器架构</b>（点击展开）</summary>

```mermaid
graph TB
    subgraph 核心服务
        UI[前端 UI<br/>React + TypeScript]
        API[后端 API<br/>Go + GraphQL]
        DB[(向量存储<br/>PostgreSQL + pgvector)]
        MQ[任务队列<br/>异步处理]
        Agent[AI 智能体<br/>多智能体系统]
    end

    subgraph 知识图谱
        Graphiti[Graphiti<br/>知识图谱 API]
        Neo4j[(Neo4j<br/>图数据库)]
    end

    subgraph 监控
        Grafana[Grafana<br/>仪表板]
        VictoriaMetrics[VictoriaMetrics<br/>时序数据库]
        Jaeger[Jaeger<br/>分布式追踪]
        Loki[Loki<br/>日志聚合]
        OTEL[OpenTelemetry<br/>数据收集]
    end

    subgraph 分析
        Langfuse[Langfuse<br/>LLM 分析]
        ClickHouse[ClickHouse<br/>分析数据库]
        Redis[Redis<br/>缓存 + 速率限制]
        MinIO[MinIO<br/>S3 存储]
    end

    subgraph 安全工具
        Scraper[网络爬虫<br/>隔离浏览器]
        PenTest[安全工具<br/>20+ 专业工具<br/>沙箱化执行]
    end

    UI --> |HTTP/WS| API
    API --> |SQL| DB
    API --> |事件| MQ
    MQ --> |任务| Agent
    Agent --> |命令| PenTest
    Agent --> |查询| DB
    Agent --> |知识| Graphiti
    Graphiti --> |图| Neo4j

    API --> |遥测| OTEL
    OTEL --> |指标| VictoriaMetrics
    OTEL --> |追踪| Jaeger
    OTEL --> |日志| Loki

    Grafana --> |查询| VictoriaMetrics
    Grafana --> |查询| Jaeger
    Grafana --> |查询| Loki

    API --> |分析| Langfuse
    Langfuse --> |存储| ClickHouse
    Langfuse --> |缓存| Redis
    Langfuse --> |文件| MinIO

    classDef core fill:#f9f,stroke:#333,stroke-width:2px,color:#000
    classDef knowledge fill:#ffa,stroke:#333,stroke-width:2px,color:#000
    classDef monitoring fill:#bbf,stroke:#333,stroke-width:2px,color:#000
    classDef analytics fill:#bfb,stroke:#333,stroke-width:2px,color:#000
    classDef tools fill:#fbb,stroke:#333,stroke-width:2px,color:#000

    class UI,API,DB,MQ,Agent core
    class Graphiti,Neo4j knowledge
    class Grafana,VictoriaMetrics,Jaeger,Loki,OTEL monitoring
    class Langfuse,ClickHouse,Redis,MinIO analytics
    class Scraper,PenTest tools
```

</details>

PentAGI 的架构设计为模块化、可扩展和安全的。以下是关键组件：

1. **核心服务**
   - 前端 UI：基于 React 的 Web 界面，使用 TypeScript 确保类型安全
   - 后端 API：基于 Go 的 REST 和 GraphQL API，支持 Bearer 令牌认证，用于编程访问
   - 向量存储：PostgreSQL 配合 pgvector，用于语义搜索和记忆存储
   - 任务队列：异步任务处理系统，确保可靠运行
   - AI 智能体：具有专门角色的多智能体系统，用于高效测试

2. **知识图谱**
   - Graphiti：知识图谱 API，用于语义关系跟踪和上下文理解
   - Neo4j：图数据库，用于存储和查询实体、动作和结果之间的关系
   - 自动捕获智能体响应和工具执行，以构建全面的知识库

3. **监控栈**
   - OpenTelemetry：统一的可观察性数据收集和关联
   - Grafana：实时可视化和警报仪表板
   - VictoriaMetrics：高性能时序指标存储
   - Jaeger：端到端分布式追踪，用于调试
   - Loki：可扩展的日志聚合和分析

4. **分析平台**
   - Langfuse：高级 LLM 可观察性和性能分析
   - ClickHouse：面向列的分析数据仓库
   - Redis：高速缓存和速率限制
   - MinIO：S3 兼容的对象存储，用于存储文件

5. **安全工具**
   - 网络爬虫：隔离的浏览器环境，用于安全的网络交互
   - 渗透测试工具：包含 20+ 专业安全工具的综合套件
   - 沙箱化执行：所有操作都在隔离的容器中运行

6. **记忆系统**
   - 长期记忆：知识和经验的持久化存储
   - 工作记忆：当前操作的主动上下文和目标
   - 情景记忆：历史动作和成功模式
   - 知识库：结构化的领域专业知识和工具能力
   - 上下文管理：使用链式摘要智能管理增长的 LLM 上下文窗口

系统使用 Docker 容器进行隔离和易于部署，为核心服务、监控和分析设置单独的网络，以确保适当的安全边界。每个组件都设计为可水平扩展，并可在生产环境中配置为高可用性。

## 🚀 快速开始

### 系统要求

- Docker 和 Docker Compose（或 Podman - 请参阅 [Podman 配置](#使用-podman-运行-pentagi)）
- 最低 2 vCPU
- 最低 4GB RAM
- 20GB 可用磁盘空间
- 用于下载镜像和更新的互联网访问

### 使用安装程序（推荐）

PentAGI 提供一个带有终端 UI 的交互式安装程序，用于简化的配置和部署。安装程序将引导您完成系统检查、LLM 提供商设置、搜索引擎配置和安全加固。

**支持的平台：**
- **Linux**：amd64 [下载](https://pentagi.com/downloads/linux/amd64/installer-latest.zip) | arm64 [下载](https://pentagi.com/downloads/linux/arm64/installer-latest.zip)
- **Windows**：amd64 [下载](https://pentagi.com/downloads/windows/amd64/installer-latest.zip)
- **macOS**：amd64（Intel）[下载](https://pentagi.com/downloads/darwin/amd64/installer-latest.zip) | arm64（M 系列）[下载](https://pentagi.com/downloads/darwin/arm64/installer-latest.zip)

**快速安装（Linux amd64）：**

```bash
# 创建安装目录
mkdir -p pentagi && cd pentagi

# 下载安装程序
wget -O installer.zip https://pentagi.com/downloads/linux/amd64/installer-latest.zip

# 解压
unzip installer.zip

# 运行交互式安装程序
./installer
```

**先决条件和权限：**

安装程序需要适当的权限才能与 Docker API 正确交互。默认情况下，它使用 Docker 套接字（`/var/run/docker.sock`），这需要以下条件之一：

- **选项 1（推荐用于生产环境）：** 以 root 身份运行安装程序：
  ```bash
  sudo ./installer
  ```

- **选项 2（开发环境）：** 通过将您的用户添加到 `docker` 组来授予其对 Docker 套接字的访问权限：
  ```bash
  # 将您的用户添加到 docker 组
  sudo usermod -aG docker $USER
  
  # 注销并重新登录，或立即激活该组
  newgrp docker
  
  # 验证 Docker 访问（应无需 sudo 运行）
  docker ps
  ```

  ⚠️ **安全提示：** 将用户添加到 `docker` 组会授予相当于 root 的权限。仅对受控环境中的受信任用户执行此操作。对于生产部署，请考虑使用无根 Docker 模式或使用 sudo 运行安装程序。

安装程序将执行以下操作：
1. **系统检查**：验证 Docker、网络连接和系统要求
2. **环境设置**：创建并配置 `.env` 文件，使用最佳默认值
3. **提供商配置**：设置 LLM 提供商（OpenAI、Anthropic、Gemini、Bedrock、Ollama、自定义）
4. **搜索引擎**：配置 DuckDuckGo、Google、Tavily、Traversaal、Perplexity、Sploitus、Searxng
5. **安全加固**：生成安全凭证并配置 SSL 证书
6. **部署**：使用 docker-compose 启动 PentAGI

**用于生产环境增强安全：**

对于生产部署或对安全敏感的环境，我们**强烈建议**使用分布式双节点架构，其中工作器操作在单独的服务器上隔离。这可以防止不受信任的代码执行和您主系统上的网络访问问题。

👉 **查看详细指南**：[工作器节点设置](examples/guides/worker_node.md)

双节点设置提供：
- **隔离执行**：工作器容器在专用硬件上运行
- **网络隔离**：用于渗透测试的单独网络边界
- **安全边界**：带有 TLS 身份验证的 Docker-in-Docker
- **OOB 攻击支持**：用于带外技术的专用端口范围

### 手动安装

1. 创建工作目录或克隆仓库：

```bash
mkdir pentagi && cd pentagi
```

2. 将 `.env.example` 复制到 `.env` 或下载它：

```bash
curl -o .env https://raw.githubusercontent.com/vxcontrol/pentagi/master/.env.example
```

3. 创建示例配置文件（`example.custom.provider.yml`、`example.ollama.provider.yml`）或下载它们：

```bash
curl -o example.custom.provider.yml https://raw.githubusercontent.com/vxcontrol/pentagi/master/examples/configs/custom-openai.provider.yml
curl -o example.ollama.provider.yml https://raw.githubusercontent.com/vxcontrol/pentagi/master/examples/configs/ollama-llama318b.provider.yml
```

4. 在 `.env` 文件中填写所需的 API 密钥。

```bash
# 必需：至少一个这些 LLM 提供商
OPEN_AI_KEY=your_openai_key
ANTHROPIC_API_KEY=your_anthropic_key
GEMINI_API_KEY=your_gemini_key

# 可选：AWS Bedrock 提供商（企业级模型）
BEDROCK_REGION=us-east-1
BEDROCK_ACCESS_KEY_ID=your_aws_access_key
BEDROCK_SECRET_ACCESS_KEY=your_aws_secret_key

# 可选：本地 LLM 提供商（零成本推理）
OLLAMA_SERVER_URL=http://localhost:11434
OLLAMA_SERVER_MODEL=your_model_name

# 可选：额外搜索功能
DUCKDUCKGO_ENABLED=true
SPLOITUS_ENABLED=true
GOOGLE_API_KEY=your_google_key
GOOGLE_CX_KEY=your_google_cx
TAVILY_API_KEY=your_tavily_key
TRAVERSAAL_API_KEY=your_traversaal_key
PERPLEXITY_API_KEY=your_perplexity_key
PERPLEXITY_MODEL=sonar-pro
PERPLEXITY_CONTEXT_SIZE=medium

# Searxng 元搜索引擎（聚合多个来源的结果）
SEARXNG_URL=http://your-searxng-instance:8080
SEARXNG_CATEGORIES=general
SEARXNG_LANGUAGE=
SEARXNG_SAFESEARCH=0
SEARXNG_TIME_RANGE=

# Graphiti 知识图谱设置
GRAPHITI_ENABLED=true
GRAPHITI_TIMEOUT=30
GRAPHITI_URL=http://graphiti:8000
GRAPHITI_MODEL_NAME=gpt-5-mini

# Neo4j 设置（由 Graphiti 栈使用）
NEO4J_USER=neo4j
NEO4J_DATABASE=neo4j
NEO4J_PASSWORD=devpassword
NEO4J_URI=bolt://neo4j:7687

# 助手配置
ASSISTANT_USE_AGENTS=false         # 创建新助手时代理使用的默认值
```

5. 更改 `.env` 文件中所有与安全相关的环境变量以提高安全性。

<details>
    <summary>安全相关的环境变量</summary>

### 主要安全设置
- `COOKIE_SIGNING_SALT` - Cookie 签名的盐值，更改为随机值
- `PUBLIC_URL` - 服务器的公共 URL（例如 `https://pentagi.example.com`）
- `SERVER_SSL_CRT` 和 `SERVER_SSL_KEY` - 您的现有 SSL 证书和密钥的自定义路径，用于 HTTPS（这些路径应在 docker-compose.yml 文件中用作卷挂载）

### 爬虫访问
- `SCRAPER_PUBLIC_URL` - 如果要为公共 URL 使用不同的爬虫服务器，则设置爬虫的公共 URL
- `SCRAPER_PRIVATE_URL` - 爬虫的私有 URL（docker-compose.yml 文件中的本地爬虫服务器用于访问本地 URL）

### 访问凭证
- `PENTAGI_POSTGRES_USER` 和 `PENTAGI_POSTGRES_PASSWORD` - PostgreSQL 凭证
- `NEO4J_USER` 和 `NEO4J_PASSWORD` - Neo4j 凭证（用于 Graphiti 知识图谱）

</details>

6. 如果要在 VSCode 或其他 IDE 中将 `.env` 文件用作 envFile 选项，请删除其中的所有内联注释：

```bash
perl -i -pe 's/\s+#.*$//' .env
```

7. 运行 PentAGI 栈：

```bash
curl -O https://raw.githubusercontent.com/vxcontrol/pentagi/master/docker-compose.yml
docker compose up -d
```

访问 [localhost:8443](https://localhost:8443) 以访问 PentAGI Web UI（默认为 `admin@pentagi.com` / `admin`）

> [!NOTE]
> 如果您遇到关于 `pentagi-network` 或 `observability-network` 或 `langfuse-network` 的错误，需要先运行 `docker-compose.yml` 创建这些网络，然后运行 `docker-compose-langfuse.yml`、`docker-compose-graphiti.yml` 和 `docker-compose-observability.yml` 来使用 Langfuse、Graphiti 和可观察性服务。
>
> 您必须至少设置一个语言模型提供商（OpenAI、Anthropic、Gemini、AWS Bedrock 或 Ollama）才能使用 PentAGI。AWS Bedrock 为来自领先 AI 公司的多个基础模型提供企业级访问，而 Ollama 在您有足够的计算资源时提供零成本的本地推理。搜索引擎的其他 API 密钥是可选的，但建议使用以获得更好的结果。
>
> `LLM_SERVER_*` 环境变量是实验性功能，将来会更改。现在您可以使用它们指定自定义 LLM 服务器 URL 和所有智能体类型的一个模型。
>
> `PROXY_URL` 是所有 LLM 提供商和外部搜索系统的全局代理 URL。您可以使用它来与外部网络隔离。
>
> `docker-compose.yml` 文件以 root 用户身份运行 PentAGI 服务，因为它需要访问 docker.sock 进行容器管理。如果您使用 TCP/IP 网络连接到 Docker 而不是套接字文件，可以删除 root 权限并使用默认的 `pentagi` 用户以提高安全性。

### 从外部网络访问 PentAGI

默认情况下，PentAGI 绑定到 `127.0.0.1`（仅限本地主机）以确保安全。要从网络上的其他机器访问 PentAGI，需要配置外部访问。

#### 配置步骤

1. **更新 `.env` 文件**，使用服务器的 IP 地址：

```bash
# 网络绑定 - 允许外部连接
PENTAGI_LISTEN_IP=0.0.0.0
PENTAGI_LISTEN_PORT=8443

# 公共 URL - 使用实际的服务器 IP 或主机名
# 将 192.168.1.100 替换为您的服务器 IP 地址
PUBLIC_URL=https://192.168.1.100:8443

# CORS 源 - 列出所有将访问 PentAGI 的 URL
# 包括 localhost 用于本地访问，以及您的服务器 IP 用于外部访问
CORS_ORIGINS=https://localhost:8443,https://192.168.1.100:8443
```

> [!IMPORTANT]
> - 将 `192.168.1.100` 替换为您的实际服务器 IP 地址
> - 请勿在 `PUBLIC_URL` 或 `CORS_ORIGINS` 中使用 `0.0.0.0` - 使用实际的 IP 地址
> - 在 `CORS_ORIGINS` 中包括 localhost 和您的服务器 IP，以增加灵活性

2. **重新创建容器**以应用更改：

```bash
docker compose down
docker compose up -d --force-recreate
```

3. **验证端口绑定：**

```bash
docker ps | grep pentagi
```

您应该看到 `0.0.0.0:8443->8443/tcp` 或 `:::8443->8443/tcp`。

如果您看到 `127.0.0.1:8443->8443/tcp`，说明环境变量未被识别。在这种情况下，直接编辑 `docker-compose.yml` 第 31 行：

```yaml
ports:
  - "0.0.0.0:8443:8443"
```

然后再次重新创建容器。

4. **配置防火墙**以允许端口 8443 上的传入连接：

```bash
# Ubuntu/Debian 使用 UFW
sudo ufw allow 8443/tcp
sudo ufw reload

# CentOS/RHEL 使用 firewalld
sudo firewall-cmd --permanent --add-port=8443/tcp
sudo firewall-cmd --reload
```

5. **访问 PentAGI：**

- **本地访问：** `https://localhost:8443`
- **网络访问：** `https://your-server-ip:8443`

> [!NOTE]
> 通过 IP 地址访问时，您需要在浏览器中接受自签名 SSL 证书警告。

---

### 使用 Podman 运行 PentAGI

PentAGI 完全支持 Podman 作为 Docker 的替代品。但是，在以**无根模式使用 Podman**时，爬虫服务需要特殊配置，因为无根容器无法绑定特权端口（1024 以下的端口）。

#### Podman 无根配置

默认的爬虫配置使用端口 443（HTTPS），这是一个特权端口。对于 Podman 无根模式，将爬虫重新配置为使用非特权端口：

**1. 编辑 `docker-compose.yml`** - 修改 `scraper` 服务（约第 199 行）：

```yaml
scraper:
  image: vxcontrol/scraper:latest
  restart: unless-stopped
  container_name: scraper
  hostname: scraper
  expose:
    - 3000/tcp  # 从 443 更改为 3000
  ports:
    - "${SCRAPER_LISTEN_IP:-127.0.0.1}:${SCRAPER_LISTEN_PORT:-9443}:3000"  # 映射到端口 3000
  environment:
    - MAX_CONCURRENT_SESSIONS=${LOCAL_SCRAPER_MAX_CONCURRENT_SESSIONS:-10}
    - USERNAME=${LOCAL_SCRAPER_USERNAME:-someuser}
    - PASSWORD=${LOCAL_SCRAPER_PASSWORD:-somepass}
  logging:
    options:
      max-size: 50m
      max-file: "7"
  volumes:
    - scraper-ssl:/usr/src/app/ssl
  networks:
    - pentagi-network
  shm_size: 2g
```

**2. 更新 `.env` 文件** - 更改爬虫 URL 以使用 HTTP 和端口 3000：

```bash
# Podman 无根模式的爬虫配置
SCRAPER_PRIVATE_URL=http://someuser:somepass@scraper:3000/
LOCAL_SCRAPER_USERNAME=someuser
LOCAL_SCRAPER_PASSWORD=somepass
```

> [!IMPORTANT]
> Podman 的关键更改：
> - 对 `SCRAPER_PRIVATE_URL` 使用 **HTTP** 而不是 HTTPS
> - 使用端口 **3000** 而不是 443
> - 更改内部 `expose` 为 `3000/tcp`
> - 更新端口映射以将目标改为 `3000` 而不是 `443`

**3. 重新创建容器：**

```bash
podman-compose down
podman-compose up -d --force-recreate
```

**4. 测试爬虫连接性：**

```bash
# 从 pentagi 容器内部测试
podman exec -it pentagi wget -O- "http://someuser:somepass@scraper:3000/html?url=http://example.com"
```

如果您看到 HTML 输出，则爬虫工作正常。

#### Podman 有根模式

如果您以有根模式（使用 sudo）运行 Podman，则可以使用默认配置而无需修改。爬虫将在端口 443 上按预期工作。

#### Docker 兼容性

所有 Podman 配置都完全与 Docker 兼容。非特权端口方法在两种容器运行时上的工作方式相同。

### 助手配置

PentAGI 允许您配置助手的默认行为：

| 变量名               | 默认值 | 描述                                                             |
| ---------------------- | ------- | ----------------------------------------------------------------------- |
| `ASSISTANT_USE_AGENTS` | `false` | 控制创建新助手时代理使用的默认值 |

`ASSISTANT_USE_AGENTS` 设置会影响在 UI 中创建新助手时"使用智能体"切换按钮的初始状态：
- `false`（默认）：新助手创建时默认禁用智能体委托
- `true`：新助手创建时默认启用智能体委托

请注意，用户始终可以通过在 UI 中创建或编辑助手时切换"使用智能体"按钮来覆盖此设置。此环境变量仅控制初始默认状态。

## 🔌 API 访问

PentAGI 通过 REST 和 GraphQL API 提供全面的编程访问，允许您将渗透测试工作流程集成到自动化管道、CI/CD 流程和自定义应用程序中。

### 生成 API 令牌

API 令牌通过 PentAGI Web 界面进行管理：

1. 导航到 Web UI 中的 **设置** → **API 令牌**
2. 点击 **创建令牌** 以生成新的 API 令牌
3. 配置令牌属性：
   - **名称**（可选）：令牌的描述性名称
   - **到期日期**：令牌何时到期（最少 1 分钟，最多 3 年）
4. 点击 **创建** 并 **立即复制令牌** - 出于安全原因，它只会显示一次
5. 在 API 请求中使用该令牌作为 Bearer 令牌

每个令牌都与您的用户帐户关联，并继承您角色的权限。

### 使用 API 令牌

在 HTTP 请求的 `Authorization` 标头中包含 API 令牌：

```bash
# GraphQL API 示例
curl -X POST https://your-pentagi-instance:8443/api/v1/graphql \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query": "{ flows { id title status } }"}'

# REST API 示例
curl https://your-pentagi-instance:8443/api/v1/flows \
  -H "Authorization: Bearer YOUR_API_TOKEN"
```

### API 探索和测试

PentAGI 提供交互式文档用于探索和测试 API 端点：

#### GraphQL Playground

访问 `https://your-pentagi-instance:8443/api/v1/graphql/playground` 的 GraphQL Playground

1. 点击底部的 **HTTP Headers** 选项卡
2. 添加您的授权标头：
   ```json
   {
     "Authorization": "Bearer YOUR_API_TOKEN"
   }
   ```
3. 探索模式、运行查询和测试变更

#### Swagger UI

访问 `https://your-pentagi-instance:8443/api/v1/swagger/index.html` 的 REST API 文档

1. 点击 **授权** 按钮
2. 输入您的令牌，格式为：`Bearer YOUR_API_TOKEN`
3. 点击 **授权** 应用
4. 直接从 Swagger UI 测试端点

### 生成 API 客户端

您可以使用 PentAGI 附带的架构文件为首选编程语言生成类型安全的 API 客户端：

#### GraphQL 客户端

GraphQL 架构位于：
- **Web UI**：导航到设置下载 `schema.graphqls`
- **直接文件**：仓库中的 `backend/pkg/graph/schema.graphqls`

使用以下工具生成客户端：
- **GraphQL Code Generator** (JavaScript/TypeScript)：[https://the-guild.dev/graphql/codegen](https://the-guild.dev/graphql/codegen)
- **genqlient** (Go)：[https://github.com/Khan/genqlient](https://github.com/Khan/genqlient)
- **Apollo iOS** (Swift)：[https://www.apollographql.com/docs/ios](https://www.apollographql.com/docs/ios)

#### REST API 客户端

OpenAPI 规范位于：
- **Swagger JSON**：`https://your-pentagi-instance:8443/api/v1/swagger/doc.json`
- **Swagger YAML**：在 `backend/pkg/server/docs/swagger.yaml` 中可用

使用以下工具生成客户端：
- **OpenAPI Generator**：[https://openapi-generator.tech](https://openapi-generator.tech)
  ```bash
  openapi-generator-cli generate \
    -i https://your-pentagi-instance:8443/api/v1/swagger/doc.json \
    -g python \
    -o ./pentagi-client
  ```

- **Swagger Codegen**：[https://github.com/swagger-api/swagger-codegen](https://github.com/swagger-api/swagger-codegen)
  ```bash
  swagger-codegen generate \
    -i https://your-pentagi-instance:8443/api/v1/swagger/doc.json \
    -l typescript-axios \
    -o ./pentagi-client
  ```

- **swagger-typescript-api** (TypeScript)：[https://github.com/acacode/swagger-typescript-api](https://github.com/acacode/swagger-typescript-api)
  ```bash
  npx swagger-typescript-api \
    -p https://your-pentagi-instance:8443/api/v1/swagger/doc.json \
    -o ./src/api \
    -n pentagi-api.ts
  ```

### API 使用示例

<details>
<summary><b>创建新流程（GraphQL）</b></summary>

```graphql
mutation CreateFlow {
  createFlow(
    modelProvider: "openai"
    input: "测试 https://example.com 的安全性"
  ) {
    id
    title
    status
    createdAt
  }
}
```

</details>

<details>
<summary><b>列出流程（REST API）</b></summary>

```bash
curl https://your-pentagi-instance:8443/api/v1/flows \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  | jq '.flows[] | {id, title, status}'
```

</details>

<details>
<summary><b>Python 客户端示例</b></summary>

```python
import requests

class PentAGIClient:
    def __init__(self, base_url, api_token):
        self.base_url = base_url
        self.headers = {
            "Authorization": f"Bearer {api_token}",
            "Content-Type": "application/json"
        }
    
    def create_flow(self, provider, target):
        query = """
        mutation CreateFlow($provider: String!, $input: String!) {
          createFlow(modelProvider: $provider, input: $input) {
            id
            title
            status
          }
        }
        """
        response = requests.post(
            f"{self.base_url}/api/v1/graphql",
            json={
                "query": query,
                "variables": {
                    "provider": provider,
                    "input": target
                }
            },
            headers=self.headers
        )
        return response.json()
    
    def get_flows(self):
        response = requests.get(
            f"{self.base_url}/api/v1/flows",
            headers=self.headers
        )
        return response.json()

# 使用
client = PentAGIClient(
    "https://your-pentagi-instance:8443",
    "your_api_token_here"
)

# 创建新流程
flow = client.create_flow("openai", "扫描 https://example.com 的漏洞")
print(f"已创建流程: {flow}")

# 列出所有流程
flows = client.get_flows()
print(f"总流程数: {len(flows['flows'])}")
```

</details>

<details>
<summary><b>TypeScript 客户端示例</b></summary>

```typescript
import axios, { AxiosInstance } from 'axios';

interface Flow {
  id: string;
  title: string;
  status: string;
  createdAt: string;
}

class PentAGIClient {
  private client: AxiosInstance;

  constructor(baseURL: string, apiToken: string) {
    this.client = axios.create({
      baseURL: `${baseURL}/api/v1`,
      headers: {
        'Authorization': `Bearer ${apiToken}`,
        'Content-Type': 'application/json',
      },
    });
  }

  async createFlow(provider: string, input: string): Promise<Flow> {
    const query = `
      mutation CreateFlow($provider: String!, $input: String!) {
        createFlow(modelProvider: $provider, input: $input) {
          id
          title
          status
          createdAt
        }
      }
    `;

    const response = await this.client.post('/graphql', {
      query,
      variables: { provider, input },
    });

    return response.data.data.createFlow;
  }

  async getFlows(): Promise<Flow[]> {
    const response = await this.client.get('/flows');
    return response.data.flows;
  }

  async getFlow(flowId: string): Promise<Flow> {
    const response = await this.client.get(`/flows/${flowId}`);
    return response.data;
  }
}

// 使用
const client = new PentAGIClient(
  'https://your-pentagi-instance:8443',
  'your_api_token_here'
);

// 创建新流程
const flow = await client.createFlow(
  'openai',
  '对 https://example.com 执行渗透测试'
);
console.log('已创建流程:', flow);

// 列出所有流程
const flows = await client.getFlows();
console.log(`总流程数: ${flows.length}`);
```

</details>

### 安全最佳实践

使用 API 令牌时：

- **切勿将令牌提交到版本控制** - 使用环境变量或密钥管理
- **定期轮换令牌** - 设置适当的到期日期并定期创建新令牌
- **为不同应用程序使用单独的令牌** - 这样可以更容易在需要时撤销访问权限
- **监控令牌使用情况** - 在设置页面查看 API 令牌活动
- **撤销未使用的令牌** - 禁用或删除不再需要的令牌
- **仅使用 HTTPS** - 切勿通过未加密的连接发送 API 令牌

### 令牌管理

- **查看令牌**：在设置 → API 令牌中查看所有活动令牌
- **编辑令牌**：更新令牌名称或撤销令牌
- **删除令牌**：永久删除令牌（此操作无法撤消）
- **令牌 ID**：每个令牌都有唯一的 ID，可以复制以供参考

令牌列表显示：
- 令牌名称（如果提供）
- 令牌 ID（唯一标识符）
- 状态（活动/已撤销/已过期）
- 创建日期
- 到期日期

### 自定义 LLM 提供商配置

使用 `LLM_SERVER_*` 变量与自定义 LLM 提供商时，您可以微调请求中使用的推理格式：

| 变量名                        | 默认值 | 描述                                                                             |
| ------------------------------- | ------- | --------------------------------------------------------------------------------------- |
| `LLM_SERVER_URL`                |         | 自定义 LLM API 端点的基础 URL                                                |
| `LLM_SERVER_KEY`                |         | 自定义 LLM 提供商的 API 密钥                                                     |
| `LLM_SERVER_MODEL`              |         | 要使用的默认模型（可以在提供商配置中覆盖）                             |
| `LLM_SERVER_CONFIG_PATH`        |         | 特定智能体模型的 YAML 配置文件路径                           |
| `LLM_SERVER_PROVIDER`           |         | 模型名称的提供商名称前缀（例如，用于 LiteLLM 代理的 `openrouter`、`deepseek`） |
| `LLM_SERVER_LEGACY_REASONING`   | `false` | 控制在 API 请求中使用的推理格式                                               |
| `LLM_SERVER_PRESERVE_REASONING` | `false` | 在多轮对话中保留推理内容（某些提供商需要）     |

`LLM_SERVER_PROVIDER` 设置对于使用 **LiteLLM 代理**特别有用，该代理向模型名称添加提供商前缀。例如，通过 LiteLLM 连接到 Moonshot API 时，`kimi-2.5` 等模型会变成 `moonshot/kimi-2.5`。通过设置 `LLM_SERVER_PROVIDER=moonshot`，您可以对直接 API 访问和 LiteLLM 代理访问使用相同的提供商配置文件，而无需修改。

`LLM_SERVER_LEGACY_REASONING` 设置影响推理参数如何发送到 LLM：
- `false`（默认）：使用现代格式，将推理作为具有 `max_tokens` 参数的结构化对象发送
- `true`：使用传统格式，基于字符串的 `reasoning_effort` 参数

此设置对于与不同的 LLM 提供商一起工作非常重要，因为它们可能期望 API 请求中有不同的推理格式。如果您使用自定义提供商时遇到推理相关错误，请尝试更改此设置。

`LLM_SERVER_PRESERVE_REASONING` 设置控制推理内容是否在多轮对话中保留：
- `false`（默认）：推理内容不在对话历史中保留
- `true`：推理内容被保留并在后续 API 调用中发送

某些 LLM 提供商（例如 Moonshot）需要此设置，当多轮对话中未包含推理内容时，它们会返回类似"thinking is enabled but reasoning_content is missing in assistant tool call message"的错误。如果您的提供商需要保留推理内容，请启用此设置。

### 本地 LLM 提供商配置

PentAGI 支持 Ollama 进行本地 LLM 推理，提供零成本操作和增强的隐私：

| 变量名                            | 默认值                     | 描述                             |
| ----------------------------------- | --------------------------- | --------------------------------------- |
| `OLLAMA_SERVER_URL`                 |                             | 您的 Ollama 服务器 URL               |
| `OLLAMA_SERVER_MODEL`               | `llama3.1:8b-instruct-q8_0` | 推理的默认模型             |
| `OLLAMA_SERVER_CONFIG_PATH`         |                             | 自定义智能体配置文件的路径 |
| `OLLAMA_SERVER_PULL_MODELS_TIMEOUT` | `600`                       | 模型下载超时（秒）   |
| `OLLAMA_SERVER_PULL_MODELS_ENABLED` | `false`                     | 启动时自动下载模型         |
| `OLLAMA_SERVER_LOAD_MODELS_ENABLED` | `false`                     | 查询服务器以获取可用模型       |

配置示例：

```bash
# 使用默认模型的基本 Ollama 设置
OLLAMA_SERVER_URL=http://localhost:11434
OLLAMA_SERVER_MODEL=llama3.1:8b-instruct-q8_0

# 具有自动拉取和模型发现的生产设置
OLLAMA_SERVER_URL=http://ollama-server:11434
OLLAMA_SERVER_PULL_MODELS_ENABLED=true
OLLAMA_SERVER_PULL_MODELS_TIMEOUT=900
OLLAMA_SERVER_LOAD_MODELS_ENABLED=true

# 使用特定于智能体的模型进行自定义配置
OLLAMA_SERVER_CONFIG_PATH=/path/to/ollama-config.yml

# Docker 容器内的默认配置文件
OLLAMA_SERVER_CONFIG_PATH=/opt/pentagi/conf/ollama-llama318b.provider.yml
```

**性能考虑：**

- **模型发现**（`OLLAMA_SERVER_LOAD_MODELS_ENABLED=true`）：查询 Ollama API 增加约 1-2 秒的启动延迟
- **自动拉取**（`OLLAMA_SERVER_PULL_MODELS_ENABLED=true`）：首次启动可能需要几分钟下载模型
- **拉取超时**（`OLLAMA_SERVER_PULL_MODELS_TIMEOUT=900`）：15 分钟，以秒为单位
- **静态配置**：禁用这两个标志并在配置文件中指定模型以获得最快的启动速度

#### 创建具有扩展上下文的自定义 Ollama 模型

PentAGI 需要具有比默认 Ollama 配置更大的上下文窗口的模型。您需要通过 Modelfiles 创建具有增加的 `num_ctx` 参数的自定义模型。虽然典型的智能体工作流消耗大约 64K 令牌，但 PentAGI 使用 110K 上下文大小以确保安全余量和处理复杂的渗透测试场景。

**重要**：`num_ctx` 参数只能在通过 Modelfile 创建模型时设置 - 它不能在创建后更改或在运行时覆盖。

##### 示例：具有扩展上下文的 Qwen3 32B FP16

创建一个名为 `Modelfile_qwen3_32b_fp16_tc` 的 Modelfile：

```dockerfile
FROM qwen3:32b-fp16
PARAMETER num_ctx 110000
PARAMETER temperature 0.3
PARAMETER top_p 0.8
PARAMETER min_p 0.0
PARAMETER top_k 20
PARAMETER repeat_penalty 1.1
```

构建自定义模型：

```bash
ollama create qwen3:32b-fp16-tc -f Modelfile_qwen3_32b_fp16_tc
```

##### 示例：具有扩展上下文的 QwQ 32B FP16

创建一个名为 `Modelfile_qwq_32b_fp16_tc` 的 Modelfile：

```dockerfile
FROM qwq:32b-fp16
PARAMETER num_ctx 110000
PARAMETER temperature 0.2
PARAMETER top_p 0.7
PARAMETER min_p 0.0
PARAMETER top_k 40
PARAMETER repeat_penalty 1.2
```

构建自定义模型：

```bash
ollama create qwq:32b-fp16-tc -f Modelfile_qwq_32b_fp16_tc
```

> **注意**：QwQ 32B FP16 模型大约需要 **71.3 GB 显存**进行推理。在尝试使用此模型之前，请确保您的系统具有足够的 GPU 内存。

这些自定义模型在 Docker 镜像中包含的预构建提供商配置文件（`ollama-qwen332b-fp16-tc.provider.yml` 和 `ollama-qwq32b-fp16-tc.provider.yml`）中被引用，位于 `/opt/pentagi/conf/`。

### OpenAI 提供商配置

PentAGI 支持 OpenAI 的先进语言模型，包括最新的具有推理功能的 o 系列模型，专为复杂的分析任务设计：

| 变量名             | 默认值                     | 描述                 |
| -------------------- | --------------------------- | --------------------------- |
| `OPEN_AI_KEY`        |                             | OpenAI 服务的 API 密钥 |
| `OPEN_AI_SERVER_URL` | `https://api.openai.com/v1` | OpenAI API 端点         |

配置示例：

```bash
# 基本 OpenAI 设置
OPEN_AI_KEY=your_openai_api_key
OPEN_AI_SERVER_URL=https://api.openai.com/v1

# 使用代理以增强安全性
OPEN_AI_KEY=your_openai_api_key
PROXY_URL=http://your-proxy:8080
```

OpenAI 提供商提供尖端功能，包括：

- **推理模型**：先进的 o 系列模型（o1、o3、o4-mini），具有逐步分析思维
- **最新的 GPT-4.1 系列**：针对复杂安全研究和漏洞开发优化的旗舰模型
- **经济实惠的选项**：从用于高容量扫描的 nano 模型到用于深度分析的强大推理模型
- **多功能性能**：快速、智能的模型，非常适合多步安全分析和渗透测试
- **久经考验的可靠性**：在各种安全场景中具有一致性能的行业领先模型

系统会根据任务复杂性自动选择适当的 OpenAI 模型，以优化性能和成本效益。

### Anthropic 提供商配置

PentAGI 与 Anthropic 的 Claude 模型集成，以其卓越的安全性、推理能力和对复杂安全环境的复杂理解而闻名：

| 变量名               | 默认值                        | 描述                    |
| ---------------------- | ------------------------------ | ------------------------------ |
| `ANTHROPIC_API_KEY`    |                                | Anthropic 服务的 API 密钥 |
| `ANTHROPIC_SERVER_URL` | `https://api.anthropic.com/v1` | Anthropic API 端点         |

配置示例：

```bash
# 基本 Anthropic 设置
ANTHROPIC_API_KEY=your_anthropic_api_key
ANTHROPIC_SERVER_URL=https://api.anthropic.com/v1

# 使用代理以确保安全环境
ANTHROPIC_API_KEY=your_anthropic_api_key
PROXY_URL=http://your-proxy:8080
```

Anthropic 提供商提供卓越的功能，包括：

- **高级推理**：Claude 4 系列，具有用于复杂渗透测试的卓越推理
- **扩展思考**：Claude 3.7，具有用于系统化安全研究的逐步思考能力
- **高速性能**：Claude 3.5 Haiku，用于快速漏洞扫描和实时监控
- **全面分析**：用于复杂安全分析和威胁搜寻的 Claude Sonnet 模型
- **安全优先设计**：确保负责任安全测试实践的内置安全机制

系统利用 Claude 对安全环境的高级理解，提供全面和负责任的渗透测试指导。

### Google AI (Gemini) 提供商配置

PentAGI 通过 Google AI API 支持 Google 的 Gemini 模型，提供最先进的推理功能和多模态功能：

| 变量名            | 默认值                                     | 描述                    |
| ------------------- | ------------------------------------------- | ------------------------------ |
| `GEMINI_API_KEY`    |                                             | Google AI 服务的 API 密钥 |
| `GEMINI_SERVER_URL` | `https://generativelanguage.googleapis.com` | Google AI API 端点         |

配置示例：

```bash
# 基本 Gemini 设置
GEMINI_API_KEY=your_gemini_api_key
GEMINI_SERVER_URL=https://generativelanguage.googleapis.com

# 使用代理
GEMINI_API_KEY=your_gemini_api_key
PROXY_URL=http://your-proxy:8080
```

Gemini 提供商提供高级功能，包括：

- **思考功能**：先进的推理模型（Gemini 2.5 系列），具有逐步分析
- **多模态支持**：用于全面安全评估的文本和图像处理
- **大上下文窗口**：高达 2M 令牌，用于分析大型代码库和文档
- **经济实惠的选项**：从高性能专业模型到经济实用的 flash 变体
- **安全专注模型**：针对渗透测试工作流程优化的专业配置

系统会根据智能体需求自动选择适当的 Gemini 模型，平衡性能、功能和成本效益。

### AWS Bedrock 提供商配置

PentAGI 与 Amazon Bedrock 集成，提供来自领先 AI 公司的基础模型访问权限，包括 Anthropic、AI21、Cohere、Meta 和 Amazon 自己的模型：

| 变量名                    | 默认值     | 描述                                             |
| --------------------------- | ----------- | ------------------------------------------------------- |
| `BEDROCK_REGION`            | `us-east-1` | Bedrock 服务的 AWS 区域                          |
| `BEDROCK_ACCESS_KEY_ID`     |             | 用于身份验证的 AWS 访问密钥 ID                    |
| `BEDROCK_SECRET_ACCESS_KEY` |             | 用于身份验证的 AWS 秘密访问密钥                |
| `BEDROCK_SESSION_TOKEN`     |             | AWS 会话令牌，作为身份验证的替代方式 |
| `BEDROCK_SERVER_URL`        |             | 可选的自定义 Bedrock 端点 URL                    |

配置示例：

```bash
# 使用凭证的基本 AWS Bedrock 设置
BEDROCK_REGION=us-east-1
BEDROCK_ACCESS_KEY_ID=your_aws_access_key
BEDROCK_SECRET_ACCESS_KEY=your_aws_secret_key

# 使用代理以增强安全性
BEDROCK_REGION=us-east-1
BEDROCK_ACCESS_KEY_ID=your_aws_access_key
BEDROCK_SECRET_ACCESS_KEY=your_aws_secret_key
PROXY_URL=http://your-proxy:8080

# 使用自定义端点（用于 VPC 端点或测试）
BEDROCK_REGION=us-east-1
BEDROCK_ACCESS_KEY_ID=your_aws_access_key
BEDROCK_SECRET_ACCESS_KEY=your_aws_secret_key
BEDROCK_SERVER_URL=https://bedrock-runtime.us-east-1.amazonaws.com
```

> [!IMPORTANT]
> **AWS Bedrock 速率限制警告**
>
> PentAGI 的 AWS Bedrock 默认配置使用两个主要模型：
> - `us.anthropic.claude-sonnet-4-20250514-v1:0`（用于大多数智能体）- **每分钟 2 个请求**，适用于新 AWS 帐户
> - `us.anthropic.claude-3-5-haiku-20241022-v1:0`（用于简单任务）- **每分钟 20 个请求**，适用于新 AWS 帐户
>
> 这些默认速率限制对于舒适的渗透测试场景**极其严格**，将显着影响您的工作流程。我们**强烈建议**：
>
> 1. 通过 AWS Service Quotas 控制台**请求增加您的 AWS Bedrock 模型的配额**
> 2. **使用按小时计费的预配置吞吐量模型**以满足更高的吞吐量要求
> 3. **切换到具有更高默认配额的替代模型**（例如 Amazon Nova 系列、Meta Llama 模型）
> 4. **考虑使用不同的 LLM 提供商**（OpenAI、Anthropic、Gemini），如果您需要立即获得高吞吐量访问
>
> 如果没有足够的速率限制，您可能会遇到频繁的延迟、超时和测试性能下降。

AWS Bedrock 提供商提供全面的功能，包括：

- **多提供商访问**：通过单一界面访问来自 Anthropic (Claude)、AI21 (Jamba)、Cohere (Command)、Meta (Llama)、Amazon (Nova, Titan) 和 DeepSeek (R1) 的模型
- **高级推理**：支持具有逐步思考的 Claude 4 和其他能够推理的模型
- **多模态模型**：支持文本、图像和视频处理的 Amazon Nova 系列，用于全面的安全分析
- **企业安全性**：AWS 原生安全控制、VPC 集成和合规认证
- **成本优化**：广泛的各种尺寸和功能的模型，用于经济实惠的渗透测试
- **区域可用性**：在您首选的 AWS 区域中部署模型，以实现数据驻留和性能
- **高性能**：通过 AWS 全球基础设施实现低延迟推理

系统会根据任务复杂性和需求自动选择适当的 Bedrock 模型，利用全部可用基础模型以获得最佳安全测试结果。

> [!WARNING]
> **Converse API 要求**
>
> PentAGI 使用 **Amazon Bedrock Converse API** 进行模型交互，该 API 要求模型支持以下功能：
> - ✅ **Converse** - 基本对话 API 支持
> - ✅ **ConverseStream** - 流式响应支持
> - ✅ **工具使用** - 用于渗透测试工具的函数调用功能
> - ✅ **流式工具使用** - 实时工具执行反馈
>
> **在选择模型之前**，请验证它们的功能支持：[支持的模型和模型功能](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference-supported-models-features.html)
>
> ⚠️ **重要**：某些模型（如 AI21 Jurassic-2 和 Cohere Command (Text)）的**聊天支持有限**，可能无法与 PentAGI 的多轮对话工作流程正常工作。
>
> **注意**：AWS 凭证也可以通过 IAM 角色、环境变量或 AWS 凭证文件按照标准 AWS SDK 身份验证模式提供。确保您的 AWS 帐户具有适当的 Amazon Bedrock 服务访问权限。

有关高级配置选项和详细设置说明，请访问我们的[文档](https://docs.pentagi.com)。

## 🔧 高级配置

### Langfuse 集成

Langfuse 提供高级功能，用于监控和分析 AI 智能体操作。

1. 在现有的 `.env` 文件中配置 Langfuse 环境变量。

<details>
    <summary>有价值的 Langfuse 环境变量</summary>

### 数据库凭证
- `LANGFUSE_POSTGRES_USER` 和 `LANGFUSE_POSTGRES_PASSWORD` - Langfuse PostgreSQL 凭证
- `LANGFUSE_CLICKHOUSE_USER` 和 `LANGFUSE_CLICKHOUSE_PASSWORD` - ClickHouse 凭证
- `LANGFUSE_REDIS_AUTH` - Redis 密码

### 加密和安全密钥
- `LANGFUSE_SALT` - Langfuse Web UI 中用于哈希的盐值
- `LANGFUSE_ENCRYPTION_KEY` - 加密密钥（32 字节十六进制）
- `LANGFUSE_NEXTAUTH_SECRET` - NextAuth 的密钥

### 管理员凭证
- `LANGFUSE_INIT_USER_EMAIL` - 管理员电子邮件
- `LANGFUSE_INIT_USER_PASSWORD` - 管理员密码
- `LANGFUSE_INIT_USER_NAME` - 管理员用户名

### API 密钥和令牌
- `LANGFUSE_INIT_PROJECT_PUBLIC_KEY` - 项目公钥（也从 PentAGI 端使用）
- `LANGFUSE_INIT_PROJECT_SECRET_KEY` - 项目密钥（也从 PentAGI 端使用）

### S3 存储
- `LANGFUSE_S3_ACCESS_KEY_ID` - S3 访问密钥 ID
- `LANGFUSE_S3_SECRET_ACCESS_KEY` - S3 秘密访问密钥

</details>

2. 在 `.env` 文件中启用 PentAGI 服务与 Langfuse 的集成。

```bash
LANGFUSE_BASE_URL=http://langfuse-web:3000
LANGFUSE_PROJECT_ID= # 默认值：来自 ${LANGFUSE_INIT_PROJECT_ID}
LANGFUSE_PUBLIC_KEY= # 默认值：来自 ${LANGFUSE_INIT_PROJECT_PUBLIC_KEY}
LANGFUSE_SECRET_KEY= # 默认值：来自 ${LANGFUSE_INIT_PROJECT_SECRET_KEY}
```

3. 运行 Langfuse 栈：

```bash
curl -O https://raw.githubusercontent.com/vxcontrol/pentagi/master/docker-compose-langfuse.yml
docker compose -f docker-compose.yml -f docker-compose-langfuse.yml up -d
```

访问 [localhost:4000](http://localhost:4000) 以访问 Langfuse Web UI，使用 `.env` 文件中的凭证：

- `LANGFUSE_INIT_USER_EMAIL` - 管理员电子邮件
- `LANGFUSE_INIT_USER_PASSWORD` - 管理员密码

### 监控和可观察性

用于详细系统操作跟踪，可与监控工具集成。

1. 在 `.env` 文件中启用 PentAGI 与 OpenTelemetry 和所有可观察性服务的集成。

```bash
OTEL_HOST=otelcol:8148
```

2. 运行可观察性栈：

```bash
curl -O https://raw.githubusercontent.com/vxcontrol/pentagi/master/docker-compose-observability.yml
docker compose -f docker-compose.yml -f docker-compose-observability.yml up -d
```

访问 [localhost:3000](http://localhost:3000) 以访问 Grafana Web UI。

> [!NOTE]
> 如果要将可观察性栈与 Langfuse 一起使用，需要在 `.env` 文件中启用集成，将 `LANGFUSE_OTEL_EXPORTER_OTLP_ENDPOINT` 设置为 `http://otelcol:4318`。
>
> 要运行所有可用栈（Langfuse、Graphiti 和可观察性）：
>
> ```bash
> docker compose -f docker-compose.yml -f docker-compose-langfuse.yml -f docker-compose-graphiti.yml -f docker-compose-observability.yml up -d
> ```
>
> 您还可以在 shell 中注册这些命令的别名以更快地运行：
>
> ```bash
> alias pentagi="docker compose -f docker-compose.yml -f docker-compose-langfuse.yml -f docker-compose-graphiti.yml -f docker-compose-observability.yml"
> alias pentagi-up="docker compose -f docker-compose.yml -f docker-compose-langfuse.yml -f docker-compose-graphiti.yml -f docker-compose-observability.yml up -d"
> alias pentagi-down="docker compose -f docker-compose.yml -f docker-compose-langfuse.yml -f docker-compose-graphiti.yml -f docker-compose-observability.yml down"
> ```

### 知识图谱集成 (Graphiti)

PentAGI 与 [Graphiti](https://github.com/vxcontrol/pentagi-graphiti) 集成，这是一个由 Neo4j 驱动的时序知识图谱系统，为 AI 智能体操作提供高级语义理解和关系跟踪。vxcontrol 分支提供了针对渗透测试目的的自定义实体和边类型。

#### 什么是 Graphiti？

Graphiti 自动从智能体交互中提取和存储结构化知识，构建实体、关系和时序上下文的图谱。这使得：

- **语义记忆**：存储和调用工具、目标、漏洞和技术之间的关系
- **上下文理解**：跟踪不同的渗透测试操作如何随时间相互关联
- **知识重用**：从过去的渗透测试中学习，并将见解应用于新评估
- **高级查询**：搜索复杂模式，例如"对类似目标有效的工具是什么？"

#### 启用 Graphiti

Graphiti 知识图谱是**可选的**，默认情况下禁用。要启用它：

1. 在 `.env` 文件中配置 Graphiti 环境变量：

```bash
## Graphiti 知识图谱设置
GRAPHITI_ENABLED=true
GRAPHITI_TIMEOUT=30
GRAPHITI_URL=http://graphiti:8000
GRAPHITI_MODEL_NAME=gpt-5-mini

# Neo4j 设置（由 Graphiti 栈使用）
NEO4J_USER=neo4j
NEO4J_DATABASE=neo4j
NEO4J_PASSWORD=devpassword
NEO4J_URI=bolt://neo4j:7687

# OpenAI API 密钥（Graphiti 用于实体提取所需）
OPEN_AI_KEY=your_openai_api_key
```

2. 与主要的 PentAGI 服务一起运行 Graphiti 栈：

```bash
# 如果需要，下载 Graphiti compose 文件
curl -O https://raw.githubusercontent.com/vxcontrol/pentagi/master/docker-compose-graphiti.yml

# 启动带有 Graphiti 的 PentAGI
docker compose -f docker-compose.yml -f docker-compose-graphiti.yml up -d
```

3. 验证 Graphiti 正在运行：

```bash
# 检查服务运行状况
docker compose -f docker-compose.yml -f docker-compose-graphiti.yml ps graphiti neo4j

# 查看 Graphiti 日志
docker compose -f docker-compose.yml -f docker-compose-graphiti.yml logs -f graphiti

# 访问 Neo4j 浏览器（可选）
# 访问 http://localhost:7474 并使用 NEO4J_USER/NEO4J_PASSWORD 登录

# 访问 Graphiti API（可选，用于调试）
# 访问 http://localhost:8000/docs 查看 Swagger API 文档
```

> [!NOTE]
> Graphiti 服务在 `docker-compose-graphiti.yml` 中定义为单独的栈。必须同时运行两个 compose 文件才能启用知识图谱功能。默认使用预构建的 Docker 镜像 `vxcontrol/graphiti:latest`。

#### 存储的内容

启用后，PentAGI 自动捕获：

- **智能体响应**：所有智能体推理、分析和决策
- **工具执行**：执行的命令、使用的工具及其结果
- **上下文信息**：流程、任务和子任务层次结构

### GitHub 和 Google OAuth 集成

与 GitHub 和 Google 的 OAuth 集成允许用户使用这些平台上的现有帐户进行身份验证。这提供了几个好处：

- 简化的登录过程，无需创建单独的凭证
- 通过可信的身份提供商增强安全性
- 从 GitHub/Google 帐户访问用户配置文件信息
- 与现有开发工作流程的无缝集成

要使用 GitHub OAuth，您需要在 GitHub 帐户中创建新的 OAuth 应用程序，并在 `.env` 文件中设置 `OAUTH_GITHUB_CLIENT_ID` 和 `OAUTH_GITHUB_CLIENT_SECRET`。

要使用 Google OAuth，您需要在 Google 帐户中创建新的 OAuth 应用程序，并在 `.env` 文件中设置 `OAUTH_GOOGLE_CLIENT_ID` 和 `OAUTH_GOOGLE_CLIENT_SECRET`。

### Docker 镜像配置

PentAGI 允许您配置用于执行各种任务的 Docker 镜像选择。系统会根据任务类型自动选择最合适的镜像，但您可以通过指定首选镜像来限制此选择：

| 变量名                           | 默认值                | 描述                                                 |
| ---------------------------------- | ---------------------- | ----------------------------------------------------------- |
| `DOCKER_DEFAULT_IMAGE`             | `debian:latest`        | 用于一般任务和模糊情况的默认 Docker 镜像  |
| `DOCKER_DEFAULT_IMAGE_FOR_PENTEST` | `vxcontrol/kali-linux` | 用于安全/渗透测试任务的默认 Docker 镜像 |

当设置这些环境变量时，AI 智能体将被限制为您指定的镜像选择。这对于以下情况特别有用：

- **安全执行**：限制仅使用已验证和受信任的镜像
- **环境标准化**：在所有操作中使用企业或自定义镜像
- **性能优化**：使用预先安装了必要工具的预构建镜像

配置示例：

```bash
# 使用自定义镜像进行一般任务
DOCKER_DEFAULT_IMAGE=mycompany/custom-debian:latest

# 使用专用镜像进行渗透测试
DOCKER_DEFAULT_IMAGE_FOR_PENTEST=mycompany/pentest-tools:v2.0
```

> [!NOTE]
> 如果用户在其任务中明确指定了特定的 Docker 镜像，系统将尝试使用该确切镜像，而忽略这些设置。这些变量仅影响系统的自动镜像选择过程。

## 💻 开发

### 开发要求

- golang
- nodejs
- docker
- postgres
- commitlint

### 环境设置

#### 后端设置

运行一次 `cd backend && go mod download` 以安装所需的软件包。

要生成 swagger 文件，必须运行：

```bash
swag init -g ../../pkg/server/router.go -o pkg/server/docs/ --parseDependency --parseInternal --parseDepth 2 -d cmd/pentagi
```

在通过以下方式安装 `swag` 软件包之前：

```bash
go install github.com/swaggo/swag/cmd/swag@v1.8.7
```

要生成 graphql 解析器文件，必须运行：

```bash
go run github.com/99designs/gqlgen --config ./gqlgen/gqlgen.yml
```

之后，您可以在 `pkg/graph` 文件夹中看到生成的文件。

要从 sqlc 配置生成 ORM 方法（数据库包）：

```bash
docker run --rm -v $(pwd):/src -w /src --network pentagi-network -e DATABASE_URL="{URL}" sqlc/sqlc generate -f sqlc/sqlc.yml
```

要从 OpenAPI 规范生成 Langfuse SDK：

```bash
fern generate --local
```

并安装 fern-cli：

```bash
npm install -g fern-api
```

#### 测试

运行测试 `cd backend && go test -v ./...`

#### 前端设置

运行一次 `cd frontend && npm install` 以安装所需的软件包。

要生成 graphql 文件，必须运行 `npm run graphql:generate`，该文件使用 `graphql-codegen.ts` 文件。

确保您全局安装了 `graphql-codegen`：

```bash
npm install -g graphql-codegen
```

之后，您可以运行：
* `npm run prettier` 检查代码格式是否正确
* `npm run prettier:fix` 修复它
* `npm run lint` 检查代码是否符合 lint 规则
* `npm run lint:fix` 修复它

要生成 SSL 证书，您需要运行 `npm run ssl:generate`，该文件使用 `generate-ssl.ts` 文件，或者运行 `npm run dev` 时会自动生成。

#### 后端配置

在 `.vscode/launch.json` 文件中编辑 `backend` 的配置：
- `DATABASE_URL` - PostgreSQL 数据库 URL（例如 `postgres://postgres:postgres@localhost:5432/pentagidb?sslmode=disable`）
- `DOCKER_HOST` - Docker SDK API（例如，对于 macOS `DOCKER_HOST=unix:///Users/<my-user>/Library/Containers/com.docker.docker/Data/docker.raw.sock`）[更多信息](https://stackoverflow.com/a/62757128/5922857)

可选：
- `SERVER_PORT` - 运行服务器的端口（默认：`8443`）
- `SERVER_USE_SSL` - 为服务器启用 SSL（默认：`false`）

#### 前端配置

在 `.vscode/launch.json` 文件中编辑 `frontend` 的配置：
- `VITE_API_URL` - 后端 API URL。*省略* URL 方案（例如，`localhost:8080` *不是* `http://localhost:8080`）
- `VITE_USE_HTTPS` - 为服务器启用 SSL（默认：`false`）
- `VITE_PORT` - 运行服务器的端口（默认：`8000`）
- `VITE_HOST` - 运行服务器的主机（默认：`0.0.0.0`）

### 运行应用程序

#### 后端

在 `backend` 文件夹中运行命令：
- 使用 `.env` 文件设置环境变量，例如 `source .env`
- 运行 `go run cmd/pentagi/main.go` 启动服务器

> [!NOTE]
> 首次运行可能需要一段时间，因为需要下载依赖项和 docker 镜像来设置后端环境。

#### 前端

在 `frontend` 文件夹中运行命令：
- 运行 `npm install` 安装依赖项
- 运行 `npm run dev` 运行 Web 应用
- 运行 `npm run build` 构建 Web 应用

在浏览器中打开并访问 Web 应用 URL。

## 🧪 测试 LLM 智能体

PentAGI 包含一个名为 `ctester` 的强大实用程序，用于测试和验证 LLM 智能体功能。该工具有助于确保您的 LLM 提供商配置与不同的智能体类型正常工作，允许您为每个特定的智能体角色优化模型选择。

该实用程序具有并行测试多个智能体、详细报告和灵活的配置选项。

### 关键功能

- **并行测试**：同时测试多个智能体以加快结果
- **全面的测试套件**：评估基本完成、JSON 响应、函数调用和渗透测试知识
- **详细报告**：生成带有成功率和性能指标的 markdown 报告
- **灵活配置**：根据需要测试特定的智能体或测试组
- **专业测试组**：包括针对网络安全和渗透测试场景的特定领域测试

### 使用场景

#### 对于开发人员（使用本地 Go 环境）

如果您克隆了仓库并安装了 Go：

```bash
# 使用 .env 文件的默认配置
cd backend
go run cmd/ctester/*.go -verbose

# 自定义提供商配置
go run cmd/ctester/*.go -config ../examples/configs/openrouter.provider.yml -verbose

# 生成报告文件
go run cmd/ctester/*.go -config ../examples/configs/deepinfra.provider.yml -report ../test-report.md

# 仅测试特定的智能体类型
go run cmd/ctester/*.go -agents simple,simple_json,primary_agent -verbose

# 仅测试特定的测试组
go run cmd/ctester/*.go -groups basic,advanced -verbose
```

#### 对于用户（使用 Docker 镜像）

如果您更喜欢使用预构建的 Docker 镜像，而无需设置开发环境：

```bash
# 使用 Docker 通过默认环境进行测试
docker run --rm -v $(pwd)/.env:/opt/pentagi/.env vxcontrol/pentagi /opt/pentagi/bin/ctester -verbose

# 使用您的自定义提供商配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  -v $(pwd)/my-config.yml:/opt/pentagi/config.yml \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/config.yml -agents simple,primary_agent,coder -verbose

# 生成详细报告
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  -v $(pwd):/opt/pentagi/output \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -report /opt/pentagi/output/report.md
```

#### 使用预配置提供商

Docker 镜像内置了对主要提供商（OpenAI、Anthropic、Gemini、Ollama）的支持，以及用于其他服务（OpenRouter、DeepInfra、DeepSeek、Moonshot）的预配置提供商文件：

```bash
# 使用 OpenRouter 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/openrouter.provider.yml

# 使用 DeepInfra 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/deepinfra.provider.yml

# 使用 DeepSeek 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/deepseek.provider.yml

# 使用 Moonshot 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/moonshot.provider.yml

# 使用 OpenAI 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -type openai

# 使用 Anthropic 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -type anthropic

# 使用 Gemini 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -type gemini

# 使用 AWS Bedrock 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -type bedrock

# 使用自定义 OpenAI 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/custom-openai.provider.yml

# 使用 Ollama 配置进行测试（本地推理）
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/ollama-llama318b.provider.yml

# 使用 Ollama Qwen3 32B 配置进行测试（需要自定义模型创建）
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/ollama-qwen332b-fp16-tc.provider.yml

# 使用 Ollama QwQ 32B 配置进行测试（需要自定义模型创建和 71.3GB VRAM）
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/ollama-qwq32b-fp16-tc.provider.yml
```

要使用这些配置，您的 `.env` 文件只需包含：

```
LLM_SERVER_URL=https://openrouter.ai/api/v1      # 或 https://api.deepinfra.com/v1/openai 或 https://api.deepseek.com 或 https://api.openai.com/v1 或 https://api.moonshot.ai/v1
LLM_SERVER_KEY=your_api_key
LLM_SERVER_MODEL=                                # 留空，模型在配置中指定
LLM_SERVER_CONFIG_PATH=/opt/pentagi/conf/openrouter.provider.yml  # 或 deepinfra.provider.yml 或 deepseek.provider.yml 或 custom-openai.provider.yml 或 moonshot.provider.yml
LLM_SERVER_PROVIDER=                             # 用于 LiteLLM 代理的提供商名称（例如，openrouter、deepseek、moonshot）
LLM_SERVER_LEGACY_REASONING=false                # 控制推理格式，对于 OpenAI 必须为 true（默认：false）
LLM_SERVER_PRESERVE_REASONING=false              # 在多轮对话中保留推理内容（Moonshot 需求，默认：false）

# 对于 OpenAI（官方 API）
OPEN_AI_KEY=your_openai_api_key                  # 您的 OpenAI API 密钥
OPEN_AI_SERVER_URL=https://api.openai.com/v1     # OpenAI API 端点

# 对于 Anthropic (Claude 模型)
ANTHROPIC_API_KEY=your_anthropic_api_key         # 您的 Anthropic API 密钥
ANTHROPIC_SERVER_URL=https://api.anthropic.com/v1  # Anthropic API 端点

# 对于 Gemini (Google AI)
GEMINI_API_KEY=your_gemini_api_key               # 您的 Google AI API 密钥
GEMINI_SERVER_URL=https://generativelanguage.googleapis.com  # Google AI API 端点

# 对于 AWS Bedrock（企业基础模型）
BEDROCK_REGION=us-east-1                         # Bedrock 服务的 AWS 区域
BEDROCK_ACCESS_KEY_ID=your_aws_access_key        # AWS 访问密钥 ID
BEDROCK_SECRET_ACCESS_KEY=your_aws_secret_key    # AWS 秘密访问密钥
BEDROCK_SESSION_TOKEN=your_aws_session_token     # AWS 会话令牌（替代身份验证方法）
BEDROCK_SERVER_URL=                              # 可选的自定义 Bedrock 端点

# 对于 Ollama（本地推理）
OLLAMA_SERVER_URL=http://localhost:11434
OLLAMA_SERVER_MODEL=llama3.1:8b-instruct-q8_0
OLLAMA_SERVER_CONFIG_PATH=/opt/pentagi/conf/ollama-llama318b.provider.yml
OLLAMA_SERVER_PULL_MODELS_ENABLED=false
OLLAMA_SERVER_LOAD_MODELS_ENABLED=false
```

#### 使用未验证组织的 OpenAI

对于没有访问最新推理模型（o1、o3、o4-mini）权限的未验证组织 OpenAI 帐户，您需要使用自定义配置。

要使用未验证组织的 OpenAI，请按如下方式配置 `.env` 文件：

```bash
LLM_SERVER_URL=https://api.openai.com/v1
LLM_SERVER_KEY=your_openai_api_key
LLM_SERVER_MODEL=                                # 留空，模型在配置中指定
LLM_SERVER_CONFIG_PATH=/opt/pentagi/conf/custom-openai.provider.yml
LLM_SERVER_LEGACY_REASONING=true                 # OpenAI 推理格式必需
```

此配置使用预构建的 `custom-openai.provider.yml` 文件，该文件将所有智能体类型映射到未验证组织可用的模型，使用 `o3-mini` 而不是 `o1`、`o3` 和 `o4-mini` 等模型。

您可以使用以下命令测试此配置：

```bash
# 使用未验证帐户的自定义 OpenAI 配置进行测试
docker run --rm \
  -v $(pwd)/.env:/opt/pentagi/.env \
  vxcontrol/pentagi /opt/pentagi/bin/ctester -config /opt/pentagi/conf/custom-openai.provider.yml
```

> [!NOTE]
> `LLM_SERVER_LEGACY_REASONING=true` 设置对于 OpenAI 兼容性至关重要，因为它确保推理参数以 OpenAI 的 API 期望的格式发送。

#### 使用 LiteLLM 代理

使用 LiteLLM 代理访问各种 LLM 提供商时，模型名称以提供商名称为前缀（例如，`moonshot/kimi-2.5` 而不是 `kimi-2.5`）。要对直接 API 访问和 LiteLLM 代理使用相同的提供商配置文件，设置 `LLM_SERVER_PROVIDER` 变量：

```bash
# 直接访问 Moonshot API
LLM_SERVER_URL=https://api.moonshot.ai/v1
LLM_SERVER_KEY=your_moonshot_api_key
LLM_SERVER_CONFIG_PATH=/opt/pentagi/conf/moonshot.provider.yml
LLM_SERVER_PROVIDER=                             # 直接访问时为空

# 通过 LiteLLM 代理访问
LLM_SERVER_URL=http://litellm-proxy:4000
LLM_SERVER_KEY=your_litellm_api_key
LLM_SERVER_CONFIG_PATH=/opt/pentagi/conf/moonshot.provider.yml
LLM_SERVER_PROVIDER=moonshot                     # LiteLLM 的提供商前缀
```

使用 `LLM_SERVER_PROVIDER=moonshot`，系统会自动将配置文件中的所有模型名称前缀为 `moonshot/`，使其与 LiteLLM 的模型命名约定兼容。

**LiteLLM 支持的提供商名称：**
- `openai` - 通过 LiteLLM 访问的 OpenAI 模型
- `anthropic` - 通过 LiteLLM 访问的 Anthropic/Claude 模型
- `gemini` - 通过 LiteLLM 访问的 Google Gemini 模型
- `openrouter` - 用于 OpenRouter 聚合器
- `deepseek` - DeepSeek 模型
- `deepinfra` - DeepInfra 托管
- `moonshot` - Moonshot AI (Kimi)
- 您的 LiteLLM 实例中配置的任何其他提供商名称

这种方法允许您：
- 对直接和代理访问使用相同的配置文件
- 在不修改配置文件的情况下切换提供商
- 使用 LiteLLM 轻松测试不同的路由策略

#### 在生产环境中运行测试

如果您已经有一个运行的 PentAGI 容器并想要测试当前配置：

```bash
# 使用当前环境变量在现有容器中运行 ctester
docker exec -it pentagi /opt/pentagi/bin/ctester -verbose

# 使用确定性顺序测试特定的智能体类型
docker exec -it pentagi /opt/pentagi/bin/ctester -agents simple,primary_agent,pentester -groups basic,knowledge -verbose

# 在容器内生成报告文件
docker exec -it pentagi /opt/pentagi/bin/ctester -report /opt/pentagi/data/agent-test-report.md

# 从主机访问报告
docker cp pentagi:/opt/pentagi/data/agent-test-report.md ./
```

### 命令行选项

该实用程序接受几个选项：

- `-env <path>` - 环境文件路径（默认：`.env`）
- `-type <provider>` - 提供商类型：`custom`、`openai`、`anthropic`、`ollama`、`bedrock`、`gemini`（默认：`custom`）
- `-config <path>` - 自定义提供商配置路径（默认：来自 `LLM_SERVER_CONFIG_PATH` 环境变量）
- `-tests <path>` - 自定义测试 YAML 文件路径（可选）
- `-report <path>` - 写入报告文件的路径（可选）
- `-agents <list>` - 要测试的智能体类型逗号分隔列表（默认：`all`）
- `-groups <list>` - 要运行的测试组逗号分隔列表（默认：`all`）
- `-verbose` - 启用详细输出，显示每个智能体的详细测试结果

### 可用的智能体类型

智能体按以下确定性顺序进行测试：

1. **simple** - 基本完成任务
2. **simple_json** - JSON 结构化响应
3. **primary_agent** - 主要推理智能体
4. **assistant** - 交互式助手模式
5. **generator** - 内容生成
6. **refiner** - 内容细化和改进
7. **adviser** - 专家建议和咨询
8. **reflector** - 自我反思和分析
9. **searcher** - 信息收集和搜索
10. **enricher** - 数据扩充和扩展
11. **coder** - 代码生成和分析
12. **installer** - 安装和设置任务
13. **pentester** - 渗透测试和安全评估

### 可用的测试组

- **basic** - 基本完成和提示响应测试
- **advanced** - 复杂推理和函数调用测试
- **json** - JSON 格式验证和结构测试（专门为 `simple_json` 智能体设计）
- **knowledge** - 特定领域的网络安全和渗透测试知识测试

> **注意**：`json` 测试组专门为 `simple_json` 智能体类型设计，而所有其他智能体都使用 `basic`、`advanced` 和 `knowledge` 组进行测试。这种专业化确保了为每个智能体的预期目的提供最佳的测试覆盖范围。

### 示例提供商配置

提供商配置定义了用于不同智能体类型的模型：

```yaml
simple:
  model: "provider/model-name"
  temperature: 0.7
  top_p: 0.95
  n: 1
  max_tokens: 4000

simple_json:
  model: "provider/model-name"
  temperature: 0.7
  top_p: 1.0
  n: 1
  max_tokens: 4000
  json: true

# ... 其他智能体类型 ...
```

### 优化工作流程

1. **建立基线**：使用默认配置运行测试以建立基准性能
2. **分析特定于智能体的性能**：审查确定性智能体顺序以识别性能不佳的智能体
3. **测试专门配置**：使用特定于提供商的配置为每个智能体类型尝试不同的模型
4. **专注于领域知识**：特别注意网络安全专业知识的知识组测试
5. **验证函数调用**：确保关键智能体类型的基于工具的测试始终通过
6. **比较结果**：在所有测试组中寻找最佳成功率和性能
7. **部署最佳配置**：在您的优化设置中使用

该工具有助于确保您的 AI 智能体使用对其特定任务最有效的模型，在优化成本的同时提高可靠性。

## 🧮 嵌入配置与测试

PentAGI 使用向量嵌入进行语义搜索、知识存储和记忆管理。系统支持多个可以根据您的需求和偏好配置的嵌入提供商。

### 支持的嵌入提供商

PentAGI 支持以下嵌入提供商：

- **OpenAI**（默认）：使用 OpenAI 的文本嵌入模型
- **Ollama**：通过 Ollama 的本地嵌入模型
- **Mistral**：Mistral AI 的嵌入模型
- **Jina**：Jina AI 的嵌入服务
- **HuggingFace**：来自 HuggingFace 的模型
- **GoogleAI**：Google 的嵌入模型
- **VoyageAI**：VoyageAI 的嵌入模型

<details>
<summary><b>嵌入提供商配置</b>（点击展开）</summary>

### 环境变量

要配置嵌入提供商，请在 `.env` 文件中设置以下环境变量：

```bash
# 主要嵌入配置
EMBEDDING_PROVIDER=openai       # 提供商类型（openai、ollama、mistral、jina、huggingface、googleai、voyageai）
EMBEDDING_MODEL=text-embedding-3-small  # 要使用的模型名称
EMBEDDING_URL=                  # 可选的自定义 API 端点
EMBEDDING_KEY=                  # 提供商的 API 密钥（如果需要）
EMBEDDING_BATCH_SIZE=100        # 一批中处理的文档数
EMBEDDING_STRIP_NEW_LINES=true  # 是否在嵌入之前从文本中删除新行

# 高级设置
PROXY_URL=                      # 所有 API 调用的可选代理

# SSL/TLS 证书配置（用于与 LLM 后端和工具服务器的外部通信）
EXTERNAL_SSL_CA_PATH=           # 容器内自定义 CA 证书文件的路径（PEM 格式）
                                # 必须指向 /opt/pentagi/ssl/ 目录（例如 /opt/pentagi/ssl/ca-bundle.pem）
EXTERNAL_SSL_INSECURE=false     # 跳过证书验证（仅用于测试）
```

<details>
<summary><b>如何添加自定义 CA 证书</b>（点击展开）</summary>

如果您看到此错误：`tls: failed to verify certificate: x509: certificate signed by unknown authority`

**步骤 1：** 以 PEM 格式获取您的 CA 证书包（可以包含多个证书）

**步骤 2：** 将文件放在主机上的 SSL 目录中：
```bash
# 默认位置（如果未设置 PENTAGI_SSL_DIR）
cp ca-bundle.pem ./pentagi-ssl/

# 或自定义位置（如果在 docker-compose.yml 中使用 PENTAGI_SSL_DIR）
cp ca-bundle.pem /path/to/your/ssl/dir/
```

**步骤 3：** 在 `.env` 文件中设置路径（路径必须在容器内）：
```bash
# pentagi-ssl 卷挂载到容器内的 /opt/pentagi/ssl
EXTERNAL_SSL_CA_PATH=/opt/pentagi/ssl/ca-bundle.pem
EXTERNAL_SSL_INSECURE=false
```

**步骤 4：** 重启 PentAGI：
```bash
docker compose restart pentagi
```

**注意：**
- `pentagi-ssl` 卷挂载到容器内的 `/opt/pentagi/ssl`
- 您可以使用 docker-compose.yml 中的 `PENTAGI_SSL_DIR` 变量更改主机目录
- 文件支持在一个 PEM 文件中包含多个证书和中间 CA
- 仅将 `EXTERNAL_SSL_INSECURE=true` 用于测试（不建议用于生产环境）

</details>

### 特定于提供商的限制

每个提供商都有特定的限制和支持的功能：

- **OpenAI**：支持所有配置选项
- **Ollama**：不支持 `EMBEDDING_KEY`，因为它使用本地模型
- **Mistral**：不支持 `EMBEDDING_MODEL` 或自定义 HTTP 客户端
- **Jina**：不支持自定义 HTTP 客户端
- **HuggingFace**：需要 `EMBEDDING_KEY` 并支持所有其他选项
- **GoogleAI**：不支持 `EMBEDDING_URL`，需要 `EMBEDDING_KEY`
- **VoyageAI**：支持所有配置选项

如果未指定 `EMBEDDING_URL` 和 `EMBEDDING_KEY`，系统将尝试使用相应的 LLM 提供商设置（例如，当 `EMBEDDING_PROVIDER=openai` 时使用 `OPEN_AI_KEY`）。

### 为什么一致的嵌入提供商很重要

一致使用相同的嵌入提供商至关重要，因为：

1. **向量兼容性**：不同的提供商产生具有不同维度和数学属性的向量
2. **语义一致性**：更改提供商可能会破坏以前嵌入的文档之间的语义相似性
3. **记忆损坏**：混合嵌入可能导致搜索结果不佳和知识库功能损坏

如果您更改嵌入提供商，应该刷新并重新索引整个知识库（请参阅下面的 `etester` 实用程序）。

</details>

### 嵌入测试程序实用程序 (etester)

PentAGI 包含一个专门的 `etester` 实用程序，用于测试、管理和调试嵌入功能。该工具对于诊断和解决与向量嵌入和知识存储相关的问题至关重要。

<details>
<summary><b>Etester 命令</b>（点击展开）</summary>

```bash
# 测试嵌入提供商和数据库连接
cd backend
go run cmd/etester/main.go test -verbose

# 显示有关嵌入数据库的统计信息
go run cmd/etester/main.go info

# 删除嵌入数据库中的所有文档（谨慎使用！）
go run cmd/etester/main.go flush

# 重新计算所有文档的嵌入（更改提供商后）
go run cmd/etester/main.go reindex

# 在嵌入数据库中搜索文档
go run cmd/etester/main.go search -query "如何安装 PostgreSQL" -limit 5
```

### 使用 Docker

如果您在 Docker 中运行 PentAGI，可以从容器内使用 etester：

```bash
# 测试嵌入提供商
docker exec -it pentagi /opt/pentagi/bin/etester test

# 显示详细的数据库信息
docker exec -it pentagi /opt/pentagi/bin/etester info -verbose
```

### 高级搜索选项

`search` 命令支持各种过滤器以缩小结果范围：

```bash
# 按文档类型过滤
docker exec -it pentagi /opt/pentagi/bin/etester search -query "安全漏洞" -doc_type guide -threshold 0.8

# 按流程 ID 过滤
docker exec -it pentagi /opt/pentagi/bin/etester search -query "代码示例" -doc_type code -flow_id 42

# 所有可用的搜索选项
docker exec -it pentagi /opt/pentagi/bin/etester search -help
```

可用的搜索参数：
- `-query STRING`：搜索查询文本（必需）
- `-doc_type STRING`：按文档类型过滤（answer、memory、guide、code）
- `-flow_id NUMBER`：按流程 ID 过滤（正数）
- `-answer_type STRING`：按答案类型过滤（guide、vulnerability、code、tool、other）
- `-guide_type STRING`：按指南类型过滤（install、configure、use、pentest、development、other）
- `-limit NUMBER`：最大结果数（默认：3）
- `-threshold NUMBER`：相似度阈值（0.0-1.0，默认：0.7）

### 常见故障排除场景

1. **更改嵌入提供商后**：始终运行 `flush` 或 `reindex` 以确保一致性
2. **搜索结果不佳**：尝试调整相似度阈值或检查嵌入是否正确生成
3. **数据库连接问题**：验证 PostgreSQL 正在运行并安装了 pgvector 扩展
4. **缺少 API 密钥**：检查您选择的嵌入提供商的环境变量

</details>

## 🔍 使用 ftester 测试功能

PentAGI 包含一个名为 `ftester` 的多功能实用程序，用于调试、测试和开发特定功能和 AI 智能体行为。虽然 `ctester` 专注于测试 LLM 模型功能，但 `ftester` 允许您以精确的控制执行上下文直接调用单个系统功能和 AI 智能体组件。

### 关键功能

- **直接功能访问**：测试单个功能，而无需运行整个系统
- **模拟模式**：使用内置模拟测试功能，而无需实时 PentAGI 部署
- **交互式输入**：以交互方式填写功能参数以进行探索性测试
- **详细输出**：带有格式化响应和错误的彩色终端输出
- **上下文感知测试**：在特定流程、任务和子任务的上下文中调试 AI 智能体
- **可观察性集成**：所有功能调用都记录到 Langfuse 和可观察性栈

### 使用模式

#### 命令行参数

直接从命令行使用特定功能和参数运行 ftester：

```bash
# 使用模拟模式的基本用法
cd backend
go run cmd/ftester/main.go [function_name] -[arg1] [value1] -[arg2] [value2]

# 示例：在模拟模式下测试终端命令
go run cmd/ftester/main.go terminal -command "ls -la" -message "列出文件"

# 使用真实的流程上下文
go run cmd/ftester/main.go -flow 123 terminal -command "whoami" -message "检查用户"

# 在特定任务/子任务上下文中测试 AI 智能体
go run cmd/ftester/main.go -flow 123 -task 456 -subtask 789 pentester -message "查找漏洞"
```

#### 交互式模式

不带参数运行 ftester，以获得引导式的交互式体验：

```bash
# 启动交互式模式
go run cmd/ftester/main.go [function_name]

# 例如，以交互方式填写浏览器工具参数
go run cmd/ftester/main.go browser
```

<details>
<summary><b>可用功能</b>（点击展开）</summary>

### 环境功能
- **terminal**：在容器中执行命令并返回输出
- **file**：在容器中执行文件操作（读取、写入、列出）

### 搜索功能
- **browser**：访问网站并捕获屏幕截图
- **google**：使用 Google 自定义搜索搜索网络
- **duckduckgo**：使用 DuckDuckGo 搜索网络
- **tavily**：使用 Tavily AI 搜索引擎搜索
- **traversaal**：使用 Traversaal AI 搜索引擎搜索
- **perplexity**：使用 Perplexity AI 搜索
- **sploitus**：搜索安全漏洞利用、漏洞 (CVE) 和渗透测试工具
- **searxng**：使用 Searxng 元搜索引擎搜索（聚合多个引擎的结果）

### 向量数据库功能
- **search_in_memory**：在向量数据库中搜索信息
- **search_guide**：在向量数据库中查找指南文档
- **search_answer**：在向量数据库中查找问题的答案
- **search_code**：在向量数据库中查找代码示例

### AI 智能体功能
- **advice**：从 AI 智能体获取专家建议
- **coder**：请求代码生成或修改
- **maintenance**：运行系统维护任务
- **memorist**：在向量数据库中存储和组织信息
- **pentester**：执行安全测试和漏洞分析
- **search**：跨多个源进行复杂搜索

### 实用功能
- **describe**：显示有关流程、任务和子任务的信息

</details>

<details>
<summary><b>调试流程上下文</b>（点击展开）</summary>

`describe` 功能提供有关流程内的任务和子任务的详细信息。这对于诊断 PentAGI 遇到问题或卡住时特别有用。

```bash
# 列出系统中的所有流程
go run cmd/ftester/main.go describe

# 显示特定流程的所有任务和子任务
go run cmd/ftester/main.go -flow 123 describe

# 显示特定任务的详细信息
go run cmd/ftester/main.go -flow 123 -task 456 describe

# 显示特定子任务的详细信息
go run cmd/ftester/main.go -flow 123 -task 456 -subtask 789 describe

# 显示详细输出，包括完整的描述和结果
go run cmd/ftester/main.go -flow 123 describe -verbose
```

此功能允许您确定流程可能卡住的确切点，并通过直接调用相应的智能体功能来恢复处理。

</details>

<details>
<summary><b>功能帮助和发现</b>（点击展开）</summary>

每个功能都有帮助模式，显示可用的参数：

```bash
# 获取特定功能的帮助
go run cmd/ftester/main.go [function_name] -help

# 示例：
go run cmd/ftester/main.go terminal -help
go run cmd/ftester/main.go browser -help
go run cmd/ftester/main.go describe -help
```

您还可以不带参数运行 ftester 以查看所有可用功能的列表：

```bash
go run cmd/ftester/main.go
```

</details>

<details>
<summary><b>输出格式</b>（点击展开）</summary>

`ftester` 实用程序使用彩色输出以便于解释：

- **蓝色标题**：部分标题和键名
- **青色 [INFO]**：常规信息消息
- **绿色 [SUCCESS]**：成功操作
- **红色 [ERROR]**：错误消息
- **黄色 [WARNING]**：警告消息
- **黄色 [MOCK]**：指示模拟模式操作
- **洋红色值**：功能参数和结果

JSON 和 Markdown 响应会自动格式化以提高可读性。

</details>

<details>
<summary><b>高级使用场景</b>（点击展开）</summary>

### 调试卡住的 AI 流程

当 PentAGI 在流程中卡住时：

1. 通过 UI 暂停流程
2. 使用 `describe` 确定当前任务和子任务
3. 使用相同的任务/子任务 ID 直接调用智能体功能
4. 检查详细输出以识别问题
5. 恢复流程或根据需要手动干预

### 测试环境变量

验证 API 密钥和外部服务配置正确：

```bash
# 测试 Google 搜索 API 配置
go run cmd/ftester/main.go google -query "渗透测试工具"

# 测试对外部网站的浏览器访问
go run cmd/ftester/main.go browser -url "https://example.com"
```

### 开发新的 AI 智能体行为

在开发新的提示模板或智能体行为时：

1. 在 UI 中创建测试流程
2. 使用 ftester 使用不同的提示直接调用智能体
3. 观察响应并相应地调整提示
4. 检查 Langfuse 以获取所有功能调用的详细跟踪

### 验证 Docker 容器设置

确保容器正确配置：

```bash
go run cmd/ftester/main.go -flow 123 terminal -command "env | grep -i proxy" -message "检查代理设置"
```

</details>

<details>
<summary><b>Docker 容器使用</b>（点击展开）</summary>

如果您在 Docker 中运行 PentAGI，可以从容器内使用 ftester：

```bash
# 在运行的 PentAGI 容器内运行 ftester
docker exec -it pentagi /opt/pentagi/bin/ftester [arguments]

# 示例：
docker exec -it pentagi /opt/pentagi/bin/ftester -flow 123 describe
docker exec -it pentagi /opt/pentagi/bin/ftester -flow 123 terminal -command "ps aux" -message "列出进程"
```

这对于您没有本地开发环境的生产部署特别有用。

</details>

<details>
<summary><b>与可观察性工具集成</b>（点击展开）</summary>

通过 ftester 进行的所有功能调用都记录到：

1. **Langfuse**：捕获整个 AI 智能体交互链，包括提示、响应和功能调用
2. **OpenTelemetry**：记录指标、跟踪和日志，用于系统性能分析
3. **终端输出**：提供功能执行和错误的即时反馈

要访问详细日志：

- 检查 Langfuse UI 以获取 AI 智能体跟踪（通常在 `http://localhost:4000`）
- 使用 Grafana 仪表板获取系统指标（通常在 `http://localhost:3000`）
- 检查终端输出以获取即时的功能结果和错误

</details>

### 命令行选项

主实用程序接受几个选项：

- `-env <path>` - 环境文件路径（可选，默认：`.env`）
- `-provider <type>` - 要使用的提供商类型（默认：`custom`，选项：`openai`、`anthropic`、`ollama`、`bedrock`、`gemini`、`custom`）
- `-flow <id>` - 测试的流程 ID（0 表示使用模拟，默认：`0`）
- `-task <id>` - 智能体上下文的任务 ID（可选）
- `-subtask <id>` - 智能体上下文的子任务 ID（可选）

特定于功能的参数在功能名称之后使用 `-name value` 格式传递。

## 🏗️ 构建

### 构建 Docker 镜像

Docker 构建过程会自动嵌入来自 git 标签的版本信息。要正确地为构建添加版本，请使用提供的脚本：

#### Linux/macOS

```bash
# 加载版本变量
source ./scripts/version.sh

# 标准构建
docker build \
  --build-arg PACKAGE_VER=$PACKAGE_VER \
  --build-arg PACKAGE_REV=$PACKAGE_REV \
  -t pentagi:$PACKAGE_VER .

# 多平台构建
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  --build-arg PACKAGE_VER=$PACKAGE_VER \
  --build-arg PACKAGE_REV=$PACKAGE_REV \
  -t pentagi:$PACKAGE_VER .

# 构建并推送
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  --build-arg PACKAGE_VER=$PACKAGE_VER \
  --build-arg PACKAGE_REV=$PACKAGE_REV \
  -t myregistry/pentagi:$PACKAGE_VER \
  --push .
```

#### Windows (PowerShell)

```powershell
# 加载版本变量
. .\scripts\version.ps1

# 标准构建
docker build `
  --build-arg PACKAGE_VER=$env:PACKAGE_VER `
  --build-arg PACKAGE_REV=$env:PACKAGE_REV `
  -t pentagi:$env:PACKAGE_VER .

# 多平台构建
docker buildx build `
  --platform linux/amd64,linux/arm64 `
  --build-arg PACKAGE_VER=$env:PACKAGE_VER `
  --build-arg PACKAGE_REV=$env:PACKAGE_REV `
  -t pentagi:$env:PACKAGE_VER .
```

#### 不带版本的快速构建

对于不带版本跟踪的开发构建：

```bash
docker build -t pentagi:dev .
```

> [!NOTE]
> - 构建脚本自动从 git 标签确定版本
> - 发布构建（在标签提交上）没有修订后缀
> - 开发构建（标签之后）包括作为修订的提交哈希（例如 `1.1.0-bc6e800`）
> - 要在本地使用构建的镜像，请更新 `docker-compose.yml` 中的镜像名称或使用 `build` 选项

## 👏 致谢

该项目得益于以下研究和发展：
- [Emerging Architectures for LLM Applications](https://lilianweng.github.io/posts/2023-06-23-agent)
- [A Survey of Autonomous LLM Agents](https://arxiv.org/abs/2403.08299)

## 📄 许可证

### PentAGI 核心许可证

**PentAGI 核心**：在 [MIT 许可证](LICENSE) 下获得许可  
版权所有 (c) 2025 PentAGI 开发团队

### VXControl Cloud SDK 集成

**VXControl Cloud SDK 集成**：此仓库在**特殊许可例外**下集成了 [VXControl Cloud SDK](https://github.com/vxcontrol/cloud)，该例外**仅**适用于官方 PentAGI 项目。

#### ✅ 官方 PentAGI 项目
- 此官方仓库：`https://github.com/vxcontrol/pentagi`
- 由 VXControl LLC 分发的官方版本
- 在 VXControl LLC 的直接授权下使用的代码

#### ⚠️ 对分支和第三方使用很重要

如果您分叉此项目或创建衍生作品，VXControl SDK 组件受 **AGPL-3.0** 许可条款约束。您必须：

1. **删除 VXControl SDK 集成**
2. **开源您的整个应用程序**（遵守 AGPL-3.0 副本条款）
3. **从 VXControl LLC 获取商业许可证**

#### 商业许可

要在专有应用程序中使用 VXControl Cloud SDK 进行商业用途，请联系：
- **电子邮件**：info@vxcontrol.com  
- **主题**："VXControl Cloud SDK 商业许可证"
