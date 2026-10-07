# Custom rig (any skeleton)

**Talking tier: depends on the rig.** Mouth blendshapes reach tier 2, a jaw or beak bone reaches tier 3, and anything else talks with its body plus a caption (tier 4).

Worked example in `BAB_Villa`: **Marlowe**, an eight-legged spider (`SampleCharacters/marlowe_spider.glb`, 47 parts on one skeleton, multileg archetype, 12 baked clips). The custom-rig slot is now **Toucantino** (`SampleCharacters/customrig.glb`: 48 bones, a hinged beak driven by his Composer voice, look-at eyes, eyelids, brow morph targets, feather-fan wings, 15 clips). Rebuild: `tools/toucantino_import.py`, `tools/build_villa_map.py`, then `tools/toucantino_setup.py` (Composer character id, jaw cap 18 deg, gesture roles, lights). Play in `BAB_Villa` always starts in the normal walkable view: the film camera plan is NOT in that map. `tools/toucantino_film_setup.py` builds a separate film map (`/Game/Fermata/Film/BAB_Villa_Film`: cast cleared, Toucantino by the heart arch, nameplate, caption and mood light off, measured shot plan). Launch it with `-FermataNoHud` for a clean picture. (`SampleCharacters/` and `tools/` live in Fermata's source repository for maintainers. They are **not** in the download: in the download, the sample characters come already imported and placed in `BAB_Villa`.)

## Steps

1. **Export** your character as FBX or GLB with its skeleton and clips (one clip per role if you have them).
2. **Animate it** (optional, recommended). One clip per action: idle, talk, and if you have them happy, sad, angry, surprised and nod. A character with only an idle still works: every missing role falls back to idle.
3. **Import** into Unreal (drag and drop). A model exported as parts imports as several skeletal meshes on one skeleton; that is fine.
4. **Place** `Content/Fermata/Templates/BP_FermataCharacter_AnyRig`:
   - **Mesh**: the main mesh. **Parts**: the rest. **Model Scale** if needed.
   - **Role Animator > Roles**: role to AnimSequence, by hand or with the script below.
   - **Jaw Bone** (optional): blank finds the first bone named like `jaw`. Set **Jaw Open Rotation** to the axis your rig opens on.
   - **Mouth Morph Targets** (optional, on the Fermata Character component) if your blendshapes use other names.
   - **Model Yaw Offset** on the Fermata Character component if your model faces sideways (so it turns to face whoever it talks to).
5. **Choose who it is** and press Play. The Output Log prints `<Name> talking tier: ...`.

## Map your animations to roles

The **Fermata Role Animator** plays one clip per *role*. These are the roles:

| Role | When it plays |
|---|---|
| `idle` | when the character is quiet (and for any role you leave empty) |
| `talk` | while it speaks |
| `emote_happy` | happy, excited, amused, impressed |
| `emote_sad` | sad, disappointed, bored |
| `emote_angry` | angry, annoyed, disgusted |
| `emote_surprised` | surprised, fearful, curious |
| `nod` | skeptical, wary |
| `wave`, `walk`, `celebrate` | when you call **Play Role** from Blueprint |

**By hand:** select the character, find **Fermata Role Animator** in Details, and under **Roles** click **+** for each role. Then pick the role name and the clip.

**With the script** (ships in the project as `Content/Python/fermata_roles.py`, needs nothing else):
1. Open **Window > Output Log**, and switch the box at the bottom from **Cmd** to **Python**.
2. Guess roles from your clip names and write a file you can edit:
   `import fermata_roles; fermata_roles.suggest('/Game/MyBird')`
   It prints the guesses and the path of the `.roles.json` it wrote (under `Saved/FermataRoles/`).
3. Fix anything it guessed wrong in that file. It is plain JSON, as in this example:
   `{"folder": "/Game/MyBird", "roles": {"idle": "Bird_Idle", "talk": "Bird_Talk", "emote_happy": "Bird_Hop"}, "jawBone": "beak_lower", "jawOpenRotation": [0, 0, 18]}`
4. Select your character(s) in the level and run `fermata_roles.apply('C:/path/to/MyBird.roles.json')`. To set a Blueprint's defaults instead, add `blueprint='/Game/MyBird/BP_MyBird'`.
5. `fermata_roles.show()` prints what the selected characters have now.

**Talking mouths:**
- **Jaw or beak bone:** set **Jaw Bone** (blank finds a bone named like `jaw`), and **Jaw Open Rotation** for the direction it opens.
- **Mouth blendshapes:** list their names in **Mouth Morph Targets** on the Fermata Character component.
- **Anything else:** read **Get Mouth Open** (0 to 1) from the Fermata Character component in your own Animation Blueprint, and drive whatever you like with it (a material, a scale, a lid).

## Humanoid custom rigs

A humanoid with its own skeleton can also borrow the UE Mannequin's animations through the **IK Retargeter** (create an IK Rig for your skeleton, retarget from `IK_Mannequin`), then use it like the Mannequin template with your retargeted Animation Blueprint.

## Your own behaviour

Bind the component events (OnEmotionChanged, OnLineSpoken, OnConversationStarted, OnAwareOfObject...) or call **Play Role** on the Role Animator (for example `wave` when a conversation starts).
