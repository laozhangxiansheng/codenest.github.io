---
title: Websoket的使用及封装
tags: Websoket
banner_img: https://cdn.houdemingxin.com/image/default/B380716569044A5DA885EAFA36EE4FAF-6-2.png
date: 2024-07-02 16:22:39
---

## Websoket 的使用及封装

#### WebSocket 是什么？

WebSocket 是基于 TCP 的一种新的应用层网络协议。它提供了一个**全双工**的通道，允许服务器和客户端之间实时双向通信。因此，在 WebSocket 中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输，客户端和服务器之间的数据交换变得更加简单。

#### WebSocket 特点

- 建立在 TCP 协议之上，服务器端的实现比较容易。
- 与 HTTP 协议有着良好的兼容性。默认端口也是 80 和 443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。
- 数据格式比较轻量，性能开销小，通信高效。
- 可以发送文本，也可以发送二进制数据。
- 没有同源限制，客户端可以与任意服务器通信。
- 协议标识符是 ws（如果加密，则为 wss），服务器网址就是 URL。

#### WebSocket 优缺点

##### 优点

- 较少的控制开销。
- 更强的实时性。
- 能更好的节省服务器资源和带宽。
- 支持双向通信，实时性更强。
- 更好的二进制支持。
- 支持扩展。

##### 缺点

- 协议标识符是 ws，而不是我们常使用的 http，所以无法通过浏览器直接访问，必须从支持 WebSocket 协议的客户端发起请求才能建立连接。
- 服务器端的实现必须对 WebSocket 协议进行支持。
- 客户端支持度不好，需要考虑浏览器兼容性。

#### 与 HTTP 协议的区别

与 HTTP 协议相比，WebSocket 具有以下优点：

- 更高的实时性能：WebSocket 允许服务器和客户端之间实时双向通信，从而提高了实时通信场景中的性能。
- 更少的网络开销：HTTP 请求和响应之间需要额外的数据传输，而 WebSocket 通过在同一个连接上双向通信，减少了网络开销。
- 更灵活的通信方式：HTTP 请求和响应通常是一一对应的，而 WebSocket 允许服务器和客户端之间以多种方式进行通信，例如消息 Push、事件推送等。
- 更简洁的 API：WebSocket 提供了简洁的 API，使得客户端开发人员可以更轻松地进行实时通信。

#### WebSocket 对象的属性和方法：

- **WebSocket** 对象：WebSocket 对象表示一个新的 WebSocket 连接。
- **WebSocket.onopen** 事件处理程序：当 WebSocket 连接打开时触发。
- **WebSocket.onmessage** 事件处理程序：当接收到来自 WebSocket 的消息时触发。
- **WebSocket.onerror** 事件处理程序：当 WebSocket 发生错误时触发。
- **WebSocket.onclose** 事件处理程序：当 WebSocket 连接关闭时触发。
- **WebSocket.send** 方法：向 WebSocket 发送数据。
- **WebSocket.close** 方法：关闭 WebSocket 连接。

#### 实现

1. 创建和连接 WebSocket

```js
// 创建WebSocket对象
const socket = new WebSocket("ws://localhost:8080");
```

其中，ws://localhost:8080 是 WebSocket 的 URL，表示要连接的服务器。

2. 连接 WebSocket

```js
// 连接成功事件
socket.onopen = function () {
  console.log("WebSocket 连接已打开");
};
```

3. 接收来自 WebSocket 的消息

```js
// 接收到消息事件
socket.onmessage = function (event) {
  console.log("接收到消息：", event.data);
};
```

4. 向 WebSocket 发送消息

```js
// 发送消息
socket.send("Hello, WebSocket!");
```

5. 关闭 WebSocket 连接

```js
// 关闭WebSocket连接
socket.close();
```

#### WebSocket 代码示例

以下是一个简单的 WebSocket 示例，通过 WebSocket 向服务器发送数据，并接收服务器返回的数据：

