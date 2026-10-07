# Tripo (text or image to 3D)

**Talking tier: body talk + caption** for the sample. A Tripo model with mouth blendshapes reaches tier 2; one rigged with a jaw bone reaches tier 3.

Worked example in `BAB_Villa`: **Vesper Quill**, an owl made with Tripo P2, rigged in Blender, with role clips baked by the anim-roles pipeline. Source: `SampleCharacters/vesper_tripo.glb` plus `vesper_tripo.runtime.json` (which clip plays which role) and `vesper_tripo.manifest.json` (the full role manifest).

## From prompt to talking character

1. **Make the model.** Tripo, text or image to 3D, in an A-pose or T-pose. Ask for separate parts (head, body, wings, accessories) if you want them animated separately.
2. **Rig and give it roles.** Tripo's auto-rig works for humanoids. For anything else, rig it in Blender. Then run the anim-roles pipeline (Fermata's `lib/anim-roles`): it detects the rig type (biped, quadruped, multileg, flyer, wheeled...), maps your clips to roles, and bakes the missing ones (idle, talk, emote_happy, emote_sad, emote_angry, emote_surprised, nod...). Export a GLB with one clip per role.
3. **Import into Unreal.** Drag the GLB into the Content Browser (or run `tools/import_sample_characters.py`). You get one or more skeletal meshes on one skeleton, plus one AnimSequence per role.
4. **Place it.** Drag `Content/Fermata/Templates/BP_FermataCharacter_AnyRig` into the level.
   - **Mesh** component: the main skeletal mesh (the body).
   - **Parts**: the other meshes from the same import (head, wings, scarf...). They follow the body.
   - **Role Animator > Roles**: role name to AnimSequence (`idle`, `talk`, `emote_happy`...).
   - **Capsule**: half-height about half the model's height. The mesh's Z offset puts its feet on the floor.
5. **Choose who it is** on the Fermata Character component (Custom Character + Bio + Voice From, or a Character Id).
6. Press Play.

## What it does on its own

- Idle when quiet, `talk` while speaking, an emote when its emotion changes (happy, excited, amused and impressed play `emote_happy`; sad, disappointed and bored play `emote_sad`; angry, annoyed and disgusted play `emote_angry`; surprised, fearful and curious play `emote_surprised`; skeptical and wary play `nod`), crossfaded.
- A missing role falls back to `idle`, so nothing is ever unplayable.
- Caption bubble, mood light and nameplate, like every character.

Spend note: generating new Tripo models costs money. The sample uses an existing model.
