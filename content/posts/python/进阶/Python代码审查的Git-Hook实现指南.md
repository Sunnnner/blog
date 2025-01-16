---
title: "Python代码审查的Git Hook实现指南"
description: 
date: 2025-01-16T16:14:01+08:00
draft: false
categories:
  - python
tags:
  - python
  - git
---
<!--more-->


## Git Hook简介
Git Hook是在Git操作（如commit、push等）执行前后自动运行的脚本，可用于实现代码质量控制、工作流程自动化等功能。本文将介绍如何利用Git Hook实现Python代码的自动审查。

## 实现步骤

### 1. 环境准备
在开始之前，请确保已安装以下工具：
- Python 3.11或更高版本
- poetry
- Git

安装所需的Python包：
```bash
poetry add ruff mypy
```

### 2. 项目配置
#### 创建配置文件
在项目根目录创建`pyproject.toml`文件，配置代码检查工具。

##### Ruff配置
```toml
[tool.ruff.lint]
select = [
    "E",  # pycodestyle错误
    "W",  # pycodestyle警告
    "F",  # pyflakes
    "I",  # isort
    "B",  # flake8-bugbear
    "C4", # flake8-comprehensions
    "UP", # pyupgrade
    "ARG001", # 未使用的函数参数检查
]
ignore = [
    "E501", # 行长度超限（由black处理）
    "B008", # 函数参数默认值中的函数调用
    "W191", # 使用tab缩进
    "B904", # 允许不带from子句的异常抛出
]

[tool.ruff.lint.pyupgrade]
keep-runtime-typing = true  # 保留运行时类型注解

[tool.ruff.format]
quote-style = "double"  # 使用双引号
```

##### Mypy配置
```toml
[tool.mypy]
python_version = "3.11"
install_types = true
check_untyped_defs = true
files = ["*.py"]
allow_redefinition = true

[[tool.mypy.overrides]]
module = "isodate.*"
ignore_missing_imports = true
```

### 3. Git Hook脚本设置

#### 创建安装脚本
在项目根目录创建`.script`文件夹，并添加以下安装脚本：

```bash
#!/bin/bash
# .script/setup.sh
set -e
PROJECT_ROOT=$(git rev-parse --show-toplevel)

setup_hook() {
    local name=$1
    local hook_path="${PROJECT_ROOT}/.git/hooks/${name}"
    local script_path="${PROJECT_ROOT}/.script/${name}.sh"
    
    mkdir -p "${PROJECT_ROOT}/.git/hooks"
    
    cat > "$hook_path" << EOF
#!/bin/bash
set -e
bash "${script_path}"
EOF
    
    chmod +x "$hook_path"
    echo "成功设置 ${hook_path}"
}

setup_hook "pre-commit"
```

#### 创建pre-commit脚本
在`.script`文件夹中创建pre-commit脚本：

```bash
#!/bin/bash
# .script/pre-commit.sh
set -e
PROJECT_ROOT_DIR=$(git rev-parse --show-toplevel)
cd $PROJECT_ROOT_DIR

# 获取待提交的Python文件
py_files=$(git --no-pager diff --cached --name-only --diff-filter=d | grep '\.py$' || true)

if [ ! -z "$py_files" ]; then
    # 代码格式化和自动修复
    ruff format
    ruff check --fix
    
    # 重新添加修改后的文件
    echo "$py_files" | while read file; do
        if [ ! -z "$file" ]; then
            git add "$file"
        fi
    done
    
    # 最终代码检查
    ruff check
    mypy
fi
```

### 4. 部署步骤
1. 为脚本添加执行权限：
```bash
chmod +x .script/setup.sh
chmod +x .script/pre-commit.sh
```

2. 运行安装脚本：
```bash
.script/setup.sh
```

### 5. 工作原理
- 当执行`git commit`时，pre-commit hook会自动运行
- 对暂存区中的Python文件进行以下处理：
  - 使用ruff进行代码格式化
  - 自动修复可修复的代码问题
  - 运行代码质量检查
  - 执行类型检查
- 如果检查未通过，commit将被阻止

### 6. 注意事项
- 确保所有团队成员都安装了必要的依赖包
- 建议在项目README中说明代码规范和Hook的使用方法
- 可根据项目需求调整ruff和mypy的配置规则
