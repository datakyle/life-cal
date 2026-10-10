<p align="center"><img src="logo.svg" alt="Life in Weeks logo" width="132" height="132"></p>

# Life in Weeks

**Your whole life on one screen. One square per week. Color in the chapters.**

### ▶ [Open the app](https://datakyle.github.io/life-cal/)

<!-- Add a screenshot at docs/screenshot.png, then uncomment:
<img src="docs/screenshot.png" alt="A grid of weekly squares with colored bands for different life chapters" width="400">
-->

Every row is a year. Every square is a week. Colored bubbles show where you lived, what you worked on, who you were with. The current week glows red.

## Why this exists

I'd been using lifecalendar.io and loved it. Then it announced it was shutting down, and I wasn't about to lose my grid.

So I rebuilt it, made it open source, and made sure it reads the same backup file. If you were a lifecalendar.io person too, your data comes right over.

Here's the part I didn't expect: once you see the weeks laid out, you start counting the ones you spend with people. That's the real feature.

## Make yours in two minutes

1. Open the app and enter your birthday.
2. Add a chapter: a city, a job, a school, a friendship. Give it a color.
3. Drop milestones as dots (first marathon, adopted the dog, the trip you still talk about).
4. Tap any week to see the dates, your age, and what was happening.

## Why you'll come back to it

- **It fills in.** Every week a new square goes from future to lived. Watch it happen.
- **Lock screen wallpaper.** Export a PNG sized for your phone with the clock area kept clear. Make a fresh one every few months.
- **Share a calendar.** Send someone a read-only link to one chapter or all of them. Great for "here's everywhere I've lived" or comparing grids with a friend. Nothing gets uploaded; the data lives inside the link.
- **Multiple calendars.** Places, work, school, relationships, side quests. Each gets its own tab.
- **Print it.** Clean poster-style output for the wall.
- **No account, works offline, add it to your Home Screen.** Zero dependencies, no build step, dark mode included.

## Bring over your lifecalendar.io data

Click **Import**, pick your `life-calendars-backup.json`, and choose **Replace everything** or **Add alongside mine**. **Export** gives you a fresh backup in the same format anytime.

## Set it as your wallpaper (iPhone)

1. Tap **Wallpaper**.
2. Pick your phone model, **Lock screen** or **Home screen**, and a style.
3. Tap **Save**, then **Save Image** (or press and hold the preview).
4. In Photos, tap share → **Use as Wallpaper**.

<details>
<summary><b>How your data is saved</b></summary>

Everything saves automatically in your browser, on your device. Nothing is uploaded and there's no account. The badge next to the title tells you where things stand:

- **Green dot / Saved**: your latest change is stored in this browser.
- **Back up** (amber): 30+ days of changes aren't in a backup file yet.
- **Reconnect file** (amber): your linked backup file needs permission again (browsers ask after a restart).
- **Not saving** (red): the browser is blocking storage (often private browsing). Download a backup before closing the tab.

Tap the badge (or **••• → Saving & backups** on a phone) for:

- **Restore points**: up to 15 earlier versions, taken as you work and right before imports, restores and deletes. One tap rolls back.
- **Download a backup**: a JSON file you can keep, move to another device, or re-import.
- **Keep a backup file updated** (Chrome and Edge on desktop): pick a file once, for example in iCloud Drive, Dropbox or OneDrive, and every change is written to it.
- **Protected storage**: the app asks the browser not to clear its data, and shows whether that was granted.

**iPhone tip:** Safari can erase a site's data after about a week without a visit. Add the app to your Home Screen (Share → Add to Home Screen) and it keeps your data and works offline. Still download a backup now and then.

Data stays on the device where you entered it. To switch devices, export and import.

Share links carry the data inside the link. Anyone with the link can see your birthdate and the events you chose to share.

</details>

<details>
<summary><b>Under the hood</b></summary>

### Run it

Open `index.html` in a browser. That's it.

### Host your own copy on GitHub Pages

1. Fork this repo (or create a new one and upload every file here to the root).
2. Go to **Settings → Pages**, set **Source** to "Deploy from a branch", choose `main` and `/ (root)`, and save.
3. In a minute it's live at `https://<your-username>.github.io/<repo-name>/`.

### Data format

```json
{
  "format": "lifecalendar.io",
  "version": 1,
  "preferences": { "birthdate": "1995-06-12", "timezone": "America/Chicago", "displayPrecision": "week" },
  "calendars": [
    {
      "calendar": { "id": "...", "name": "Where I have lived", "color": { "kind": "preset", "name": "slate" },
                    "length": 90, "startDate": "1995-06-12", "displayEventLabels": true, "displayCalendarName": true },
      "events": [
        { "id": "...", "name": "Ohio", "startDate": "1995-06-12", "endDate": "2013-08-15",
          "color": { "kind": "preset", "name": "orange" } },
        { "id": "...", "name": "Moved to Denver", "type": "milestone", "startDate": "2019-06-01",
          "color": { "kind": "preset", "name": "rose" } }
      ]
    }
  ]
}
```

- Colors are Tailwind preset names (`orange`, `sky`, `teal`, ...) or `{ "kind": "custom", "hex": "#aabbcc" }`.
- Leave out `endDate` for an ongoing event; it fills through the current week.
- `"type": "milestone"` marks a single-date event, drawn as a dot. lifecalendar.io ignores this field, so there a milestone would show as an ongoing event.
- Unknown fields from older backups are kept as-is.

See [`example-backup.json`](example-backup.json) for a full sample.

### How weeks are counted

Each row runs from one birthday to the next. Squares 1 to 51 are 7 days each; square 52 absorbs the 1 or 2 leftover days, so every year is exactly 52 squares and your birthday always starts a new row.

</details>

---

Built by [Kyle](https://github.com/datakyle). The weeks go faster than you think. Spend a few on people.

Also made: [Name 3 in 5](https://github.com/datakyle/5-in-3), a pass-the-phone party game where five seconds is never enough.

[MIT](LICENSE)
