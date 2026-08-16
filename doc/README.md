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

支持动态标记：

```text
#@state=...
#@tracks
#@chapters
#@playlist
#@profiles
```

## `menu.conf` 配置说明

配置文件位置：

```text
portable_config/script-opts/menu.conf
```

如果 `font_name=` 留空，菜单会按照平台自动选择字体：

- Windows：`Microsoft YaHei UI`
- macOS：`PingFang SC`
- Linux/其他：`Noto Sans CJK SC`

## `menu.conf` 参数

| 参数                           |                   示例 | 作用                                                 |
| ------------------------------ | ---------------------: | ---------------------------------------------------- |
| `font_name`                    | `"Microsoft YaHei UI"` | 菜单字体                                             |
| `font_size`                    |                   `18` | 字号                                                 |
| `bold`                         |                   `no` | 粗体                                                 |
| `italic`                       |                   `no` | 斜体                                                 |
| `row_height`                   |                   `36` | 普通行高                                             |
| `separator_height`             |                    `6` | 分隔线高度                                           |
| `padding_x`                    |                   `13` | 水平内边距                                           |
| `padding_y`                    |                    `7` | 垂直内边距                                           |
| `root_indent_chars`            |                  `1.5` | 一级菜单文字缩进                                     |
| `child_indent_chars`           |                    `2` | 子菜单文字缩进                                       |
| `background`                   |              `#303030` | 菜单背景色                                           |
| `border`                       |              `#6A6A6A` | 外框颜色                                             |
| `border_width`                 |                    `1` | 外框宽度                                             |
| `corner_radius`                |                    `7` | 菜单圆角                                             |
| `text`                         |              `#F2F2F2` | 普通文字                                             |
| `disabled_text`                |              `#888888` | 禁用文字                                             |
| `hover_bg`                     |              `#505050` | Hover 背景                                           |
| `hover_text`                   |              `#FFFFFF` | Hover 文字                                           |
| `hover_border`                 |            `#00000000` | Hover 边框色                                         |
| `hover_border_width`           |                    `0` | Hover 边框宽度                                       |
| `hover_corner_radius`          |                    `0` | Hover 圆角                                           |
| `hover_margin_x`               |                    `1` | 控制 Hover 背景相对菜单外框左右边缘的留白            |
| `hover_margin_y`               |                    `0` | 控制上下留白。它们不会改变文字、快捷键和箭头的位置。 |
| `shortcut`                     |              `#D6D6D6` | 快捷键颜色                                           |
| `hover_shortcut`               |              `#FFFFFF` | Hover 快捷键                                         |
| `shortcut_gap`                 |                    `6` | 快捷键间距                                           |
| `arrow`                        |              `#EEEEEE` | 箭头颜色                                             |
| `arrow_alpha`                  |                    `0` | 箭头透明度                                           |
| `hover_arrow`                  |              `#FFFFFF` | Hover 箭头                                           |
| `hover_arrow_alpha`            |                    `0` | Hover 箭头透明度                                     |
| `arrow_width`                  |                   `18` | 箭头区域宽度                                         |
| `arrow_font_size`              |                   `30` | 箭头字号                                             |
| `separator`                    |              `#6A6A6A` | 分隔线颜色                                           |
| `check`                        |              `#F2F2F2` | 勾选颜色                                             |
| `shadow`                       |              `#000000` | 阴影颜色                                             |
| `bg_alpha`                     |                    `0` | 背景透明度                                           |
| `shadow_alpha`                 |                   `95` | 阴影透明度                                           |
| `shadow_blur`                  |                    `7` | 阴影模糊                                             |
| `submenu_gap`                  |                    `4` | 子菜单间距                                           |
| `screen_margin`                |                    `6` | 屏幕边距                                             |
| `min_width`                    |                  `320` | 最小宽度                                             |
| `max_width`                    |                  `640` | 最大宽度                                             |
| `max_visible_rows`             |                    `0` | 可见行限制；`0` 不按固定行数截断                     |
| `click_to_show_submenus`       |                   `no` | 是否点击后展开                                       |
| `hide_root_separators`         |                  `yes` | 隐藏一级菜单内部的分隔线                             |
| `playlist_header_indent_chars` |                    `1` | 播放列表顶部计数缩进                                 |
| `menu_z`                       |                `10000` | 菜单 OSD 层级                                        |
| `suppress_osc`                 |                  `yes` | 菜单期间抑制 OSC                                     |
| `suppress_mouse_move`          |                  `yes` | 菜单期间抑制普通鼠标移动交互                         |
| `modal_mask`                   |                  `yes` | 启用模态遮罩                                         |
| `modal_mask_alpha`             |                  `255` | 遮罩透明度                                           |
| `modal_z`                      |              `1000000` | 模态层级                                             |
| `scroll_threshold`             |                 `0.80` | 超过窗口高度该比例后启用滚动                         |
| `scrollbar_width`              |                    `5` | 滚动条宽度                                           |
| `scrollbar_gap`                |                    `0` | 滚动条与内容间距                                     |
| `scrollbar_right_gap`          |                    `1` | 右侧边距                                             |
| `scrollbar_min_thumb`          |                   `20` | 滑块最小高度                                         |
| `scrollbar_track`              |              `#555555` | 滚动轨道颜色                                         |
| `scrollbar_thumb`              |              `#2A2A2A` | 滚动滑块颜色                                         |
| `scrollbar_track_alpha`        |                   `70` | 轨道透明度                                           |
| `scrollbar_thumb_alpha`        |                  `145` | 滑块透明度                                           |
| `scroll_step`                  |                    `1` | 每次滚动步长                                         |

## 组件职责

### `menu.lua`

负责菜单绘制、布局、Hover、子菜单、滚动、播放列表定位和 Modal 层。

### `dyn_menu.lua`

负责解析 `input.conf` 并生成动态菜单，例如轨道、章节、播放列表和配置文件。

### `dialog.lua`

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

1. `scripts/menu.lua`、`dyn_menu.lua`、`dialog.lua` 在 `portable_config/scripts/` 下。
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
