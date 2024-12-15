# Random Linux Commands

## Disk & Files

Check disk usage by directory: `du -sh */ | sort -h`

Empty a file without deleting it: `truncate -s 0 <file>`

Find files modified in last 24h: `find . -mtime -1 -type f`

Find large files (>100MB): `find . -size +100M -type f`

Mount NFS: `sudo mount -t nfs4 -o proto=tcp,port=2049 $ADDRESS:/ /mnt/path`

Transfer files with bandwidth limit: `rsync --progress -av --bwlimit=60000k --remove-source-files`

Watch directory size in real-time: `watch -n 5 'du -sh /path/to/dir'`

## Awk

Print single column: `awk '{print $N}'`

## Cut

Remove first X characters: `cut -c X-`

Remove last X characters: `rev | cut -c X- | rev`

## Grep

Search for either of two strings: `grep -E "string1|string2" <file>`

## Hardware

Hot-remove PCIe device: `echo 1 | sudo tee /sys/bus/pci/devices/0000:XX:00.0/remove`

Rescan PCIe bus: `echo 1 | sudo tee /sys/bus/pci/rescan`

## Network

List open ports: `ss -tulpn`

Test port connectivity: `nc -zv hostname port`

## KDE Plasma

Restart KDE desktop: `kwin_x11 --replace & plasmashell --replace &`

## System

List running services: `systemctl list-units --type=service --state=running`

View today's logs for unit: `journalctl -S today -u <unit.name>`

View logs since today: `journalctl -S today`


## Video / FFmpeg

Convert to H.265/HEVC: `ffmpeg -i input.mp4 -c:v libx265 -crf 28 -preset medium -c:a copy output.mp4`

Cut video at specific times: `ffmpeg -i input.mp4 -ss 00:00:00 -to 00:00:00 -c copy out.mp4`

Extract audio from video: `ffmpeg -i input.mp4 -vn -acodec copy output.aac`

Extract frames as images: `ffmpeg -i input.mp4 -vf fps=1 frame_%04d.png`

Get video info: `ffprobe -v quiet -print_format json -show_format -show_streams input.mp4`

Re-encode with GPU (NVIDIA): `ffmpeg -i input.mp4 -c:v hevc_nvenc -preset slow -crf 23 output.mp4`

Re-encode with VAAPI (Intel/AMD): `ffmpeg -vaapi_device /dev/dri/renderD128 -i input.mp4 -vf 'format=nv12,hwupload' -c:v hevc_vaapi -c:a copy output.mp4`
