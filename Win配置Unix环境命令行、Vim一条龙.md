# Win配置Unix环境命令行、Vim一条龙
#技术栈/兴趣爱好/奇巧淫技
#公开笔记

## 我的选择

*   Cygwin：完整的POSIX环境
*   Windows Terminal：外观不错的终端管理
*   Git Bash For Windows：随手git方便
*   Tmux: 同一shell下多窗口管理

## Cygwin

*   安装包要留着（setup-x86_64.exe），这也是后续的包管理器
*   `$ mount` 可以看到windows系统的文件挂载
*   cygwin系统的root就是安装目录
*   cygwin内安装的git和Git Bash安装的git（基于MINGW32）是可以共用的

### 软件包

| Name     | Category |
| -------- | -------- |
| curl     | Net      |
| dos2unix | Utils    |
| tmux     | Utils    |
| git      | Devel    |
| unzip    | Archive  |
| vim      | Editors  |
| vim-doc  | Editors  |

### 用户权限

1.  用到`/etc/passwd`文件，cygwin默认不需要这个文件
2.  使用这个命令生成cygwin下的文件`$ mkpasswd -l > /etc/passwd`
3.  编辑passwd文件，每行代表一个用户，单行用`:`分割，修改第三、第四个元素为0，代表最高权限
4.  如 `<username>:*:0:0:XX-XX,XX-XX-XX:/home/<username>:/bin/bash`
5.  保存后重启shell，看到`$`变为`#`，说明生效

### Shell Prompt

*   [polyglot](https://github.com/agkozak/polyglot)
    *   轻量，无需安装
    *   纯shell脚本
*  设置bash的vi输入模式，在`.bashrc`加入`set -o vi`


## Git

### 初始化设置

*   设置后才会生成 `.gitconfig`文件
*   `$ git config --global user.name "XX"`
*   `$ git config --global user.email "XX@XX.XX"`
*   `$ git config --global --list`

## Windows Terminal

### 添加Cygwin的启动命令

*   `<cygwin_path>\bin\bash.exe -i -l`
*   启动交互式登录 shell 的方法是使用 `-i -l` 选项

### Shell外观的默认设置

#### settings.json

```json
{
    ...
    "profiles": {
        "defaults": {
                "colorScheme": "One Half Dark",
                "cursorHeight": 30,
                "cursorShape": "vintage",
                "opacity": 80,
                "scrollbarState": "visible"
        },
        ...
    }
}
```

### 如何关闭Cursor闪烁

*   这点Windows Terminal很坑，内部没有设置选项
*   打开Windows系统的键盘属性设置，设置光标闪烁速度=无

### AutoHotKey的快捷键配置

```ahk
^`::Run "wt.exe"
```

## .vimrc配置
``` vimscript
"~/.vimrc 没有plugin就是最轻量级配置
syntax on                 " 支持语法高亮显示
filetype plugin indent on " 启用根据文件类型自动缩进
set autoindent            " 开始新行时处理缩进
set expandtab             " 将制表符Tab展开为空格，这对于Python尤其有用
set tabstop=4             " 要计算的空格数
set shiftwidth=4          " 用于自动缩进的空格数
set backspace=2           " 在多数终端上修正退格键Backspace的行为
colorscheme murphy        " 修改配色
set relativenumber        " 相对行号
set wildmenu              " 自动不全文件名菜单
set wildmode=list:longest,full    " 补全为允许的最长字符串，然后打开wildmenu
set hlsearch              " 高亮每个匹配项
set incsearch             " 还未完整输入搜索命令时，就将光标动态跳转到第一个匹配处

nnoremap <c-l> :noh<enter> " 正常模式下清除高亮

" 使Vim将所有交换文件都统一存放在同一个目录中
if !isdirectory("~/.vim/swap")
    call mkdir($HOME . "/.vim/swap", "p")
endif
set directory=$HOME/.vim/swap/

" 为所有文件设置持久性撤销
set undofile
if !isdirectory("~/.vim/undodir")
  call mkdir($HOME . "/.vim/undodir", "p")
endif
set undodir=$HOME/.vim/undodir

" 初始化插件目录
if !isdirectory("~/.vim/pack/plugins/start")
  call mkdir($HOME . "/.vim/pack/plugins/start", "p")
endif
```

## tmux

### Windows Terminal 下的.bashrc配置
``` sh
# inside .bashrc
# 还有一种是直接输入 $ script -c "tmux -u" /dev/null
# tmux work with windows terminal
tmux () {
    TMUX="command tmux ${@}"
    SHELL=/usr/bin/bash script -q /dev/null -c "eval $TMUX";
}
```

### .tmux.conf配置
``` conf
set -g default-terminal "tmux-256color"

# 使用Ctrl+\作为前缀键
unbind-key C-b
set -g prefix 'C-\'
bind-key 'C-\' send-prefix

bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

# 使用-生成垂直分割
bind - split-window -v
unbind %

# 使用|生成水平分割
bind | split-window -h
unbind "
```

