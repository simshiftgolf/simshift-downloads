# SimShift Auto-Shift — Setup (GSPro, Infinite Tees, ShotForge)

Moves your SimShift rail automatically when your golf sim software switches between a right- and left-handed player.
Works with GSPro, and with Infinite Tees and ShotForge through the Rela connector.

## Before you start
- SimShift rail powered on, connected to your home WiFi, and showing in your SimShift dashboard.
- Your sim PC and the rail on the **same home network**.
- The **Auto-shift (GSPro)** switch in your SimShift dashboard turned **ON**. (This one switch controls Auto-shift for all supported sim software.)
- Using Infinite Tees or ShotForge? Rela must be running on the same PC as the sim software.

## WiFi setup
Your SimShift rail creates its own setup network the first time it powers on, or any time it can't reach your WiFi.

1. Power the rail. Wait about 30 seconds.
2. On your phone or laptop, join the WiFi network **SimShift-Setup-XXXX** (password: `simshift123`).
3. Open a browser and go to **http://192.168.4.1**
4. Enter your home WiFi name and password, then tap **Save**.
5. The rail restarts and joins your network. Your phone will reconnect to your normal WiFi.

Your phone may say the setup network has "no internet." That's expected, so stay connected.
Works on iPhone, Android, and computers.

**After a power outage or router restart:** if the rail's setup network appears, wait about 10 minutes. The rail automatically reconnects to your WiFi once your router is back. Unplugging the rail and plugging it back in also makes it retry right away.

## Install (about 2 minutes)
1. Create a folder such as `C:\SimShift` and copy `SimShiftAutoShift.exe` and `install_autostart.bat` into it.
2. Double-click **`install_autostart.bat`** and click **Yes** when Windows asks for permission.
   Auto-shift starts now and will start whenever you log in to Windows.

> **Windows or your antivirus may show a warning** the first time. The program is code-signed by SIMSHIFT LLC, but Windows SmartScreen can still warn about new software until enough people have downloaded it. In Windows SmartScreen click **More info → Run anyway**. If your antivirus blocks or removes the file, add an exception for the `C:\SimShift` folder and run `install_autostart.bat` again.

## Use it
- Start your sim software as normal (GSPro, or Infinite Tees / ShotForge with Rela running) and pick a player. When the player's handedness changes, the rail moves.
- If the sim opens on a different side than the rail, switch player once and the rail will catch up.
- To stop the rail moving automatically, turn the **Auto-shift (GSPro)** switch **OFF** in the dashboard. The Full Left / Full Right buttons still work.

## Dashboard status
- **Auto-shift program connected:** green while the program on your PC is running and can reach the rail.
- **Rail last seen:** the last time the rail checked in. If this time stops updating, the rail has lost power or WiFi.

## Stop or restart Auto-Shift
Open **PowerShell as administrator** (search PowerShell in the Start menu, right-click it, choose *Run as administrator*).

- **Stop it completely:**
  `taskkill /IM SimShiftAutoShift.exe /F /T`
- **Start it again:**
  `schtasks /Run /TN "SimShift AutoShift"`
- **Check whether it's running:**
  `tasklist | findstr /i SimShift`
  (no output means it is not running)

The dashboard's **Auto-shift program connected** light turns red about 10 seconds after it stops, and green a few seconds after it starts.

If you only want the rail to stop moving automatically, you don't need to stop the program: turn the **Auto-shift (GSPro)** switch **OFF** in the dashboard.

## If "Auto-shift program connected" is red
Red means the program isn't running, or it can't reach the rail.

1. **Check whether it's running.** In PowerShell run `tasklist | findstr /i SimShift`. No output means it is not running.
2. **Start it.** Run `schtasks /Run /TN "SimShift AutoShift"`. If Windows says the task doesn't exist, double-click `install_autostart.bat` again and click **Yes**.
3. **Don't start the program by double-clicking `SimShiftAutoShift.exe`.** It has to run as administrator, and if it doesn't, it closes by itself right away. `install_autostart.bat` sets this up for you.
4. **Still red after a minute?** Open `%LOCALAPPDATA%\SimShift\autoshift.log`.
   - `Not running as Administrator` or `Windows refused raw capture`: run `install_autostart.bat` again.
   - No log file at all: your antivirus may have removed the program. Add an exception for `C:\SimShift`, then run `install_autostart.bat` again.
5. **Check your network.** Your PC and the rail must be on the same home network, not a guest WiFi or a VPN.
6. **Using more than one SimShift rail on the same network?** Give each PC its own `simshift_config.json` with that rail's IP address (see below).

## If the rail doesn't move
- Check the rail shows **Online** and **Ready** in the dashboard.
- Open `%LOCALAPPDATA%\SimShift\autoshift.log` and send it to support. The log lists the connections the program watches, and shows a line like `LH reported by ...` each time a player's handedness changes. If you never see that line when you switch players, the sim isn't sending its handedness to the program.
- Using Infinite Tees or ShotForge? Make sure Rela is running and connected to the sim.
- If your PC can't find the rail by name, create a file named `simshift_config.json` next to the program containing:
  `{ "mode": "lan", "host": "THE_RAIL_IP_ADDRESS" }`
- If your sim or Rela uses a different port, support can give you a line to add to the same file, for example:
  `"extra_sources": [{ "name": "My Sim", "port": 1234 }]`
