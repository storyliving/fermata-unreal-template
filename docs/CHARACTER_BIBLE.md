# Make your own character: the Character Bible and the Scene Description

Two things decide what a character says:
- **The Character Bible** says who they are: their personality, their life, what they want, what scares them, how they talk.
- **The Scene Description** says where they are right now: the setting, the time, the mood, what is going on, and who you (the player) are to them.

You only edit text. There is no Blueprint graph to wire and no code. Change a field, press **Play**, and the character talks differently.

You need: Unreal Engine 5.8, and this project opened (`BuildABachelor.uproject`). If you have not installed it yet, see the [README](../README.md#1-install).

Screenshots for each step are in [`images/bible/`](images/bible/), linked from each step.

---

## The 60-second version

1. Open `Content/Fermata/Bibles/DA_Bible_Example`. Change **Fears** to something else, for example *"Geese. One chased him across a parking lot in 2016."*
2. Save (Ctrl+S).
3. Press **Play** in `BAB_Villa`. Tony stands right in front of you.
4. Look at Tony, press **C**, type *What are you scared of?* and press Enter.

Tony's answers change: the bridges he was afraid of are gone, and geese come up. He also remembers your earlier conversations with him, so he may mix in what you talked about before.

---

## 1. Start from the template character

The starting point is `Content/Fermata/Templates/BP_MyCharacter_Template`. It comes with:
- a body: the UE Mannequin, until you swap it;
- the **Bible** slot already filled with the example bible, `DA_Bible_Example` (Tony Pellegrino, a driving instructor from Staten Island);
- three events already placed in its Event Graph, each in a comment box that says what it is for: **On Emotion Changed**, **On Line Spoken** and **On Aware Of Object**. Each one prints to the screen until you replace the Print String with your own nodes.

Screenshot: [BP_MyCharacter_Template, with the start-here comment and the three stubbed events](images/bible/02_template_bp.png)

To make your own:

1. In the Content Browser, right click `BP_MyCharacter_Template` and choose **Duplicate**. Name the copy `BP_<YourCharacter>`, for example `BP_Dolores`.
2. Right click `DA_Bible_Example` (in `Content/Fermata/Bibles`) and choose **Duplicate**. Name the copy `DA_Bible_<YourCharacter>`.
3. Open your new Blueprint. In the **Components** panel select **Fermata**. In **Details**, under **Fermata | Your character**, set **Bible** to your new bible.
4. Give it a body: select **Mesh** and set **Skeletal Mesh Asset** and **Anim Class**. If you leave them blank, it uses the UE Mannequin. For a MetaHuman, a Tripo model or any other rig, see [Bring any character](BRING_ANY_CHARACTER.md).
5. Compile and save. Drag it into the level and press **Play**.

The other templates (`BP_FermataCharacter`, `BP_FermataCharacter_MetaHuman` and `BP_FermataCharacter_AnyRig`) have the same **Bible** slot on their **Fermata** component. Any actor with a **Fermata Character** component can take a bible.

## 2. Configure the personality: edit the Character Bible

Double click your bible asset. Every field is plain text.

Screenshot: [DA_Bible_Example open in the Data Asset editor](images/bible/01_bible_asset.png)

| Field | What to write | Limit |
|---|---|---|
| **Name** | What everyone calls them. It is shown above the head. | 40 |
| **Who They Are** | **The personality.** Age, job, how they come across in the first minute, and what they think of themselves. | 800 |
| **Life So Far** | Their backstory: places, people, money, years. | 1200 |
| **Wants** | What they want tonight, in their own words. | 300 |
| **Fears** | What scares them. | 300 |
| **Secret** | Something they hide, and what it would cost them if it came out. They will not say it unless they are cornered. | 300 |
| **How They Talk** | Speaking style: accent or region, pace, short or long sentences, the one word they overuse, what they never say. | 400 |
| **Example Lines** | Up to six lines that sound exactly like them. These shape their voice more than anything else. | 160 each |
| **Relationships** | The other people in the room, one per line: who they are, what happened between them, and how this character feels about them now. | 600 |
| **Quirks** | Habits and odd details. | 400 |
| **Voice From** | Whose voice they borrow (one of the event cast). | |

Longer text is trimmed. Every field is optional, and an empty field is simply left out.

**What makes a bible work:** specifics, not adjectives.

| Instead of... | write... |
|---|---|
| insecure | "failed his own road test twice and the school sign says first-time passers" |
| funny | "laughs at his own stories before he gets to the end" |
| has an ex | "his ex Gina passed first try, then drove straight to her new boyfriend Ray's house" |
| talks casually | "starts everything with 'listen', never says 'journey'" |

Example lines should be plain and specific. *"Me? Nervous? Nah. I'm just checking my mirrors."* works. A clever one-liner that any character could say does not.

**Make a new bible from scratch:** in the Content Browser, right click, then **Miscellaneous > Data Asset**, and pick **Fermata Character Bible**.

**Change it while the game runs (Blueprint):** the bible's fields are Blueprint read/write, and the **Fermata** component has **Set Bible** (and **Get Bible**). The next line the character says uses the new text.

### Which "who is this" wins

The **Fermata** component can be told who the character is in four ways. The first one that is set wins:
1. **Submission Id**: a guest-built character (press **U** in game).
2. **Bible**: your Character Bible.
3. **Custom Character** + **Bio**: one short paragraph, for a quick test.
4. **Character Id**: a Composer cast member (Willa, Chad, Vati...). Their personality is Composer's official record.

## 3. Set the Scene Description

Each level can have one **Fermata Scene** actor. `BAB_Villa` has one, called `FermataScene` (find it in the Outliner under the **Scene** folder). Select it and fill in **Details > Scene**.

Screenshot: [the FermataScene actor selected in BAB_Villa, with its Scene fields in Details](images/bible/03_scene_actor.png)

| Field | Example (from `BAB_Villa`) |
|---|---|
| **Setting** | The Build a Bachelor villa lounge on the water: a heart-shaped arch of lights, a fire pit with sofas around it, a pink-lit bar and a pool. |
| **Time Of Day** | Golden hour, about twenty minutes before the rose ceremony. |
| **Mood** | Giddy and on edge. Everyone is being nice the way people are nice right before a vote. |
| **What Is Going On** | The Last Rose sits on a brass pedestal by the fire pit and nobody will say who it is for. The bar ran out of ice an hour ago and everyone is blaming Chad. |
| **Who The Player Is** | A new arrival who walked in ten minutes ago with one suitcase. Nobody knows yet if they are competition. |

Every character in the level hears this, both when they talk to you and when they talk to each other. **What Is Going On** is the field they pick up most, so make it concrete.

- **A new level:** drag in **Fermata Scene** (Place Actors panel, search "Fermata Scene") or `Content/Fermata/Templates/BP_FermataScene`.
- **A level with no Fermata Scene:** the characters fall back to **Project Settings > Plugins > Fermata > Location Description**, a single sentence for the whole project.
- **Change it during play (Blueprint):** use **Get Fermata Scene** and set its fields. For example, change **What Is Going On** when a cutscene ends. The next line uses it.

When you press Play, the Output Log confirms what the characters were given:

```
[FermataEvent] scene (FermataScene): The Build a Bachelor villa lounge ... | player: A new arrival ...
[FermataEvent] Tony plays Character Bible DA_Bible_Example (voice from Ethan) | wants: ... | fears: ...
```

## 4. Hook behaviour to what they say

Open your Blueprint's **Event Graph**. The three stubs are already there:

| Event | Fires when | Try |
|---|---|---|
| **On Emotion Changed** (Old Emotion, New Emotion) | their feeling changes | play a montage, change a material, spawn VFX |
| **On Line Spoken** (Line, Emotion, Spoken To) | they say a line to you or to another character | gestures, subtitles, camera cuts |
| **On Aware Of Object** (Object, Object Name, Description) | they notice an Aware Object nearby | look at it, walk to it |

More events, such as **On Line Heard**, **On Conversation Started** and **On Conversation Ended**, are on the **Fermata** component's Details panel under **Events**. Click **+** next to one to add it. The full list is in the [README](../README.md#5-hook-custom-behaviour).

## Known limit (2026-10-07)

The server update that reads every bible and scene field on its own (HQ PR #35) is awaiting approval. Until it is live:
- **Bible:** the plugin also sends a packed copy, which today's server reads. Everything still reaches the character:
  - Who They Are, Wants, Fears, How They Talk and Quirks as one 800-character summary;
  - Life So Far and Relationships as one 1200-character description.

  Very long bibles get cut at those limits. Secret and Example Lines are only used after the update.
- **Scene Description:** only **Setting** (first 160 characters) reaches the characters today, together with the Aware Objects. Time Of Day, Mood, What Is Going On and Who The Player Is are sent and logged, and take effect when the update is live. You do not need to change anything in the project.

## Proof

What Tony said, before and after a one-field bible change, is in [`proof/bible/`](proof/bible/). It was run on the release zip, unzipped to a fresh folder.
