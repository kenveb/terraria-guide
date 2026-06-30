# Windows PowerShell 编码陷阱记录

## 问题回顾

1. **首次乱码**：PowerShell 批量替换后，`—`（U+2014）变成 `鈥?`
2. **文件全损坏**：用正则 `-replace` 修复乱码时，正则匹配异常，在每个字符间插入 `—`

## 根因

### 问题1：`Set-Content -Encoding UTF8` 编码损坏

Windows PowerShell 5.1 的 `Set-Content -Encoding UTF8` 在读写含多字节 UTF-8 字符的文件时，内部编码转换可能出错。`—` 的 UTF-8 字节 `E2 80 94` 被错误转成 `E9 88 A5 3F`，浏览器显示为 `鈥?`。

**触发条件**：先 `Get-Content` 读入字符串 → 做替换 → 再 `Set-Content -Encoding UTF8` 写回。

### 问题2：正则替换灾难

```powershell
$text -replace '鈥\?', '—'
```

`-replace` 用的是 .NET 正则。`\?` 在 .NET 正则中仍有歧义，匹配行为异常。更关键的是 `鈥?` 可能匹配空字符串位置，导致每个字符间都插入 `—`。

**教训**：对含非 ASCII 字符的字符串做替换，**永远不要用正则**，用 `string.Replace()` 纯字符串替换。

## 正确做法

### 读写文件

```powershell
# 读 — 用 .NET API，不用 Get-Content
$text = [System.IO.File]::ReadAllText($path, [System.Text.Encoding]::UTF8)

# 写 — 用 .NET API，显式 UTF-8 无 BOM
[System.IO.File]::WriteAllText($path, $text, [System.Text.UTF8Encoding]::new($false))
```

### 字符串替换

```powershell
# 纯字符串替换，不用正则
$text = $text.Replace('old', 'new')
```

### 批量文件操作模板

```powershell
$files = Get-ChildItem -Path "..." -Recurse -Filter "*.html"
foreach ($f in $files) {
    $text = [System.IO.File]::ReadAllText($f.FullName, [System.Text.Encoding]::UTF8)
    $orig = $text
    # 所有替换用 .Replace()，不要用 -replace
    $text = $text.Replace('A', 'B').Replace('C', 'D')
    if ($text -ne $orig) {
        [System.IO.File]::WriteAllText($f.FullName, $text, [System.Text.UTF8Encoding]::new($false))
    }
}
```

## 问题3：emoji surrogate pair 实体显示为 `��`

HTML 文件里写了 `&#55357;&#56551;`（UTF-16 surrogate pair 的十进制实体）来表示 🔧。
这种方式在通过 HTTP 服务器（Cloudflare）提供时通常正常，但本地 `file://` 协议下浏览器可能无法正确解析。

**解决**：直接用 emoji 字符本身（🔧），不写 HTML 实体编码。

## 最后的兜底

所有文件都在 git 仓库里。如果再次损坏，直接恢复：

```powershell
cd D:\claude\web_ads\terraria-guide
git checkout -- site/
```
