---
theme: seriph
background: https://images.unsplash.com/photo-1616941482131-489295011919?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=1080&ixid=MnwxfDB8MXxyYW5kb218MHw5NDczNDU2Nnx8fHx8fHwxNjg0NzYxMjQ2&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=1920
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
css: unocss
title: 《Web 前端监控系统的设计与实现》答辩
---

# Web 前端监控系统的设计与实现

班级：信安 191 <br /> 学号：1965500019

杨文锋

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/Plasticine-Yang/plasticine-monitor-sdk" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# 可以干什么？

Web 前端监控系统可以用来监控站点性能体验，及时发现异常，记录用户行为，帮助追踪和分析问题。

<v-click>

- 📝 **稳定性监控** - 支持 JavaScript 运行时异常监控，采集程序调用堆栈，帮助开发者快速感知、定位和处理问题。

</v-click>

<v-click>

- 🎨 **性能监控** - 支持监控各个页面的渲染性能，提供各种常见性能指标的数据看板，帮助开发者分析页面渲染性能的优化点

</v-click>

<v-click>

- 💻 **网站访问情况监控** - 支持监控页面的 PV(page view) 和 UV(user view)，帮助开发者分析各页面的访问流量情况，从而决策页面研发优化的投入

</v-click>

<v-click>

- 🎥 **网络请求监控** - 支持记录用户在网站中发起的包括 XMLHttpRequest 和 Fetch API 在内的所有网络请求，帮助开发者分析接口请求性能以及异常情况

</v-click>

<v-click>

- 🤹 **用户行为监控** - 支持记录用户在一次会话中访问网站的时间线，精准记录每个时间节点进行了什么操作，帮助开发者分析问题发生的上下文

</v-click>

<v-click>

- 📤 **用户行为录屏** - 支持以录屏的方式记录用户在一次会话中的整个操作流程，以直观的方式帮助开发者定位用户遇到异常时的操作环境

</v-click>

---

# 项目组成部分

本项目包含三大部分：监控 SDK、接收上报数据的服务端、监控数据看板 Dashboard

三大部分均已开源到 Github 上，分别以三个仓库进行维护

|                                            |                                                       |                                                                 |
| ------------------------------------------ | ----------------------------------------------------- | --------------------------------------------------------------- |
| 监控 SDK：plasticine-monitor-sdk           | 监控用户浏览器的核心，能够监控和上报数据              | https://github.com/Plasticine-Yang/plasticine-monitor-sdk       |
| 服务端：plasticine-monitor-server          | 用于接收 SDK 上报的数据，并组装监控面板渲染所需的数据 | https://github.com/Plasticine-Yang/plasticine-monitor-server    |
| 监控数据看板: plasticine-monitor-dashboard | 用于展示 SDK 上报的数据                               | https://github.com/Plasticine-Yang/plasticine-monitor-dashboard |

---

# 如何使用？

部署后端服务、 部署控数据看板前端服务、接入 SDK

### 部署后端服务

<v-click>

1. 安装 Docker

</v-click>

<v-click>

2. clone 后端仓库源码

   ```shell
   git clone https://github.com/Plasticine-Yang/plasticine-monitor-server
   ```

</v-click>

<v-click>

3. 执行以下命令一键部署

   ```shell
   pnpm run deploy
   ```

</v-click>

---

# 如何使用？

部署后端服务、 部署控数据看板前端服务、接入 SDK

### 部署控数据看板前端服务

<v-click>

1. clone 数据看板前端仓库源码

   ```shell
   git clone https://github.com/Plasticine-Yang/plasticine-monitor-dashboard
   ```

</v-click>

<v-click>

2. 修改环境变量配置文件中的 VITE_PLASTICINE_MONITOR_SDK_URL，配置为部署的后端服务地址

   ```
   VITE_PLASTICINE_MONITOR_SDK_URL=http://localhost:8888/api/v1/browser-event
   ```

</v-click>

<v-click>

