
## 项目目标

我们想制作一个面向 Mindustry 玩家和初学者的 VS Code 插件，让用户能够：

- 使用比原生 mlog 更接近 C/C++ 或 Python 的高级语法；
    
- 获得 Mindustry 内置逻辑指令、变量和常量的自动补全；
    
- 查看指令参数、用途和版本信息；
    
- 编写函数、条件、循环、变量和数组；
    
- 一键将代码编译成游戏可以直接使用的 mlog；
    
- 最终支持蓝图解析、生成和处理器代码嵌入。
    

## 技术路线

项目分为三层：

1. **Mindustry 源码层**
    
    以 Mindustry v8 源码为权威来源，提取：
    
    - 逻辑指令；
        
    - `@health`、`@unit`、`@time` 等内置变量；
        
    - `sensor`、`control`、`ucontrol` 等指令的参数；
        
    - 内容类型、枚举值和版本差异。
        
2. **高级语言和编译层**
    
    第一阶段使用成熟的 Mindcode 作为编译后端：
    
    ```
    高级代码 → Mindcode → mlog
    ```
    
    Mindcode 负责处理变量、函数、循环、条件、跳转优化和 mlog 生成。以后如果需要，再开发自己的编译器。
    
3. **VS Code 插件层**
    
    插件负责：
    
    - `.mnd` 文件识别；
        
    - 语法高亮；
        
    - 自动补全；
        
    - 参数提示；
        
    - 鼠标悬停帮助；
        
    - 编译命令；
        
    - 编译错误定位；
        
    - mlog 输出和复制；
        
    - 后续蓝图工具集成。
        

## 当前已经完成

- 已下载 Mindustry 游戏源码；
    
- 已下载并构建 Mindcode；
    
- 已初始化 Mindcode 所需的 `mimex-data` 子模块；
    
- 已成功使用 Mindcode 将 `.mnd` 编译成 `.mlog`；
    
- 已建立 VS Code 插件原型；
    
- 已实现 `.mnd` 文件识别；
    
- 已实现基础语法高亮；
    
- 已实现自动补全；
    
- 已从 Mindustry v8 源码提取 53 条逻辑语句和 73 个内置访问值；
    
- 插件补全已经接入这份源码生成的数据。
    

## 当前项目位置

```
D:\Data\Git\Mindustry
```

主要目录：

```
apps\vscode-mindustry\
    VS Code 插件原型

third_party\Mindustry\
    Mindustry 游戏源码

third_party\mindcode\
    Mindcode 编译器源码

apps\vscode-mindustry\data\mindustry-v8.json
    从 Mindustry 源码提取的 v8 逻辑数据

tools\extract_mindustry_logic_v8.py
    v8 源码提取工具

examples\mindcode\
    Mindcode 示例文件

docs\
    项目说明和开发路线图
```

## 当前最重要的下一步

### 第一优先级：完善源码数据提取

目前已经提取了指令名称，但还需要继续提取：

- 参数数量；
    
- 参数顺序；
    
- 参数名称；
    
- 参数类型；
    
- 可用枚举值；
    
- 适用处理器；
    
- v7/v8 版本差异；
    
- 中文说明。
    

目标是让输入：

```
sensor
```

时显示：

```
sensor(result, object, property)
读取建筑、单位或其他对象的属性
```

### 第二优先级：改善 VS Code 使用体验

需要增加：

- 参数占位补全；
    
- 鼠标悬停帮助；
    
- 指令搜索；
    
- 中文说明；
    
- 编译错误定位；
    
- v8.2、v8.1、v7 等版本选择；
    
- 一键复制 mlog。
    

### 第三优先级：设计自己的语言层

暂时不直接重写完整编译器，而是先确定一种适合初学者的语法：

```
我们的高级语法 → Mindcode → mlog
```

先确保语法简单、补全清晰、错误容易理解。

### 第四优先级：蓝图工具

逻辑编辑器稳定后，再加入：

- 蓝图字符串导入；
    
- `.msch` 文件解析；
    
- 建筑布局读取；
    
- 处理器链接读取；
    
- Mindcode 嵌入处理器；
    
- 蓝图导出；
    
- 蓝图和逻辑联动。
    

## 推荐的分工

### 我负责

- Mindustry 源码分析；
    
- v8 指令数据提取；
    
- 编译流程；
    
- mlog 生成；
    
- 插件核心功能；
    
- 蓝图格式研究。
    

### 同伴可以负责

- VS Code 界面和交互；
    
- 补全显示效果；
    
- 中文文档；
    
- 示例代码；
    
- 测试不同 Mindustry 版本；
    
- 蓝图设计器界面；
    
- 用户体验和项目文档。
    

## 第一阶段目标

先完成一个稳定的最小版本：

1. 打开 `.mnd` 文件；
    
2. 输入 `sensor`、`ucontrol`、`@health` 时出现准确补全；
    
3. 显示参数模板和中文说明；
    
4. 按快捷键编译成 `.mlog`；
    
5. 将 mlog 粘贴进 Mindustry 后可以运行。
    

完成这个版本后，再扩展复杂语法和蓝图功能。