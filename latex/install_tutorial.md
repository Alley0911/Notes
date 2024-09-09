# 利用远程linux服务器，结合vscode进行latex编辑的部署步骤
1. 下载Tex Live
[下载地址](http://mirrors.cqu.edu.cn/CTAN/systems/texlive/Images/)
上次下载的是texlive2024.iso
2. 在远程linux服务器上安装
   ```shell
   # 创建挂载文件夹
   sudo mkdir /mnt/temp
   # 挂载iso文件
   sudo mount texlive2024-20240312.iso /mnt/temp
   # 安装
   cd /mnt/temp
   sudo ./install-tl
   # 进入安装界面后直接输入<i>回车
   # 添加环境变量到~/.bashrc, 并运行source ~/.bashrc
    #tex live 2024
    export MANPATH=${MANPATH}:/usr/local/texlive/2024/texmf-dist/doc/man
    export INFOPATH=${INFOPATH}:/usr/local/texlive/2024/texmf-dist/doc/info
    export PATH=${PATH}:/usr/local/texlive/2024/bin/x86_64-linux
   # 验证安装是否成功
   latex -version
   ```
3. 在本地vscdoe上配置
   1. 首先需要连接该远程服务器
   2. 安装LaTeX Workshop插件
   3. 配置vscdoe的Latex编译信息
   File -> preference -> settings -> json配置文件点右上角的小图标
   将下面这段内容添加进去, 注意不是直接覆盖.
   ```json
       // LaTeX配置
    //自动换行
    "[latex]": {
        "editor.wordWrap": "on"
    },
    //默认应用上次使用的方法来编译
    "latex-workshop.latex.recipe.default": "lastUsed",
    //补全提示时显示 Unimath 符号
    "latex-workshop.intellisense.unimathsymbols.enabled": true,
    //从已引用的包中补全
    "latex-workshop.intellisense.package.enabled": true,
    "latex-workshop.view.pdf.viewer": "tab",

    "latex-workshop.latex.recipes": [
        {
            "name": "pdfLaTeXmk",
            "tools": [
                "pdfLaTeXmk"
            ]
        },
        {
          "name": "XeLaTeXmk",
          "tools": [
              "XeLaTeXmk"
          ]
        },
        {
          "name": "pdflatex -> bibtex -> pdflatex*2",
          "tools": [
              "pdflatex",
              "bibtex",
              "pdflatex",
              "pdflatex"
          ]
        },
        {
          "name": "latexmk",
          "tools": [
              "latexmk"
          ]
        },
        {
          "name": "xelatex",
          "tools": [
              "xelatex"
          ]
        }, 
        ],

        "latex-workshop.latex.tools": [
        {
            "name": "XeLaTeXmk",
            "command": "latexmk",
            "args": [
                "-xelatex",
                "-synctex=1",
                "-shell-escape",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "pdfLaTeXmk",
            "command": "latexmk",
            "args": [
                "-pdflatex",
                "-synctex=1",
                "-shell-escape",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
        "name": "latexmk",
        "command": "latexmk",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
        }, {
        "name": "xelatex",
        "command": "xelatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
        }, 
        {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
        }, {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
          "%DOCFILE%"
        ]
        }],
        "latex-workshop.view.pdf.viewer": "tab",
        "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk"
        ],
   ```
   4. reload window
   5. 随便打开一个tex文件, 自动保存就可以自动编译了
   6. ctrl+alt+v可以在右侧显示编辑结果
   7. 在右侧pdf文件中按住ctrl+鼠标键就可以从pdf中的位置跳转到tex文件对应的位置
