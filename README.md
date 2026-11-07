# NOTZYH Low-Lag Recorder — Windows 10

A lightweight screen recorder GUI using FFmpeg. The GitHub Actions workflow builds a standalone EXE and packages `ffmpeg.exe` beside it. Python is not required on the user's Windows PC.

## Build
1. Add `notzyh_recorder.py` to the existing `Notzyh-Optimizer` GitHub repository.
2. Create `.github/workflows/build-recorder.yml` and paste the workflow from this package.
3. Open GitHub Actions.
4. Select **Build NOTZYH Low-Lag Recorder** and click **Run workflow**.
5. Download the `NOTZYH_LowLag_Recorder_Windows10` artifact.

## Run
Extract the artifact ZIP. Keep both files in the same folder:
- `NOTZYH_LowLag_Recorder.exe`
- `ffmpeg.exe`

Double-click the EXE. Choose a save folder, resolution, frame rate, and encoder, then Start recording. Stop recording to finalize the MP4.

## Performance notes
- Start with 1280x720 at 30 FPS and Auto encoder for lower overhead.
- Auto prefers Intel Quick Sync, NVIDIA NVENC, then AMD AMF if FFmpeg exposes the encoder; otherwise it uses x264 ultrafast.
- A GT 710 generally does not provide modern NVENC support. Your Intel CPU may or may not support Quick Sync depending on its exact model and enabled graphics driver.
- No software can promise zero FPS impact or zero lag. Desktop capture, encoding, storage speed, game load, and drivers all affect performance.
- Microphone audio can be captured from DirectShow audio devices. System audio requires a Stereo Mix or equivalent loopback recording device exposed by your sound driver; it may not be available on your laptop. The app shows only detected loopback devices. Both can be mixed into the MP4 when available.
- It uses Windows' GDI desktop capture, which is broadly compatible but may not be the lowest-overhead capture path for every game.

## Audio setup
Select your microphone from the Microphone dropdown. To capture system audio, Windows must expose a Stereo Mix or equivalent loopback device. Check Windows Sound Control Panel > Recording > right-click > Show Disabled Devices; enable Stereo Mix if it exists. If none exists, this build cannot capture system audio. Select both inputs to mix game audio and microphone into one AAC audio track. Headphones are recommended to prevent feedback.

## Audio notes
- Select a microphone from the detected DirectShow audio devices.
- For system audio select Stereo Mix / loopback if your audio driver provides it. The app does not automatically install virtual audio devices.
- If both are selected, they are mixed into a single audio track.
- Audio device selection is reset when refreshed.
