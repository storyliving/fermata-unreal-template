# Tripo (text or image to 3D)

**Talking tier: body talk + caption** for the sample. A Tripo model with mouth blendshapes reaches tier 2; one rigged with a jaw bone reaches tier 3.

Worked example in `BAB_Villa`: **Vesper Quill**, an owl made with Tripo P2 and rigged in Blender. She ships already imported and placed (`Content/Fermata/Samples/Tripo_Vesper`). Select her and look at **Role Animator > Roles** to see a finished mapping.

## From prompt to talking character

1. **Make the model.** Tripo, text or image to 3D, in an A-pose or T-pose. Ask for separate parts (head, body, wings, accessories) if you want them animated separately.
2. **Rig and animate it.** Tripo's auto-rig works for humanoids. For anything else, rig it in Blender, or any tool you like. Make the clips you want, one per action: an idle, a talk loop, and if you can a happy, a sad, an angry and a surprised reaction and a nod. Name them so you can tell them apart (`Owl_Idle`, `Owl_Talk`, `Owl_Happy`...). Export a GLB or FBX with the clips.
3. **Import into Unreal.** Drag the GLB or FBX into the Content Browser. You get one or more skeletal meshes on one skeleton, plus one AnimSequence per role.
4. **Place it.** Drag `Content/Fermata/Templates/BP_FermataCharacter_AnyRig` into the level.
   - **Mesh** component: the main skeletal mesh (the body).
   - **Parts**: the other meshes from the same import (head, wings, scarf...). They follow the body.
   - **Role Animator > Roles**: role name to AnimSequence (`idle`, `talk`, `emote_happy`...). Fill it by hand, or let the script do it: see [Map your animations to roles](CUSTOM_RIG.md#map-your-animations-to-roles).
   - **Capsule**: half-height about half the model's height. The mesh's Z offset puts its feet on the floor.
5. **Choose who it is** on the Fermata Character component (Custom Character + Bio + Voice From, or a Character Id).
6. Press Play.

## What it does on its own

- Idle when quiet, `talk` while speaking, an emote when its emotion changes (happy, excited, amused and impressed play `emote_happy`; sad, disappointed and bored play `emote_sad`; angry, annoyed and disgusted play `emote_angry`; surprised, fearful and curious play `emote_surprised`; skeptical and wary play `nod`), crossfaded.
- A missing role falls back to `idle`, so nothing is ever unplayable.
- Caption bubble, mood light and nameplate, like every character.

Spend note: generating new Tripo models costs money. The sample uses an existing model.
