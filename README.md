# StepScore

[English](README.md) | [日本語](README.ja.md)

StepScore is a text format for sharing note pitches and onset times between score editors and playback tools.

It records notes, chords, and rests at fixed intervals, one step per line. Its simple structure is easy to edit by hand and process in code.

```text
format=stepscore,version=1,step_ms=125,title=Example
C5,E5,G5

D5
```

- [Specification v1](SPEC.md)
- Examples: [basic](examples/basic.txt), [metadata](examples/metadata.txt)
- [Test cases](test-cases.json): compare parsed `input` with `expected`. `steps` is the step count; `notes` is an unordered list of `[zero-based step, MIDI note number]` pairs. `error: true` means parsing must fail.
- Compatible app: [musicbox](https://musicbox.markn2000.com)
- License: [MIT](LICENSE)
