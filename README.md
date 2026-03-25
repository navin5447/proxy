# Browser-based Media Proctoring Module

Real-time client-side proctoring module for interview sessions using webcam + microphone.

## Features

- Video monitoring with MediaPipe Face Mesh
- Audio monitoring with Web Audio API
- Structured suspicious-event emission
- React hook API: `useMediaProctoring(candidateId, sessionId)`
- Visual debug overlay (landmarks + status + audio meter)
- No video/audio storage

## Quick Start

```bash
npm install
npm run dev
```

Open `http://localhost:3000`.

## Event Format

```ts
{
  candidateId: string;
  sessionId: string;
  event_type:
    | "no_face_detected"
    | "multiple_faces_detected"
    | "looking_away"
    | "face_distance_abnormal"
    | "background_speech_detected"
    | "high_noise_detected";
  duration_ms?: number;
  timestamp: number;
}
```

## Integration

The module dispatches browser custom events named `media-proctoring-event`.
Host app can subscribe and forward events to backend APIs.

```ts
window.addEventListener("media-proctoring-event", (evt) => {
  const customEvent = evt as CustomEvent;
  console.log(customEvent.detail);
});
```
