# Lemon Clicker Bug Report

**Name:**
**Tickets solved:** 5

Copy the template below once for each ticket you solved. 

---

## Ticket 5: Leaderboard dates show "undefined"

### Actual cause

**File / function:**
ResultsScreenView.ts : export type LeaderboardEntry
ResultsScreenModel.ts : updateLeaderboard

**What was wrong:**
The leaderboard never shows when a score was set. I just finished a game with 18 points and the "Top Scores" list says 1. 18 - undefined. The score itself is right, but where the date should be it just says "undefined". 

### Fix

ResultsScreenView.ts : on line 106, entry.timestamp should be entry.time, because index.ts uses time to create the entries. Since the other functions use "timestamp", JavaScript tries to access it, but that property doesn't exist in the object returned by the server.

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


---

## Ticket 4: Stuck on the Game Over screen

### Actual cause

**File / function:**
GameScreenController.ts : endGame()

**What was wrong:**
When a game ends, the game-over sound keeps replaying every second and the leaderboard fills up with copies of my score. I can't get out of the results screen: Play Again shows the menu for a moment and then jumps right back to "GAME OVER!".

### Fix

GameScreenController.ts : on line 87, there is a call to this.stopTimer;. Add a set of parentheses at the end: this.stopTimer();

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** I can't get out of the results screen: Play Again shows the menu for a moment and then jumps right back to "GAME OVER!".
2. **Traced back to:** The error would be somewhere in the function that calls game over.
3. **Traced back to:** I found the endGame() function in GameScreenController.
4. **Buggy code:** GameScreenController.ts : on line 87, there is a call to this.stopTimer;. This is wrong because without the parentheses there is no call to the function. Add a set of parentheses at the end: this.stopTimer(); 

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix
I played the game again and the Game Over screen didn't keep updating, and I was able to successfully click the Play Again button.

<!-- How did you confirm the problem is gone? -->



---

## Ticket 3: Stuck on the Game Over screen

### Actual cause

**File / function:**
GameScreenView.ts : randomizeLemonPosition()

**What was wrong:**
The lemon isn't really random. After I click it, it keeps jumping between the same four spots near the corners, and sometimes it doesn't seem to move at all. Once you notice, you can just wait in a corner for it to show up.

### Fix

GameScreenView.ts : On line 85 and 86, delete Math.round()

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** After I click the lemon, it keeps jumping between the same four spots near the corners
2. **Traced back to:** The error would be somewhere in the function displays the lemon.
3. **Traced back to:** I found the randomizeLemonPosition() function in the file GameScreenView.ts
4. **Buggy code:** GameScreenView.ts : on line 85 and 86, the randomize function uses Math.round around the function Math.random(). This makes it so the random number generated would always be rounded to either 0 or 1. Because of this, on the x and y axis there will only be two options for the lemon to show up each.

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix
I played the game again and the lemon spawns in different locations.

<!-- How did you confirm the problem is gone? -->


---

## Ticket 6: My high score disappeared from the leaderboard

### Actual cause

**File / function:**
index.ts : app.post("/api/leaderboard"

**What was wrong:**
The "Top Scores" list looks like it's showing the worst scores instead of the best ones, and my score of 1 is listed as #1.

### Fix

index.ts : On line 38, switch a.score and b.score

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** The leaderboard keeps displaying the worst scores at the top.
2. **Traced back to:** The error would be somewhere where the scores get ordered.
3. **Traced back to:** I found the code for the order in index.ts
4. **Buggy code:** index.ts: on line 38, the scores are supposed to be sorted in descending order, but doing a.score - b.score makes it sorted in ascending order.

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix
I played the game again and my leaderboard is sorted in descending order.

<!-- How did you confirm the problem is gone? -->


---

## Ticket 1: Stats always say "Stats unavailable"
### Actual cause

**File / function:**
index.ts : app.post("/api/leaderboard"

**What was wrong:**
The "Top Scores" list looks like it's showing the worst scores instead of the best ones, and my score of 1 is listed as #1.

### Fix

index.ts : On line 38, switch a.score and b.score

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** The leaderboard keeps displaying the worst scores at the top.
2. **Traced back to:** I first looked at MenuScreenView.ts to see where the stats were being displayed.
3. **Traced back to:** I looked in MenuScreenModel.ts, and saw how it was being displayed.
4. **Traced back to:** I looked in MenuScreenController.ts because in the browser console log it said "Unable to load stats"
5. **Traced back to:** I went to index.ts and saw that it was api/stats and not api/stat
6. **Buggy code:** MenuScreenController.ts : on line 47, it is supposed to be fetch("/api/stats") and not fetch("/api/stat")
<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix
I played the game again and the stats are showing up at the bottom.

<!-- How did you confirm the problem is gone? -->