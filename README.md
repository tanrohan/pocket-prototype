# The minute after
An iPhone prototype by Rohan Tandon.

Maya has a minute between meetings to understand what was decided, check important details, and answer Rachel. This prototype explores that moment using the supplied recording, transcript, model-generated notes, calendar, and arrival timeline.

## Run the prototype

1. Download **Pocket-Prototype-Rohan-Tandon.zip** from the file list above.
2. Unzip it and open **Pocket.xcodeproj**.
3. In **Xcode 27.1 or newer**, select the **Pocket** scheme and an iPhone simulator, then press **Run**.

No API keys, backend, or third-party packages are required. Use an iOS 26 or newer simulator for the Liquid Glass appearance.

## Explore

- Open the Pocket notification to watch notes arrive.
- Review the launch date against the conversation and prepare a reply to Rachel.
- Check task owners and correct speaker names throughout the recording.
- Choose a person and topic to prepare a message, then review its contents before copying or sharing.
- Use the top-right menu to **Replay arrival** or **Skip to end**.
- Open the sidebar to try **Studio review**, or import the included **Example Recording** folder.

## Prototype scope

The app reads recording files directly and supports other recordings in the same JSON format. The Lock Screen and processing pipeline are simulated. Review suggestions use local rules; they are prompts for human checking, not verified conclusions.

The prototype does not transcribe raw audio or send messages automatically.
