# UE Mannequin

**Talking tier: body talk + caption.** The zero-work default and the fallback body for any character that has no model yet.

Worked examples in `BAB_Villa`: **Willa**, **Chad** and **Raj**, each a tinted Mannequin.

## Use it

1. Drag `Content/Fermata/Templates/BP_FermataCharacter` into a level.
2. On its **Fermata Character** component, choose who it is:
   - **Character Id**: a Composer cast member (Willa, Chad, Adonis, Ethan, Raj, Vati, Milton). Their voice and character come from Composer.
   - or **Submission Id**: a guest-built Build a Bachelor character.
   - or tick **Custom Character**, write a **Bio**, pick **Voice From**.
3. Press Play.

The body is the UE5 Mannequin (Quinn by default) with its idle and locomotion Animation Blueprint. Set **Stand In Tint** to tell several stand-ins apart.

## Swap the body later

Select the actor, then its **Mesh** component, and set **Skeletal Mesh** and **Anim Class**. For a model with its own animations, use the [Custom rig](CUSTOM_RIG.md) template instead, which plays role clips.

## How it talks

The Mannequin has no face rig, so it speaks through the body: a caption bubble shows the line above its head while it talks, the mood light at its chest takes the emotion's colour and pulses with the voice, and the nameplate reads `Name - emotion`. Bind **OnEmotionChanged** or **OnLineSpoken** to play your own montages (for example a gesture from the Mannequin animation set).
