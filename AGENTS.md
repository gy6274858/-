# AGENTS.md

## Cursor Cloud specific instructions

本仓库是一个**纯数据仓库**（个人减脂记录），不是软件项目。

- 内容仅有两个文件：`README.md` 和 `减脂记录.xlsx`（Excel 表格）。
- 没有源代码、包管理清单、构建系统或可运行的服务，因此**没有可执行的 lint / test / build / run 步骤**，也没有需要安装的项目依赖。
- `减脂记录.xlsx` 包含 6 个工作表：`体重记录`、`运动汇总`、`运动详情`、`每日总览`、`使用说明`、`食谱`。

### 如何查看/校验数据文件

环境未预装 `openpyxl` / `pandas` / LibreOffice。`.xlsx` 本质是一个 zip 包，可**仅用 Python 标准库**（`zipfile` + `xml.etree`）读取，无需安装任何依赖：

- 注意 `xl/_rels/workbook.xml.rels` 中的 worksheet 目标路径可能是**绝对路径**（以 `/` 开头，如 `/xl/worksheets/sheet1.xml`）；解析时若以 `/` 开头需去掉前缀，否则相对 `xl/` 目录拼接。
- 文本单元格使用**内联字符串**（`t="inlineStr"`），`sharedStrings.xml` 为空；读取文本时需处理 `inlineStr` 情况，否则文本列会显示为空。

如需更便捷的读取，可临时 `pip install openpyxl`，但这不是仓库依赖，无需写入更新脚本。
