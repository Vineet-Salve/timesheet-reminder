# Timesheet reminder: privacy

Timesheet reminder works entirely on your computer. Nothing about you or your timesheet is sent anywhere.

## The short version

- **Stays on this device.** Settings are kept in the browser's local extension storage (`chrome.storage.local`). They aren't synced to your browser account or shared with other devices.
- **No servers, no tracking.** The extension makes no network requests. There's no account, no analytics and no usage tracking. Its font, icons and images are all bundled inside it.
- **Can't see your timesheet.** It has no host permissions, so it can't read the content of any web page, including your hours, projects or anything you type. "Open timesheet" just opens `https://agrid.savetime.com/app/timesheet-page?tab=Time+Entry` in a normal tab.
- **Easy to remove.** Settings → Privacy → Delete my data clears everything. Removing the extension also deletes everything it stored.

## What's stored

| Item | Contents |
| --- | --- |
| Settings | Reminder day, time, repeat interval, the reminders on/off switch, the detection on/off switch, and the fixed timesheet address |
| This week's status | ISO week number (for example `2026-W41`), whether you marked it completed and when, and when the last reminder was shown |
| Visit time (only if detection is on) | When you first opened the timesheet page this week. The page address itself isn't saved |

Only the current week is kept. Each new week replaces the previous one, so no history builds up.

You can see the exact stored data at any time under Settings → Privacy → "See exactly what's stored right now".

## Permissions

| Permission | Why | |
| --- | --- | --- |
| Alarms | Schedules the weekly reminder and its repeats | Required |
| Notifications | Shows the reminder on screen | Required |
| Storage | Saves settings and this week's status on this device | Required |
| Tabs | Reads tab addresses to notice when you open the timesheet page. The address is compared with the timesheet address on your computer and never stored or sent. Only requested when you turn on detection, and given back when you turn it off or delete your data | Optional |

## For IT and security reviewers

- Manifest V3; no `host_permissions`, no content scripts, no remote code.
- No `fetch`, `XMLHttpRequest`, `WebSocket` or `sendBeacon` calls anywhere in the code.
- Uses `chrome.storage.local` only, never `chrome.storage.sync`.
- All source is plain, unminified JavaScript, so it can be reviewed directly.
