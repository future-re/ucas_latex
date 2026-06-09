# UCAS LaTeX Thesis Template

中国科学院大学学位论文 LaTeX 模板，适合在 Windows 环境下使用 `MiKTeX + VS Code + LaTeX Workshop` 进行写作与编译。

## 推荐环境

- Windows 10 / 11
- [MiKTeX](https://miktex.org/download)
- [Visual Studio Code](https://code.visualstudio.com/)
- VS Code 扩展: `LaTeX Workshop`

不建议新手一开始手动拼装复杂命令链。这个仓库已经自带 `artratex.bat`，直接调用即可完成编译。

## 1. 安装 MiKTeX

### 1.1 下载与安装

1. 打开 MiKTeX 官网并下载安装包。
2. 按默认选项安装即可。
3. 安装完成后，打开 `MiKTeX Console`。

### 1.2 建议设置

在 `MiKTeX Console` 中检查以下项目：

- `Settings -> General -> Install missing packages on-the-fly`
  建议设为 `Ask me first` 或 `Yes`
- 确认可以正常更新 MiKTeX 宏包

第一次编译论文时，MiKTeX 可能会提示安装缺失宏包，这是正常现象。

## 2. 安装 VS Code 与 LaTeX Workshop

### 2.1 安装 VS Code

从官网安装 `Visual Studio Code`。

### 2.2 安装扩展

在 VS Code 扩展市场搜索并安装：

- `LaTeX Workshop`

推荐使用这个扩展，原因很直接：

- 能直接在 VS Code 内预览 PDF
- 能快速跳转编译错误
- 能管理 TeX 构建流程
- 适合日常写论文，不需要频繁切换工具

## 3. 打开项目

建议直接用 VS Code 打开整个仓库文件夹，而不是只打开单个 `.tex` 文件。

主文件是：

- `Thesis.tex`

正文与附录等内容在：

- `Tex/`

参考文献在：

- `Biblio/ref.bib`

图片资源在：

- `Img/`

## 4. 当前仓库的 VS Code 配置

本仓库已经提供了 [.vscode/settings.json](./.vscode/settings.json)，核心作用如下：

- 禁用 LaTeX Workshop 的自动编译
- 使用外部脚本 `artratex.bat` 进行编译
- 将 PDF 输出到 `Tmp/`
- 让 VS Code 预览器从 `Tmp/Thesis.pdf` 读取结果

因此你不需要自己再手写复杂的 `xelatex` / `bibtex` 命令。

## 5. 如何编译

### 方法一：推荐，直接运行批处理脚本

在项目根目录下运行：

```powershell
.\artratex.bat
```

编译结果会生成到：

- `Tmp/Thesis.pdf`

### 方法二：在 VS Code 中使用 LaTeX Workshop

如果已经打开整个项目：

1. 打开 `Thesis.tex`
2. 执行 `LaTeX Workshop: Build LaTeX project`
3. 再执行 `LaTeX Workshop: View LaTeX PDF file`

注意：

- 不要单独编译 `Tex/Appendix.tex`、`Tex/Backmatter.tex` 这类子文件
- 必须编译 `Thesis.tex`

因为这些章节文件只是通过 `\input{...}` 被主文件包含，并不是独立文档。

## 6. 输出文件说明

编译产生的中间文件和 PDF 都在：

- `Tmp/`

这是模板设计的一部分，目的是保持根目录整洁。

所以如果你看到类似报错：

```text
Cannot view file PDF file. File not found: Thesis.pdf
```

通常不是没编译成功，而是 PDF 实际在：

- `Tmp/Thesis.pdf`

## 7. 常用写作位置

你通常只需要改这些文件：

- `Thesis.tex`
  主控文件，一般只改整体结构和全局设置
- `Tex/Frontinfo.tex`
  论文题目、作者、院系等封面信息
- `Tex/Frontmatter.tex`
  中英文摘要、关键词
- `Tex/Mainmatter.tex`
  正文章节入口
- `Tex/Chap_Intro.tex`
  章节内容示例
- `Tex/Appendix.tex`
  附录
- `Tex/Backmatter.tex`
  致谢、作者简历等
- `Biblio/ref.bib`
  参考文献

## 8. 常见问题

### 8.1 为什么打开子文件全是空白

因为像 `Tex/Appendix.tex` 这样的文件不是主文档，单独编译不会得到完整结果。请编译：

```text
Thesis.tex
```

### 8.2 为什么会出现空白页

模板默认是双面排版，且摘要、目录、正文、参考文献、附录、致谢等部分通常要求从右页开始，所以会自动插入空白页。这通常不是错误。

### 8.3 为什么第一次编译很慢

因为 MiKTeX 可能会自动下载缺失宏包，第一次慢是正常的，后续会快很多。

### 8.4 为什么 GitHub 推送总弹账号选择

如果你使用 HTTPS 远程地址，Windows 上可能会反复触发账号选择。建议改用 SSH。

## 9. 推荐工作流

推荐按照下面的方式使用：

1. 安装 MiKTeX
2. 安装 VS Code
3. 安装 `LaTeX Workshop`
4. 打开本项目根目录
5. 编辑 `Thesis.tex` 和 `Tex/` 下各章节
6. 用 `artratex.bat` 或 LaTeX Workshop 编译
7. 在 VS Code 中直接预览 `Tmp/Thesis.pdf`

这样配置最稳定，也最适合论文长期写作。
