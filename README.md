# Life in Weeks

**[Open the app](https://datakyle.github.io/life-cal/)**

Visualize your life one week at a time. Every row is a year of your life, every square is a week, and colored "bubbles" show where you lived, worked, studied, or anything else you want to track.

An open-source, self-hostable alternative to lifecalendar.io. It reads and writes the same JSON backup format, so you can import your old export directly.

## Features

- **90-year grid** (configurable 1 to 120 years): 52 squares per row, one row per year of age, starting at your birthdate
- **Multiple calendars**: "Where I have lived", "Work", "Education", relationships, whatever you like, each in its own tab
- **Events with real dates**: give each chapter a name, start date, end date (or "still going"), and a color
- **Milestones**: mark a single moment (got married, first marathon, adopted the dog) as a dot on its week, alongside your ranges
- **Tap any week** to see the exact dates, your age, and what was happening
- **Drag to select** on desktop: click and drag across squares to create an event covering that range
- **Select weeks** on phones: tap a first and last square to do the same
- **Lived vs. future**: past weeks shade in, the current week is outlined in red
- **Saving mode**: autosaves to your browser on every change, with a status badge, restore points, backup reminders, and an optional backup file that updates itself
- **Works offline** once it's been opened (and added to your Home Screen)
- **Import / Export** lifecalendar.io-compatible JSON backups
- **Share links**: a read-only copy of one or all calendars, encoded in the URL (no server, nothing uploaded)
- **Phone wallpapers**: export a PNG sized for your iPhone (or Android), with a lock-screen layout that keeps the clock area clear, four styles, a color legend, week count, and an optional caption
- **Print**: clean, poster-style output similar to the original PDF
- **Mobile first**: bottom-sheet dialogs, a floating + button, swipeable event chips, and week-by-week / year-by-year arrows so you never have to hit a tiny square exactly
- **Add to Home Screen**: runs full screen with its own icon on iPhone and Android
- **Dark mode**, zero dependencies, no build step

## Set it as your wallpaper (iPhone)

1. Open the app and tap **Wallpaper**.
2. Pick your phone model, **Lock screen** or **Home screen**, and a style.
3. Tap **Save**, then **Save Image** (or press and hold the preview).
4. In Photos, open the image, tap the share icon, and choose **Use as Wallpaper**.

The red square is the current week, so make a fresh wallpaper every so often to watch the grid fill in.

## Run it

Just open `index.html` in a browser. That's it.

## Publish on GitHub Pages

1. Create a new repository on GitHub (for example `life-in-weeks`).
2. Upload every file in this folder (`index.html`, `sw.js`, `manifest.webmanifest`, `icon-180.png`, `icon-512.png`, `README.md`, `LICENSE`, `example-backup.json`) to the repo root.
3. Go to **Settings > Pages**, set **Source** to "Deploy from a branch", choose `main` and `/ (root)`, and save.
4. In a minute your app is live at `https://<your-username>.github.io/life-in-weeks/`.

Live demo: **https://datakyle.github.io/life-cal/**

## Bring over your lifecalendar.io data

Click **Import** and pick your `life-calendars-backup.json`. Choose **Replace everything** or **Add alongside mine**. Use **Export** anytime to download a fresh backup in the same format.

## Saving your progress

Everything you do is saved automatically in your browser, on your device. Nothing is uploaded and there's no account. The badge next to the title tells you where things stand:

- **Green dot / Saved**: your latest change is stored in this browser.
- **Back up** (amber): you've made changes over the last 30+ days that aren't in a backup file yet.
- **Reconnect file** (amber): your linked backup file needs permission again (browsers ask after a restart).
- **Not saving** (red): the browser is blocking storage (often private browsing). Download a backup before closing the tab.

Tap the badge (or **••• → Saving & backups** on a phone) for:

- **Restore points**: up to 15 earlier versions, taken as you work and right before imports, restores and deletes. One tap rolls back.
- **Download a backup**: a JSON file you can keep, move to another device, or re-import.
- **Keep a backup file updated** (Chrome and Edge on desktop): pick a file once, for example in an iCloud Drive, Dropbox or OneDrive folder, and every change is written to it automatically.
- **Protected storage**: the app asks the browser not to clear its data on its own, and shows whether that was granted.

**iPhone tip:** Safari can erase a website's saved data after about a week without a visit. Add the app to your Home Screen (Share → Add to Home Screen) and it keeps your data and works offline. Downloading a backup now and then is still a good habit.

Data stays on the device and browser where you entered it. To use another device, download a backup and import it there.

Share links carry the data inside the link itself. Anyone with the link can see your birthdate and the events you chose to share.

## Data format

```json
{
  "format": "lifecalendar.io",
  "version": 1,
  "preferences": { "birthdate": "1998-04-19", "timezone": "America/Chicago", "displayPrecision": "week" },
  "calendars": [
    {
      "calendar": { "id": "...", "name": "Where I have lived", "color": { "kind": "preset", "name": "slate" },
                    "length": 90, "startDate": "1998-04-19", "displayEventLabels": true, "displayCalendarName": true },
      "events": [
        { "id": "...", "name": "California", "startDate": "1998-04-19", "endDate": "2003-05-23",
          "color": { "kind": "preset", "name": "orange" } },
        { "id": "...", "name": "Moved to Kansas City", "type": "milestone", "startDate": "2024-10-05",
          "color": { "kind": "preset", "name": "rose" } }
      ]
    }
  ]
}
```

- Colors are Tailwind preset names (`orange`, `sky`, `teal`, ...) or `{ "kind": "custom", "hex": "#aabbcc" }`.
- Leave out `endDate` for an ongoing event; it fills through the current week.
- `"type": "milestone"` marks a single-date event, drawn as a dot. lifecalendar.io ignores this field, so on that site a milestone would show as an ongoing event.
- Unknown fields from older backups are kept as-is.

## How weeks are counted

Each row runs from one birthday to the next. Squares 1 to 51 are 7 days each; square 52 absorbs the 1 or 2 leftover days, so every year is exactly 52 squares and your birthday always starts a new row.

## License

MIT
