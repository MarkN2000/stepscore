# StepScore

固定間隔・1行1ステップの発音データ形式。

```text
format=stepscore,version=1,step_ms=125,title=サンプル
C5,E5,G5

D5
```

- [仕様 v1](SPEC.md)
- [例](examples/basic.txt)
- [検証データ](test-cases.json)：`input` の解析結果を `expected` と比較する。`steps` はステップ数、`notes` は順不同の `[ステップ番号（0始まり）, MIDI番号]`。`error: true` はエラー。
- 対応アプリ：[musicbox](https://musicbox.markn2000.com)
- ライセンス：[MIT](LICENSE)
