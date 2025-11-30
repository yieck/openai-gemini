## 缘由
Gemini API 是[免费的](https://ai.google.dev/pricing "有额度限制！")，
但许多工具只支持 OpenAI API。
本项目免费提供一个个人使用的、与 OpenAI 兼容的 API 端点。

## 无服务器 (Serverless)？
尽管它运行在云端，但无需进行服务器维护。
它可以轻松地免费部署到各种服务提供商
（其免费额度足以满足个人使用）。
> [!TIP]
> 在本地运行代理端点也是一个选择，
> 尽管这更适合于开发用途。

## 如何开始
您需要一个个人 Google [API 密钥](https://makersuite.google.com/app/apikey)。
> [!IMPORTANT]
> 即使您所在的地区不在[支持的区域](https://ai.google.dev/gemini-api/docs/available-regions#available_regions)内，
> 仍然可以使用 VPN 获取一个。

请按照下方的说明，将项目部署到任一服务提供商。
您需要在相应的平台注册一个账户。
如果您选择“一键部署”，系统会引导您首先 fork 本仓库，
这是实现持续集成（CI）所必需的。

### 使用 Vercel 部署
[![使用 Vercel 部署](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/PublicAffairs/openai-gemini&repository-name=my-openai-gemini)
- 或者，您也可以使用 [cli](https://vercel.com/docs/cli) 进行部署：
  `vercel deploy`
- 在本地运行： `vercel dev`
- Vercel _Functions_ 的[限制](https://vercel.com/docs/functions/limitations)（使用 _Edge_ 运行时）

### 部署到 Netlify
[![部署到 Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/PublicAffairs/openai-gemini&integrationName=integrationName&integrationSlug=integrationSlug&integrationDescription=integrationDescription)
- 或者，您也可以使用 [cli](https://docs.netlify.com/cli/get-started/) 进行部署：
  `netlify deploy`
- 在本地运行： `netlify dev`
- 提供了两种不同的 API 基础路径：
  - `/v1` (例如 `/v1/chat/completions` 端点)  
    _Functions_ 的[限制](https://docs.netlify.com/functions/get-started/?fn-language=js#synchronous-function-2)
  - `/edge/v1`  
    _Edge functions_ 的[限制](https://docs.netlify.com/edge-functions/limits/)

### 部署到 Cloudflare
[![部署到 Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/PublicAffairs/openai-gemini)
- 或者，您可以手动将 [`src/worker.mjs`](src/worker.mjs) 的内容粘贴到
  https://workers.cloudflare.com/playground 进行部署（点击页面上的 `Deploy` 按钮）。
- 或者，您也可以使用 [cli](https://developers.cloudflare.com/workers/wrangler/) 进行部署：
  `wrangler deploy`
- 在本地运行： `wrangler dev`
- _Worker_ 的[限制](https://developers.cloudflare.com/workers/platform/limits/#worker-limits)

### 部署到 Deno
详情请见[此处](https://github.com/PublicAffairs/openai-gemini/discussions/19)。

### 在本地运行 - 使用 Node, Deno, Bun
仅适用于 Node：`npm install`。
然后运行 `npm run start` / `npm run start:deno` / `npm run start:bun`。

#### 开发模式（监视源文件变化）
仅适用于 Node：`npm install --include=dev`
然后运行：`npm run dev` / `npm run dev:deno` / `npm run dev:bun`。

## 如何使用
如果您在浏览器中打开刚部署好的网站，只会看到一个 `404 Not Found` 的消息。这是正常现象，因为此 API 并非为浏览器直接访问而设计。
要使用它，您应在所用软件的设置中，将您的 API 地址和 Gemini API 密钥填入相应的字段。
> [!NOTE]
> 并非所有软件工具都允许覆盖 OpenAI 端点，但许多工具支持这样做
> （不过这些设置有时可能隐藏得很深）。

通常，您应该按以下格式指定 API 基础路径：  
`https://my-super-proxy.vercel.app/v1`

相关字段的标签可能是“_OpenAI proxy_”。
您可能需要在“_高级设置_”或类似版块下查找。
或者，它也可能在某个配置文件中（详情请查阅相关文档）。
对于一些命令行工具，您可能需要设置环境变量，例如：
```sh
OPENAI_BASE_URL="https://my-super-proxy.vercel.app/v1"
