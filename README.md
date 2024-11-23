# awesome-selfhosted-nixos
Example configurations for self-hosting stuff on NixOS

## Music

### [navidrome](https://www.navidrome.org/)

```nix
services.navidrome = {
  enable = true;
  settings = {
    Address = "127.0.0.1";
    Port = 4533;
    MusicFolder = "/var/lib/navidrome/Music";
  };
  openFirewall = true;
};
```

**Tip**: Use `yt-dlp -x <url>` to download YouTube videos as audio, and place them under `MusicFolder` (owned by `navidrome` user) to start populating your music library ([credit](https://x.com/sridca/status/1860154543247655267)).
