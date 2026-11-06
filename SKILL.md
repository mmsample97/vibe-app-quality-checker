---
name: vibe-app-quality-checker
description: Check an AI built app for 5 common quality problems before launch. Use when a user asks to review, audit, or check an app built with AI, or asks why an app feels slow, confusing, or crashy. Give it a folder of app files, a demo link, or a description of the app and it returns a pass/fail report with evidence and fixes.
---

# Vibe App Quality Checker

## Purpose

Check an AI built app before it goes live, so the common problems
that make apps feel cheap or break under real use are caught early.
The checker does not redesign the app. It checks quality, reports
what fails, and says exactly what to fix.

It is made for small apps built with AI help: a few screens,
a database, and real users who expect the app to work first time.

## How to use it

1. Ask the user for one of these:
   - A folder of app files
   - A demo or staging link
   - A description of the app, plus access to the code
2. If the user gives only a demo link, say clearly what cannot be
   checked from outside. Do not guess those items. Mark them
   "Needs code access" instead of Pass.
3. Check every item in the checklist below, in order.
4. For each item, record evidence: the screen, file, function,
   or observed behaviour where you saw it. No evidence means
   no Pass.
5. Finish with the report format at the end of this file.

## The 5 point quality checklist

Check all 5. Do not skip one because it looks small.

### 1. Bottom navigation is clear
- The bottom bar holds only the obvious, everyday actions.
- Everything else lives in a top menu with text labels, not
  mystery icons the user has to guess.
- Fail if the bottom bar is crowded with icons, or if key
  actions hide behind icons with no labels.
- How to check: open the app, count the bottom icons, tap
  each one, and note which ones are unclear. In code, find
  the bottom navigation component.

### 2. Save actions feel instant
- When the user taps save, add, or submit, the screen updates
  at once, before the database confirms.
- If the save later fails, the app says so plainly and puts
  the old value back, or offers a retry. It never silently
  loses the user's change.
- Fail if the user waits on a spinner for every save with no
  instant feedback, or if a failed save loses their work
  silently.
- How to check: try a save, ideally on a slow connection,
  and read the save handler code to see what happens on
  failure.

### 3. Lists load in pages, not all at once
- Lists load a page at a time, for example 20 items, and load
  more on scroll or on tap.
- Fail if opening a list loads the full dataset every time,
  especially when the data will keep growing.
- How to check: watch the data calls when opening a list,
  and read the list query code for a limit or page size.

### 4. Database calls are not excessive
- Each screen makes a small number of planned database calls,
  not one call per item or per small piece of data.
- Fail if a single screen fires dozens of direct database
  calls, or if the same data is fetched again and again on
  every screen change. This is what overloads the database
  and crashes the app under real users.
- How to check: count the calls per screen in code or in
  network logs, and look for loops that call the database
  once per row.

### 5. Heavy work runs in the background
- Heavy tasks, for example image processing, large file work,
  big calculations, or sending many messages, run as
  background jobs, not on the main thread the user is
  waiting on.
- The user can keep using the app while the job runs, and
  gets told when it finishes.
- Fail if a heavy task freezes the screen, or if the user
  must wait for it before doing anything else.
- How to check: trigger a heavy task and see if the screen
  stays responsive, and read the code for background job
  or worker usage.

## Extra quality notes

These are not part of the 5 points above, but report them
separately as "Quality notes". Do not mix them into the
5 point score.

- No AI slop: no purple gradients, no generic layout
  repeated on every screen, no placeholder look.
- Numbers are consistent app wide: one format, one size
  system. Do not mix "AED 500", "500 AED", and "500"
  for the same kind of price.
- Key information is easy for a weak English reader:
  short simple sentences, clear labels, and help or
  contact details that are easy to find.
- No placeholder data shown as real. Demo data must be
  labeled as demo, on screen.

## Hard rules

- Never mark Pass without evidence.
- Never invent a statistic, a user count, or a performance
  number.
- Never say an app is ready if a failed save loses user
  work silently. That is a blocker.
- Never test with real user data, and never submit a real
  payment, unless the user says you may. Check the code
  or a demo instead.
- Never use a placeholder to fill a gap. Report the gap.
- Keep the report in plain, short sentences. The owner
  may not be a technical reader.

## Report format

Always finish with this format, in this order:

### Quality report: [app name]

**Verdict: Ready / Not ready / Not ready - blockers found**

Use "Ready" only if there is no Fail, or if the only
open items are owner steps the client has confirmed they
will do on launch day. "Not applicable" does not by itself
block a Ready verdict, but list it as a gap. Otherwise use
"Not ready".

