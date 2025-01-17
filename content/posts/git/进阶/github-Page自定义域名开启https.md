---
title: "GitHub Pages HTTPS 配置指南"
date: 2019-11-03T15:36:46+08:00
draft: false
categories:
  - github
tags:
  - github-page
---
<!--more-->

## 1. 背景说明
- GitHub Pages 已与 Let's Encrypt 合作提供免费 HTTPS 服务
- 无需使用 Cloudflare CDN 也能实现 HTTPS 访问
- 配置过程简单，无需额外证书

## 2. 配置步骤

### 2.1 关闭 Cloudflare CDN
1. 登录 Cloudflare 控制面板
2. 确认域名状态为 Active
3. 关闭域名的 CDN 代理（橙色云朵图标）
   - 将 DNS 记录的代理状态设置为 DNS only（灰色云朵）

### 2.2 配置 DNS 解析
```

# 添加以下 DNS 记录
类型: A
主机记录: @
值: 185.199.108.153
    185.199.109.153
    185.199.110.153
    185.199.111.153

# 如果需要配置 www 子域名，添加 CNAME 记录
类型: CNAME
主机记录: www
值: 你的GitHub用户名.github.io
```

### 2.3 配置 GitHub Pages

1. 进入仓库设置
   - Settings > Pages

2. 更新自定义域名
   - 删除当前的 Custom domain
   - 点击 Save
   - 重新输入域名
   - 再次点击 Save

3. 确认 HTTPS 设置
   - 等待几分钟
   - 检查 "Enforce HTTPS" 选项是否自动启用

## 3. 验证配置

### 3.1 检查项目
- [ ] DNS 解析是否生效
- [ ] GitHub Pages 设置中显示域名
- [ ] "Enforce HTTPS" 选项已启用
- [ ] 网站可通过 HTTPS 访问

### 3.2 常见问题
```

# DNS 解析未生效
- 等待 DNS 记录生效（通常需要几分钟到几小时）
- 使用 dig 命令检查 DNS 解析

# HTTPS 证书问题
- 确保域名解析正确
- 等待 Let's Encrypt 证书颁发
- 检查域名 DNS 设置
```

## 4. 最佳实践

### 4.1 安全建议
1. 始终启用 "Enforce HTTPS"
2. 定期检查证书状态
3. 保持 GitHub Pages 设置更新

### 4.2 性能优化
1. 考虑使用 GitHub 自带的 CDN
2. 优化网站资源加载
3. 使用适当的缓存策略

## 5. 故障排除

### 5.1 常见错误
- DNS 解析错误
- HTTPS 证书未正确配置
- 域名验证失败

### 5.2 解决方案
1. 检查 DNS 记录配置
2. 确认域名所有权
3. 等待证书部署完成
4. 清除浏览器缓存

## 6. 参考资源
- [GitHub Pages 文档](https://docs.github.com/pages)
- [Let's Encrypt 文档](https://letsencrypt.org/docs/)
- [Cloudflare DNS 设置指南](https://developers.cloudflare.com/dns/)