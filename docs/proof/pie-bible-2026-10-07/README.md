# Proof: Play In Editor, a bible edit changes the answer on a fresh memory (2026-10-07)

**Run setup**
- Machine: FermataJose, UE 5.8.3, a visible editor.
- Level: `BAB_Villa`, with the project from the release zip v2026.10.07b.
- Server: live HQ at `ea743cb`. That build sends each bible field on its own, keys a character's memory to a hash of its bible, and adds fears to the personality line.

**The test**
Four Play In Editor runs. Before each run, one field (`Fears` on `DA_Bible_Example`) was set and saved. The two questions to Tony were the same every time.

**Note on the questions**
- They came from a maintainers' test harness that typed them in automatically.
- That harness was deleted from the plugin the same day (Cameron: "NO SCRIPTED DIALOGUE"). The shipped build cannot do this.
- Nothing the characters said was scripted.

**Files**
- `editor-log-excerpt.txt`: each edit, plus every request and its full reply.
- `*/transcript.jsonl`: each run's lines.

## Run 1: Fears "...nobody picks. Also bridges, specifically the Verrazzano." (as shipped)

**Q: What are you scared of?**
> "Listen, Guest, I'm scared of bein' that guy everyone likes but nobody picks, you know what I mean? ... That scares me more than the Verrazzano Bridge on a foggy night."

## Run 2: Fears changed to "Geese. One chased him across the parking lot of the Staten Island Mall in 2016..."

**Q: What are you scared of?**
> "Listen, Guest, I'm scared of two things: one, geese, full stop. One of those feathered assholes chased me 'round Staten Island Mall like I stole its kid. ..."

## Run 3: Fears changed to "Escalators. He fell up the one at the Staten Island Ferry terminal in 2009..."

**Q: What are you scared of?**
> "Listen, Guest, I'm scared of that goddamn escalator at the Ferry terminal, fell right up the steps in front of my whole class. True story, and everyone laughed except me. ..."

## Run 4: Fears changed to "Clowns. His cousin Sal hired one for his 30th and it sat in the passenger seat of Lorraine..."

**Q: What are you scared of?**
> "Listen, Guest, I'm scared of clowns, alright? Not the funny birthday kind, no, no, the creepy ones that sit shotgun in your car while you parallel park. Cousin Sal hired one once, swore it was a joke. I nearly stalled Lorraine three times. ..."

## The Scene Description, same runs

Q: *So what is going on tonight, and how is everyone feeling?*

Answers drew on the level's Fermata Scene:
- the Last Rose ("Chad clutching that rose like it's a damn trophy");
- the mood ("everyone's walking on eggshells", "everyone's playing nice");
- the ice ("Chad's messing with the ice now");
- who the player is ("you just walked in with one suitcase").

Before the server update earlier the same day, only the first 160 characters of the scene reached the characters.

**Result**
- 4 of 4 runs: the answer reflected the edited field.
- 4 of 4: the old fear did not leak into the new run.
- Two independent edits each worked on a fresh memory.
