POCKET - THE MINUTE AFTER
Rohan Tandon | Interactive iPhone prototype

START HERE
1. Unzip the entire folder and open Pocket.xcodeproj in Xcode.
2. Select the shared Pocket scheme and an iPhone simulator, then Run (Command-R).
3. On first launch, Atlas opens at the lock-screen preview. Tap the Pocket
   notification to enter the recording, or Skip to End to see the completed state.

Verified toolchain: Xcode 27.1. Use that version or newer for this project.
Deployment target: iOS 18.0. Use iOS 26 or newer for the Liquid Glass appearance.
No third-party packages, API keys, backend, or network connection are needed to
run the prototype once Xcode and an iPhone simulator runtime are installed.

To run on a physical iPhone, select your own signing team under Signing &
Capabilities and a unique bundle identifier if required, then choose the iPhone
as the run destination. This source ZIP is not an installable iPhone app.

TRY THE FLOW
- Atlas uses the supplied transcript, notes, calendar, audio, and arrival stream.
  Its original model mistakes are preserved. Arrival follows stream.json.
- Open the top-right menu for Replay arrival or Skip to end. Replay resets the
  current recording's review work as well as its arrival timeline.
- Review the priority launch date against the later exchange, choose a date,
  and draft a reply to Rachel. Review the message, then copy or share it.
- Check an action's owner against the exchange. Manage speakers in the top-right
  menu to correct a display name throughout the recording.
- Use People to choose a recipient and a topic. Notes & recording opens the
  summary, decisions, next steps, and full transcript. Audio plays at its source.
- Open the recordings sidebar to switch to Studio review, a second dataset with
  different people, topics, dates, and a shorter arrival sequence. It has no audio.

IMPORT ANOTHER RECORDING
Sidebar > Import recording > Choose folder. The included Example Recording
folder is ready to import; put it somewhere accessible through the Files picker.
Required: transcript.json and notes.json.
Optional: calendar.json, stream.json, and the audio file named in transcript.json.
Recording Format.md is the original kit's schema reference.

WHAT IS REAL / SIMULATED
The app parses the supplied files directly, supports another valid recording in
the same format, and saves review edits separately from the original files.
Date/topic/review suggestions use local English-language rules, not a live AI
service. They are clues for human review, not verified facts.
The lock screen is an in-app simulation; it is not an ActivityKit extension.
Hardware transfer, uploads, and processing are simulated by the supplied stream.
Raw audio is not transcribed. Copy/share sends only the selected reply text, not
the full transcript or audio. The app does not send messages automatically.

PROJECT CONTENTS
Pocket.xcodeproj       Project and shared run scheme
Pocket/                Swift sources, assets, original kit, bundled second fixture
Example Recording/     Small, importable second fixture
Recording Format.md    Supplied data schema

OPTIONAL CHECKS
In Edit Scheme > Run > Arguments, add -self-test for the built-in Debug checks.
The report is written to the app's Documents/prototype-checks.json. Remove that
argument before the walkthrough. No debug launch arguments are enabled by default.

INTERACTION REFERENCES
Exploration used the supplied TelegramHeader, BorderBeam, and XStyleSideBar
samples, plus patterns from my Frenzei app. The original case-study recording
and model files are included for evaluation; the brief itself is not included.
