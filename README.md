<p align="center">
  <a href="https://github.com/homebridge/verified/blob/master/verified-plugins.json"><img alt="Homebridge Verified" src="https://raw.githubusercontent.com/Brandawg93/homebridge-nest-cam/master/branding/Homebridge_x_Nest.svg?sanitize=true" width="500px"></a>
</p>

# homebridge-nest-cam

View your Nest cams in HomeKit using [Homebridge](https://github.com/nfarina/homebridge) with this plugin.

[![NPM](https://nodei.co/npm/homebridge-nest-cam.png?compact=true)](https://nodei.co/npm/homebridge-nest-cam/)

[![PayPal](https://img.shields.io/badge/paypal-donate-yellow)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=CEYYGVB7ZZ764&item_name=homebridge-nest-cam&currency_code=USD&source=url)
[![verified-by-homebridge](https://badgen.net/badge/homebridge/verified/purple)](https://github.com/homebridge/homebridge/wiki/Verified-Plugins)
![build](https://github.com/Brandawg93/homebridge-nest-cam/workflows/build/badge.svg)
[![Discord](https://camo.githubusercontent.com/7494d4da7060081501319a848bbba143cbf6101a/68747470733a2f2f696d672e736869656c64732e696f2f646973636f72642f3433323636333333303238313232363237303f636f6c6f723d373238454435266c6f676f3d646973636f7264266c6162656c3d646973636f7264)](https://discord.gg/pc2pqmh)
[![Downloads](https://img.shields.io/npm/dt/homebridge-nest-cam)](https://nodei.co/npm/homebridge-nest-cam/)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/df36db66217e4b96bd5994b42a6e27f2)](https://www.codacy.com/manual/Brandawg93/homebridge-nest-cam?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Brandawg93/homebridge-nest-cam&amp;utm_campaign=Badge_Grade)

| [FAQ](https://github.com/Brandawg93/homebridge-nest-cam/wiki/FAQ)    | [Troubleshooting](https://github.com/Brandawg93/homebridge-nest-cam/wiki/Troubleshooting) |
|--------|-----------------|

## Notes
- This plugin *does not* use the old access token authentication method as Google is urging users to [switch to Google accounts](https://www.macrumors.com/2020/05/05/nest-two-factor-authentication-from-may/).

## Installation
1. Install this plugin using: `npm install -g homebridge-nest-cam`
2. Add google authentication to `config.json`
3. Run [Homebridge](https://github.com/nfarina/homebridge)

### FFMPEG
In order to use the below ffmpeg options, you must specify your custom ffmpeg path in the `pathToFfmpeg` config option.

#### Raspberry Pi
You may want to use OMX for transcoding as the CPU on the board can be slow. If so, make sure the ffmpeg installed on your Pi has `h264_omx` support and set the `ffmpegCodec` option below to `h264_omx`. You can always compile ffmpeg from source using [these instructions](https://github.com/legotheboss/YouTube-files/wiki/(RPi)-Compile-FFmpeg-with-the-OpenMAX-H.264-GPU-acceleration).

#### Mac OS
You may want to use VideoToolbox hardware acceleration for transcoding. If so, make sure the ffmpeg installed on your Mac has `videotoolbox` support and set `ffmpegCodec` option below to `h264_videotoolbox`.

### Setting up the Config.json
#### googleAuth
Google Accounts are configured using the `"googleAuth"` object in `config.json`, which contains three fields, `"issueToken"`, `"cookies"` and `"apiKey"`, and looks like this:

```
{
    "platform": "Nest-cam",
    "ffmpegCodec": "libx264",
    "options": {
      "motionDetection": true,
      "streamingSwitch": true,
      "disableAudio": false
    },
    "googleAuth": {
        "issueToken": "https://accounts.google.com/o/oauth2/iframerpc?action=issueToken...",
        "cookies": "SMSV=ADHTe...",
        "apiKey": "AIzaS..."
    }
}
```
1. If the plugin is installed globally, run `homebridge-nest-cam login`, otherwise, run `npx -p homebridge-nest-cam homebridge-nest-cam login` within the plugin folder. If your account has 2 factor authentication, use the `-h` flag.
2. Login to your Nest account.
3. Copy the output to your `config.json`.
4. (Optional) Run `homebridge-nest-cam clean` to remove extra packages used to login.

**Note:** If the steps above do not work, refer to the [manual authentication method](https://github.com/Brandawg93/homebridge-nest-cam/wiki/Manual-Authentication).

#### options
Extra options can be enabled/disabled depending on which switches and sensors you would like to see in the Home app. Here is the current list of available options:

| Name              | Description                                                         | Type             |
|-------------------|---------------------------------------------------------------------|------------------|
| alertCheckRate    | How often to check for alerts                                       | number (seconds) |
| alertCooldownRate | How long between consecutive alert notifications                    | number (seconds) |
| motionDetection   | enable/disable the motion sensor                                    | boolean          |
| doorbellAlerts    | enable/disable doorbell ring notifications                          | boolean          |
| doorbellSwitch    | enable/disable doorbell automation switch                           | boolean          |
| streamingSwitch   | enable/disable the ability to turn the camera on or off             | boolean          |
| disableAudio      | enable/disable the audio stream                                     | boolean          |
| pathToFfmpeg      | specify the path to a custom ffmpeg binary                          | string           |
| structures        | specify the structure names of which structures' cameras to see     | array            |

## Join the Discord
Unfortunately, there is no way for me to test every subscription, camera type, and feature. If you would like to help me test new features and enhancements, or if you have general questions or need support, join the official [Homebridge Discord Server](https://discord.gg/pc2pqmh).

## Credits
This plugin was originally developed by [KhaosT](https://github.com/KhaosT).

This plugin was converted to typescript using both [homebridge-ring](https://github.com/dgreif/ring) and [homebridge-examples](https://github.com/homebridge/homebridge-examples).

## Donate to Support homebridge-nest-cam
This plugin was made with you in mind. If you would like to show your appreciation for its continued development, please consider making [a small donation](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=CEYYGVB7ZZ764&item_name=homebridge-nest-cam&currency_code=USD&source=url).

## Disclaimer
This plugin and its contributers are not affiliated with Google LLC or Nest Labs in any way.