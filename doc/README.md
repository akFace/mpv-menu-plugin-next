# mpv-menu-plugin-next — mpv 跨平台右键选项菜单插件

## `input.conf` 如何定义菜单

菜单项目通过 `#menu:` 注释定义，命令本身仍然是普通 mpv `input.conf` 命令。例如：

```text
Ctrl+1  add contrast -1       #menu: 视频 > 调色 > 对比度 -1
Ctrl+2  add contrast  1       #menu: 视频 > 调色 > 对比度 +1
_       ignore                #menu: 视频 > 调色 > -
```

这里：

- `Ctrl+1`：菜单中显示的`快捷键`。
- `add contrast -1`：真正执行的 mpv 命令。
- `视频 > 调色 > 对比度 -1`：菜单层级和显示文字。
- `-`：表示分隔线。
- [完整示例：Full example](https://github.com/akFace/mpv-menu-plugin-next/tree/main/example)

再例如：

```text
Enter   cycle fullscreen  #menu: 窗口 > 全屏 #@state=(fullscreen and 'checked')
```

会把 `窗口 > 全屏` 做成一个带动态勾选状态的菜单项。

### 动态菜单标记

`input.conf` 可以使用动态标记，`dyn_menu.lua` 会根据当前 mpv 状态重新生成菜单内容：

| 标记                     | 作用                                                         |
| ------------------------ | ------------------------------------------------------------ |
| `#@tracks`               | 轨道总菜单                                                   |
| `#@tracks/video`         | 视频轨道                                                     |
| `#@tracks/audio`         | 音频轨道                                                     |
| `#@tracks/sub`           | 主字幕轨道                                                   |
| `#@tracks/sub-secondary` | 次字幕轨道                                                   |
| `#@chapters`             | 章节                                                         |
| `#@editions`             | 版本/edition                                                 |
| `#@audio-devices`        | 音频输出设备                                                 |
| `#@playlist`             | 播放列表                                                     |
| `#@profiles`             | mpv 配置文件/profiles                                        |
| `#@state=(...)`          | 根据 mpv 属性动态生成 `checked` / `disabled` / `hidden` 状态 |

`script-opts/dyn_menu.conf` 当前包含 `max_playlist_items`：设置为 `0` 表示不截断播放列表，完整生成并交给菜单滚动容器处理。

## `menu_style.conf` 配置说明

配置文件位置：

```text
portable_config/script-opts/menu_style.conf
```

如果 `font_name=` 留空，菜单会按照平台自动选择字体：

- Windows：`Microsoft YaHei UI`
- macOS：`PingFang SC`
- Linux/其他：`Noto Sans CJK SC`

### 完整配置表

| 参数                           |  当前值 | 功能                                                     |
| ------------------------------ | ------: | -------------------------------------------------------- |
| `font_name`                    |      '' | 指定字体名称                                             |
| `font_size`                    |      18 | 菜单字号                                                 |
| `bold`                         |   false | 是否粗体                                                 |
| `italic`                       |   false | 是否斜体                                                 |
| `row_height`                   |      26 | 普通菜单行高                                             |
| `separator_height`             |       8 | 分隔线高度                                               |
| `padding_x`                    |      14 | 菜单内容左右内边距                                       |
| `padding_y`                    |       4 | 菜单上下内边距                                           |
| `root_indent_chars`            |       1 | 一级菜单文字缩进                                         |
| `child_indent_chars`           |       1 | 子菜单文字缩进                                           |
| `background`                   | #303030 | 菜单背景色                                               |
| `radius`                       |       7 | 菜单圆角                                                 |
| `border`                       | #6F6F6F | 菜单外框色                                               |
| `border_width`                 |       1 | 外框宽度                                                 |
| `text`                         | #F2F2F2 | 普通文字颜色                                             |
| `disabled_text`                | #8A8A8A | 禁用文字颜色                                             |
| `hover_bg`                     |      '' | Hover 背景色                                             |
| `hover_text`                   |      '' | Hover 文字色                                             |
| `hover_border`                 | #656565 | Hover 边框颜色                                           |
| `hover_border_width`           |     0.5 | Hover 边框宽度                                           |
| `hover_corner_radius`          |       7 | Hover 圆角                                               |
| `hover_margin_x`               |       1 | Hover 背景左右留白                                       |
| `hover_margin_y`               |       0 | Hover 背景上下留白                                       |
| `shortcut`                     | #D0D0D0 | 普通快捷键颜色                                           |
| `hover_shortcut`               |      '' | Hover 快捷键颜色                                         |
| `shortcut_gap`                 |       8 | 标题和快捷键布局间距                                     |
| `shortcut_right_gap`           |       0 | 快捷键右侧对齐基准                                       |
| `playlist_shortcut_right_gap`  |       6 | 播放列表右侧格式后缀额外距离                             |
| `arrow`                        |      '' | 子菜单箭头颜色                                           |
| `arrow_char`                   |     '›' | 子菜单箭头字符号（比如： »,→, ->）                       |
| `arrow_alpha`                  |       0 | 普通箭头透明度                                           |
| `hover_arrow`                  |      '' | Hover 箭头颜色                                           |
| `hover_arrow_alpha`            |       0 | Hover 箭头透明度                                         |
| `arrow_width`                  |      18 | 箭头区域宽度                                             |
| `arrow_font_size`              |      24 | 箭头字号                                                 |
| `separator`                    | #BEBEBE | 分隔线颜色                                               |
| `check`                        | #F0F0F0 | 勾选颜色                                                 |
| `shadow`                       | #000000 | 阴影颜色                                                 |
| `bg_alpha`                     |       8 | 菜单背景透明度                                           |
| `shadow_alpha`                 |     100 | 阴影透明度                                               |
| `shadow_blur`                  |       6 | 阴影模糊                                                 |
| `submenu_gap`                  |       4 | 子菜单间距                                               |
| `screen_margin`                |       6 | 菜单距离 OSD 边缘的最小距离                              |
| `min_width`                    |     360 | 菜单最小宽度                                             |
| `max_width`                    |     640 | 菜单最大宽度                                             |
| `max_visible_rows`             |       0 | 最大可见行数配置项                                       |
| `click_to_show_submenus`       |   false | 是否要求点击才展开子菜单                                 |
| `hide_root_separators`         |    true | 是否隐藏一级菜单内部的分隔线                             |
| `playlist_header_indent_chars` |       1 | 播放列表顶部计数缩进                                     |
| `modal_mask`                   |    true | 是否启用全屏模态遮罩                                     |
| `modal_mask_alpha`             |     255 | 模态遮罩透明度                                           |
| `modal_z`                      | 1000000 | 模态遮罩层级                                             |
| `scroll_threshold`             |    0.80 | 超过窗口高度多少比例后进入滚动                           |
| `scrollbar_width`              |       6 | 滚动条宽度                                               |
| `scrollbar_gap`                |       4 | 滚动条与内容区域间距                                     |
| `scrollbar_right_gap`          |       2 | 滚动条与右边框间距                                       |
| `scrollbar_min_thumb`          |      24 | 滚动条滑块最小高度                                       |
| `scrollbar_track`              | #555555 | 滚动条轨道颜色                                           |
| `scrollbar_thumb`              | #222222 | 滚动条滑块颜色                                           |
| `scrollbar_track_alpha`        |     150 | 滚动轨道透明度                                           |
| `scrollbar_thumb_alpha`        |     115 | 滚动滑块透明度                                           |
| `scroll_step`                  |       1 | 单次滚动步长                                             |
| **自适应屏幕分辨率配置**       |         |                                                          |
| `ui_scale`                     |    auto | UI 缩放根据当前 OSD 分辨率自动计算。填空值不再自适应缩放 |
| `design_width`                 |    1920 | 设计基准分辨率                                           |
| `design_height`                |    1080 | 设计基准分辨率                                           |
| `min_ui_scale`                 |     0.8 | 最小缩放范围                                             |
| `max_ui_scale`                 |     2.5 | 最大缩放范围                                             |
| `macos_font_scale`             |     1.0 | macos 字体视觉补偿                                       |

## 组件职责

#### `menu.lua`

负责菜单绘制、布局、Hover、子菜单、滚动、播放列表定位和 Modal 层。

#### `dyn_menu.lua`

负责解析 `input.conf` 并生成动态菜单，例如轨道、章节、播放列表和配置文件。

#### `dialog.lua`

负责文件选择、文件夹选择、保存以及剪贴板等辅助功能。

### Windows

当前首选路径采用 `mp.utils.subprocess()` 调用 PowerShell，再使用 .NET 图形文件对话框；文件选择、文件夹选择、保存对话框均通过独立 subprocess 完成。打开文件时会返回 UTF-8 路径，并按 `input.conf` 选择 `replace` / `append` 等动作。

### macOS

使用 `osascript` 调用系统的 `choose file` / `choose folder` / `choose file name`。

### Linux

按可用性自动查找：

1. `zenity`
2. `kdialog`
3. `yad`

如果系统没有这些工具，文件对话框功能会提示缺少依赖。

## 剪贴板

剪贴板后端按平台选择：

| 平台    | 读取                          | 写入                         |
| ------- | ----------------------------- | ---------------------------- |
| Windows | PowerShell `Get-Clipboard`    | PowerShell `Set-Clipboard`   |
| macOS   | `pbpaste`                     | `pbcopy`                     |
| Linux   | `wl-paste` → `xclip` → `xsel` | `wl-copy` → `xclip` → `xsel` |

Linux 需要系统中至少存在一组可用的剪贴板命令。

## 故障排查

### 菜单完全不显示

确认：

1. `scripts/menu/menu.lua`、`dyn_menu.lua`、`dialog.lua` 在 `portable_config/scripts/menu` 下。
2. 没有同时加载旧 `menu.dll`。
3. `input.conf` 存在并包含 `#menu:` 定义。

### 右键菜单打开，但动态项目为空

播放文件后重新打开菜单。当前版本会在 `file-loaded`、`start-file` 和右键打开前刷新动态菜单。

### Windows 文件选择框失败

先确认 PowerShell 可执行文件可用；当前 Windows 路径会优先寻找系统 PowerShell，并通过 `mp.utils.subprocess()` 调用。

### Linux 文件选择框失败

确认至少安装：

```text
zenity
```

或：

```text
kdialog
```

或：

```text
yad
```