3. 构建前端项目

   ```shell
   pnpm build
   ```

</v-click>

---

# 如何使用？

部署后端服务、 部署控数据看板前端服务、接入 SDK

### 接入 SDK

SDK 已发布到 npm 上，可在你的前端项目中安装 `@plasticine-monitor-sdk/browser` 进行接入，对已有项目无侵入性

<div class="flex justify-center w-full">
  <img src="/sdk-npm.png" class="h-300px" />
</div>

---

# 如何使用？

部署后端服务、 部署控数据看板前端服务、接入 SDK

首先需要在数据看板中创建项目，用于和 SDK 进行关联

<div class="flex justify-center w-full">
  <img src="/create-project.png" class="h-350px" />
</div>

---

# 如何使用？

部署后端服务、 部署控数据看板前端服务、接入 SDK

然后复制 projectId，接入到项目中

```ts
import { init, xhrSender } from '@plasticine-monitor-sdk/browser'

import pkg from '../../package.json'

export function setupPlasticineMonitor() {
  init({
    url: 'http://localhost:8868/api/v1/browser-event',
    projectId: '64607b2af3f06f90577fed12',
    enableLogger: true,
    sender: xhrSender,
  })
}
```

---

# SDK 的设计

本项目的核心在于 SDK 的设计与实现，它决定了能够监控用户浏览器的哪些数据，因此它的设计方式很重要

<v-click>

基于内核 + 插件的架构进行设计

</v-click>

<v-click>

<div class="flex justify-center w-full">
  <img src="/sdk-design.png" class="h-300px" />
</div>

</v-click>

---

# SDK 的设计

这种设计的好处有哪些？

<v-click>

- 用户可以按需启用插件，起到一个热插拔的效果

</v-click>

<v-click>

- 内核与平台无关，有利于实现多端监控，比如浏览器、字节跳动小程序、抖音小程序、飞书小程序、微信小程序、支付宝小程序、百度小程序、Node.js、下一代 JavaScript 运行时环境 Deno.js 和 Bun.js 等等

</v-click>

<v-click>

- 可以以 monorepo 的方式开发和发布这些环境的包，降低代码耦合程度和打包体积，本项目采用的 monorepo 方案为 pnpm-workspace，目前主流的还有 turborepo

</v-click>

<v-click>

<div class="flex justify-center w-full">
  <img src="/sdk-design-1.png" class="h-260px" />
</div>

</v-click>

---

# 效果演示 - JavaScript 运行时异常监控

一个已接入 SDK 的示例项目

<div class="flex justify-center w-full">
  <img src="/js-error-demo.png" class="h-400px" />
</div>

---

# 效果演示 - JavaScript 运行时异常监控

查看过去 1 小时内发生的 JavaScript 运行时异常

<div class="flex justify-center w-full">
  <img src="/js-error-dashboard.gif" />
</div>

---

# 效果演示 - 页面性能监控

查看各个页面的渲染性能指标折线图

<div class="flex justify-center w-full">
  <img src="/performance-dashboard.gif" />
</div>

---

# 页面渲染性能指标讲解

<div class="flex justify-center w-full">
  <img src="/performance-metrics.png" />
</div>

---

# 如何记录这些性能指标？

通过浏览器提供的 PerformanceObserver API 实现

```ts {all|4-5|8-9|10-11|12-13|5}
export class PerformanceMetricsManager {
  private performanceObserver: PerformanceObserver
  private reportCallback: OnReportCallback | null = null
  constructor() {
    this.performanceObserver = new PerformanceObserver(this.performanceObserverCallback)
  }
  public observe() {
    // FP & FCP
    this.performanceObserver.observe({ type: 'paint', buffered: true })
    // LCP
    this.performanceObserver.observe({ type: 'largest-contentful-paint', buffered: true })
    // FID
    this.performanceObserver.observe({ type: 'first-input', buffered: true })
  }
}
```

---

# 如何记录这些性能指标？

