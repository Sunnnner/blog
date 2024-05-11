---
title: "Tauri Http连接池"
description: 
date: 2024-05-09T14:04:05+08:00
draft: false
categories:
  - tauri
tags:
  - http
  - reqwest
---
<!--more-->

- [Tauri Http连接池](#tauri-http连接池)
  - [reqwest](##reqwest)
  - [连接池](##连接池)
  - [使用](##使用)
  - [参考](##参考)

# Tauri Http连接池
- 近期有个需求是在Tauri中使用http请求，但是发现每次请求都会创建一个新的连接，这样会导致请求速度变慢，所以需要使用连接池来提高请求速度。
- tauri内建的http库是`reqwest`，所以我们需要使用`reqwest`的连接池来实现。

## reqwest
- `reqwest`是一个基于`hyper`的http客户端库，提供了很多功能，包括连接池。
- `Client` 内部维护了一个连接池，可以通过`Client::new()`创建一个新的连接池。不需要包在`Rc`或者`Arc`中，因为`Client`本身就是线程安全的。

## 连接池

```rust
use tauri::api::http::{Client, ClientBuilder};

pub struct Context{
    client: Client,
}

impl Context{
    pub fn new() -> Self{
        Self{
            client: ClientBuilder::new().max_redirections(1).build().expect("Unable to create http client")
        }
    }
    
    pub fn http_client(&self) -> &Client{
        &self.client
    }
}

impl Default for Context{
    fn default() -> Self{
        Self::new()
    }
}

```

## 使用
- tauri 如何使用

```rust
#[tauri::command(rename_all = "snake_case")]
async fn test(ctx: State<'_, Context>) -> Result<()> {
    let test = ctx.http_client();
    let response = client.send(
            HttpRequestBuilder::new("GET", url)?
                .response_type(ResponseType::Binary)
        ).await;
    info!("response: {:?}", response);
    Ok(())
}

fn main() {
    let context = Context::default();
    tauri::Builder::default()
        .manage(context)
        .invoke_handler(tauri::generate_handler![test
    // ...略
```

- 测试结果显示的确是使用了连接池，速度明显提高了。只创建了一个连接，后续请求都是复用这个连接。
![](/img/tauri-http.png)

## 参考
- [Tauri Http 简介](https://docs.rs/tauri/latest/tauri/api/http/index.html)
- [reqwest Client 简介](https://docs.rs/reqwest/latest/reqwest/struct.Client.html)