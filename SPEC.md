# StepScore v1

[English](SPEC.md) | [日本語](SPEC.ja.md)

Fixed-interval note-on events. Note duration, timbre, dynamics, and instrument range are handled by the player.

## Header

The first line contains comma-separated `key=value` fields. Input field order is arbitrary. Output starts with `format=stepscore`.

| Required key | Value |
| --- | --- |
| `format` | `stepscore` |
| `version` | `1` |
| `step_ms` | Decimal integer from 1 to 9007199254740991. Interval per step in milliseconds |

- Keys must be nonempty and unique, and must not contain `,`, `=`, CR, or LF.
- Escape values by replacing `%` with `%25`, then `,` with `%2C`. CR and LF are forbidden. Preserve other characters; quotation marks have no special meaning.
- Parse by splitting on `,`, splitting each field at the first `=`, then decoding `%25` and `%2C` once. `%252C` becomes `%2C`. Other `%` sequences are errors.
- Preserve unknown keys and values when writing. Onset times depend only on `step_ms` and the body; other metadata is not used for playback.
- When writing, use this specification's `format` and `version` values and the edited interval for `step_ms`. Changing the display language must not change `title`.

### Optional metadata

Display metadata does not change onset times or `version`. Store each language's name separately; a name identical to the base name may be omitted.

| Key | Meaning and example |
| --- | --- |
| `title` | Base title, preferably the original title; otherwise a freely chosen title. Example: `title=Air` |
| `title_<language>` | Localized title. Examples: `title_ja=G線上のアリア`, `title_en=Air on the G String` |

Additional metadata used by [musicbox](https://musicbox.markn2000.com); interpreting these fields is optional:

| Key | Meaning and example |
| --- | --- |
| `composer` | Base composer name. Example: `composer=Johann Sebastian Bach` |
| `composer_<language>` | Localized composer name. Examples: `composer_ja=バッハ`, `composer_en=Johann Sebastian Bach` |
| `arranged_for` | Arrangement target. Examples: `musicbox30`, `piano88`, `piano61`, `xylophone32` |
| `reading_ja` | Japanese title reading for sorting and search. Example: `reading_ja=じーせんじょうのありあ` |
| `steps_per_quarter` | Steps per quarter note. Examples: `4`, `8`, `12` |
| `time_signature` | Time signature. Examples: `4/4`, `3/4`, `6/8` |

See the [metadata example](examples/metadata.txt).

## Body

- Each line after the header is one step. Comma-separated note names sound together. Ignore whitespace around note names.
- A blank line triggers no new notes. It does not stop notes already sounding.
- Note names use `C C# D D# E F F# G G# A A# B` followed by an octave number. `C4` = MIDI 60. Range: `C-1` through `G9` (MIDI 0–127).
- Merge duplicate notes within a step; repeat the note-on in different steps. Write notes in ascending pitch order.
- Preserve leading, internal, and trailing rests. A final newline terminates the last line. Body `C5\n` is one step; `C5\n\n` is two (`\n` = LF).

## Input and output

- Extension: `.txt`. Output: UTF-8 without BOM, LF, a newline after every step. Input: UTF-8, optional BOM, LF/CRLF/CR.
- Missing required keys, duplicate keys, invalid values, note names or escapes, and unsupported versions are errors.
- Comments, settings in the body, and the legacy format are unsupported.