通过浏览器提供的 PerformanceObserver API 实现

```ts
private performanceObserverCallback: PerformanceObserverCallback = (entryList) => {
  for (const entry of entryList.getEntries()) {
    // FP & FCP
    if (entry.entryType === 'paint') {
      const performancePaintTiming = entry as PerformancePaintTiming

      switch (entry.name) {
        case 'first-paint':
          this.reportCallback?.(
            this.generatePerformanceEvent({
              name: PerformanceMetricsEnum.FP,
              value: performancePaintTiming.startTime,
            }),
          )
          break

        case 'first-contentful-paint':
          this.reportCallback?.(
            this.generatePerformanceEvent({
              name: PerformanceMetricsEnum.FCP,
              value: performancePaintTiming.startTime,
            }),
          )
          break

        default:
          break
      }
    }
  }
}
```

---

# 如何记录这些性能指标？

通过浏览器提供的 PerformanceObserver API 实现

```ts
private performanceObserverCallback: PerformanceObserverCallback = (entryList) => {
  for (const entry of entryList.getEntries()) {
    // ...

    // LCP
    if (entry.entryType === 'largest-contentful-paint') {
      this.reportCallback?.(
        this.generatePerformanceEvent({
          name: PerformanceMetricsEnum.LCP,
          value: entry.startTime,
        }),
      )
    }
  }
}
```

---

# 如何记录这些性能指标？

通过浏览器提供的 PerformanceObserver API 实现

```ts
private performanceObserverCallback: PerformanceObserverCallback = (entryList) => {
  for (const entry of entryList.getEntries()) {
    // ...

    // FID
    if (entry.entryType === 'first-input') {
      const performanceEventTiming = entry as PerformanceEventTiming

      this.reportCallback?.(
        this.generatePerformanceEvent({
          name: PerformanceMetricsEnum.FID,
          value: performanceEventTiming.processingStart - performanceEventTiming.startTime,
        }),
      )
    }
  }
}
```

---

# 效果演示 - 网站访问情况监控

<div class="flex justify-center w-full">
  <img src="/pv-uv-dashboard.gif" class="h-400px" />
</div>

---

# 如何记录 pv？

这段代码是 MongoDB 的 aggregate pipeline 的代码片段

```ts
// 查询 PV
{
  $group: {
    _id: '$environmentInfo.pagePath',
    pv: { $sum: { $cond: [{
            // 统计 page-view 类型的数据的数量
            // 通过 $map 遍历 payload 数组，如果存在 name 为 page-view 的对象则进行计数
            $in: [1, { $map: { input: '$payload', as: 'item',
                  in: {
                    $cond: [{ $eq: ['$$item.name', UserBehaviorMetricsEnum.PageView] }, 1, 0],
                  }}}]},
          // true case
          1,
          // false case
          0,
        ],
      },
    },
  },
},
```

---

# 如何记录 uv？

```ts
// 查询 PV
uv: {
  $addToSet: {
    // 只从 payload 数组中包含 page-view 的对象中进行计数
    $cond: [
      {
        $in: [
          1,
          {
            $map: {
              input: '$payload',
              as: 'item',
              in: {
                $cond: [{ $eq: ['$$item.name', UserBehaviorMetricsEnum.PageView] }, 1, 0],
              },
            },
          },
        ],
      },
      '$environmentInfo.userId',
      // 在使用 $size 计算 Set 的大小时，null 也会被计数，这里作为占位，之后需要将其过滤掉
      null,
    ],
  },
},
```

---

# 效果演示 - 用户行为监控

场景 1：用户访问页面，并点击几个按钮，触发了 JavaScript 运行时异常报错

<div class="flex justify-center w-full">
  <img src="/user-behavior-demo.gif" class="h-400px" />
</div>

---

# 效果演示 - 用户行为监控

打开监控面板，查看用户行为时间线

<div class="flex justify-center w-full">
  <img src="/user-behavior-dashboard.gif" class="h-400px" />
</div>

---

