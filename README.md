# web-mic-linux
My fork of the [web-mic](https://github.com/russelltg/web-mic), which has various improvements.
Ever wished you could use your phone mic from your linux computer (exposed as a PulseAudio source)?
This provides a simple solution to this problem, all wrapped in a single staticly-linked binary written in rust without unsafe code.

# Installation
```bash
cargo install --git https://github.com/kotleni/web-mic-linux
```

# Usage
Run `web-mic` (or `~/.cargo/bin/web-mic-linux`), and connect to it on your phone with `https://<your ip>:8000`. Note the `s`--it must be https. 
You will see a security warning, choose "advanced" then "proceed to xxx".

# Limitations
1. TLS requirement
The Web Audio APIs [_only work in secure contexts_](https://developer.mozilla.org/en-US/docs/Web/API/AudioWorkletNode), so it runs using self-signed certificates. 
However, these certificates are cached (in `~/.cache/web_mic`), so you should only have to bypass the security warning once.
2. Focus
At least on android chrome, it seems to throttle the capture worker when the phone is locked or similar, so you need to disable the screen timeout.
I personally have the setting in developer settings turned on to not timeout the screen when its plugged in.
3. Latency
This app should obviously not be used when low latency is required. In my limited test, I got around 100ms of latency, which is fine for VoIP.