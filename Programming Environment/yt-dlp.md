# yt-dlp

## yt-dlp

- installed using pip. In a `ytdlp` [conda](Programming%20Environment/conda.md) environment on macos: `python3 -m pip install -U "yt-dlp[default]"`
- download youtube videos
- Setting configurations: [1](https://www.reddit.com/r/youtubedl/comments/qoc17t/ytdlp_where_do_i_put_a_custom_configuration_file/), [2](https://www.reddit.com/r/youtubedl/comments/130i9og/ytdlp_how_to_automatically_convert_all_audio/)
- Configs saved at `~/.config/yt-dlp/config`
- [Github page](https://github.com/yt-dlp/yt-dlp)
## Audio only, flac

``` bash
yt-dlp -f 251 -x --audio-format flac --audio-quality 0 URL
```

## List available formats

```bash
yt-dlp --list-formats <URL>
```

## Download the webm file and do conversion yourself (faster)

```
yt-dlp --ignore-config --js-runtimes node -f 251 <URL>
ffmpeg -i <input.webm> <output.flac>
```