# Media stack

## Purpose and placement

The media stack runs on `NuQeGG`, the reused gaming PC with the documented GTX 1060 6 GB. It combines streaming, requests, library management, downloads, subtitles, and file processing in separate LXC guests.

| Service | Guest | Role |
| --- | ---: | --- |
| Jellyfin | 100 | Playback and streaming |
| Radarr | 102 | Movie management |
| Sonarr | 103 | Series management |
| Prowlarr | 104 | Indexer integration |
| Seerr | 105 | Request interface |
| Gluetun and qBittorrent | 106 | VPN component and download client in the same LXC guest |
| Bazarr | 109 | Subtitle management |
| FileFlows | 112 | File processing and encoding |
| Doplarr | 116 | Discord request integration |
| Maintainerr | 118 | Library maintenance |
| FlareSolverr | 120 | Indexer companion service |

qBittorrent runs inside the Gluetun guest, CT 106. Sharing that guest establishes placement; the precise network attachment and VPN routing should be recorded from its configuration. Seerr is the current guest name, replacing the earlier repository's Overseerr reference.

## How the services fit together

Requests, discovery, downloading, importing, processing, and playback are different stages. The library management applications organise movies and series; Bazarr handles subtitle needs; Jellyfin presents the resulting library to clients. FileFlows adds a processing step for the media files.

This explains the responsibilities, rather than prescribing a verified sequence for every file. The exact downloader mappings, FileFlows triggers, and rescan integrations need to be taken from the active configuration.

## Shared paths and permissions

Earlier troubleshooting identified a missing media mount in Bazarr. Restoring access to the same media paths used by Radarr and Sonarr allowed the subtitle scans to work properly.

The practical lesson is to check both path mapping and service-user permissions. An application can have a healthy web interface while still being unable to read or write the library it manages.

The documented host library uses `/mnt/media`, with movie and series directories beneath it. Docker path mappings inside a guest can introduce another layer, so host, LXC, and Docker paths must be distinguished during troubleshooting.

## GPU and encoding

FileFlows setup included NVIDIA device access in the LXC and NVIDIA Container Toolkit integration for Docker. GPU discovery succeeded during setup, and the media processing workflow subsequently progressed beyond the initial plugin-loading issue.

The latest saved FileFlows change increased its simple encoder **Quality setting from 3 to 4** for future files after blockiness was noticed in dark scenes. This application setting should not be treated as an FFmpeg CRF value. Larger output files are a possible trade-off, and an already compressed file cannot recover discarded detail by being encoded again.

Recent Jellyfin testing showed successful transcoding and GPU access. The exact encoder should be checked in the FFmpeg log when validating a particular playback session. Flashing and a bottom bar on the TV remain playback issues to investigate; the low bitrate used in one diagnostic test is not a normal quality target.

## Subtitles

The documented preference is Danish subtitles, with English as a fallback. Bazarr was configured to recognise embedded subtitles and rescan existing media. Provider download limits were one observed reason that subtitle downloads could stop temporarily.

Two selectable subtitle tracks and two subtitles drawn simultaneously are different problems. A useful report includes the affected file, selected language/track, client, and whether the issue is timing, appearance, or duplicate display.

## Checks after a change

- Confirm the relevant application can access the library with its actual service account.
- Test one representative file before broad processing changes.
- Inspect audio and subtitle streams as well as video output.
- Compare a difficult scene with the source when investigating compression artefacts.
- Verify playback on the target device; browser success does not establish TV compatibility.

[FileFlows video encoding documentation](https://fileflows.com/docs/plugins/video-nodes/ffmpeg-builder/video-encode) · [Jellyfin hardware acceleration](https://jellyfin.org/docs/general/post-install/transcoding/hardware-acceleration/) · [Back to overview](../../README.md)
