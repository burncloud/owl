# Burncloud AI 供应商实现

## 概述

本实现为 OWL (Organized Worldwide Language) 系统添加了 Burncloud AI 平台的支持。Burncloud AI 提供多种业界领先的大语言模型，通过 OpenAI 兼容的 API 接口提供服务。

## 支持的模型

Burncloud AI 平台支持以下模型：

### Claude 模型系列
- `claude-sonnet-4-20250514` - 最新的 Claude Sonnet 4 模型
- `claude-3-7-sonnet-20250219` - Claude 3.7 Sonnet 模型
- `claude-3-5-sonnet-20241022` - Claude 3.5 Sonnet 模型（支持视觉任务）

### GPT 模型系列
- `GPT-4o` - OpenAI GPT-4 Omni 模型
- `GPT-4o-mini` - OpenAI GPT-4 Omni Mini 模型
- `o1` - OpenAI o1 推理模型
- `o1-mini` - OpenAI o1 Mini 推理模型
- `GPT-4.5-preview` - GPT-4.5 预览版
- `GPT-image-1` - GPT 图像生成模型

### 其他模型
- `gemini-2.5-pro-preview-05-06` - Google Gemini 2.5 Pro 预览版
- `DeepSeek-R1` - DeepSeek R1 推理模型
- `DeepSeek-V3` - DeepSeek V3 模型

## 实现细节

### 文件结构
```
examples/
├── run_burncloud.py          # Burncloud 供应商实现
owl/
├── webapp.py                 # 更新了 MODULE_DESCRIPTIONS
├── .env_template             # 添加了 Burncloud 环境变量模板
```

### 环境变量配置

在 `.env` 文件中添加以下配置：

```bash
# Burncloud API 配置
BURNCLOUD_API_KEY="your_burncloud_api_key_here"
BURNCLOUD_MODEL="claude-sonnet-4-20250514"
BURNCLOUD_VISION_MODEL="claude-3-5-sonnet-20241022"
```

### 模型配置策略

1. **默认模型**: 使用 `claude-sonnet-4-20250514` 作为默认模型，因为它是最新且最强大的模型
2. **视觉模型**: 对于需要图像/视频分析的任务，使用 `claude-3-5-sonnet-20241022`
3. **可配置性**: 通过环境变量 `BURNCLOUD_MODEL` 和 `BURNCLOUD_VISION_MODEL` 允许用户自定义模型选择

### 功能特性

- **完整的工具集成**: 支持所有现有的工具包，包括浏览器工具、代码执行、图像分析、视频分析等
- **多模态支持**: 通过视觉模型支持图像和视频分析
- **灵活配置**: 支持通过环境变量自定义模型和参数
- **OpenAI 兼容**: 使用 OpenAI 兼容的 API 接口，确保最佳兼容性

## 使用方法

1. **配置 API 密钥**:
   ```bash
   # 在 .env 文件中添加
   BURNCLOUD_API_KEY="your_api_key_here"
   ```

2. **选择模型** (可选):
   ```bash
   # 设置默认模型
   BURNCLOUD_MODEL="claude-sonnet-4-20250514"
   
   # 设置视觉任务模型
   BURNCLOUD_VISION_MODEL="claude-3-5-sonnet-20241022"
   ```

3. **在 Web 界面中使用**:
   - 在模型选择下拉菜单中选择 "run_burncloud"
   - 输入您的问题或任务
   - 系统将使用 Burncloud AI 平台处理您的请求

4. **命令行使用**:
   ```bash
   python examples/run_burncloud.py "Your question here"
   ```

## API 端点

- **基础 URL**: `https://ai.burncloud.com/v1`
- **兼容性**: OpenAI API 兼容
- **认证**: 使用 API Key 认证

## 注意事项

1. 确保您有有效的 Burncloud API 密钥
2. 根据您的使用需求选择合适的模型
3. 某些模型可能有特定的使用限制或定价
4. 建议在生产环境中使用时设置适当的错误处理和重试机制

## 技术实现

该实现基于 CAMEL-AI 框架，使用 `ModelPlatformType.OPENAI_COMPATIBLE_MODEL` 来确保与 Burncloud API 的兼容性。通过环境变量提供灵活的配置选项，同时保持与现有 OWL 系统的完全兼容。