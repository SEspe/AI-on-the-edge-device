[Overview](_OVERVIEW.md) 

## REST API endpoint: ota

`http://IP-ADDRESS/ota`


Perform an Over-The-Air (OTA) update


Payload:
- `task` Task
  - Available options:
    - `emptyfirmwaredir`
      - Delete all content in `/firmware`
      - No additional parameter necessary
    - `update`
      - Perform an OTA update / Upload any content to sd card
      - Mandatory parameter: `file` 
- `file` Filename with extension but without path
  - Supported file extensions:
    - `TFLITE`: TFLite model
    - `TFL`: TFLite model (legacy)
    - `ZIP`: ZIP file (e.g. OTA release package)
    - `BIN`: MCU firmware (e.g. firmware.bin)
  - Note: File needs to be existing and located in folder `/firmware`
- `delete` Filename with extension but without path
  - Deletes the given file from folder `/firmware`
  - Example: `/ota?delete=AI-on-the-edge-device__esp32cam__1234567.zip`
    
Example: `/ota?task=update&file=AI-on-the-edge-device__update__*.zip`


Response:
- Content type: `HTML`
- Content: Query response

| File type          | Response                                       | Reboot required
|:-------------------|:-----------------------------------------------|:----------------
| `TFLITE` / `TFL`   | `Neural network file updated. No reboot required` | No
| `ZIP` / `BIN`      | `reboot`                                       | **Yes, see below**


!!! Warning
    **`task=update` with a ZIP or BIN file only *stages* the update. It does not flash anything.**

    The endpoint writes the package path to `/sdcard/update.txt` and returns the literal string
    `reboot`. That string is an instruction for the WebUI to trigger a reboot - it is **not** a
    confirmation that an update was performed. The update is applied during the next boot, by
    `checkOTAUpdate()`, which reads `update.txt`, unpacks the package and writes the firmware.

    When driving this endpoint from a script or any client other than the WebUI, you **must**
    issue a reboot yourself, otherwise nothing is updated and the device keeps running the old
    firmware indefinitely.

    Complete sequence for a scripted OTA update:

    1. `POST /upload/firmware/<name>.zip` - upload the package (responds `303`)
    2. Optionally verify the staged file, e.g. by reading it back via
       `/fileserver/firmware/<name>.zip` and comparing a checksum
    3. `GET /ota?task=update&file=<name>.zip` - stages the update, returns `reboot`.
       Can be confirmed by reading `/fileserver/update.txt`
    4. `GET /reboot` - **this is the step that actually applies the update**

    The device is unreachable for roughly 60-80 seconds while the update is applied. Confirm
    success by reading `git_revision` from [/info](info.md); do not use a request to `/` as the
    check, because the web server answers again within about a second of a reboot request and
    will appear to indicate that nothing happened.

    A corrupt or truncated package is rejected by the device: the archive fails to unpack, or
    `esp_ota_end()` fails image validation before the boot partition is switched. In that case
    the device reboots and continues running the previous firmware, and the failure is written
    to the log at `ERROR` level.
