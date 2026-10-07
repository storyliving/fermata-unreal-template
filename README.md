# Build a Bachelor: the Unreal Engine 5.8 template

Drop characters into a level and press **Play**. They talk to each other, and when you walk up they talk to you. They have feelings, voices and memories. You decide who they are by writing a **Character Bible**, and where they are with a **Scene Description**. No code, no Blueprint wiring, no Visual Studio.

**[Download BuildABachelor-UE5.8.zip (1.7 GB)](https://github.com/storyliving/fermata-unreal-template/releases/latest/download/BuildABachelor-UE5.8.zip)** · [all releases](https://github.com/storyliving/fermata-unreal-template/releases)

## 1. Install

1. Install **Unreal Engine 5.8** from the Epic Games Launcher (Windows).
2. Download `BuildABachelor-UE5.8.zip` (link above) and unzip it anywhere, for example `Documents\BuildABachelor`.
3. Double-click `BuildABachelor\BuildABachelor.uproject`. If Windows asks which program to use, pick Unreal Engine 5.8.
   - The first open compiles shaders and can take 5 to 15 minutes. That is normal.
   - The plugin is already compiled, so you do not need Visual Studio. If Unreal says modules are missing, you opened it with another engine version: use 5.8.
4. The level `BAB_Villa` opens. Press **Play** (Alt+P).

## 2. Play

Within a few seconds the cast starts talking to each other. **Tony**, the template character, is standing right in front of you.

| Key | What it does |
|---|---|
| **WASD + mouse** | Walk and look |
| **C** | Type a line to the character you are looking at (Enter sends, Esc closes) |
| **T** (hold) | Talk out loud with your microphone. Let go to send. |
| **V** | Director camera |
| **U** | Load the newest guest-built Build a Bachelor character into whoever you are looking at |

It works out of the box on a shared public event key. That key is rate limited and will be switched off after the event; when it is, the characters go quiet. To use your own key, go to **Project Settings > Plugins > Fermata > Fermata API Key**.

## 3. Make your own character: edit the Character Bible

The character's personality lives in a **Character Bible**, a Data Asset you edit like a form.

1. Open `Content/Fermata/Bibles/DA_Bible_Example` (Tony). Change **Fears**, or **Who They Are**, or anything else.
2. Save, press **Play**, walk up to Tony, press **C** and ask him about it.

To make your own: duplicate `Content/Fermata/Templates/BP_MyCharacter_Template` and `DA_Bible_Example`, rewrite the bible, and set your Blueprint's **Fermata > Bible** to it.

**Step-by-step guide: [docs/CHARACTER_BIBLE.md](docs/CHARACTER_BIBLE.md).**

| Bible field | What it is |
|---|---|
| Name | what everyone calls them |
| Who They Are | the personality |
| Life So Far | the backstory |
| Wants · Fears · Secret | what drives them |
| How They Talk · Example Lines | the speaking style |
| Relationships · Quirks | the people in the room, the odd details |
| Voice From | whose voice they borrow |

## 4. Set the Scene Description

Select the **FermataScene** actor in `BAB_Villa` (Outliner > Scene). Fill in **Setting**, **Time Of Day**, **Mood**, **What Is Going On** and **Who The Player Is**. Every character in the level hears it. For a new level, drag in **Fermata Scene** from Place Actors. ([guide](docs/CHARACTER_BIBLE.md#3-set-the-scene-description))

## 5. Hook custom behaviour

`BP_MyCharacter_Template` already has three events placed and explained in comment boxes: **On Emotion Changed**, **On Line Spoken** and **On Aware Of Object**. Replace the Print String nodes with your own. More events are on the **Fermata** component under **Events**:
- On Line Heard
- On Conversation Started and On Conversation Ended
- On Character Swapped

| Bring your own body | Guide |
|---|---|
| A MetaHuman, a Tripo model, any rigged FBX or GLB, or the UE Mannequin | [docs/BRING_ANY_CHARACTER.md](docs/BRING_ANY_CHARACTER.md) |

## Requirements and limits

- Windows, Unreal Engine **5.8**, and an internet connection. The characters' minds and voices run on Fermata's servers.
- The zip is the complete project, compiled. This repository holds the docs; the project ships as the release download.
- Known limits today are listed at the end of [docs/CHARACTER_BIBLE.md](docs/CHARACTER_BIBLE.md#known-limit-2026-10-07).

## Install by QR

Scan to open this page on your phone:

[QR code (PNG)](assets/bab-install-qr.png) · [SVG](assets/bab-install-qr.svg)

Copyright Fermata, Inc. Provided for Build a Bachelor participants to use and modify. MP3 decoding uses [dr_mp3](https://github.com/mackron/dr_libs) (public domain / MIT-0). MetaHuman assets are used under Epic's MetaHuman and Unreal Engine terms.
