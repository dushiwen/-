
# 雷达检测项目（RadarDetect）

该项目是一个基于 Qt 和 C++ 开发的雷达检测系统，旨在处理雷达数据的采集、解析与显示。该系统提供了灵活的二次开发接口，支持雷达与视频目标的检测和报警。

## 目录

- [项目简介](#项目简介)
- [功能概述](#功能概述)
- [代码结构](#代码结构)
  - [DataWorker.cpp](#dataworker.cpp)
  - [dataworker.h](#dataworker.h)
  - [main.cpp](#main.cpp)
  - [RadarDetect.pro](#radardetect.pro)
  - [Widget.cpp](#widget.cpp)
  - [Widget.h](#widget.h)
- [安装与运行](#安装与运行)
- [贡献指南](#贡献指南)
- [许可协议](#许可协议)

## 项目简介

该项目实现了一个雷达数据检测与处理系统，基于 Qt 框架提供了用户界面和后台数据处理的集成。项目支持雷达数据的采集与处理，并提供了一个可视化的 GUI 来显示数据，同时支持通过 SDK 进行二次开发，扩展数据处理逻辑。

## 功能概述

- **雷达数据采集**：支持通过外部 SDK 进行雷达数据的采集。
- **数据处理与解析**：处理并解析雷达数据，生成结构化的检测信息。
- **数据展示**：通过 Qt 界面，实时展示雷达检测到的目标和状态。
- **支持二次开发**：项目模块化设计，提供扩展接口以支持自定义逻辑和额外功能。

## 代码结构

### 1. `DataWorker.cpp`

**`DataWorker.cpp`** 实现了核心的数据处理逻辑，负责从雷达设备获取数据并进行解析。该模块是通过异步线程处理雷达传感器的输入，并将处理后的数据传递给界面显示。

- **主要功能**：
  - 读取雷达传感器的数据。
  - 解析并提取目标信息，包括目标位置、速度、方向等。
  - 实时更新处理后的数据供 GUI 显示。

- **关键实现**：
  - `processData()`: 负责从雷达设备读取原始数据，并将其解析为结构化的格式。
  - `updateData()`: 触发数据更新，将解析后的数据通过信号传递给界面。

### 2. `dataworker.h`

**`dataworker.h`** 是 `DataWorker` 类的头文件，声明了 `DataWorker` 的主要功能和数据结构。

- **主要功能**：
  - 提供数据处理的接口声明。
  - 声明了与雷达数据相关的主要结构体和枚举类型。

- **关键内容**：
  - `RadarData`: 用于存储处理后的雷达目标信息，包括目标的 ID、位置、速度和检测状态。
  - `processData()`: 该函数被声明为处理雷达数据的核心逻辑。

### 3. `main.cpp`

**`main.cpp`** 是整个应用程序的入口文件，负责初始化应用程序和主窗口，并启动 Qt 事件循环。

- **主要功能**：
  - 初始化 Qt 应用程序。
  - 创建 `Widget` 对象作为主界面，加载并显示窗口。
  - 进入事件循环，处理用户交互和数据更新。

- **关键实现**：
  - `int main(int argc, char *argv[])`: 入口函数，初始化应用程序并启动 GUI。

### 4. `RadarDetect.pro`

**`RadarDetect.pro`** 是项目的 Qt 工程文件，定义了项目的构建配置，包括项目的依赖、源文件列表等。该文件是 Qt 项目构建系统的入口。

- **主要功能**：
  - 列出项目所需的源文件和头文件。
  - 指定项目依赖的 Qt 模块（例如 `core`、`gui`）。

- **关键配置**：
  - `QT += core gui`: 指定项目依赖的 Qt 模块，使用了核心功能和 GUI 功能。
  - `SOURCES += main.cpp Widget.cpp DataWorker.cpp`: 定义了需要编译的源文件。

### 5. `Widget.cpp`

**`Widget.cpp`** 实现了 GUI 界面逻辑，负责用户界面的布局和与雷达数据处理模块的交互。该类提供了连接与断开雷达设备的接口，并在界面上显示雷达数据。

- **主要功能**：
  - 提供用户界面的布局，包括按钮、文本框和显示区域。
  - 通过 SDK 接口连接雷达设备并获取实时数据。
  - 显示数据处理结果，包括连接状态、检测目标等。

- **关键实现**：
  - `connectRader()`: 连接雷达设备，启动长连接，并通过回调函数获取实时数据。
  - `disconnectRader()`: 断开与雷达设备的连接，停止数据获取。
  - `paintEvent()`: 重绘窗口，更新显示的雷达数据图形。

### 6. `Widget.h`

**`Widget.h`** 是 `Widget` 类的头文件，定义了用户界面类的接口和成员变量。

- **主要功能**：
  - 声明了用于雷达数据展示的控件和布局。
  - 定义了与雷达设备的连接与断开操作。

- **关键内容**：
  - `QPushButton *pbtnConnect`: 用于连接雷达的按钮。
  - `QPushButton *pbtnDisconnect`: 用于断开雷达的按钮。
  - `QTextEdit *txtedtInfo`: 显示系统状态和调试信息的文本框。

## 安装与运行

### 系统要求

- **Qt**：版本 5.14 或更高
- **编译器**：支持 C++11 标准
- **操作系统**：Windows、Linux、macOS

### 编译步骤

1. 安装 [Qt 开发环境](https://www.qt.io/download)。
2. 克隆项目代码：

   ```bash
   git clone https://github.com/dushiwen/-
   ```

3. 使用 Qt Creator 打开 `RadarDetect.pro` 工程文件。
4. 编译并运行项目。

## 贡献指南

欢迎对本项目进行改进和扩展。如果你有新的功能或修复，请按照以下步骤贡献：

1. Fork 本项目到你自己的仓库。
2. 创建一个新的分支进行开发：
   ```bash
   git checkout -b new-feature
   ```
3. 提交你的更改并推送到你的分支：
   ```bash
   git commit -m "添加了新功能"
   git push origin new-feature
   ```
4. 提交 Pull Request 并详细描述你所做的更改。

