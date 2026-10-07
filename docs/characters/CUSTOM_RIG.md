# Custom rig (any skeleton)

**Talking tier: depends on the rig.** Mouth blendshapes reach tier 2, a jaw or beak bone reaches tier 3, and anything else talks with its body plus a caption (tier 4).

Worked example in `BAB_Villa`: **Marlowe**, an eight-legged spider (`SampleCharacters/marlowe_spider.glb`, 47 parts on one skeleton, multileg archetype, 12 baked clips). The custom-rig slot is now **Toucantino** (`SampleCharacters/customrig.glb`: 48 bones, a hinged beak driven by his Composer voice, look-at eyes, eyelids, brow morph targets, feather-fan wings, 15 clips). Rebuild: `tools/toucantino_import.py`, `tools/build_villa_map.py`, then `tools/toucantino_setup.py` (Composer character id, jaw cap 18 deg, gesture roles, lights and the film camera sequence).

## Steps

1. **Export** your character as FBX or GLB with its skeleton and clips (one clip per role if you have them).
2. **Give it roles** (optional, recommended). Run the anim-roles pipeline on it: it reads bone names and rest geometry, detects the archetype (biped, quadruped, multileg, wheeled, flyer, rigid), matches your clips to roles and bakes procedural ones for anything missing. It never invents limbs: a car has nothing to wave with, and the coverage report says so.
3. **Import** into Unreal (drag and drop). A model exported as parts imports as several skeletal meshes on one skeleton; that is fine.
4. **Place** `Content/Fermata/Templates/BP_FermataCharacter_AnyRig`:
   - **Mesh**: the main mesh. **Parts**: the rest. **Model Scale** if needed.
   - **Role Animator > Roles**: role to AnimSequence.
   - **Jaw Bone** (optional): blank finds the first bone named like `jaw`. Set **Jaw Open Rotation** to the axis your rig opens on.
   - **Mouth Morph Targets** (optional, on the Fermata Character component) if your blendshapes use other names.
   - **Model Yaw Offset** on the Fermata Character component if your model faces sideways (so it turns to face whoever it talks to).
5. **Choose who it is** and press Play. The Output Log prints `<Name> talking tier: ...`.

## Humanoid custom rigs

A humanoid with its own skeleton can also borrow the UE Mannequin's animations through the **IK Retargeter** (create an IK Rig for your skeleton, retarget from `IK_Mannequin`), then use it like the Mannequin template with your retargeted Animation Blueprint.

## Your own behaviour

Bind the component events (OnEmotionChanged, OnLineSpoken, OnConversationStarted, OnAwareOfObject...) or call **Play Role** on the Role Animator (for example `wave` when a conversation starts).
