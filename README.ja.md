# StepScore

[English](README.md) | [日本語](README.ja.md)

音高と発音タイミングを、楽譜エディターや再生ツールの間で共有するためのテキスト形式です。

固定間隔・1行1ステップで音名・和音・休符を記録します。人が直接読み書きでき、プログラムでも扱いやすい簡潔な構成です。

```text
format=stepscore,version=1,step_ms=125,title=Example
C5,E5,G5

D5
```

- [仕様 v1](SPEC.ja.md)
- 例：[基本](examples/basic.txt)、[メタデータ](examples/metadata.txt)
- [検証データ](test-cases.json)：`input` の解析結果を `expected` と比較する。`steps` はステップ数、`notes` は順不同の `[ステップ番号（0始まり）, MIDI番号]`。`error: true` は解析エラー。
- 対応アプリ：[musicbox](https://musicbox.markn2000.com)
- ライセンス：[MIT](LICENSE)
