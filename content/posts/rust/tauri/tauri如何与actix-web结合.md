---
title: "Tauri如何与actix Web结合"
description: 
date: 2024-05-11T10:17:42+08:00
draft: false
categories:
  - tauri
tags:
  - tauri
  - actix-web
---
<!--more-->

- [Tauri如何与actix Web结合](#tauri如何与actix-web结合)
  - [actix-web](##actix-web)
  - [actix-web与tauri结合](##actix-web与tauri结合)
  - [参考](##参考)

# 文件目录
```txt
│   ├── src
│   │   ├── main.rs
│   │   └── server
│   │       └── mod.rs
```

# Tauri如何与actix Web结合
- Tauri是一个用于构建现代桌面应用程序的工具包，它使用web技术来构建应用程序，同时提供了一些原生API来访问系统资源。
- actix-web是一个基于Rust的Web框架，它提供了高性能的HTTP服务，可以用于构建Web应用程序。
- 本文将介绍如何将Tauri与actix-web结合，以实现一个桌面应用程序。

## actix-web
- actix-web是一个基于Rust的Web框架，它提供了高性能的HTTP服务，可以用于构建Web应用程序。
- actix-web使用actor模型来处理HTTP请求，每个请求都会被封装成一个actor，然后由系统调度执行。
- 在server模块中创建一个新的actix-web应用程序。

```rust
use actix_web::{get, middleware, web, App, HttpServer};
use tauri::{AppHandle, Manager};

pub struct TauriAppState {
    app: AppHandle,
}

#[get("/")]
pub async fn handle(app: web::Data<TauriAppState>) -> actix_web::Result<String> {
    let main_window = app.app.get_window("main").unwrap();
    main_window.show().unwrap();
    main_window.set_focus().unwrap();
    Ok("".to_string())
}

#[actix_web::main]
pub async fn init(_app: AppHandle) -> std::io::Result<()> {
    let tauri_app = web::Data::new(TauriAppState {
        app: _app,
    });
    HttpServer::new(move || {
        App::new()
            .app_data(tauri_app.clone())
            .wrap(middleware::Logger::default())
            .service(handle)
    })
    .bind(("127.0.0.1", 3001))?
    .run()
    .await
}
```

## actix-web与tauri结合
- 在main.rs中启动actix-web应用程序。

```rust
// Prevents additional console window on Windows in release, DO NOT REMOVE!!
#![cfg_attr(not(debug_assertions), windows_subsystem = "windows")]

mod server;
use std::{thread, vec};

use tauri::{CustomMenuItem, Manager, SystemTray, SystemTrayEvent, SystemTrayMenu, SystemTrayMenuItem};
use tauri_plugin_autostart::MacosLauncher;

// Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
#[tauri::command]
fn greet(name: &str) -> String {
    format!("Hello, {}! You've been greeted from Rust!", name)
}

fn main() {
    tauri::Builder::default()
    .setup(|app| {
        let app_handle = app.handle();
        let boxed_app_handle = Box::new(app_handle);
        thread::spawn(move || {
            server::init(*boxed_app_handle).expect("failed to start actix server");
        });
        Ok(())
    })
        .invoke_handler(tauri::generate_handler![greet])
        .run(tauri::generate_context!())
        .expect("error while running tauri application")
}
```

## 参考
- [Tauri](https://tauri.app/zh-cn/v1/guides/getting-started/setup/)
- [actix-web](https://actix.rs/docs/)