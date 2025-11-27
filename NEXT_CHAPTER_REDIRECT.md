# Next Chapter 跳转域名配置说明

## 功能说明

当用户在章节页面点击 "Next" 按钮或使用键盘右箭头键时，会自动跳转到配置的目标域名，而不是本站的下一章节。

## 配置方法

### 1. 编辑配置文件

打开 `config.json` 文件，找到 `site` 配置项：

```json
{
  "site": {
    "name": "NovelVibe",
    "description": "Free Werewolf Novels for American Women",
    "url": "https://www.arknovel1.xyz",
    "next_chapter_domain": "https://www.xixifreenovel.com",
    "language": "en-US",
    "author": "NovelVibe Team"
  }
}
```

### 2. 修改目标域名

只需修改 `next_chapter_domain` 的值即可：

```json
"next_chapter_domain": "https://你的目标域名.com"
```

### 3. 重新构建网站

```bash
python3 tools/build-website.py --force
```

### 4. 推送更新

```bash
git add .
git commit -m "更新 next chapter 跳转域名"
git push
```

## 工作原理

### 当前域名示例
```
https://www.arknovel1.xyz/novels/the-last-spirit-wolf/chapter-1.html
```

### 点击 Next 后跳转
```
https://www.xixifreenovel.com/novels/the-last-spirit-wolf/chapter-2.html
```

**关键点：**
- 只替换域名部分
- 保留完整的路径（/novels/小说名/章节文件）
- 支持键盘快捷键（右箭头）
- 支持点击按钮

## 禁用跳转

如果想让 Next 按钮跳转回本域名，只需：

1. 删除或清空 `next_chapter_domain` 配置：
```json
"next_chapter_domain": ""
```

2. 或者删除这一行配置

3. 重新构建网站

## 技术实现

- JavaScript 拦截 Next 按钮点击事件
- 解析原始 URL 并提取路径
- 将路径拼接到配置的目标域名
- 支持键盘导航（右箭头键）

## 注意事项

1. 目标域名必须包含 `https://` 或 `http://`
2. 目标域名不要以 `/` 结尾
3. 确保目标网站有相同的小说和章节结构
4. 每次修改配置后必须重新构建网站
