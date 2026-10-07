# Proof: release v2026.10.07b, played from a fresh unzip (2026-10-07)

**What was tested**
- Zip: `BuildABachelor-UE5.8.zip`, sha256 `73aa3fe9fed4a3a40a70b75fe45b6787ce2ff9a8b323d2c6797c0b53fdb7b970`, built from build-a-bachelor `13d576f`.
- The plugin was rebuilt from that source; the shipped DLL contains `-FermataNoHud` and `-FermataAutoSayDelay`.
- Before release: clean-room check PASS, and `secret-dispatch-gate` clean.

**How it was run**
- Machine: FermataJose, UE 5.8.3, from a fresh unzip in `C:\Users\jose\bab-zipproof3`. No `Source/`, no `Saved/`.
- Plain `-game` Play of `BAB_Villa`, rendered offscreen at 1280x720.
- Flags: `-FermataProofShots` (captures frames), plus one scripted line to Tony after 20 s.

**Results**
- `line_00_overview.png` is the player's own view from VisitorStart, 5 s in. It shows the walkable-room HUD ("Walk up to someone to talk to them") and the whole cast. Tony, the green stand-in at the far left, is in the foreground.
- No film sequence:
  - the log has no LevelSequenceActor, LevelSequencePlayer, LS_ToucantinoFilm, TB_FilmSequence or TB_Cam_ entries (count 0);
  - the frame is the player view.
- Tony and the FermataScene are present. The log shows:
  - `scene (FermataScene): The Build a Bachelor villa lounge on the water ...`
  - `Tony plays Character Bible DA_Bible_Example`
  - talking tiers for all seven characters (Toucantino: jaw bone).
- Q *"Hey, I just got here. What did I miss?"* Tony answered:
  > "Listen, Guest, what you missed? You missed Chad hoggin' that damn rose like it's the last slice of pizza at a family dinner. You missed Willa givin' off these icy vibes that could freeze Lorraine's engine, and Vati sittin' there classy but clockin' everyone like a hawk... you just walked into the middle of it, you know what I mean?"

  The template's On Line Spoken stub prints that line on screen (the cyan text in `line_02`).

**Note**
- `-FermataProofShots` switches on the director camera, which frames the later shots (`line_01`..`03`).
- A normal Play without that flag stays in the player view the whole time.
