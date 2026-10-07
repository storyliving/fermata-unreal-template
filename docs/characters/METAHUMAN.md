# MetaHuman

**Talking tier: full face.** The face is driven from our audio: jaw and lips with the voice, blinks, and each emotion's expression (recorded takes or your own recorder poses override the built-in ones). Worked example in `BAB_Villa`: **Vati**, placed from `Content/Fermata/Templates/BP_FermataCharacter_MetaHuman` (Vati's MetaHuman with a Fermata Character component added).

**Editor only.** A MetaHuman is assembled in the editor (MetaHuman Creator) and its rig and face are built there. You add it to the project; nobody can upload a MetaHuman into a running game.


This takes about five minutes once your MetaHuman exists.

## 1. Bring the MetaHuman into the project

**Made in Unreal 5.8 (MetaHuman Creator in-editor)**
1. Open your MetaHuman Character asset, then click **Assemble** and choose **UE Optimized** or **Cinematic**.
2. Either assemble straight into this project, or right-click the assembled folder in your other project, choose **Asset Actions > Migrate...**, and pick `BuildABachelor/Content`.

**Downloaded from Fab / Quixel Bridge**
- Add it to this project. It lands in `Content/MetaHumans/<Name>/` next to `Content/MetaHumans/Common/`.

In every case you end up with a Blueprint called `BP_<Name>` that has a `Face` component.

## 2. Make it a Fermata character

1. Drag `BP_<Name>` into `Content/BuildABachelor/Maps/BAB_Villa` (or any level).
2. With it selected, click **Add** in Details and choose **Fermata Character**.
3. On that component, pick who it is:

| Field | Put |
|---|---|
| Character Id | a Composer cast member from the dropdown (Willa, Chad, Adonis, Ethan, Raj, Vati, Milton) |
| or Custom Character | tick it, write the **Bio** in a few sentences (*"A sweet, nervous firefighter who overshares about his three rescue cats."*), pick **Voice From** |
| or Submission Id | a guest-built Build a Bachelor character |
| Display Name | the name shown above their head (optional) |
| Emotion Set | optional, see step 4 |
| Wardrobe | outfit, shoes and props skinned to the body (optional) |

4. Press **Play**. Your character joins the room conversation on its own. Walk up, look at them, and hold **T** or press **C**.

To make every copy of your MetaHuman a Fermata character, add the component inside `BP_<Name>` itself instead of on the level instance.

## 3. Check the face is live

Ask something that should land, like *"I think you're amazing"* or *"I ate your sandwich."* The label above the head changes (`Brock - happy`), the mood light takes that emotion's colour, and the face blends to match while they speak.

If the face stays still:
- The component has to be named `Face`. If yours is named differently, set **Face Component Name** on the Fermata Talk component.
- The face mesh needs its MetaHuman **post-process Animation Blueprint**. Assembled MetaHumans have one by default. The Output Log line `face driver installed on Face (post-process ABP ...)` confirms it.

## 4. Record your character's emotions

**Quick, in game:** press **R**. Connect Live Link Face or MetaHuman Live Link. Pick an emotion with **[** and **]**, hold the face, and press **Space**. The pose is saved for that character.

**Full takes (Take Recorder / MetaHuman Animator):**
1. Record a short facial take on your MetaHuman's face skeleton. You get an AnimSequence.
2. In the Content Browser choose **Add > Miscellaneous > Data Asset > Fermata Emotion Set**.
3. Under **Face Takes**, add one entry per emotion (`happy`, `sad`, `angry`, ...) and point it at its take.
4. Assign the set to your roster entry, or set **Emotion Set** on the Fermata Talk component.

When a character feels an emotion, the face uses the first of these that exists:
1. your recorded take
2. your recorder pose
3. the built-in pose

## What leaves your machine

Only the words you said or typed, and the name and bio you wrote for your character, go to Fermata HQ to generate the reply. Your MetaHuman's mesh, textures and recorded faces never leave your computer.
