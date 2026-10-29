# Lemon Clicker Bug Report

**Name:**
**Tickets solved:** 5

Copy the template below once for each ticket you solved. 

---

## Ticket <5>: <Leaderboard dates show "undefined">

### Actual cause

**File / function:**
ResultsScreenView.ts : export type LeaderboardEntry
ResultsScreenModel.ts : updateLeaderboard

**What was wrong:**
The leaderboard never shows when a score was set. I just finished a game with 18 points and the "Top Scores" list says 1. 18 - undefined. The score itself is right, but where the date should be it just says "undefined". 

### Fix

<!-- What did you change, and why does that change fix the problem? -->

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** I saw that the timestamp was "undefined" even though the score was present on the leaderboard
2. **Traced back to:** The error would be in ResultsScreenView
3. **Traced back to:** The variables don't match up with the one used in index.ts
4. **Buggy code:** ResultsScreenView.ts : on line 106, entry.timestamp should be entry.time, because index.ts uses time to create the entries. Since the other functions use "timestamp", JavaScript tries to access it, but that property doesn't exist in the object returned by the server.

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix
I played the game again and saw the timestamps.

<!-- How did you confirm the problem is gone? -->
