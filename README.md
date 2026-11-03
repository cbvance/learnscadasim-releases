# LearnSCADASim

The LearnSCADA Modbus device simulator for your **test workbench**. It runs on your own machine, fully offline,
and twins several Modbus TCP devices at once: each simulated device runs on its own port. It uses the same engine
and dashboard as the online LearnSCADA PLC Simulator.

This repository holds the **downloads only**. Get them from [Releases](../../releases/latest).

## Downloads

| File | For |
|---|---|
| `learnscadasim-<version>.zip` | **Linux with Docker.** The image tarball, `compose.yaml`, `INSTALL.txt` and the traffic generator. |
| `learnscadasim-<version>-windows-x64.zip` | **Windows 10/11 (64-bit), no Docker.** A portable folder with its own Python. Nothing to install, no admin rights needed. |
| `*.sha256` | Checksums for each zip. |

One license file works with both versions.

## What it does

- **Device hub** in the browser at port 8080. A Default sim is already running on Modbus port 502.
- **Add devices** from PLCSIM workbooks or CSV/JSON register maps, several at once, each on any port you choose.
  You can start, stop, restart and view logs for each device, change its port, or load a new workbook into it.
  A device that crashes restarts on its own.
- **Ignition 8.1 UDT** for every device, generated from its register map, plus the simulator workbook.
- **Diagnostics:** live Modbus TCP traffic from every device, decoded with tag names, with the frame bytes
  colored by field.
- **Traffic generator** to keep a device busy while you watch it.
- **Offline licensing:** no activation and no phone-home, so it works air-gapped.

## Install

**Linux (Docker):**

```bash
unzip learnscadasim-0.1.2.zip -d learnscadasim && cd learnscadasim
sha256sum -c SHA256SUMS
docker load -i learnscadasim-0.1.2.tar
docker compose up -d
```

Then open `http://<this machine>:8080`. To upgrade, run the same commands with the new bundle. Your devices,
workbooks and license are kept in the Docker volume. `INSTALL.txt` in the bundle covers networking and options.

**Windows:** right-click the zip and choose **Extract All**, then double-click **Start LearnSCADASim.bat**. The hub
opens at http://localhost:8080/. To let other PCs, HMIs or SCADA connect, run
**Allow through Windows Firewall.bat** as administrator. `README-Windows.txt` in the zip has the details. Your data
is kept in `%LOCALAPPDATA%\LearnSCADASim`, so you can replace the folder with a newer version without losing it.

## Licensing: read-only until licensed

Without a license, everything works except Modbus writes. You can add devices, import maps, download UDTs and use
the dashboards, but writes are refused with exception 01 (illegal function). To turn writes on, install the
license file from LearnSCADA on the hub page. Get a license from [LearnSCADA](https://learnscada.com).

## Security

There's no sign-in by default, so keep the hub on your workbench network. Anyone who can reach port 8080 can add
and delete devices. Set `LSS_LOGIN=1` to add an admin password.

## License

LearnSCADASim is proprietary software, not open source. See [LICENSE](LICENSE).
A simulator models a device's documented interface only. It isn't a substitute for testing with the real device.
