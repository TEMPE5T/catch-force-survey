# Catch Force Survey

A walk-up web app for an **unattended** survey on how strong a magnetic catch should be. A tablet or laptop sits on a table next to letter-labelled boxes; passers-by read the screen, handle the boxes and answer. No one needs to run it.

**Data stays on the device.** There is no server. Answers are kept in the browser's local storage until staff export them as CSV or as a JSON backup. Nothing is sent anywhere, and no names are asked for.

## The table

- **One identical box per catch**, each with the same contents, labelled A, B, C … The catches differ only in force (for example, printed spacers set different gaps). Participants never swap catches. **Assign the letters to the boxes at random**, not in force order, and set the boxes out in letter order.
- **Three comparison closures** at the end of the table (default: gift box, eyeglass case, cabinet catch).
- The device, locked to this page: Guided Access on an iPad, screen pinning on Android, or kiosk mode in a desktop browser. **Staff → Full screen** helps on a laptop.
- **Staff → Print table labels and sign** prints a table sign, one big letter per box and a label per comparison closure.

## What a participant does

About 3 minutes:

0. Ticks one box (18 or older, first time, agrees) and taps **Start**.
1. **Picks** the weakest box they would still accept, the one they would choose, and the strongest they would still accept (or "none acceptable").
2. For each comparison closure, picks the **box that feels most like it**, or "None is close".
3. Optional comment, then **Finish**. The thank-you screen resets for the next person after 12 s.

**Cut on 17 Nov, because they added little to the voice of the customer:**

- A sorting step. It only tested whether people can tell the boxes apart, and it was the slowest step. Out-of-order picks are now caught from the measured forces instead.
- A self-run shake test. It was uncontrolled and self-reported, so staff now run the tip test on every box.
- A 6 × 5 matching grid. It became three questions with the same information.

**Leaving early.** "Stop" deletes that person's answers. If the screen goes untouched (120 s by default), a "Still there?" prompt appears; after 30 s more the survey resets and the answers are deleted. In both cases only a count is kept, shown on the Results screen.

## Staff

The small **Staff** button (bottom right of the welcome screen) opens setup and results. Set a **PIN** in Setup before leaving the table. It keeps visitors out but is not real security: anyone with the device and the browser's developer tools could still read the data.

In **Setup**:

- enter each box's force, measured on the pull tester. You can also fill these in later; participants never see them.
- edit the comparison closures, the use participants imagine, the PIN and the idle time.

**Results** turns each person's picks into newtons:

- the median weakest-accepted, chosen and strongest-accepted forces, with a per-person range chart;
- **flagged responses**: picks out of order in measured force, excluded from the medians but kept in the exports;
- whether the window fits **inside the ladder**: how many accept even the weakest or the strongest box. If many do, that edge lies beyond the ladder.
- the median force of the box picked as most like each comparison closure, with a check that they come out in order;
- the number who stopped or walked away.

Exports:

- `catch-survey-people-*.csv`: one row per participant;
- `catch-survey-boxes-*.csv`: one row per participant and box;
- a JSON backup, restorable on another device.

**Back up at the end of each day.** Clearing the browser's site data, or using a private window, loses the responses.

## Running it

It is a single static page (`index.html`, plus `sw.js` so it keeps working offline after the first visit). Open the GitHub Pages link once while online, or serve the folder locally:

```bash
python -m http.server 8765
```
