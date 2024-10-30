# 项目简介
逆向Piece-OS GRPC流并转换为标准OpenAI接口的项目
所有模型均由 Piece-OS 提供
如果帮助到了你，能否给一个Star呢？
# todo
- [x] 流式实现
- [x] Serverless部署
- [x] 静态Proto JS

# 项目结构
```
GPTInferenceService.proto # GPT的GRPC定义
VertexInferenceService.proto # 其余几乎所有模型的GRPC定义
index.js Node.js的项目文件，即开即用
cloud_model.json 云端模型的配置文件，请提取unique中的模型使用
```

# 使用方法
```curl
curl --request POST 'http://127.0.0.1:8787/v1/chat/completions' \
  --header 'Content-Type: application/json' \
  --data '{
    "messages": [
      {
        "role": "user",
        "content": "你好！"
      }
    ],
    "model": "gpt-4o",
    "stream": true
  }'
```

# 环境变量
## `API_PREFIX`
- **描述**: API 请求的前缀路径。
- **默认值**: `'/'`
- **获取方式**: `process.env.API_PREFIX || '/'`

## `API_KEY`
- **描述**: API 请求的密钥。
- **默认值**: 空字符串 `''`
- **获取方式**: `process.env.API_KEY || ''`

## `MAX_RETRY_COUNT`
- **描述**: 最大重试次数。
- **默认值**: `3`
- **获取方式**: `process.env.MAX_RETRY_COUNT || 3`

## `RETRY_DELAY`
- **描述**: 重试延迟时间，单位为毫秒。
- **默认值**: `5000`（5秒）
- **获取方式**: `process.env.RETRY_DELAY || 5000`

## `PORT`
- **描述**: 服务监听的端口。
- **默认值**: `8787`
- **获取方式**: `process.env.PORT || 8787`

## `COMMON_PROTO`
- **描述**: 通用 gRPC 服务的 proto 文件路径。
- **默认值**: `'./VertexInferenceService.proto'`

## `GPT_PROTO`
- **描述**: GPT 推理 gRPC 服务的 proto 文件路径。
- **默认值**: `'./GPTInferenceService.proto'`

