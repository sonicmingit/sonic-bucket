# sonic-bucket
scoop自用源


# 说明
要创建自己的 Scoop bucket（软件库），你可以按照以下步骤进行操作：

### 1. 创建一个 Git 仓库

首先，你需要在 GitHub、GitLab 或其他 Git 托管平台上创建一个新的 Git 仓库，用来存放你要发布的软件包定义文件。

仓库名称可以随意选择，比如 my-scoop-bucket。

### 2. 初始化 Bucket 结构

在本地克隆你的仓库，然后在其中创建一个基础的 bucket 目录结构。通常情况下，你可以直接在仓库根目录下开始：

#### 创建 bucket 文件夹：

在你的本地仓库中，创建一个名为 bucket 的文件夹。
所有的 .json 文件（即软件包定义文件）都应放在这个文件夹内。

```bash
mkdir <your-bucket-name>
cd <your-bucket-name>
```

### 3. 添加 Manifest 文件

添加软件的 manifest 文件：

在 bucket 文件夹内，为每个你要发布的软件包创建一个 .json 文件。
文件名通常与软件包的名称一致，例如 example-software.json。
确保 .json 文件格式正确，定义了版本号、下载链接、哈希值等必要信息。


Scoop 使用 JSON 格式的 Manifest 文件来定义软件包的安装信息。在你的 bucket 中，每个软件包对应一个独立的 JSON 文件。文件名通常与软件包名称相同，例如 `example-software.json`。以下是一个简单的 Manifest 模板：


```json
{
    "version": "1.0.0",
    "description": "Example software description",
    "homepage": "https://example.com",
    "license": "MIT",
    "url": "https://example.com/downloads/example-software-1.0.0.zip",
    "hash": "SHA256:your-file-sha256-hash",
    "bin": "example-software.exe",
    "checkver": {
        "url": "https://example.com/version",
        "regex": "v([\\d.]+)"
    },
    "autoupdate": {
        "url": "https://example.com/downloads/example-software-$version.zip",
        "hash": {
            "url": "https://example.com/downloads/sha256sums.txt"
        }
    }
}
```

- **version**: 软件的当前版本号。
- **description**: 软件的描述。
- **homepage**: 软件的主页链接。
- **license**: 软件的许可证类型。
- **url**: 下载软件的地址。
- **hash**: 软件包的 SHA256 哈希值，用于验证下载的文件是否完整。
- **bin**: 安装后的可执行文件路径，可以是一个字符串或字符串数组。
- **checkver**: 可选，定义检查软件新版本的规则。
- **autoupdate**: 可选，定义自动更新时的下载链接和哈希值的规则。

### 4. 提交并推送

将 JSON 文件提交到你的仓库并推送到远程：

```bash
git add .
git commit -m "Add example software"
git push origin main
```

### 5. 在 Scoop 中添加你的 Bucket

你可以通过以下命令在 Scoop 中添加你的 bucket：

```bash
scoop bucket add <your-bucket-name> <your-bucket-repo-url>
scoop bucket add sonicoop https://github.com/sonicmingit/sonic-bucket
```

替换 `<your-bucket-name>` 为你选择的 bucket 名称，`<your-bucket-repo-url>` 为你的 Git 仓库地址。

查看bucket信息

```
# 已安装的 bucket
scoop bucket list

# 列出 bucket 中的所有软件
scoop search <bucket_name>/

```



### 6. 安装和测试

在添加你的 bucket 后，可以通过 Scoop 来安装测试你的软件包：

```bash
scoop install <software-name>
```

### 7. 维护和更新

在日后，你可以随时更新 Manifest 文件以发布新版本的软件，或者添加新的软件包到同一个 bucket 中。

### 8. 目录结构示例：


```
my-scoop-bucket/
│
└─── bucket/
     ├── example-software.json
     ├── another-software.json
     └── ... (更多软件包的json文件)

```