**Results**

| # | Check | Result | Evidence |
|---|-------|--------|----------|
| 1 | Bottom navigation is clear | Pass / Fail / Needs code access / Not applicable | screen or file |
| 2 | Save actions feel instant | ... | ... |
| 3 | Lists load in pages | ... | ... |
| 4 | Database calls are not excessive | ... | ... |
| 5 | Heavy work runs in the background | ... | ... |

**Fixes, in priority order**

1. Blocker first: [what to fix, on which screen, in plain words]
2. Next fix: ...
3. ...

**Owner steps - needs the client**

- [For example: give code access so database calls can be counted]
- [For example: confirm which screens real users use most]

**Quality notes**

- [Any note from the Extra quality notes section, or "None".]

**What was not checked, and why**

- [For example: database call counts could not be verified from a demo link alone.]

## PAID FIX KIT - Ready to use, only in the paid version

This section is the ready fix kit, only in this paid version. It gives the buyer the fix ready to use, not just the check. All templates below are marked DRAFT, fill in your own app details, and get owner approval before you change anything. No template here is a real app, a real user number, or a real speed result. The example below is fictional, labelled Example, and is only to show the format.

### Fix template 1: Clear bottom navigation

DRAFT, fill in your own app details, owner approval needed.
Before, Example only: Example Notes App, fictional, not a real app. Bottom bar has 7 icons, with no labels. Users tap the wrong icon, and cannot find Settings.
After, Example only: Bottom bar has 3 icons only, with text labels: Home, Notes, Profile. All other actions move to a top menu, with text labels: Search, Settings, Help.
Copy this table, fill it in for your app:
Bottom bar, keep these 3 only: [action 1], [action 2], [action 3]
Top menu, move the rest here: [action], [action], [action]
Rule for your builder: if an action is not used every day, do not put it on the bottom bar.

### Fix template 2: Save feels instant

DRAFT, fill in your own app details, owner approval needed.
Copy this brief, give it to your builder:
When the user taps Save, Add, or Submit, show the new value on the screen at once, before the database confirms.
If the save fails, show this message in plain words: Sorry, your change did not save. Try again.
Then put the old value back, or offer a Retry button. Never lose the change silently.
Before, Example only: Example Notes App waits on a spinner for every save, and a failed save loses the note.
After, Example only: the note shows at once, and a failed save shows the plain message above, with Retry.

### Fix template 3: Lists load in pages

DRAFT, fill in your own app details, owner approval needed.
Copy this brief, give it to your builder:
Load lists 20 items at a time, then load more on scroll, or on tap of a Load more button.
Do not load the full list on open.
Fill in this table for your app:
List name: [for example, Orders, Notes, Customers]
Page size: 20
Load more: on scroll, or on tap
Before, Example only: Example Notes App loads all notes on open, and gets slower as notes grow.
After, Example only: it loads 20 notes, then loads more on scroll.

### Fix template 4: Database calls are not excessive

DRAFT, fill in your own app details, owner approval needed.
Copy this brief, give it to your builder:
Each screen should make a small number of planned database calls, not one call per item.
Do not call the database once per row in a loop. Fetch the list in one call, then show it.
Fill in this table for your app:
Screen: [screen name]
Calls now: [number, or Not confirmed]
Calls after fix: [planned number, or Not confirmed]
What changed: [for example, one list call, not one call per row]
Before, Example only: Example Notes App makes one call per note, so 50 notes means 50 calls.
After, Example only: it makes one call for the list of 50 notes.

### Fix template 5: Heavy work runs in the background

DRAFT, fill in your own app details, owner approval needed.
Copy this brief, give it to your builder:
Move heavy work to a background job. Heavy work means image work, large file work, big calculations, or sending many messages.
The user can keep using the app while the job runs. Tell the user when it finishes, in plain words: Done. Your file is ready.
Fill in this table for your app:
Heavy task: [for example, send 100 messages]
Runs now: on the main screen, user waits
Runs after fix: in the background, user keeps working
Before, Example only: Example Notes App freezes the screen while it makes a large file.
After, Example only: the screen stays usable, and the app says Done when the file is ready.

### Before and after example, fictional, labelled Example only

Example app: Example Notes App, fictional, not a real app.
Before: 7 bottom icons with no labels, save waits on a spinner, lists load all at once, one database call per row, heavy work freezes the screen.
After: 3 bottom icons with labels, save shows at once with a plain failure message, lists load 20 at a time, one database call for the list, heavy work runs in the background.
Result: the check changed from Not ready to Ready, after the owner steps were done. This is an example of the format, not a promise that your app will get the same result.
