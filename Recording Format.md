# The minute after: kit

Everything here is fictional. Northwind, its people and this meeting are made up, and the recording uses synthetic voices.

Like real model output, the transcript and notes contain mistakes.

**Times.** All times are in seconds. In `transcript.json` and `notes.json` they count from the start of the recording. In `stream.json`, `t` counts from the moment Maya pressed stop.

## Files

| File | What it is |
| --- | --- |
| `meeting.m4a` | The recording: 28 minutes, mono AAC. Maya started it at 4:00:12 PM and stopped it at 4:28:18 PM Pacific on Thursday, October 8, 2026. |
| `transcript.json` | What the speech recognizer heard. |
| `notes.json` | What the notes model wrote from the transcript. |
| `stream.json` | When each piece arrives on Maya's phone after she presses stop. |
| `calendar.json` | The meeting's event and attendees, from Maya's calendar. |

## transcript.json

- `recording`: `id`, `audioFile`, `startedAt` and `endedAt` (ISO 8601 with time zone), `durationSec`, `language`, `source`.
- `speakers`: who the recognizer told apart, as `S1` to `S4`. It doesn't know names. Suggested names are in `notes.json`.
- `segments`: one per turn, sorted by `start`.
  - `id` (`seg_001`…), `speaker`, `start`, `end`, `text`.
  - `confidence`: 0 to 1, the average of the word confidences.
  - `overlap`: `true` when someone else is talking at the same time.
  - `words`: `text` (with punctuation), `start`, `end`, `confidence` (0 to 1).
    - `alternatives` (only on some words): other things the recognizer thinks the word might be, with their confidence.
    - `[inaudible]`: a stretch the recognizer couldn't make out. Its `start` and `end` cover the gap, and its confidence is 0.

## notes.json

- `recordingId`, `generatedAt`, `title`.
- `summary`, `decisions` and `actionItems` are lists of items. Every item has:
  - `id` and `text`.
  - `confidence`: the model's own estimate, 0 to 1. Models are not always well calibrated.
  - `sensitivity`: the model's guess at whether the item is private: `none`, `personal` or `confidential`.
  - `sources`: the moments it came from, each with `segmentId`, `start`, `end` and `quote` (that segment's transcript text).
  - Action items also have `owner` (`speaker` and `name`) and `due` (an ISO date, or `null`).
- `speakers`: the model's guess at who each speaker is: `speaker`, `suggestedName`, `attendeeEmail` (when it matched someone on the calendar, otherwise `null`), `confidence`, and `evidence` (segments where that person is addressed by name).
- `chapters`: `id`, `title`, `start`, `end`.

## stream.json

- `startsAt`: when Maya pressed stop.
- `events`: in order. Each has `t` (seconds after stop), `type`, and the fields below.

| Type | Meaning and fields |
| --- | --- |
| `recording.stopped` | Maya pressed stop. `durationSec`. |
| `transfer.started`, `transfer.progress`, `transfer.completed` | Pocket sends the recording to the phone. `bytes`, `percent`. |
| `upload.started`, `upload.progress`, `upload.completed` | The phone uploads it. `percent`. |
| `transcription.started` | The recognizer starts. |
| `transcript.segments` | A batch of segments is ready. `segmentIds`, and `coversUntil` (seconds of audio transcribed so far). |
| `transcription.completed` | The full transcript is ready. `segmentCount`. |
| `speakers.suggested` | Suggested names are ready (see `notes.json` → `speakers`). |
| `notes.started` | The notes model starts reading the transcript. |
| `notes.title` | `text`. |
| `notes.item.started`, `notes.item.delta`, `notes.item.completed` | An item streams in. `section` (`summary`, `decisions` or `actionItems`), `id`, and `text` fragments on each delta. Joining the deltas gives the item's full text. Its other fields are in `notes.json` under the same `id`, available once the item is completed. |
| `notes.chapters` | Chapters are ready. `chapterIds`. |
| `notes.completed` | The notes are done. |
| `processing.completed` | Everything is done, about 90 seconds after stop. |

## calendar.json

- `event`: `id`, `title`, `start`, `end`, `timeZone`, `location`, `organizer`, `description`, and `attendees`, each with `name`, `email`, `title`, `response`, and `organizer` or `optional` where they apply.

If something you need isn't here, ask. Telling us what you'd want from the data is useful too.
