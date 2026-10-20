# Groundwork

Habit tracker + task focus timer, published as a private Claude artifact.

**Live:** https://claude.ai/code/artifact/44836f7b-0c38-41be-9d02-43ed79cb8c22

## Files

| file | role |
|---|---|
| `groundwork.html` | **the source.** Artifact source form — no `<!doctype>`/`<html>`/`<head>`/`<body>`; the publish step adds those. Edit this. |
| `index.html` | generated preview wrapper. Disposable — regenerate with the command below. |

## Updating

Republish `groundwork.html` to the same URL (pass the URL so it updates in place
rather than creating a second artifact). Re-read the live version first — the app
publishes new versions by itself whenever data is saved.

## Careful: `data/tracker.json`

The artifact publishes two files. `data/tracker.json` is **live user data**, written
by the page itself on every check-in — not source, and not in this folder on purpose.
A normal republish of the page carries it over untouched. Never publish a local copy
of it; that would overwrite real history.

## Backups

Settings → **Your data**:

- **Download backup** saves `groundwork-backup-YYYY-MM-DD.json` — every habit, check-in,
  task, layout and setting.
- **Import backup** reads one of those files back in (on this or any other device). It
  asks before replacing anything, and keeps the replaced data in this browser's
  localStorage under `day-rings-v1:before-import`, just in case.

## Layout

Layouts are named and shared by every device (up to 8, synced with the data). Each device
picks which one it shows from the dropdown on Today (kept in that browser), so a phone and
a desktop can differ. **Edit layouts** opens the arranger: tabs switch which layout you're
editing, **+ New layout** copies the one on screen, and each layout has its own name,
mode, board and circle size. **Use on this device** and **Delete layout** apply on Save.

On screens 900px and wider, Today shrinks the circles as needed so the whole page fits
the window without scrolling; the layout's circle size is the most they will grow to.
Phones scroll as usual. *Auto* is the default (rows fill left to right,
as many as fit). *Custom grid* lets you pick columns × rows, then drag habits from the
tray onto spots — or tap a habit, then tap a spot. Empty spots stay empty on Today.
Habits left in the tray show under the board, and new habits drop into the first free
spot. Grouping by category takes precedence over the custom board while it is on.

## Workout mode

