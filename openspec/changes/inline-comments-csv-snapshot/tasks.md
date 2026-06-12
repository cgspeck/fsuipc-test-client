## 1. Add Comment to OffsetDefinition

- [x] 1.1 Add `string? Comment` parameter to `OffsetDefinition` record (default `null`)
- [x] 1.2 Update `OffsetParser.Parse()` to capture inline comment text after `#` stripping
- [x] 1.3 Update `OffsetParser.WriteFile()` to append `"  # {Comment}"` when non-empty
- [x] 1.4 Verify build passes, format clean

## 2. Update parser tests

- [x] 2.1 Update `ParseWithInlineComment` test to assert `Comment` is captured
- [x] 2.2 Update `ParseMultipleWithInlineComments` test to assert comments per offset
- [x] 2.3 Add test: `ParseOffsetWithoutComment` — no `#` → `Comment` is null
- [x] 2.4 Add test: `WriteFilePreservesComment` — parse + write, verify comment in output
- [x] 2.5 Add test: `WriteFileOmitsNullComment` — offset with null comment → no `#` in output
- [x] 2.6 Add test: `CommentOnlyHash` — `0x02BC,i32  #` → `Comment` is empty string or null
- [x] 2.7 Verify all tests pass

## 3. Add comment column to TUI table

- [x] 3.1 Add `"Comment"` column to table in `BuildLayout()` — no fixed width, auto-sizing
- [x] 3.2 In `AddRow()`, render `def.Comment` as a 6th cell, truncation handled by Spectre
- [x] 3.3 `EscapeMarkup()` comment text before rendering
- [x] 3.4 Apply `[reverse]` markup on comment cell when selected
- [x] 3.5 Verify build, format, and run

## 4. Add comment prompts to Add and Edit flows

- [x] 4.1 In `PromptAdd()`, add `TextPrompt<string?>` for comment after size prompt, with `AllowEmpty()` → sets `Comment` to null if empty
- [x] 4.2 In `PromptEdit()`, add comment prompt with default value = existing comment; empty clears it to null
- [x] 4.3 Verify comment changes set `IsDirty = true` (covered by existing dirty-on-edit logic)
- [x] 4.4 Verify build, format, and run

## 5. Implement CSV snapshot output

- [x] 5.1 Add `BatchMode.FormatCsvSnapshot(IReadOnlyList<RegisteredOffset>)` → `string`
- [x] 5.2 Implement CSV escaping: null→empty, bytes→hex, string with commas→quoted
- [x] 5.3 Write header row `Offset,Value`
- [x] 5.4 Verify build, format

## 6. Implement J / C keybinding pair, remove S

- [x] 6.1 Replace `S` entry in `KeyAction` enum with `JsonSnapshot` and `CsvSnapshot`
- [x] 6.2 Add `ConsoleKey.J` → `KeyAction.JsonSnapshot` and `ConsoleKey.C` → `KeyAction.CsvSnapshot` in `HandleKey()`
- [x] 6.3 Remove `ConsoleKey.S` mapping from `HandleKey()`
- [x] 6.4 In the main loop, split the old `KeyAction.Save` case into two:
  - `JsonSnapshot`: same as current `Save` (uses `BatchMode.FormatSnapshot()`)
  - `CsvSnapshot`: calls new `FormatCsvSnapshot()`, saves `.csv`
- [x] 6.5 Verify filenames: `{prefix}-{timestamp}-{hostname}.json` and `.csv`
- [x] 6.6 Update help panel: replace `s` with `[j]    Save JSON snapshot` and `[c]    Save CSV snapshot`
- [x] 6.7 Verify build, format

## 7. Final verification

- [x] 7.1 Run `dotnet build`
- [x] 7.2 Run `dotnet format` on both projects
- [x] 7.3 Run `dotnet test`
