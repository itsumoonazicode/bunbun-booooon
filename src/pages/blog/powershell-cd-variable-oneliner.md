---
layout: "../../layouts/BlogPost.astro"
title: "【PowerShell】変数に入れた文字列でフォルダを作成・移動するワンライナー"
description: "Lorem ipsum dolor sit amet"
pubDate: "Aug 28 2022"
heroImage: "/placeholder-hero.jpg"
---

# 何を説明する記事か
mkdirで作成したフォルダにcdで移動するワンライナーを書く際、cdに与える文字列が変数の場合でも動作させる方法

# コード

```powershell
$dirName = "goodLuck"; md $dirName | cd
```

# この記事を書くに至るまでの過程

mkdirしたフォルダに飛ぶ方法として、`cd $$`が存在しているのを知っていた。
```powershell
md dirName
cd $$
```

ところが、mdの引数に変数を指定すると、cdした際に変数名を文字列として移動しようとしてしまう。
```powershell
$dirName = "goodLuck"
md $dirName
cd $$

Set-Location: Cannot find path 'C:\Users\user\source\repos\$dirName' because it does not exist.
```

mkdirをパイプラインでつないでcdすることで、フォルダを移動することが可能。  
ということで、前段のコードに至った。


# 参考
- [PowerShell 7 からPipeline Chain Operators(&& と ||)が使える様になります](https://dev.classmethod.jp/articles/powershell-7-pipeline-chain-operator/)
- [PowerShellでmkdirしたディレクトリにcdする方法](https://blog.shibata.tech/entry/2017/09/27/215312)