# SimShift Downloads

Official firmware, apps, and setup tools for [SimShift](https://simshift.golf) rail systems.

## Get the software

Go to the [Releases](../../releases) page and download the latest:
- **New to AutoShift?** Follow the [step-by-step setup guide](docs/CUSTOMER_SETUP.md), which also covers troubleshooting if the dashboard shows the program as disconnected.
- **SimShiftAutoShift.exe** — Windows app that shifts the rail automatically by golfer handedness (GSPro). Right-click, **Run as administrator**.
- **Firmware** (`fw-v*`) — flashing instructions are attached to each release.

Verify your download with the SHA256 checksum listed in the release notes.

## WiFi setup
Your SimShift rail creates its own setup network the first time it powers on, or any time it can't reach your WiFi.

1. Power the rail. Wait about 30 seconds.
2. On your phone or laptop, join the WiFi network **SimShift-Setup-XXXX** (password: `simshift123`).
3. Open a browser and go to **http://192.168.4.1**
4. Enter your home WiFi name and password, then tap **Save**.
5. The rail restarts and joins your network. Your phone will reconnect to your normal WiFi.

Your phone may say the setup network has "no internet." That's expected, so stay connected.
Works on iPhone, Android, and computers.

## Windows SmartScreen warning

The app is not yet code-signed. If Windows warns you, click **More info → Run anyway**.

## Support

Open an [issue](../../issues) or email info@simshift.golf.