1. 首先，创建一个 HTML 文件，添加一个按钮和一个用于显示消息的文本框：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebSocket 示例</title>
  </head>
  <body>
    <button id="sendBtn">发送消息</button>
    <textarea id="messageBox" readonly></textarea>
    <script src="main.js"></script>
  </body>
</html>
```

2. 接下来，创建一个 JavaScript 文件（例如 main.js），并在其中编写以下代码：

```js
// 获取按钮和文本框元素
const sendBtn = document.getElementById("sendBtn");
const messageBox = document.getElementById("messageBox");

// 创建 WebSocket 对象
const socket = new WebSocket("ws://localhost:8080"); // 使用一个 WebSocket 服务器进行测试

// 设置 WebSocket 连接打开时的回调函数
socket.onopen = function () {
  console.log("WebSocket 连接已打开");
};

// 设置 WebSocket 接收到消息时的回调函数
socket.onmessage = function (event) {
  console.log("WebSocket 接收到消息:", event.data);
  messageBox.value += event.data + "\n";
};

// 设置 WebSocket 发生错误时的回调函数
socket.onerror = function () {
  console.log("WebSocket 发生错误");
};

// 设置 WebSocket 连接关闭时的回调函数
socket.onclose = function () {
  console.log("WebSocket 连接已关闭");
};

// 点击按钮时发送消息
sendBtn.onclick = function () {
  const message = "Hello, WebSocket!";
  socket.send(message);
  messageBox.value += "发送消息: " + message + "\n";
};
```

#### WebSocket 应用场景

- 实时聊天应用：WebSocket 可以支持在线聊天室、即时通讯工具等，实现用户之间的实时消息交换 。
- 协同编辑：在多人协作编辑文档或编程时，WebSocket 可以确保所有参与者对文档的更改能够实时同步 。
- 在线游戏：WebSocket 适用于需要实时状态同步和玩家交互的多人在线游戏 。
- 实时数据更新：例如股票、外汇市场的实时报价更新，新闻或社交媒体的实时推送通知 。
- 物联网(IoT)：在智能家居、工业自动化等场景中，WebSocket 可以用于设备状态的实时监控和远程控制 。
- 地理定位应用：实时位置追踪和导航应用中的动态路线更新 。
- 直播互动：直播平台中的实时评论、弹幕、礼物赠送等功能 。
- 数据分析与监控：实时仪表盘、日志流处理、性能监控系统的实时数据展示与报警 。
- 多媒体聊天：WebSocket 结合 HTML5 音视频元素，可以用于视频会议等多媒体聊天场景 。
- 基于位置的应用：WebSocket 可以用于基于 GPS 的实时位置数据传输，如运动轨迹记录或实时数据仪表盘更新 。
- 在线教育：WebSocket 可以用于在线教育平台，支持多媒体聊天、文字聊天以及在公共数字黑板上的协作 。

#### 利用单例模式创建 Websocket 连接

```js
class WebSocketSingleton {
  static instance;

  constructor(url) {
    if (WebSocketSingleton.instance) {
      return WebSocketSingleton.instance;
    }

    this.url = url;
    this.socket = null;

    WebSocketSingleton.instance = this;
  }

  connect() {
    if (this.socket) {
      return;
    }

    this.socket = new WebSocket(this.url);

    // 连接成功时的回调函数
    this.socket.onopen = () => {
      console.log("WebSocket连接已打开");
    };

    // 接收到消息时的回调函数
    this.socket.onmessage = (event) => {
      console.log("接收到消息:", event.data);
    };

    // 发生错误时的回调函数
    this.socket.onerror = () => {
      console.log("WebSocket发生错误");
    };

    // 连接关闭时的回调函数
    this.socket.onclose = () => {
      console.log("WebSocket连接已关闭");
    };
  }

  send(message) {
    if (this.socket) {
      this.socket.send(message);
    } else {
      console.error("WebSocket连接未建立");
    }
  }

  close() {
    if (this.socket) {
      this.socket.close();
    }
  }
}

// 使用示例
const webSocket = new WebSocketSingleton("ws://localhost:8080");
webSocket.connect();
webSocket.send("Hello, WebSocket!");
webSocket.close();
```
