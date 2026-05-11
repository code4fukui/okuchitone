# okuchitone

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A web-based synthesizer that turns your mouth movements into sound using your webcam and real-time face tracking.

[**Live Demo**](https://code4fukui.github.io/okuchitone/)

## How It Works

The application uses your webcam to detect facial landmarks via MediaPipe Face Mesh. It then maps specific lip movements to sound parameters:

-   **Volume:** The loudness of the sound is controlled by your mouth's opening. The greater the vertical distance between your upper and lower inner lips (landmarks 13 and 14), the louder the sound.
-   **Pitch:** The pitch of the sound is determined by the vertical position of your mouth on the screen. Moving your head up and down changes the note.

## Features

-   Real-time sound synthesis based on mouth shape and position.
-   Utilizes MediaPipe Face Mesh for high-fidelity facial landmark tracking.
-   Supports up to 5 faces simultaneously, each with its own independent sound channel.
-   Audio generated via the Web Audio API for dynamic control over pitch and volume.
-   Selectable sawtooth or custom periodic waveforms.

## Usage

1.  Visit the [demo page](https://code4fukui.github.io/okuchitone/).
2.  Allow the browser to access your camera.
3.  Click the **SOUND START** button to initialize the audio.
4.  Open and close your mouth, and move your head up and down to control the sound.

### Controls

-   **show original image**: Toggles the visibility of the raw camera feed.
-   **mirror mode**: Flips the video horizontally (enabled by default).
-   **backcamera mode**: Switches to the device's rear camera, if available.

## Technical Details

-   **Face Tracking:** The app uses [MediaPipe Face Mesh](https://developers.google.com/mediapipe/solutions/vision/face_landmarker) to detect 478 landmarks per face. The distance and position of lip landmarks are calculated on each frame to modulate the audio.
-   **Audio Synthesis:** The core audio engine, `XTone.js`, uses the [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) to create an `OscillatorNode` (for the tone) and a `GainNode` (for the volume). These are updated continuously to reflect the user's facial movements.

## Running Locally

1.  Clone this repository.
2.  Serve the project directory using a local web server (e.g., `python -m http.server` or the VS Code Live Server extension).
3.  Open the provided local URL in a modern web browser.

## References

-   This project was inspired by and builds upon concepts from [MediaPipe test](https://code4fukui.github.io/mediapipe-test/) and [smaphotone](https://code4fukui.github.io/smaphotone/).
-   Face Mesh Library Info: [Face Mesh - mediapipe](https://chuoling.github.io/mediapipe/solutions/face_mesh.html)

## License

This project is available under the MIT License.