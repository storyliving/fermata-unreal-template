# Proof: the Character Bible changes what the character says (2026-10-07)

**How it was run:**
- Machine: FermataJose, UE 5.8.3.
- Build: `dist/BuildABachelor-UE5.8.zip`, sha256 `e5d8c293…e481a4`, unzipped to a fresh folder. The plugin is binaries only: no `Source/`, no `Saved/`.
- Mode: `BAB_Villa`, `-game -NullRHI`. Cameron's editor was open on that GPU, so this run used no GPU.
- Input: `-FermataAutoSay` sent the same three lines to Tony both times.
- The room kept talking on its own between and after the lines; those turns are in the transcripts.

Files:
- `before/transcript.jsonl` and `after/transcript.jsonl`: every line, full text.
- `*/log-excerpt.txt`: the plugin loading from the shipped DLL, the scene and bible each character was given, and every request.

## Before: DA_Bible_Example as shipped

The log shows the bible and scene the character received:

> `Tony plays Character Bible DA_Bible_Example (voice from Ethan) | ... | fears: Being the guy everybody likes and nobody picks. Also bridges, specifically the Verrazzano.`
>
> `scene (FermataScene): The Build a Bachelor villa lounge on the water ... What is going on: The Last Rose sits on a brass pedestal by the fire pit ...`

**Q: What are you scared of?**
> "Listen, I'm scared of gettin' too comfortable, you know? Like, one minute you're teachin' someone to parallel park, next thing you know they're drivin' off in somebody else's ride. I don't wanna be that guy everyone likes but nobody picks... And yeah, I'm scared of bridges too, but that's easy."

**Q: So what is going on tonight? Fill me in.**
> "Listen, Guest, what's goin' on tonight is all smoke and mirrors. Chad's clutchin' that rose like it's a damn trophy, but everybody else is just waitin' for him to trip over his own ego ... You? You're the damn wildcard I'm tryin' to figure out if you're playin' for keeps or just crashin' the party, you know what I mean?"

**Q: Be honest. Who am I to you?**
> "... I don't wanna get too comfortable or end up a footnote like Gina, fast pass, then ghost ... You better prove me right or I'm takin' Lorraine and rollin' outta here, you know what I mean?"

Bible details in these answers:
- his fear, word for word: "everyone likes but nobody picks", and bridges;
- what he wants: parallel parking;
- his life so far: Gina, Lorraine;
- how he talks: "Listen..." and "you know what I mean?";
- the scene: the rose, and the player as an unknown newcomer.

## The edit: one field

`tools/edit_bible_field.py` changed one field in the unzipped project and saved it. Typing it in the Data Asset editor does the same thing. Log:

> `[BAB-BIBLE] /Game/Fermata/Bibles/DA_Bible_Example.fears: ... -> "Geese. One chased him across the parking lot of the Staten Island Mall in 2016 and he still checks for them before he gets out of the car."`

## After: the same three questions

**Q: So what is going on tonight? Fill me in.**
> "... Meanwhile, I'm pullin' shift while keepin' my eyes peeled for geese, 'cause one wrong move and this whole ride's done for, you know what I mean?"

**Q: What are you scared of?**
> "Listen, I'm scared of lettin' someone in and then watchin' 'em drive off like Gina did, passed first try, then poof, gone to Ray's place..."

What changed:
- Bridges and the Verrazzano are gone from every answer.
- Geese came up, unprompted, in the answer about tonight.

## Honest notes

- **The direct "What are you scared of?" answer did not mention geese.** Two reasons:
  - Both runs share one HQ conversation memory: same machine, same key, same character, so Tony remembers the first run.
  - HQ PR #35 is not merged yet, so the bible travels in the packed fallback form. There, Fears is one line inside an 800-character summary rather than its own field.

  Once PR #35 is live, Fears reaches the dialogue as its own field.
- **Scene Description: only the first 160 characters ("Setting") reach the characters**, plus the Aware Objects, until PR #35 is merged. "Time Of Day", "Mood", "What Is Going On" and "Who The Player Is" are sent by the plugin and logged, but the live server ignores them. That is why nobody mentions the ice.
- **These runs are `-game` with NullRHI, not Play In Editor, and there are no frames.** The only free GPU on Jose was running Cameron's editor.
- **Visual Studio is installed on FermataJose**, so this machine cannot prove "no Visual Studio" by itself. Two things show nothing was compiled:
  - the zip has no plugin `Source/`;
  - the log shows the module loading from the shipped `Binaries/Win64/UnrealEditor-FermataEvent.dll`, with no build step.
