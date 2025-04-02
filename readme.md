# My HTTP Server

这是一个用 Rust 编写的简单 HTTP 服务器项目，支持用户定义的处理器、中间件和基数树路由（包括路径参数功能）。本项目灵感来源于 [amirrezaask/khadem](https://github.com/amirrezaask/khadem)，并参考了其设计和实现。

## 项目特点

- **用户定义的处理器**：允许自定义处理逻辑，返回特定响应。
- **中间件支持**：例如日志中间件，用于记录请求信息。
- **基数树路由**：支持动态路径参数，例如 `/hello/:name`。
- **异步运行时**：基于 Tokio 实现高效的异步处理。

## 来源

- **原项目地址**：<https://github.com/amirrezaask/khadem>
- **教学视频**：<https://www.youtube.com/playlist?list=PLS87DlLl8etz7w-JyRjYbyqowbI88_qto>

## 运行步骤

1. **检查代码**：
   - 确保 `src/main.rs` 和 `src/http.rs` 已正确保存。
   - `http.rs` 中的 `Router` 实现是一个简化的基数树路由，可能与你的实际实现不同，但足以运行。

2. **编译并运行**：
   在项目根目录（`my_http_server`）运行：

   ```bash
   cargo run
   ```

   - 这会下载依赖、编译代码并启动服务器。
   - 如果成功，你会看到服务器监听在 `127.0.0.1:8080`。

3. **测试服务器**：
   打开另一个终端，使用 `curl` 测试：
   - 根路径：

     ```bash
     curl http://127.0.0.1:8080/
     ```

     输出：`Root`
   - 固定路径：

     ```bash
     curl http://127.0.0.1:8080/bye
     ```

     输出：`bye`
   - 带路径参数：

     ```bash
     curl http://127.0.0.1:8080/hello/alice
     ```

     输出：`hello`，控制台打印 `name alice`。

   - 每次请求，控制台还会输出日志（由 `LogMiddleware` 生成），例如：

   ```
   method:GET
   uri:"/hello/alice"
   version:HTTP1_1
   headers:{"User-Agent": "curl/8.5.0", "Host": "127.0.0.1", "Accept": "*/*"}

   name alice
   HTTP/1.1 200 Ok
   ```

## 注意事项

- 确保端口 `8080` 未被占用，否则修改监听地址。

