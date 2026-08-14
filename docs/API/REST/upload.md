[Overview](_OVERVIEW.md) 

## REST API endpoint: upload

`http://IP-ADDRESS/upload/PATH/FILENAME`


This endpoint uploades files to the SD card via an HTTP POST request.

The target location is taken from the URL: everything after `/upload` is the absolute path on the
SD card, including the filename. The file content is sent as the raw request body.

- Example: `POST /upload/firmware/AI-on-the-edge-device__esp32cam__1234567.zip`
  uploads to `/sdcard/firmware/AI-on-the-edge-device__esp32cam__1234567.zip`
- Example: `POST /upload/config/config.json` uploads to `/sdcard/config/config.json`


Constraints:
- Maximum file size: **8 MB**
- The path must not end with a trailing slash - a filename is mandatory
- The path must not contain spaces
- Maximum path length: 100 characters
- **The target file must not already exist.** There is no overwrite. Delete the existing file
  first, e.g. via [/delete](delete.md), or for the firmware folder via
  [`/ota?delete=FILENAME`](ota.md)


Response:
- Content type: `HTML`
- Success: status `303 See Other`, redirecting to the parent folder, and responds with an HTML
  table of that folder (only first 100 items)

Error responses:

| Status | Message                                      | Cause
|:-------|:---------------------------------------------|:-------------------------------------------
| `400`  | `Invalid path: Path malformed or too long`   | Path could not be resolved, or exceeds the length limit
| `400`  | `Invalid path: Trailing slash`               | No filename given
| `400`  | `File size must be less than 8MB`            | `Content-Length` exceeds the limit
| `400`  | `File already exists`                        | Target exists; delete it first
| `500`  | `Failed to create file: ...`                 | SD card write error


!!! Note
    An upload that is aborted part way through leaves a partial or zero byte file behind. Because
    the endpoint refuses to overwrite an existing file, that leftover must be deleted before the
    upload can be retried, otherwise the retry fails with `400 File already exists`.

!!! Note
    The web server processes requests in a single task. A large upload occupies it for the whole
    transfer, so other HTTP requests - including the WebUI - are queued until it completes. If the
    client disappears mid-upload, the handler stays blocked until its receive timeout expires,
    during which the device answers ICMP and MQTT normally but appears unresponsive over HTTP.
