# Bring any character

Any 3D character can be a talking Fermata character: a MetaHuman, a Tripo model, a bird, a spider, a car, your own rig, or the UE Mannequin. The character's mind, voice and memory come from Fermata. Your character supplies the body.

**Writing who they are:** [Character Bible and Scene Description](CHARACTER_BIBLE.md). Start from `BP_MyCharacter_Template`. It comes with a filled-in bible.

## Start here

| I have... | Use | Template Blueprint | Guide |
|---|---|---|---|
| nothing yet, and I want to write my own character | the template character | `BP_MyCharacter_Template` (bible + events ready) | [Character Bible](CHARACTER_BIBLE.md) |
| nothing yet | the UE Mannequin | `BP_FermataCharacter` | [Mannequin](characters/MANNEQUIN.md) |
| a MetaHuman | the MetaHuman template | `BP_FermataCharacter_MetaHuman` (or add the component to your `BP_<Name>`) | [MetaHuman](characters/METAHUMAN.md) |
| a Tripo model (text or image to 3D) | the any-rig template | `BP_FermataCharacter_AnyRig` | [Tripo](characters/TRIPO.md) |
| any rigged FBX or GLB (bird, creature, spider, car, custom humanoid) | the any-rig template | `BP_FermataCharacter_AnyRig` | [Custom rig](characters/CUSTOM_RIG.md) |

`BAB_Room` (the default level) has a Mannequin (Tony), a MetaHuman (Vati) and a custom rig (Toucantino). `BAB_Villa` also has the Tripo owl. Press Play and they talk to each other.

| Type | In the demo | Talking tier it reaches |
|---|---|---|
| UE Mannequin | Willa, Chad, Raj (tinted stand-ins) | Body talk + caption |
| MetaHuman | Vati | Full face |
| Tripo | Vesper Quill (an owl) | Body talk + caption (her rig has no jaw or mouth blendshapes) |
| Custom rig | Marlowe (a spider). Toucantino replaces him when his rig lands. | Body talk + caption |

## What every character needs

1. **A body**: a skeletal mesh. Anything that imports into Unreal works.
2. **Who it is**: on the **Fermata Character** component, either set a **Bible** (a Character Bible data asset: [guide](CHARACTER_BIBLE.md)), pick a Composer cast member from **Character Id**, tick **Custom Character** and write a short **Bio** with a **Voice From**, or paste a guest's **Submission Id**.
3. **Optional**: role animations (idle, talk, emote_happy, emote_sad, emote_angry, emote_surprised, nod...). The **Fermata Role Animator** component plays them. Anything without them still talks.

## How talking works, by tier

The plugin picks the best tier your character supports and prints it in the Output Log at Play (`<Name> talking tier: ...`). Read it back in Blueprint with `Get Talk Tier`.

| Tier | Your character has | What moves when it speaks |
|---|---|---|
| 1. Full face | a MetaHuman face (a `Face` component) | The whole face: jaw, lips, blinks, and the emotion's expression, from our audio. |
| 2. Mouth blendshapes | morph targets named `jawOpen`, `mouthOpen`, `viseme_aa`, `Mouth_Open` or `MouthOpen` (ARKit or viseme sets) | That blendshape opens and closes with the voice. Add your own names under **Mouth Morph Targets**. |
| 3. Jaw bone | a bone with `jaw` in its name, and a Role Animator | The jaw rotates with the voice (set **Jaw Open Rotation** for your rig's axis). |
| 4. Body talk + caption | none of the above | The `talk` role animation plays while it speaks, an emote plays on every emotion change, a caption bubble shows the line, and the mood light pulses. |

Every tier also gets the emotion-coloured nameplate, the mood light and every Blueprint event. To drive a jaw, beak or material yourself, read `Get Mouth Open` (0 to 1) from the Fermata Character component in your own Animation Blueprint.

## Inviting people to bring their own characters

The live intake for Build a Bachelor is the web builder on build.lovebird.show. A guest makes a character there (or uploads one) and writes who they are. In Unreal, press **U** while looking at a body to load the newest guest character into it.

What works today, and what does not:

| Step | Status |
|---|---|
| A guest writes their character on the web | Live (build.lovebird.show builder, Composer public API) |
| **U** in game loads that guest's mind, bio and a voice into the body you look at | Live, proven in `docs/proof/upload_*` |
| The guest's own 3D model, rigged, comes into the running game | **Not yet.** See below. |
| MetaHumans uploaded by guests | **Not possible.** A MetaHuman is assembled in the editor and its rig is editor-built; it cannot be uploaded into a running game. Bring a MetaHuman by adding it to the project (see the MetaHuman guide). |

### Getting a guest's body into the running game (plan)

- **In the editor today:** import the guest's GLB/FBX with the [Custom rig](characters/CUSTOM_RIG.md) steps. Five minutes per character.
- **At play time, inside the editor:** Unreal 5.8's Interchange glTF importer can run while the game plays in the editor, so **U** can download the guest's rigged GLB and import it on the spot. This is the next build step. It needs the backend to hand out the guest's rigged GLB link next to their bio.
- **In a packaged game:** use [glTFRuntime](https://github.com/rdeioris/glTFRuntime) (MIT licence, maintained). It loads skeletal meshes and animations from a GLB at runtime without editor code.
- **Rigging and role clips for uploads:** Fermata's own pipeline can detect a rig's type, match clips to roles and make missing ones in Blender. It runs on Fermata's machines today; it is not in this project and not yet a hosted service behind the upload. In this project, map clips to roles by hand or with `Content/Python/fermata_roles.py` ([how](characters/CUSTOM_RIG.md#map-your-animations-to-roles)).

## What the plugin does and does not contain

The plugin moves words, emotions and audio, and drives faces, jaws, blendshapes, role clips, captions and lights. Who the characters are, who speaks next, what they remember, their voices and every provider credential live on Fermata's servers. The plugin ships as compiled binaries only, and a clean-room scan (`tools/cleanroom-check.mjs`) checks every package for keys and for that vocabulary before it is zipped.