Off by default. Settings → **Workout mode** adds a **Workout** tab after Habits and Tasks
and opens a setup guide the first time: how a tap logs sets, lb or kg, which exercises
(picked from a list grouped by muscle, with Select all per group or for everything),
your starting numbers, and an optional weekly plan of muscle groups. Starting numbers go
in a typed table: Tab moves across, Enter moves down, and typing a name in the last row
adds a new exercise (it starts with the previous row's group and type), so a long list
goes in without clicking. Switching it off hides the tab and keeps the data.

It lives in its own slice of the data, `workout`, and never touches habits or tasks.

- **Logging.** Each exercise is a circle. A tap logs every set at once, or one set per
  tap (4 sets → each tap fills a quarter); set the default in Workout settings and
  override it per exercise. In every-set mode a second tap clears the circle; in one-set
  mode taps stop at full, so a stray tap never wipes logged sets.
- **Rest timer.** In one-set mode, logging a set that isn't the last starts a rest
  countdown (Off, 1:00, 1:30, 2:00 or 3:00 in Workout settings), with +30s and Skip.
- **Adjusting.** Press and hold a circle (or right-click it, or use its ⋯ button) for
  ▲ ▼ steppers on sets done today, sets, reps and weight (or time). Numbers can be
  typed too. They carry forward to the next session until changed. **Sets weren't all
  the same?** gives each logged set its own reps and weight. Exercise settings there
  also pick the circle's icon.
- **Progression.** Per exercise: go up by an amount every N weeks (weight, reps, sets or
  time, chosen in the starting-point table or the long-press sheet). It is due once the
  weeks have passed *and* the last two sessions had every set done; then the circle
  shows ↑ and the sheet offers **Go up** or **Not yet** (asks again in a week). If two of
  the last three sessions stopped short, the sheet offers **Step back** or **Hold here**.
  Raising the number by hand also restarts the clock.
- **Recommendations.** With a weekly plan, each planned muscle group highlights its
  most overdue exercises (1–3 per group, in Workout settings). "Overdue" is measured
  against each exercise's own usual gap, learned from your logs, and an exercise that
  keeps getting passed over drops in priority. With no plan, your week is learned from
  the last eight weeks of logs; with a plan, Today points out weekdays where your logs
  regularly differ and offers to update it. **Day templates** (e.g. "Leg day A") put
  specific exercises on a day. Done circles take the done color, or each muscle
  group's color if you turn that on.
- **Records.** Beating your best weight (or reps or time) shows ★ New best on the circle
  and a star in History and Progress.
- **Phones** (640px wide and under) get their own Today: a plain list of muscle-group
  buttons (with a count once something in the group is logged) under an **In progress**
  button that gathers every half-done exercise from any group. Tapping a group opens
  one-line rows: icon, name, numbers and
  a check button that shows 2/3 while an exercise is part done. Wider screens keep the
  circles, which no longer shrink to fit the window; the text grows with each circle and
  every line stays inside the round edge. The circle and row size setting works
  everywhere (on a phone it sets how many circles fit across).
- **Deal me a workout.** A button on Today deals a short deck: the day's template first,
  then the highlighted picks, then whatever is most overdue (today's groups before
  others, at most half the deck from one group). On the deck screen you can swap or drop
  any pick, change how many, or **Deal again** for different picks within today's groups.
  **Start** plays it one big circle at a time: each tap is one set, the rest timer runs
  between sets, a finished exercise leaves the deck and the next one comes up. **Skip for
  now** sends it to the back, the arrows (or a swipe) move between the unfinished ones, and
  **End** shows a summary with a one-tap effort rating. The deck is kept for the day, so it
  can be resumed.
- **Layouts.** Exercises show as circles or a compact list (Auto: circles on a computer,
  a list on a phone). On a phone, Today can show muscle-group cards, only what's due today,
  or one group at a time with left/right swipes in a fixed-height box (switch with the
  Groups · Recommended · Swipe tabs). Beside them, **All · Recommended** filters any view down to
  what's highlighted today.
  Both are asked in the setup guide and live in Workout settings, as does the number of
  highlights per muscle group (1–10).
- **On a phone, Today starts with two choices:** **Deal me a workout** (or Resume your
  deal) and **Pick my own**. Pick my own opens the Groups · Recommended · Swipe views in a focus
  mode (no header, plan text, notes or buttons) until **Done workout**, which reports the
  sets logged in that workout and returns to the two choices. On a computer, **Start
  workout** beside Deal me a workout opens the same focus mode. It survives a reload for
  the rest of the day. Logging an earlier day skips the choice and shows the exercises.
- **How did that feel.** After a set is logged, a small Easy · OK · Hard bar appears at
  the bottom and goes away by itself if ignored. Each set keeps its rating and the
  exercise's effort for the day is their average. The setup guide and Workout settings
  choose every set, the last set only, or off. Two full sessions in a row that felt easy
  bring a step up forward (once a week has passed at the current numbers).
- **Add from inside a group.** On a phone, the end of a group's list (or a dashed circle)
  adds an exercise: the picker opens on just that group, with your own exercise's group
  already set to it.
- **Workout settings** are a section of the main Settings (the gear), opened already
  expanded when you're on the Workout tab.
- **Rearrange** (on Today) orders exercises within a group: drag circles, or rows by their
  handle on a phone, or use the arrows. Arrows beside a group's name (or on its card) move
  the whole group. Workout settings decide whether today's planned groups jump to the top.
- **Progress** tab: workout days, sets and volume vs the same days last week, week streak,
  sets per week by muscle group (12 weeks, hover for the split, or show it as a table),
  consistency (workouts a week, share of planned days you trained, which weekdays you
  train), muscle balance, a 16-week activity grid, and a card per exercise. A card opens
  its detail page: best set, estimated 1-rep max (Epley), volume, total reps or time over
  4 weeks to all time, with records and every session. Charts use their own validated
  color set (one color per muscle group), separate from the circle colors.
  **History** lists each day's sessions.
- **Earlier days.** The ‹ › beside the date on Today step back to an earlier day and log it
  exactly like today: taps, set dots and the long-press sheet all apply to that day, and
  the sheet's numbers edit only that day's entry (your working numbers stay put).
  Highlights, the rest timer and step-up prompts are for today only. History's **Edit**
  opens that day the same way; **Type it in a table** is still there for bulk entry. Bodyweight work counts reps alongside volume.
- **Days off.** **Rest or away…** on Today (any day, including earlier ones, and ranges up
  to 60 days) marks a rest, sick, travel or away day with an optional note. Nothing is
  highlighted on a day off; marked days don't count against your plan; sick, travel and
  away days don't make exercises look more overdue; and a week with four or more days
  marked off is skipped by the week streak instead of breaking it.
- **Effort and notes.** The long-press sheet rates how hard an exercise was (Easy to All
  out), and Today has a note box: **Save** adds the note as a line under that day, notes
  saved the same day build up, and × deletes one. Both show in History, the exercise page and
  the monthly review, and go into the CSV.
- **Self-assessment.** Progress opens with **Worth a look**: lifts with no new best in 3+
  weeks (4+ sessions, no step up) and lifts that keep stopping short. **Weekly sets vs
  target** compares each muscle group's average sets a week (last 4 weeks) with your
  target range (Workout settings, default 10–20). The **monthly review** compares a month
  with the one before (day for day while it's current): workout days, sets, volume,
  records, average effort, most improved and slipped lifts, most/least trained groups,
  days off and notes. Each exercise page lists its **progression history**: every step
  up, step back and edit to its numbers.
- **Sample data.** Workout settings → **Try with sample data** loads twelve made-up weeks
  to explore Progress and History. It's never saved: saving always writes your real data.
- **Export:** Download CSV (one row per exercise per day) or JSON from Progress, History
  or Workout settings. The regular backup includes workouts as well.

## Sync across devices (Firebase + GitHub or Google sign-in)

The artifact already syncs through your claude.ai account. The Firebase option is for
a copy you host yourself (e.g. GitHub Pages) — inside the Claude artifact the sandbox
will most likely block the Firebase scripts and the sign-in popups.

It's wired to the shared Firebase project **`github-projects-5d4e4`** (config in
`FIREBASE_CONFIG` near the top of the script; set it to `null` to turn sync off).
Live copy: https://jkw2lo.github.io/groundwork_habits_tasks/

How that project was set up (or how to point this at a different one):

1. **Create a project** at https://console.firebase.google.com.
2. **Authentication → Get started → Sign-in method → GitHub → Enable.** Copy the
   callback URL it shows (`https://<project>.firebaseapp.com/__/auth/handler`).
3. **GitHub → Settings → Developer settings → OAuth Apps → New OAuth App.** Homepage URL:
   where you'll host it. Authorization callback URL: the one from step 2. Paste the
   app's Client ID and a new Client secret back into Firebase's GitHub provider → Save.
   **Google:** Sign-in method → Add new provider → Google → Enable, pick a support
   email → Save. Nothing else to create.
4. **Firestore Database → Create database** (production mode), then set these rules
   so each account can only touch its own document:

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /groundwork/{uid} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
   ```

5. **Project settings → Your apps → Web (`</>`)** → register an app → copy the
   `firebaseConfig` object into `var FIREBASE_CONFIG = …` near the top of the script.
   (The web config is not a secret; the rules above are what protect the data.)
6. **Authentication → Settings → Authorized domains** → add your host
   (e.g. `jkw2lo.github.io`). `localhost` is there already.
7. **Host it**, e.g. GitHub Pages: repo Settings → Pages → deploy from `main` / root
   (it serves the generated `index.html`).

Then Settings → **Sign in with GitHub** or **Sign in with Google**. Each account keeps
one document, `groundwork/{uid}`, holding the whole state; the most recently saved copy
wins, and changes from another device arrive live. Whatever a sync replaces is kept in
that browser under `day-rings-v1:before-sync`.

GitHub and Google are separate Firebase accounts (separate habits) unless linked. Once
signed in, **Also use Google / GitHub** links the other one to the same data. If a
sign-in is refused because the email already uses the other provider, sign in with that
one and the refused provider is linked automatically.

## Local preview

```
cd "/Users/jenniferlo/Projects/Groundwork" && python3 -m http.server 5191
```

Regenerate the wrapper after editing the source:

```
cd "/Users/jenniferlo/Projects/Groundwork" && { printf '<!doctype html>\n<html lang="en">\n<head>\n<meta charset="utf-8">\n<meta name="viewport" content="width=device-width,initial-scale=1">\n</head>\n<body>\n'; cat groundwork.html; printf '\n</body>\n</html>\n'; } > index.html
```
