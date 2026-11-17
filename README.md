# Catch Force Survey

A small web app for running an in-person survey on how strong a magnetic catch should be. The experimenter holds a phone, tablet or laptop; each participant handles a set of blind-coded closures and answers on the screen.

**Data stays on the device.** There is no server. Answers are kept in the browser's local storage until you export them as CSV or as a JSON backup. Nothing is sent anywhere, and no names are asked for.

## What a participant does

1. **Sort** the closures (letters A, B, C …) from weakest to strongest.
2. **Mark** the weakest one they would still accept, the one they would choose, and the strongest one they would still accept.
3. **Tip test** on the marked closures: the experimenter turns the box upside down, shakes it gently and records whether the lid stayed shut.
4. **Match** each closure to a familiar one (default: gift box, eyeglass case, cabinet catch), including "weaker than" and "stronger than" options.
5. Optional comment.

Each participant gets a new random hand-over order, shown to the experimenter on the first screen.

## Before you start

Open **Setup**, then:

- enter each closure's force, measured on the pull tester. You can also fill these in after the survey; participants never see them.
- edit the three familiar closures and the use the participant imagines ("a small box you carry and open by hand").

## Results

The **Results** screen turns each person's marks into newtons and shows:

- the median weakest-accepted, chosen and strongest-accepted forces, with a per-person range chart;
- how well people could sort the closures (Kendall's τ against the measured forces). Frequent swaps of two neighbours mean their forces are too close to feel.
- the tip-test outcomes;
- the median force of the closures matched to each familiar closure, with a check that they come out in order.

Exports:

- `catch-survey-people-*.csv`: one row per participant;
- `catch-survey-closures-*.csv`: one row per participant and closure;
- a JSON backup, which can be restored on another device from Setup.

**Back up regularly.** Clearing the browser's site data, or a private window, loses the responses.

## Running it

It is a single static page (`index.html`, plus `sw.js` so it works offline after the first visit). Open the GitHub Pages link, or serve the folder locally:

```bash
python -m http.server 8765
```
