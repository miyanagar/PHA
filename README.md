# PHA Availability Calendar  
# 健康診断 空き状況カレンダー

## English

This repository contains a read-only availability calendar used for the J Medical health examination form.

The calendar is hosted with GitHub Pages and embedded into Jotform.

### Files

- `index.html` — Displays the availability calendar.
- `availability.json` — Stores the availability status for each date.

### Availability Status

| Status | Meaning | Display |
|---|---|---|
| `0` | Available | White |
| `1` | Limited availability / Almost full | Light gray |
| `2` | Unavailable / Full | Dark gray |

All Sundays are displayed as unavailable because the office is closed on Sundays.

### Calendar Behavior

- Displays two months side by side when the available width is 741 px or greater.
- Displays one month when the available width is 740 px or less.
- Users can move between months using the left and right arrows.
- The calendar starts from the current month.
- The calendar can display up to the next 12 months.
- Past dates are shown with reduced opacity.
- Today is outlined in blue.
- The calendar is display-only and is not used to select or submit dates.

### Updating Availability

Availability is managed manually in SQL Server.

SQL table:

```text
tblPHA_Calendar
```

Columns:

```text
intOffice
dtmDate
intStatus
```

Status values:

```text
0 = Available
1 = Limited availability
2 = Unavailable
```

Power Automate runs once every morning:

```text
Recurrence
→ SQL query
→ Select
→ Compose
→ Update availability.json in GitHub
```

The calendar loads `availability.json` whenever the page is opened.

### JSON Format

Example:

```json
[
  {
    "date": "2026-07-23",
    "status": 0
  },
  {
    "date": "2026-07-25",
    "status": 1
  },
  {
    "date": "2026-07-30",
    "status": 2
  }
]
```

Dates must use this format:

```text
YYYY-MM-DD
```

### GitHub Pages

The repository is published through GitHub Pages.

Example URL:

```text
https://miyanagar.github.io/PHA/
```

The GitHub Pages URL is embedded into Jotform using the IFrame Embed widget.

### Important Notes

- Do not place confidential patient information in this repository.
- Only calendar dates and availability status should be stored in `availability.json`.
- This calendar does not connect directly to SQL Server.
- SQL Server remains private.
- Power Automate updates the public JSON file.
- GitHub Pages may take a few minutes to publish changes after the file is updated.

---

## 日本語

このリポジトリには、J Medical の健康診断申込フォームで使用する、閲覧専用の空き状況カレンダーが保存されています。

カレンダーは GitHub Pages で公開し、Jotform に埋め込んで表示します。

### ファイル

- `index.html` — 空き状況カレンダーを表示します。
- `availability.json` — 各日付の空き状況を保存します。

### 空き状況の設定

| ステータス | 意味 | 表示 |
|---|---|---|
| `0` | 予約可 | 白 |
| `1` | 残り僅か | 薄いグレー |
| `2` | 予約不可・満員 | 濃いグレー |

日曜日は休診日のため、SQL の設定にかかわらず予約不可として表示されます。

### カレンダーの動作

- 表示幅が 741 px 以上の場合、2か月分を横並びで表示します。
- 表示幅が 740 px 以下の場合、1か月分のみ表示します。
- 左右の矢印で表示月を移動できます。
- 当月から表示を開始します。
- 当月から12か月先まで表示できます。
- 過去の日付は薄く表示されます。
- 当日は青い枠で表示されます。
- このカレンダーは閲覧専用であり、日付の選択や送信には使用しません。

### 空き状況の更新方法

空き状況は SQL Server で手動管理します。

SQL テーブル:

```text
tblPHA_Calendar
```

カラム:

```text
intOffice
dtmDate
intStatus
```

ステータス:

```text
0 = 予約可
1 = 残り僅か
2 = 予約不可
```

Power Automate は毎朝1回実行します。

```text
Recurrence
→ SQL query
→ Select
→ Compose
→ GitHub の availability.json を更新
```

カレンダーは、ページを開くたびに `availability.json` を読み込みます。

### JSON形式

例:

```json
[
  {
    "date": "2026-07-23",
    "status": 0
  },
  {
    "date": "2026-07-25",
    "status": 1
  },
  {
    "date": "2026-07-30",
    "status": 2
  }
]
```

日付は次の形式で入力します。

```text
YYYY-MM-DD
```

### GitHub Pages

このリポジトリは GitHub Pages で公開します。

URL例:

```text
https://miyanagar.github.io/PHA/
```

この GitHub Pages のURLを、Jotform の IFrame Embed ウィジェットに設定します。

### 注意事項

- このリポジトリには患者情報を保存しないでください。
- `availability.json` には、日付と空き状況のみを保存してください。
- このカレンダーから SQL Server へ直接接続することはありません。
- SQL Server は外部公開されません。
- Power Automate が公開用の JSON ファイルを更新します。
- GitHub のファイル更新後、GitHub Pages に反映されるまで数分かかる場合があります。
