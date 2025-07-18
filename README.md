# zyt_fileio_utils

[![PyPI Version](https://img.shields.io/pypi/v/zyt_fileio_utils.svg)](https://pypi.org/project/zyt_fileio_utils/)
[![License](https://img.shields.io/pypi/l/zyt_fileio_utils.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/pypi/pyversions/zyt_fileio_utils.svg)](https://www.python.org/downloads/)

**`zyt_fileio_utils`** 是一个专注于文件读写和配置管理的 Python 工具包，提供文本、JSON、TOML、YAML 等多格式的读写与配置文件处理函数，兼顾实用性和扩展性，方便开发者快速完成文件I/O及配置加载等任务。

> 📌 当前版本：`v0.1.0` ｜ 🆕 [查看更新日志 »](#更新日志)

---

## 功能特性

### 文本文件读写：
- 将列表保存或追加为 TXT 文件，每个元素单独一行。
- 从 TXT 文件读取列表，支持自动解析数据结构。
- 读取整个文本文件为字符串
- 将字符串保存为 TXT 文件，支持覆盖或追加写入文本内容。
- 兼容 str 与 pathlib.Path 类型路径参数。

### JSON 文件读写：
- 将字典保存为格式化 JSON 文件，支持中文及缩进。
- 读取 JSON 文件，加载为字典，支持递归合并默认配置。
- 读取与写入任何 JSON 支持的文件，支持中文及缩进。
- 兼容 str 与 pathlib.Path 类型路径参数。

### TOML 与 YAML 配置文件读写： 
- 将字典保存为 TOML 文件。
- 读取 TOML 配置文件，支持递归合并默认配置。
- 将字典保存为 YAML 文件。
- 读取 YAML 配置文件，支持递归合并默认配置。
- 支持递归合并嵌套字典，自动补全默认配置缺失字段。
- 兼容多种格式配置读写，方便统一管理项目配置。
- 兼容 str 与 pathlib.Path 类型路径参数。

---

## 安装

你可以通过 `pip` 安装这个工具集：

```bash
pip install zyt_fileio_utils
```

---

## API 文档

> 注：所有以 dict 为说明的参数，均接受 Python 字典或任意符合 Mapping 协议的对象（如 dict, ChainMap 等）。

<br>

### 文本文件读写（`textio`模块）

#### 🔹 **`save_list_to_txt(txt_path, data_list)`**
**功能**: 将列表数据保存到 TXT 文件中，每个元素占一行。如果文件不存在则创建，存在则追加。

**参数**:
- `txt_path` (str 或 Path): 保存文件路径。
- `data_list` (list): 待保存的数据列表。

**返回**:
- 无。

#### 🔹 **`read_list_from_txt(txt_path, parse=False)`**
**功能**: 从 TXT 文件中读取列表，支持将每行文本解析为 Python 数据结构。

**参数**:
- `txt_path` (str 或 Path): 读取文件路径。
- `parse` (bool, 可选): 是否对每行文本做 ast.literal_eval 解析，默认 False。

**返回**:
- list: 读取的列表数据。

#### 🔹 **`save_text(txt_path, text, mode="w")`**
**功能**: 保存字符串文本到文件，支持覆盖写入或追加写入。

**参数**:
- `txt_path` (str 或 Path): 文件路径。
- `text` (str): 要写入的文本内容。
- `mode` (str, 可选): 写入模式，"w" 覆盖，"a" 追加，默认 "w"。

**返回**:
- 无。

#### 🔹 **`read_text(txt_path)`**
**功能**: 读取整个文本文件内容为字符串。

**参数**:
- `txt_path` (str 或 Path): 文件路径。

**返回**:
- str: 文件内容字符串。

<br>

### JSON 文件读写（`jsonio`模块）

#### 🔹 **`save_dict_to_json(json_path, data_dict)`**
**功能**: 将字典数据保存为格式化 JSON 文件，支持中文字符。

**参数**:
- `json_path` (str 或 Path): 保存路径。
- `data_dict` (dict): 待保存的字典。

**返回**:
- 无。

**异常**:
- `TypeError`: `data_dict` 不是 Mapping 类型。

#### 🔹 **`read_dict_from_json(json_path, default={})`**
**功能**: 读取 JSON 文件为字典，如果文件不存在或解析失败，返回默认字典。支持递归合并默认配置。

**参数**:
- `json_path` (str 或 Path): 读取路径。
- `default` (dict, 可选): 默认配置字典。

**返回**:
- dict: 合并后的配置字典。

#### 🔹 **`save_json(json_path, data)`**
**功能**: 将任意合法 JSON 数据保存到文件。

**参数**:
- `json_path` (str 或 Path): 保存路径。
- `data` (任意 JSON 类型): JSON 可序列化的数据。

**返回**:
- 无。

#### 🔹 **`read_json(json_path)`**
**功能**: 读取任意合法 JSON 类型。

**参数**:
- `json_path` (str 或 Path): 读取路径。

**返回**:
- 读取的 JSON 类型数据。

<br>

### TOML 与 YAML 文件读写（`configio`模块）

#### 🔹 **`save_dict_to_toml(toml_path, data_dict)`**
**功能**: 将字典保存为 TOML 格式文件。

**参数**:
- `toml_path` (str 或 Path): 保存路径。
- `data_dict` (dict): 待保存字典。

**返回**:
- 无。

**异常**:
- `ImportError`: 未安装`toml`python包。
- `TypeError`: `data_dict` 不是 Mapping 类型。

#### 🔹 **`read_dict_from_toml(toml_path, default={})`**
**功能**: 读取 TOML 文件为字典，文件不存在或解析失败时返回默认配置，支持递归合并。

**参数**:
- `toml_path` (str 或 Path): 读取路径。
- `default` (dict, 可选): 默认配置字典。

**返回**:
- dict: 合并后的配置字典。

**异常**:
- `ImportError`: 未安装`toml`python包。
- `TypeError`: `default` 不是 Mapping 类型。

#### 🔹 **`save_dict_to_yaml(yaml_path, data_dict)`**
**功能**: 将字典保存为 YAML 格式文件。

**参数**:
- `yaml_path` (str 或 Path): 保存路径。
- `data_dict` (dict): 待保存字典。

**返回**:
- 无。

**异常**:
- `ImportError`: 未安装`pyyaml`python包。
- `TypeError`: `data_dict` 不是 Mapping 类型。

#### 🔹 **`read_dict_from_yaml(yaml_path, default={})`**
**功能**: 读取 YAML 文件为字典，文件不存在或解析失败时返回默认配置，支持递归合并。

**参数**:
- `yaml_path` (str 或 Path): 读取路径。
- `default` (dict, 可选): 默认配置字典。

**返回**:
- dict: 合并后的配置字典。

**异常**:
- `ImportError`: 未安装`pyyaml`python包。
- `TypeError`: `default` 不是 Mapping 类型。

<br>

### 使用示例

```python
from zyt_fileio_utils import save_text, read_text

# 保存字符串内容
save_text("data/output.txt", "Hello", mode='w')
save_text("data/output.txt", " World", mode='a')

# 读取内容
data = read_text("data/output.txt")

print(data)  # "Hello World"
```

```python
from zyt_fileio_utils import save_dict_to_toml, read_dict_from_toml

# 保存部分配置
save_dict_to_toml("data/output.toml", {"age": 15})

# 读取配置，使用默认值补全缺失字段
data = read_dict_from_toml("data/output.toml", default={"name": "Bob", "age": 20})

print(data)  # {"name": "Bob", "age": 15}
```

---

## 更新日志

### V0.1.0

### 2025-07-16

### 初次版本发布

### 📜 完整更新日志

 **点此查看所有历史版本和详细改动说明：**  
🔗[查看完整更新日志 »](CHANGELOG.md)

---

## 贡献

欢迎贡献代码！

## 许可证

本项目基于 [MIT 许可证](LICENSE) 开源。

## 作者

- **ZhangYuetao** - 项目开发者
- 邮箱: zhang894171707@gmail.com