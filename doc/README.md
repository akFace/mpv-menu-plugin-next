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

## `menu.conf` 配置说明

配置文件位置：

```text
portable_config/script-opts/menu.conf
```

如果 `font=` 留空，菜单会按照平台自动选择字体：

- Windows：`Microsoft YaHei UI`
- macOS：`PingFang SC`
- Linux/其他：`Noto Sans CJK SC`

### 完整配置表

| 参数                         |    默认值 | 类型   | 说明                                                                                            |
| ---------------------------- | --------: | ------ | ----------------------------------------------------------------------------------------------- |
| `font`                       |        空 | 字符串 | 菜单字体；留空时按平台自动选择字体。                                                            |
| `font_size`                  |      `22` | 数值   | 菜单正文基础字号。快捷键、正文、标题等布局以此为基础计算。                                      |
| `background`                 | `#303030` | 颜色   | 菜单背景色。使用 `#RRGGBB`。                                                                    |
| `border`                     | `#707070` | 颜色   | 菜单外边框颜色。                                                                                |
| `text`                       | `#F2F2F2` | 颜色   | 普通菜单文字颜色。                                                                              |
| `disabled_text`              | `#808080` | 颜色   | disabled/不可用项目的文字颜色。                                                                 |
| `hover`                      | `#505050` | 颜色   | 鼠标 hover 时的背景色。                                                                         |
| `shortcut`                   | `#D8D8D8` | 颜色   | 快捷键文字颜色。                                                                                |
| `separator`                  | `#808080` | 颜色   | 菜单分隔线颜色。                                                                                |
| `submenu_arrow`              | `#F0F0F0` | 颜色   | 子菜单箭头颜色。                                                                                |
| `check`                      | `#F0F0F0` | 颜色   | 勾选标记颜色。                                                                                  |
| `shadow`                     | `#000000` | 颜色   | 菜单阴影颜色。                                                                                  |
| `bg_alpha`                   |       `8` | 整数   | 菜单背景 ASS alpha，`0` 最不透明，`255` 完全透明。                                              |
| `shadow_alpha`               |     `100` | 整数   | 阴影 ASS alpha。                                                                                |
| `radius`                     |       `7` | 数值   | 菜单外框圆角半径。                                                                              |
| `border_width`               |       `1` | 数值   | 菜单外框线宽。                                                                                  |
| `hover_border_width`         |       `0` | 数值   | hover 项的边框宽度。                                                                            |
| `hover_border`               | `#656565` | 颜色   | hover 项边框颜色。                                                                              |
| `shadow_blur`                |       `6` | 数值   | 菜单阴影模糊程度。                                                                              |
| `row_height`                 |      `40` | 数值   | 普通菜单项目标高度。                                                                            |
| `min_row_height`             |      `32` | 数值   | 当屏幕高度不足时允许压缩到的最小行高。                                                          |
| `separator_height`           |       `8` | 数值   | 分隔线占用的垂直空间。                                                                          |
| `padding_x`                  |      `14` | 数值   | 菜单左右内边距基础值。                                                                          |
| `padding_y`                  |       `8` | 数值   | 菜单顶部/底部内边距基础值。                                                                     |
| `shortcut_gap`               |       `8` | 数值   | 快捷键与文字/箭头区域之间的间距。                                                               |
| `arrow_width`                |      `18` | 数值   | 子菜单箭头预留的横向区域宽度。                                                                  |
| `arrow_font_size`            |      `34` | 数值   | 子菜单箭头的字号；可单独调大/调小。                                                             |
| `submenu_gap`                |       `4` | 数值   | 父菜单和子菜单面板之间的横向间隙。                                                              |
| `screen_margin`              |       `6` | 数值   | 菜单距离 OSD 边缘的最小安全边距。                                                               |
| `min_width`                  |     `360` | 数值   | 菜单最小宽度。                                                                                  |
| `max_width`                  |     `640` | 数值   | 菜单最大宽度；超长文字会进一步使用 `…` 截断。                                                   |
| `max_visible_rows`           |       `0` | 整数   | 最大显示行数；`0` 表示不启用固定行数上限，按内容和屏幕空间自适应。                              |
| `hover_open_delay（已移除）` |    `0.08` | 秒     | 鼠标 hover 到子菜单项目后，延迟多久展开子菜单。                                                 |
| `click_to_show_submenus`     |      `no` | 布尔   | 是否要求点击才展开子菜单；`no` 表示鼠标 hover 即可展开。                                        |
| `hide_root_separators`       |     `yes` | 布尔   | 是否隐藏第一级菜单中的分隔线，以匹配当前 mpv.net 风格。                                         |
| `child_indent_chars`         |       `2` | 数值   | 二级及更深层菜单文字的缩进量，以字符宽度为单位。                                                |
| `root_indent_chars`          |     `1.5` | 数值   | 第一级菜单文字额外左缩进，以字符宽度为单位。                                                    |
| `menu_z`                     |   `10000` | 数值   | 菜单 overlay 请求的 OSD 层级值；用于尽可能压在其他 OSD 之上。                                   |
| `suppress_osc`               |     `yes` | 布尔   | 菜单模态期间的 OSC 抑制开关；主要用于配合 mpv 原生 OSC。                                        |
| `suppress_mouse_move`        |     `yes` | 布尔   | 菜单模态期间是否接管鼠标移动事件。                                                              |
| `modal_mask`                 |     `yes` | 布尔   | 是否启用全窗口透明 modal 遮罩。                                                                 |
| `modal_mask_alpha`           |     `255` | 整数   | 遮罩 ASS alpha；`255` 为完全透明，较小值会让遮罩可见。                                          |
| `modal_z`                    | `1000000` | 数值   | modal 遮罩请求的 OSD 层级值。                                                                   |
| `scroll_threshold`           |    `0.80` | 数值   | 当某一级菜单的内容高度超过当前 OSD 高度的 80% 时启用滚动容器；例如 `0.90` 表示超过 90% 才滚动。 |
| `scrollbar_width`            |       `6` | 数值   | 滚动条宽度。                                                                                    |
| `scrollbar_gap`              |       `4` | 数值   | 滚动条与菜单内容区域右侧之间的间距。                                                            |
| `scrollbar_min_thumb`        |      `24` | 数值   | 滚动条滑块的最小高度。                                                                          |
| `scrollbar_track`            | `#444444` | 颜色   | 滚动条颜色。                                                                                    |
| `scrollbar_thumb`            | `#888888` | 颜色   | 滚动条滑块颜色。                                                                                |
| `scroll_step`                |       `1` | 数值   | 鼠标滚轮每一格对应的滚动步长，以普通菜单行高为基准。                                            |

## 文件、文件夹和保存对话框

`dialog.lua` 负责桥接菜单命令与平台原生/系统文件选择器。

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
