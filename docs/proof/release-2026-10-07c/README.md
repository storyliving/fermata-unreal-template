# Proof: release v2026.10.07c, a stranger's Play (2026-10-07)

**The release:** zip sha256 `62bb1d75e3576ee4ca45b8faa4f0efa4c4f2cd2ef72a1f4a44cd1cd23162c9f1`, 1,755,414,542 bytes, built from build-a-bachelor `e564f83`. Checks run on it:
- clean-room check PASS, including the scripted-dialogue gate;
- secret-dispatch-gate clean.

**Where it ran:** FermataJose, unzipped into a fresh folder: no plugin source, no `Saved/`. It was opened in the UE 5.8 editor on `BAB_Room`, the default map, and played with Play In Editor. A maintainer harness pressed Play; nobody typed or spoke.

**What it shows:**
- `log-excerpt.txt`: the plugin loads from the shipped DLL. There is no LevelSequence actor and no camera takeover.
- Talking tiers: Vati full face, Toucantino jaw bone, Tony body + caption.
- The three characters talk to each other on their own. Every line is generated live and nothing is scripted.
- `room_conversation.mp4` (about 22 s, no audio) and `pie_stranger_*.png`: frames of the editor window during that play.

**Not shown here:** a real person talking with T. Nobody was at the machine, and the demo is never driven by a scripted or synthesized player voice. When a person holds T, the Output Log prints three lines: `mic: using "..."`, `peak level ...`, then `heard (200): "..."`, followed by the reply.