# 效果演示 - 用户行为监控

查看用户的运行环境信息

<div class="flex justify-center w-full">
  <img src="/user-behavior-dashboard-1.png" class="h-400px" />
</div>

---

# 效果演示 - 用户行为监控

场景 2：用户访问页面，并点击几个按钮，发送了一些网络请求

<div class="flex justify-center w-full">
  <img src="/user-behavior-demo-1.gif" class="h-400px" />
</div>

---

# 效果演示 - 用户行为监控

打开监控面板，查看用户行为时间线

<div class="flex justify-center w-full">
  <img src="/user-behavior-dashboard-1.gif" class="h-400px" />
</div>

---

# 效果演示 - 用户行为监控

可以查看请求的详细信息，包括请求方式、请求耗时、请求和响应的时间、请求头、请求体、响应头、响应体

<div class="flex justify-center w-full">
  <img src="/user-behavior-dashboard-2.png" class="h-400px" />
</div>

---

# 效果演示 - 用户行为监控

可以查看请求的详细信息，包括请求方式、请求耗时、请求和响应的时间、请求头、请求体、响应头、响应体

<div class="flex justify-center w-full">
  <img src="/user-behavior-dashboard-3.png" class="h-400px" />
</div>

---

# 如何对用户行为进行监控？

以 SDK 插件的方式实现，在插件内部维护一个用户行为队列 userBehaviorQueue，在相应的行为发生时往该队列中推入要上报的事件

<v-click>

### 上报策略

- 当队列满时进行上报并清空队列继续记录用户行为
- 当页面隐藏时进行上报
- 每隔 3 秒进行上报

</v-click>

<v-click>

### 插件的灵活性

这些特性都是可以通过插件的参数进行配置的：

- 用户行为队列的大小
- 上报的时间间隔
- 是否要拦截 XMLHttpRequest 请求
- 是否要拦截 Fetch API 请求
- ...

</v-click>

---

# 如何对用户行为进行监控？

```ts {all|9-10|1-3|13-20|11-12|21-24|19-20}
export function pluginUserBehavior(options?: PluginUserBehaviorOptions): BrowserPlugin {
  const resolvedOptions = resolveOptions(options)
  const { maxLengthToReport, recordFetch, recordXMLHttpRequest, reportIntervalTimeout } = resolvedOptions
  let browserKernel: BrowserKernel
  return {
    name: 'user-behavior',
    init(kernel) {
      browserKernel = kernel
      // 动态挂载到内核实例上，让其他插件也可以往里面添加用户行为 - 比如遇到 JS Error 时记录一下
      browserKernel.userBehaviorQueue = new UserBehaviorQueueImpl(maxLengthToReport, handleReportWhenExceed)
      // 页面不可见时上报
      document.addEventListener('visibilitychange', handleReportWhenInvisible)
      // PV
      cancelMonitorPV = monitorPV(browserKernel.userBehaviorQueue!)
      // 点击行为
      cancelMonitorClick = monitorClick(browserKernel.userBehaviorQueue!)
      // 网络请求
      cancelMonitorNetwork = monitorNetwork(browserKernel.userBehaviorQueue!, { recordFetch, recordXMLHttpRequest })
      // 录屏
      cancelMonitorRecord = monitorRecord(browserKernel.userBehaviorQueue!)
      // 每隔 reportInterval 时间上报一次用户行为事件
      reportInterval = window.setInterval(() => {
        reportUserBehavior()
      }, reportIntervalTimeout)
    },
  }
}
```

---

# 效果演示 - 用户行为录屏回放

可以查看请求的详细信息，包括请求方式、请求耗时、请求和响应的时间、请求头、请求体、响应头、响应体

<div class="flex justify-center w-full">
  <img src="/user-behavior-dashboard-2.gif" class="h-400px" />
</div>

---

# 最后 - 数据看板的一点小设计

<div class="flex justify-center w-full">
  <img src="/design.gif" class="h-400px" />
</div>
