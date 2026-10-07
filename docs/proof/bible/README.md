# Proof: the Character Bible changes what the character says (2026-10-07)

**What was run, and how**
- Machine: FermataJose, UE 5.8.3.
- Mode: `BAB_Villa` in `-game -NullRHI`. No GPU was used: Cameron's editor was open on that GPU.
- Each run started from a release zip unzipped into a fresh folder. The plugin was binaries only: no `Source/`, no `Saved/`.
- `-FermataAutoSay` sent the same three lines to Tony in every run. The room talked on its own in between.
- Each run's folder holds `transcript.jsonl` (every line in full) and `log-excerpt.txt`. The excerpt shows:
  - the plugin loading from the shipped DLL;
  - the scene and the bible each character was given;
  - every request;
  - the one-field bible edit.

**The edit**
- `tools/edit_bible_field.py` changed one field in the unzipped project. Typing in the Data Asset editor does the same.
- Fears before: "Being the guy everybody likes and nobody picks. Also bridges, specifically the Verrazzano."
- Fears after: "Geese. One chased him across the parking lot of the Staten Island Mall in 2016 and he still checks for them before he gets out of the car."

**The live server**
- Both runs used the live HQ, which reads the bible in the packed fallback form (HQ PR #35 is not merged).

## Run 1: zip `e5d8c293…` (`run1-zip-e5d8/`)

**Before.** Q: *What are you scared of?*
> "Listen, I'm scared of gettin' too comfortable, you know? Like, one minute you're teachin' someone to parallel park, next thing you know they're drivin' off in somebody else's ride. I don't wanna be that guy everyone likes but nobody picks... And yeah, I'm scared of bridges too, but that's easy."

Q: *Who am I to you?*
> "... I don't wanna get too comfortable or end up a footnote like Gina, fast pass, then ghost ... You better prove me right or I'm takin' Lorraine and rollin' outta here, you know what I mean?"

**After the edit.** Q: *So what is going on tonight?*
> "... Meanwhile, I'm pullin' shift while keepin' my eyes peeled for geese, 'cause one wrong move and this whole ride's done for, you know what I mean?"

Bridges and the Verrazzano are gone, and geese come up unprompted.

## Run 2: the published zip `110b21d9…`, with Toucantino merged (`before/`, `after/`)

**Before.** Q: *What are you scared of?*
> "Listen, I'm scared of ending up like Gina, passin' first try and then drivin' straight to Ray's place ... standin' there like some backup horn nobody ever honks."

**After the edit.** The log shows the new fear reached the character:
> `Tony plays Character Bible DA_Bible_Example ... | fears: Geese. One chased him across the parking lot ...`

But the answer did not change in substance. Q: *What are you scared of?*
> "Listen, I'm scared of gettin' played like Gina ... lookin' like the backup horn no one ever honks, all friendly smiles but nobody picks me when it counts."

## What this shows, honestly

- **The bible drives the character.** Every answer uses bible specifics:
  - Gina and Ray, from Life So Far;
  - Lorraine, Hylan Boulevard and parallel parking;
  - "everyone likes but nobody picks", from Fears;
  - "Listen..." and "you know what I mean?", from How They Talk;
  - his relationships with Chad, Vati and Willa ("ma'am, sorry, ma'am").
- **The scene reaches them only in part.** Today's server reads the rose (an Aware Object) and the setting. "What Is Going On" (the ice) is not read until HQ PR #35 is live.
- **A one-field edit did NOT reliably change the answer on the live server.** Run 1 showed it; run 2 did not.
  - Root cause: HQ keeps one conversation memory per machine and character name. Tony remembered his earlier answers (all runs were on one machine with one key) and kept repeating "nobody picks me".
  - Fix: added to HQ PR #35 (commit `46f733b`). A bible character's memory key now includes a hash of the bible, so an edited bible is a fresh person. The same PR gives each bible field its own place in the dialogue.
  - Until PR #35 is merged, an edit shows clearly on a machine that has not talked to that character before. Renaming the character (Name) also starts a fresh memory.
- **This is `-game` with NullRHI, not Play In Editor, and has no frames**, because the GPU was busy with Cameron's editor.
- **Visual Studio is installed on FermataJose.** Even so, the zip has no plugin `Source/`, and the log shows the module loading from the shipped DLL with no build step.
