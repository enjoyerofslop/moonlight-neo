# Moonlight neo

[![CI](https://github.com/enjoyerofslop/moonlight-neo/actions/workflows/ci.yml/badge.svg)](https://github.com/enjoyerofslop/moonlight-neo/actions/workflows/ci.yml)

Moonlight neo is an unofficial fork of [Moonlight for iOS/tvOS](https://github.com/moonlight-stream/moonlight-ios), the open source client for [Sunshine](https://github.com/LizardByte/Sunshine) and NVIDIA GameStream made by the [Moonlight project](https://moonlight-stream.org). It adds full support for iPhone Duo.

**This fork is not affiliated with or endorsed by the Moonlight project.** For the official app, get [Moonlight from the App Store](https://apps.apple.com/us/app/moonlight-game-streaming/id1000551566) and use the [Moonlight wiki](https://github.com/moonlight-stream/moonlight-docs/wiki) for setup help and troubleshooting. Please report problems with this fork in [this repository's issues](https://github.com/enjoyerofslop/moonlight-neo/issues), not to the Moonlight project.

Moonlight also has a [PC client](https://github.com/moonlight-stream/moonlight-qt) and an [Android client](https://github.com/moonlight-stream/moonlight-android).

## What's different

Moonlight neo is built with the iOS 27.1 SDK, so it fills both displays of iPhone Duo instead of running in a compatibility window.

- **Launches on iOS 27.** Apps built with the iOS 27 SDK must use the scene lifecycle. This change, and resizing the video when the window changes size, come from [moonlight-stream/moonlight-ios#729](https://github.com/moonlight-stream/moonlight-ios/pull/729) by antoinealbaut23.
- **Fills the inner display in any orientation.** Held upright, the inner display would otherwise shrink the landscape-only app to a band across the fold. The outer display, other iPhones and iPad stay landscape-only.
- **Tabletop streaming.** Folded like a laptop, the video sits above the fold and the on-screen controls below it. Held upright and flat, the video is at the top with the controls underneath.
- **Follows the device as it opens, closes and folds.** The video, on-screen controls, touch input and host list all lay out again, during a stream too.
- **On-screen controls stay clear of the fold and the camera.** On the inner display they use the larger iPad layout.
- **Stream resolutions stay landscape.** The Safe Area and Full resolution options no longer turn into portrait resolutions on the inner display.
- **Rebranded** with its own bundle ID (`com.enjoyerofslop.MoonlightNeo`) and name, so it installs alongside the official app.

## Building

* Install Xcode 27.1 or later, which includes the iOS 27.1 SDK and the iPhone Duo simulator.
* Run `git clone --recursive https://github.com/enjoyerofslop/moonlight-neo.git`
  * If you've already cloned the repo without `--recursive`, run `git submodule update --init --recursive`
* Open `Moonlight.xcodeproj` in Xcode and choose the `Moonlight` scheme (or `Moonlight TV` for tvOS).
* To build for the simulator from the command line:
  ```
  xcodebuild -project Moonlight.xcodeproj -scheme Moonlight \
    -destination 'platform=iOS Simulator,name=iPhone Duo' build CODE_SIGNING_ALLOWED=NO
  ```
* To run on a real device, change the signing options, because the project is set up for this fork's signing team:
    * Click on "Moonlight" at the top of the left sidebar
    * Click on the "Signing & Capabilities" tab
    * Under "Targets", select "Moonlight" (for iOS/iPadOS) or "Moonlight TV" (for tvOS)
    * In the "Team" dropdown, select your name. If your name doesn't appear, you may need to sign into Xcode with your Apple account.
    * Change the "Bundle Identifier" to something different. You can add your name or some random letters to make it unique.
    * Now you can select your Apple device in the top bar as a target and click the Play button to run.

In Xcode 27.1, Device Hub can open, close, fold and rotate the simulated iPhone Duo.

## License

Moonlight neo is licensed under the GNU General Public License v3, with the Moonlight project's App Store distribution exception. See [LICENSE.txt](LICENSE.txt). The original copyright notices of Moonlight and its contributors are kept in the source files.
