# TouchPilot v1.6 — Android prototype source

This project provides:
- Installed-app target selection.
- Overlay control panel.
- User-authorized MediaProjection screenshot capture.
- Screenshot point editor (tap to add, drag to reposition).
- Saved normalized point coordinates.
- Draggable numbered overlay points.
- One master mode: normal or long press, applied to all points.
- Repeating multi-stroke Accessibility gesture dispatch in one GestureDescription.
- Target-package foreground gating based on Accessibility window events.

## Build
Push the contents of this folder to a GitHub repository on branch `main`, then open Actions and run **TouchPilot Android APK**. Download the `touchpilot-debug-apk` artifact.

## Setup on device
1. Install the debug APK.
2. Select the target app in TouchPilot.
3. Grant overlay permission.
4. Enable TouchPilot in Android Accessibility settings.
5. Grant screen-capture permission.
6. Open the target app, use the floating panel to capture a screenshot, tap/drag points in the editor, and save.
7. Start the master control.

## Changes in v1.2
- Tap/hold strokes now use an explicit same-coordinate line, improving compatibility with Android gesture dispatch.
- Foreground-target tracking ignores unrelated accessibility content events.
- Start is blocked when there are no points or the Accessibility service is not connected.
- A rejected gesture dispatch stops the run loop and restores point touchability.
- The master normal/long-press control updates its displayed label immediately.

## Important verification status
This source has not been compiled in this environment because Android SDK/Gradle are unavailable here. The GitHub workflow is provided to perform a real build.
The OS Accessibility API accepts multiple gesture strokes in a single GestureDescription with the same start time, but actual multi-touch delivery is not guaranteed across all devices or target apps. Validate on the intended device/app.
Some apps prohibit capture or automated input. Respect their rules. This prototype does not bypass app protections.

## Changes in v1.6
- Overlay windows now opt into display-cutout areas, so chips sit exactly where gestures are sent on notched screens.
- Screenshot, saved points and gesture coordinates all use the real display size.
- Hidden overlays (during capture/editor) are also untouchable, so they no longer swallow taps in the point editor.
- Opening the keyboard no longer pauses the run loop (IME windows are ignored in foreground tracking).
- Old screenshots are deleted on each new capture instead of piling up.
