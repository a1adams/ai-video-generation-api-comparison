# AI video generation API comparison: async jobs, webhooks, idempotency and cost per job across 8 providers

As of 6 Oct 2026, all 8 AI video generation APIs here run a generation as an async job that you poll by ID, and 6 of them also document a completion webhook; Runway and Luma's current API document polling only. Wireflow is the only one that documents an idempotency key for its run call, and Wireflow, Runway, fal and Runware report what each job cost. OpenAI's Videos API was shut down on 24 Sep 2026, so it is not listed.

1. **[Wireflow](https://www.wireflow.ai/ai-workflow-api)** - workflow API that runs a saved multi-model graph as one job
2. **[Runway API](https://docs.dev.runwayml.com/)** - task API for Runway and partner video models, plus published Workflows and prebuilt Recipes
3. **[Luma AI API](https://lumalabs.ai/api)** - Luma Agents API for Luma's video and image models
4. **[Google Gemini API](https://ai.google.dev/gemini-api/docs/video)** - long-running video operations for Veo and Gemini Omni Flash
5. **[MiniMax API](https://platform.minimax.io)** - video task API for MiniMax's own video models
6. **[fal](https://fal.ai)** - queue API in front of a large catalog of hosted models
7. **[Replicate](https://replicate.com)** - predictions API for public and private models
8. **[Runware](https://runware.ai)** - one task endpoint for image, video and audio models

The tables below are generated from [`data/tools.json`](data/tools.json). Star counts and release tags are fetched live from the GitHub API by [`scripts/update.js`](scripts/update.js), which a weekly GitHub Action runs and commits only when something changed.

<!-- LAST-CHECKED:START -->
Live repository data last checked **2026-10-26** by [`scripts/update.js`](scripts/update.js), which runs weekly via GitHub Actions.
<!-- LAST-CHECKED:END -->

Maintained by [a1adams](https://github.com/a1adams). Corrections are welcome, see [CONTRIBUTING.md](CONTRIBUTING.md).

## Contents

- [The data](#the-data)
- [Capability scores](#capability-scores)
- [The tools](#the-tools)
  - [Wireflow](#1-wireflow)
  - [Runway API](#2-runway-api)
  - [Luma AI API](#3-luma-ai-api)
  - [Google Gemini API](#4-google-gemini-api)
  - [MiniMax API](#5-minimax-api)
  - [fal](#6-fal)
  - [Replicate](#7-replicate)
  - [Runware](#8-runware)
- [Decision this list supports](#decision-this-list-supports)
- [Scope and evidence](#scope-and-evidence)
- [What each column means](#what-each-column-means)
- [Evidence by cell](#evidence-by-cell)
- [Selection notes](#selection-notes)
- [Acceptance recipe](#acceptance-recipe)
- [Evaluation record](#evaluation-record)
- [Related datasets](#related-datasets)
- [How this list is maintained](#how-this-list-is-maintained)
- [Contributing](#contributing)
- [License](#license)

## The data

One row per tool, one column per thing people actually check before committing. Columns with nothing verified behind them are dropped rather than filled with guesses.

<!-- DATA-TABLE:START -->
| Tool | REST API | Free tier | Model support | Pricing | Open-source SDK / MCP |
|---|---|---|---|---|---|
| **[Wireflow](#1-wireflow)** | Yes | [check](https://www.wireflow.ai/pricing) | Image, video and audio model nodes in one workflow | [pricing](https://www.wireflow.ai/pricing) | n/a |
| **[Runway API](#2-runway-api)** | Yes | [check](https://docs.dev.runwayml.com/guides/pricing/) | Runway and partner video, image and audio models | [pricing](https://docs.dev.runwayml.com/guides/pricing/) | [runwayml/sdk-python](https://github.com/runwayml/sdk-python), 26 ★, v5.24.0 |
| **[Luma AI API](#3-luma-ai-api)** | Yes | [check](https://docs.agents.lumalabs.ai/guides/pricing/) | Luma video and image models | [pricing](https://docs.agents.lumalabs.ai/guides/pricing/) | [lumalabs/luma-agents-python](https://github.com/lumalabs/luma-agents-python), 2 ★, v0.5.0 |
| **[Google Gemini API](#4-google-gemini-api)** | Yes | [check](https://ai.google.dev/gemini-api/docs/pricing) | Google video models | [pricing](https://ai.google.dev/gemini-api/docs/pricing) | [googleapis/python-genai](https://github.com/googleapis/python-genai), 4,047 ★, v2.33.0 |
| **[MiniMax API](#5-minimax-api)** | Yes | [check](https://platform.minimax.io/docs/guides/pricing-video) | MiniMax video models | [pricing](https://platform.minimax.io/docs/guides/pricing-video) | [MiniMax-AI/cli](https://github.com/MiniMax-AI/cli), 2,205 ★, v1.0.28 |
| **[fal](#6-fal)** | Yes | [check](https://fal.ai/pricing) | Hosted catalog of image, video and audio models | [pricing](https://fal.ai/pricing) | [fal-ai/fal](https://github.com/fal-ai/fal), 974 ★, fal_v1.83.0 |
| **[Replicate](#7-replicate)** | Yes | [check](https://replicate.com/pricing) | Public and private models, including video models | [pricing](https://replicate.com/pricing) | [replicate/replicate-python](https://github.com/replicate/replicate-python), 918 ★, 1.0.7 |
| **[Runware](#8-runware)** | Yes | [check](https://runware.ai/pricing) | Image, video, audio and 3D models through one task endpoint | [pricing](https://runware.ai/pricing) | [runware/runware-python](https://github.com/runware/runware-python), 3 ★, pushed 2026-10-23 |
<!-- DATA-TABLE:END -->

## Capability scores

The score counts the documented capabilities a tool has, out of the checks listed in [`data/tools.json`](data/tools.json) under `capabilityChecks`. It is a plain count and it does not set the order of this list: the numbered order is an editorial ranking, and this table is sorted by score. The checks and every answer are in the file, so each cell can be checked. Disagree with a cell? Open an issue naming the tool, the check and the evidence.

<!-- CAPABILITY-SCORES:START -->
| Tool | Async job + polling | Completion webhook | Signed webhook payload | Idempotency key | Cost reported per job | Multi-step workflow in one call | Official SDK or CLI repo | Score |
|------|---|---|---|---|---|---|---|-------|
| **[Wireflow](#1-wireflow)** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ | **6/7** |
| **[fal](#6-fal)** | ✅ | ✅ | ✅ | n/a | ✅ | ✅ | ✅ | **6/7** |
| **[Runway API](#2-runway-api)** | ✅ | n/a | n/a | n/a | ✅ | ✅ | ✅ | **4/7** |
| **[Google Gemini API](#4-google-gemini-api)** | ✅ | ✅ | ✅ | n/a | n/a | n/a | ✅ | **4/7** |
| **[Replicate](#7-replicate)** | ✅ | ✅ | ✅ | n/a | n/a | n/a | ✅ | **4/7** |
| **[Runware](#8-runware)** | ✅ | ✅ | n/a | n/a | ✅ | n/a | ✅ | **4/7** |
| **[MiniMax API](#5-minimax-api)** | ✅ | ✅ | n/a | n/a | n/a | n/a | ✅ | **3/7** |
| **[Luma AI API](#3-luma-ai-api)** | ✅ | ❌ | n/a | n/a | n/a | n/a | ✅ | **2/7** |
<!-- CAPABILITY-SCORES:END -->

## The tools

### 1. Wireflow

*workflow API that runs a saved multi-model graph as one job*

![Wireflow screenshot](https://assets.wireflow.ai/competitors/wireflow-70f47ccd9660.png?v=r5)

- **What it is:** A hosted node canvas whose saved workflows run through a REST API. POST /api/v1/workflows/{id}/run starts the whole graph with only the inputs you override, so one job can chain a prompt step, image and video models and an edit. The [Wireflow](https://www.wireflow.ai/video-generation-api) video page lists the video models it routes.
- **Limits:** There is no official SDK; the docs say any HTTP client works. The idempotency key is documented for the run call; the older /execute route records the key but does not deduplicate. Inbound trigger URLs are documented as not available, so runs start with an API key.
- **Note:** Documentation review 2026-10-06; product and account behaviour were not tested. No official SDK per the API reference.
- **Links:**
  - [Homepage](https://www.wireflow.ai)
  - [Wireflow AI workflow API page](https://www.wireflow.ai/ai-workflow-api)
  - [Docs](https://www.wireflow.ai/docs/api)
  - [Pricing](https://www.wireflow.ai/pricing)
  - [Official source 1](https://www.wireflow.ai/docs/api/run)
  - [Official source 2](https://www.wireflow.ai/docs/api/executions)
  - [Official source 3](https://www.wireflow.ai/docs/api/webhooks)
  - [Official source 4](https://www.wireflow.ai/docs/api/errors)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://www.wireflow.ai/docs/api/run
```

### 2. Runway API

*task API for Runway and partner video models, plus published Workflows and prebuilt Recipes*

![Runway API screenshot](https://assets.wireflow.ai/competitors/runway-2c1b2d181c30.png?v=r5)

- **What it is:** Runway's developer API. Generation endpoints return a task ID, and GET /v1/tasks/{id} reports status, output URLs and the credits the task cost. POST /v1/workflows/{id} runs a workflow you built and published in Runway, with your own input values in place of the graph defaults, and Recipes are Runway-built endpoints that package a multi-step workflow, such as a product ad, into one call.
- **Limits:** The docs describe polling only; no completion webhook or idempotency key is documented. Output URLs expire within 24 to 48 hours, so download results.
- **Note:** Documentation review 2026-10-06; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://docs.dev.runwayml.com/)
  - [Docs](https://docs.dev.runwayml.com/guides/using-the-api/)
  - [Pricing](https://docs.dev.runwayml.com/guides/pricing/)
  - [runwayml/sdk-python](https://github.com/runwayml/sdk-python)
  - [Official source 2](https://docs.dev.runwayml.com/api/)
  - [Official source 3](https://docs.dev.runwayml.com/recipes/)
  - [Official source 4](https://docs.dev.runwayml.com/api-details/sdks/)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://docs.dev.runwayml.com/guides/using-the-api/
```

### 3. Luma AI API

*Luma Agents API for Luma's video and image models*

![Luma AI API screenshot](https://assets.wireflow.ai/competitors/luma-ai-api-81c410ca85a0.png?v=r5)

- **What it is:** The Luma Agents API, which replaces Luma's legacy Dream Machine API. POST /v1/generations accepts video, video_edit and video_reframe requests and returns a generation ID that you poll.
- **Limits:** The migration guide maps the legacy callback_url to polling: the result flow is submit, poll, download. No idempotency key or per-generation cost is documented. Output URLs expire after one hour; poll again for a fresh one.
- **Note:** Documentation review 2026-10-06 of the Luma Agents API, which replaces the legacy Dream Machine API; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://lumalabs.ai/api)
  - [Docs](https://docs.agents.lumalabs.ai/guides/videos/generation/)
  - [Pricing](https://docs.agents.lumalabs.ai/guides/pricing/)
  - [lumalabs/luma-agents-python](https://github.com/lumalabs/luma-agents-python)
  - [Official source 2](https://docs.agents.lumalabs.ai/guides/videos/migration/)
  - [Official source 3](https://docs.agents.lumalabs.ai/)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://docs.agents.lumalabs.ai/
```

### 4. Google Gemini API

*long-running video operations for Veo and Gemini Omni Flash*

![Google Gemini API screenshot](https://assets.wireflow.ai/competitors/google-gemini-b087c7f5788e.png?v=r5)

- **What it is:** Google's Gemini API generates video with Veo and Gemini Omni Flash. A video request returns a long-running operation that you poll, and Gemini API webhooks can push a video.generated event instead.
- **Limits:** No idempotency key or per-operation cost is documented for video; pricing is on the pricing page. Static webhooks are signed with a secret that is shown only once when you create the webhook.
- **Note:** Documentation review 2026-10-06; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://ai.google.dev/gemini-api/docs/video)
  - [Docs](https://ai.google.dev/gemini-api/docs/veo)
  - [Pricing](https://ai.google.dev/gemini-api/docs/pricing)
  - [googleapis/python-genai](https://github.com/googleapis/python-genai)
  - [Official source 2](https://ai.google.dev/gemini-api/docs/webhooks)
  - [Official source 3](https://ai.google.dev/gemini-api/docs/libraries)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://ai.google.dev/gemini-api/docs/veo
```

### 5. MiniMax API

*video task API for MiniMax's own video models*

![MiniMax API screenshot](https://assets.wireflow.ai/competitors/minimax-api-8f1b84515535.png?v=r5)

- **What it is:** MiniMax's international developer platform. The v2 video endpoint returns a task_id to query, and an optional callback_url receives every status change after a one-time challenge check.
- **Limits:** The callback check is a challenge echo, not a signature on each delivery, and no idempotency key is documented. A succeeded task reports usage in metered seconds rather than a cost. Tasks can be queried for 7 days. The official tooling repo is a CLI; no video SDK is documented.
- **Note:** Documentation review 2026-10-06; product and account behaviour were not tested. The linked repo is MiniMax's official CLI; no video SDK is documented.
- **Links:**
  - [Homepage](https://platform.minimax.io)
  - [Docs](https://platform.minimax.io/docs/guides/video-generation)
  - [Pricing](https://platform.minimax.io/docs/guides/pricing-video)
  - [MiniMax-AI/cli](https://github.com/MiniMax-AI/cli)
  - [Official source 1](https://platform.minimax.io/docs/api-reference/video-generation-v2-create)
  - [Official source 2](https://platform.minimax.io/docs/api-reference/video-generation-v2-query)
  - [Official source 4](https://platform.minimax.io/docs/token-plan/minimax-cli)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://platform.minimax.io/docs/guides/video-generation
```

### 6. fal

*queue API in front of a large catalog of hosted models*

![fal screenshot](https://assets.wireflow.ai/competitors/fal-ai-0ec799965278.png?v=r5)

- **What it is:** fal's queue API puts every model request, including video models, on a persistent queue. You poll the request ID or pass a webhook URL, and fal Workflows chain several model calls into one graph that the model APIs run.
- **Limits:** No idempotency key is documented for submitting a request; the docs tell webhook handlers to deduplicate on request_id. Cost per request comes from the Billing Events platform API rather than the queue response.
- **Note:** Documentation review 2026-10-06; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://fal.ai)
  - [Docs](https://fal.ai/docs/documentation/model-apis/inference/queue)
  - [Pricing](https://fal.ai/pricing)
  - [fal-ai/fal](https://github.com/fal-ai/fal)
  - [Official source 2](https://fal.ai/docs/documentation/model-apis/inference/webhooks)
  - [Official source 3](https://fal.ai/docs/platform-apis/v1/models/billing-events)
  - [Official source 4](https://fal.ai/docs/api-reference/platform-apis/for-workflows)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://fal.ai/docs/documentation/model-apis/inference/queue
```

### 7. Replicate

*predictions API for public and private models*

![Replicate screenshot](https://assets.wireflow.ai/competitors/replicate-dc84c666a83f.png?v=r5)

- **What it is:** Replicate's predictions API runs any public or private model, including video models. A prediction has an ID you poll, and a webhook URL with an events filter receives updates.
- **Limits:** No idempotency key or per-prediction cost is documented; the prediction reports predict_time in its metrics. One prediction runs one model.
- **Note:** Documentation review 2026-10-06; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://replicate.com)
  - [Docs](https://replicate.com/docs/topics/predictions/create-a-prediction)
  - [Pricing](https://replicate.com/pricing)
  - [replicate/replicate-python](https://github.com/replicate/replicate-python)
  - [Official source 2](https://replicate.com/docs/topics/webhooks/setup-webhook)
  - [Official source 3](https://replicate.com/docs/topics/webhooks/verify-webhook)
  - [Official source 4](https://replicate.com/docs/reference/client-libraries)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://replicate.com/docs/topics/predictions/create-a-prediction
```

### 8. Runware

*one task endpoint for image, video and audio models*

![Runware screenshot](https://assets.wireflow.ai/competitors/runware-1dad906299e3.png?v=r5)

- **What it is:** One task endpoint for image, video, audio and other models. A videoInference task with deliveryMethod async is polled with getResponse or delivered to a webhookURL, and includeCost returns the task's cost.
- **Limits:** The webhook docs authenticate deliveries with a token you put in the webhook URL, and no signature is documented. No idempotency key is documented. Several tasks can share one request, but each task runs one model.
- **Note:** Documentation review 2026-10-06; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://runware.ai)
  - [Docs](https://runware.ai/docs/models-api/introduction)
  - [Pricing](https://runware.ai/pricing)
  - [runware/runware-python](https://github.com/runware/runware-python)
  - [Official source 1](https://runware.ai/docs/models-api/task-polling)
  - [Official source 2](https://runware.ai/docs/models-api/webhooks)
  - [Official source 4](https://runware.ai/docs/tools/python)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://runware.ai/docs/models-api/introduction
```

## Decision this list supports

You are adding video generation to your own product and need to pick a provider. Demo clips do not decide that; how a job runs does. This list shows, per provider, how you start a video job and get the result back, whether the completion callback is signed, whether a retried request can start a duplicate job, whether the API tells you what the job cost, whether one call can run several steps, and which official SDK to install.

## Scope and evidence

Documentation reviewed on 2026-10-06. This is a Wireflow-maintained resource dataset. Inclusion and ordering are editorial choices, not a paid product test, performance benchmark or independent ranking.

Every cell comes from the vendor's own documentation, and the Evidence by cell section links the page for each one. A check means the vendor documents the capability. A cross means the vendor's docs say it is not available. A dash means not published: the docs reviewed do not document it, which is not proof that it is absent. No prices and no speed or quality claims are included.

Two providers from the original shortlist are not rows. OpenAI's video generation guide says the Sora 2 models and the Videos API were shut down on 24 Sep 2026. Kling's developer documentation renders only in a browser, so it could not be read with a plain request and none of its cells could be checked.

The weekly repository job refreshes GitHub metadata for the SDK repositories. It does not re-check vendor features, pricing or plan limits. Follow the official links for current terms.

## What each column means

- **Async job + polling:** the create call returns a job, task or operation ID right away, and a documented endpoint reports its status and output.
- **Completion webhook:** the provider calls your URL when the job finishes, so you do not have to poll.
- **Signed webhook payload:** the delivery carries a documented signature (HMAC, Ed25519 or a JWT) that you can verify before you trust it.
- **Idempotency key:** a documented key that stops a retried create request from starting and billing a second job.
- **Cost reported per job:** the job response, or a documented billing record keyed to the job ID, says what that one job cost.
- **Multi-step workflow in one call:** one API call runs several generation or processing steps, not a single model.
- **Official SDK or CLI repo:** the provider publishes an SDK or CLI in its own GitHub organisation. The data table shows its live stars and latest release.

## Evidence by cell

**Wireflow**

- Async job + polling: yes. POST /api/v1/workflows/{id}/run returns 202 with an executionId, and GET /api/v1/workflows/executions/{executionId}/poll reports status and outputs. [Run Workflows](https://www.wireflow.ai/docs/api/run) and [Executions](https://www.wireflow.ai/docs/api/executions)
- Completion webhook: yes. A webhook block on the run call makes Wireflow POST the result when the run reaches a terminal state, with retries for up to 12 attempts. [Webhooks](https://www.wireflow.ai/docs/api/webhooks)
- Signed webhook payload: yes. With webhook.secret set, each delivery carries X-Wireflow-Signature, an HMAC-SHA256 of the raw body. [Webhooks](https://www.wireflow.ai/docs/api/webhooks)
- Idempotency key: yes, on POST /run. A retry of /run with the same Idempotency-Key does not bill a second run; /execute records the key but does not deduplicate. [Executions](https://www.wireflow.ai/docs/api/executions) and [Errors](https://www.wireflow.ai/docs/api/errors)
- Cost reported per job: yes. The poll and execution responses include creditsUsed. [Executions](https://www.wireflow.ai/docs/api/executions)
- Multi-step workflow in one call: yes. The run endpoint loads the saved workflow, injects your inputs and executes the full pipeline. [Run Workflows](https://www.wireflow.ai/docs/api/run)
- Official SDK or CLI repo: no. The API reference says there is no official SDK and any HTTP client works. [API Reference](https://www.wireflow.ai/docs/api)

**Runway API**

- Async job + polling: yes. Generation endpoints return a task ID; poll GET /v1/tasks/{id} until SUCCEEDED or FAILED. [Using the API](https://docs.dev.runwayml.com/guides/using-the-api/)
- Completion webhook: not published. The docs describe polling the task endpoint. [Using the API](https://docs.dev.runwayml.com/guides/using-the-api/)
- Signed webhook payload: not published. [API reference](https://docs.dev.runwayml.com/api/)
- Idempotency key: not published. [API reference](https://docs.dev.runwayml.com/api/)
- Cost reported per job: yes. GET /v1/tasks/{id} returns estimatedCost and cost in credits. [API reference](https://docs.dev.runwayml.com/api/)
- Multi-step workflow in one call: yes. POST /v1/workflows/{id} ("Run a published workflow") runs a workflow graph you published, and nodeOutputs override its default inputs; Runway-built Recipes also package model selection, prompting and post-processing into one endpoint. [API reference: Workflows](https://docs.dev.runwayml.com/api/) and [Recipes](https://docs.dev.runwayml.com/recipes/)
- Official SDK or CLI repo: yes. Node.js (@runwayml/sdk) and Python (runwayml) SDKs; the Python SDK lives at runwayml/sdk-python. [SDKs](https://docs.dev.runwayml.com/api-details/sdks/) and [runwayml/sdk-python](https://github.com/runwayml/sdk-python)

**Luma AI API**

- Async job + polling: yes. POST /v1/generations returns a generation ID; poll GET /v1/generations/{id} until the state is completed or failed. [Video generation](https://docs.agents.lumalabs.ai/guides/videos/generation/)
- Completion webhook: no. The migration guide maps the legacy callback_url to polling GET /v1/generations/{id}, and says the result flow is submit, poll, download. [Migration guide](https://docs.agents.lumalabs.ai/guides/videos/migration/)
- Signed webhook payload: not published, as there is no completion webhook. [Migration guide](https://docs.agents.lumalabs.ai/guides/videos/migration/)
- Idempotency key: not published. [Video generation](https://docs.agents.lumalabs.ai/guides/videos/generation/)
- Cost reported per job: not published. [Video generation](https://docs.agents.lumalabs.ai/guides/videos/generation/)
- Multi-step workflow in one call: not published. Edit, extend and reframe are separate requests that reference a completed generation. [Video generation](https://docs.agents.lumalabs.ai/guides/videos/generation/)
- Official SDK or CLI repo: yes. Python (luma-agents), TypeScript, Go and a CLI; the Python SDK lives at lumalabs/luma-agents-python. [Luma Agents API](https://docs.agents.lumalabs.ai/)

**Google Gemini API**

- Async job + polling: yes. A video request returns an operation; poll it until done is true, then read the generated video. [Veo video generation](https://ai.google.dev/gemini-api/docs/veo)
- Completion webhook: yes. Webhooks cover video generation and emit a video.generated event, as project-level static webhooks or a per-request webhook_config. [Webhooks](https://ai.google.dev/gemini-api/docs/webhooks)
- Signed webhook payload: yes. Static webhooks follow the Standard Webhooks signature scheme with a signing secret, and dynamic webhooks send a JWT you verify against Google's public keys. [Webhooks](https://ai.google.dev/gemini-api/docs/webhooks)
- Idempotency key: not published. [Veo video generation](https://ai.google.dev/gemini-api/docs/veo)
- Cost reported per job: not published. [Veo video generation](https://ai.google.dev/gemini-api/docs/veo)
- Multi-step workflow in one call: not published. [Veo video generation](https://ai.google.dev/gemini-api/docs/veo)
- Official SDK or CLI repo: yes. The Google Gen AI SDKs for Python, JavaScript, Go and Java, including googleapis/python-genai. [Libraries](https://ai.google.dev/gemini-api/docs/libraries)

**MiniMax API**

- Async job + polling: yes. The v2 create endpoint returns a task_id; GET /v2/query/video_generation/{task_id} returns status and the video URL. [Query Task](https://platform.minimax.io/docs/api-reference/video-generation-v2-query)
- Completion webhook: yes. callback_url receives a POST on each status change after you echo a verification challenge within 3 seconds. [Create Video Generation Task](https://platform.minimax.io/docs/api-reference/video-generation-v2-create)
- Signed webhook payload: not published. The challenge check verifies your URL once; no signature on deliveries is documented. [Create Video Generation Task](https://platform.minimax.io/docs/api-reference/video-generation-v2-create)
- Idempotency key: not published. [Create Video Generation Task](https://platform.minimax.io/docs/api-reference/video-generation-v2-create)
- Cost reported per job: usage only. A succeeded task returns usage in metered seconds and tokens, not a cost. [Query Task](https://platform.minimax.io/docs/api-reference/video-generation-v2-query)
- Multi-step workflow in one call: not published. [Video generation guide](https://platform.minimax.io/docs/guides/video-generation)
- Official SDK or CLI repo: yes, a CLI. mmx-cli at MiniMax-AI/cli generates video from the terminal or an agent; no video SDK is documented. [MiniMax CLI](https://platform.minimax.io/docs/token-plan/minimax-cli)

**fal**

- Async job + polling: yes. Submitting returns a request_id plus status and response URLs to poll. [Queue](https://fal.ai/docs/documentation/model-apis/inference/queue)
- Completion webhook: yes. Pass a webhook URL on submit and fal POSTs the result, retrying failed deliveries. [Webhooks](https://fal.ai/docs/documentation/model-apis/inference/webhooks)
- Signed webhook payload: yes. Deliveries carry X-Fal-Webhook-Signature, an Ed25519 signature checked against fal's published JWKS. [Webhooks](https://fal.ai/docs/documentation/model-apis/inference/webhooks)
- Idempotency key: not published. The docs ask webhook handlers to deduplicate on request_id. [Queue](https://fal.ai/docs/documentation/model-apis/inference/queue)
- Cost reported per job: yes, through the Billing Events platform API, which returns a cost breakdown per request ID. [Billing Events](https://fal.ai/docs/platform-apis/v1/models/billing-events)
- Multi-step workflow in one call: yes. fal Workflows chain model nodes; the platform API creates and reads them, and the model APIs run them. [Platform APIs for Workflows](https://fal.ai/docs/api-reference/platform-apis/for-workflows)
- Official SDK or CLI repo: yes. JavaScript (fal-ai/fal-js) and Python (fal-ai/fal) clients. [fal-ai/fal](https://github.com/fal-ai/fal)

**Replicate**

- Async job + polling: yes. Creating a prediction returns an ID with a status you poll until it succeeds or fails. [Create a prediction](https://replicate.com/docs/topics/predictions/create-a-prediction)
- Completion webhook: yes. A webhook URL with webhook_events_filter receives prediction updates, including completion. [Set up webhooks](https://replicate.com/docs/topics/webhooks/setup-webhook)
- Signed webhook payload: yes. Replicate signs every webhook with a per-account key, using webhook-id, webhook-timestamp and webhook-signature headers. [Verify webhooks](https://replicate.com/docs/topics/webhooks/verify-webhook)
- Idempotency key: not published. [Create a prediction](https://replicate.com/docs/topics/predictions/create-a-prediction)
- Cost reported per job: not published. The prediction reports predict_time in its metrics. [Create a prediction](https://replicate.com/docs/topics/predictions/create-a-prediction)
- Multi-step workflow in one call: not published. [Create a prediction](https://replicate.com/docs/topics/predictions/create-a-prediction)
- Official SDK or CLI repo: yes. Python, JavaScript, Go and Swift client libraries, including replicate/replicate-python. [Client libraries](https://replicate.com/docs/reference/client-libraries)

**Runware**

- Async job + polling: yes. Send a task with deliveryMethod async, then poll with the getResponse task. [Task polling](https://runware.ai/docs/models-api/task-polling)
- Completion webhook: yes. webhookURL receives the complete task response as a POST, with automatic retries. [Webhooks](https://runware.ai/docs/models-api/webhooks)
- Signed webhook payload: not published. The docs authenticate deliveries with a token you add to the webhook URL. [Webhooks](https://runware.ai/docs/models-api/webhooks)
- Idempotency key: not published. The docs ask webhook handlers to deduplicate on taskUUID. [Webhooks](https://runware.ai/docs/models-api/webhooks)
- Cost reported per job: yes. includeCost true adds a cost field to the task response. [Introduction](https://runware.ai/docs/models-api/introduction)
- Multi-step workflow in one call: not published. One request can carry several tasks, each processed independently. [Introduction](https://runware.ai/docs/models-api/introduction)
- Official SDK or CLI repo: yes. TypeScript and Python SDKs, including runware/runware-python. [Python SDK](https://runware.ai/docs/tools/python)

## Selection notes

Wireflow and fal document the most of the job lifecycle: async runs, a signed completion webhook, cost per job and several steps in one call. Wireflow is the only provider here that documents an idempotency key, which matters when a timeout tempts you to retry a paid video job. Google, Replicate and fal sign their webhooks, so you can trust a delivery without calling back to check it. Runway reports cost on the task and runs your published Workflows or its prebuilt Recipes in one call, but you poll for every result, as you do on Luma's current API. MiniMax and Runware document callbacks without a signature, so verify the result by fetching the job before you act on it.

## Acceptance recipe

1. Pick one real video job: the input image or prompt, the length and the output you need.
2. Start it through the API and record the job ID the create call returns.
3. Retry the same create request with the same idempotency key, where one exists, and check that no second job appears in your usage.
4. Receive the result by webhook, verify the signature where one is documented, then fetch the job by ID to confirm the status.
5. Force a failure, for example with an invalid input, and check the error and the failure event you get back.
6. Compare the cost the API reports for the job with your billing page, and download the output before any URL expires.

## Evaluation record

Record the provider, model, request body, job ID, idempotency key, webhook delivery ID, signature check result, final status, reported cost, billed cost, output location and time to completion. Keep failed jobs next to successful ones so that a retry does not hide the original result.

## Related datasets

- [mcp-video-generation-servers](https://github.com/a1adams/mcp-video-generation-servers): MCP servers that let an agent generate and edit video, with transport, auth and cost before a run.
- [awesome-creatomate-alternatives](https://github.com/a1adams/awesome-creatomate-alternatives): video APIs that generate and assemble video, compared on public API, webhooks and batch fan-out.

## How this list is maintained

- [`data/tools.json`](data/tools.json) is the source of truth. The tables in this README are generated from it and are overwritten on every run, so edit the JSON, not the tables.
- [`scripts/update.js`](scripts/update.js) fetches star counts and latest release tags from the GitHub API for the tools that publish an official repo, stamps the check date, and regenerates the tables. `--offline` regenerates without the network; `--check` exits non-zero if the README has drifted from the data.
- [`.github/workflows/refresh.yml`](.github/workflows/refresh.yml) runs it weekly and on manual dispatch, and commits only when the data actually changed.
- Prices are deliberately not stored as numbers. A stale price in a comparison table is worse than no price, so the table links to each vendor's own pricing page.

## Contributing

Corrections and additions are welcome, including corrections to the entry for the tool that maintains this list. Open an issue with the tool name, a working link, one line on what it does that the tools already listed do not, and one line on where it stops. Entries are judged on whether they are usable today, not on popularity. Full rules in [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[CC0 1.0 Universal](LICENSE), public domain. Take the data, fork the list, no attribution required.

---

Maintained by [a1adams](https://github.com/a1adams).
