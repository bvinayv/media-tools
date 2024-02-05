## Mediamtx Usage

### Start Mediamtx docker with `mediamtx.yml` config file

```
LOCAL_CONFIG_PATH=/mediamtx.yml

docker run --rm \
            -it \
            --network=host \
            -v /etc/ssl/certs/ca-certificates.crt:/etc/ssl/certs/ca-certificates.crt \
            -v $LOCAL_CONFIG_PATH:/mediamtx.yml \
            -e MTX_PROTOCOLS=tcp \
            -e MTX_WEBRTCADDITIONALHOSTS=127.0.0.1 \
            -p 8554:8554 \
            -p 1935:1935 \
            -p 8888:8888 \
            -p 8889:8889 \
            -p 8890:8890/udp \
            -p 8189:8189/udp \
            --name temp bluenviron/mediamtx
```


### Current Config is set to input HLS and output SRT

Added example hls stream is provided at the end of yaml file under `paths` in the
[config file](mediamtx.yml).

### Capture SRT Out

`ffmpeg` with in-built SRT library can be used to capture the stream.

```
ffmpeg -i "srt://127.0.0.1:8890?streamid=read:input_1" -c copy -f mpegts test.ts
```