# awesome-selfhosted-nixos

Example configurations for self-hosting stuff on [NixOS](https://nixos.asia/en/nixos-tutorial).

## Media

For managing videos, music and photos.

### [Jellyfin](https://jellyfin.org/)

Jellyfin provides a self-hosted alternative to the likes of Netflix and Spotify.

```nix
services.jellyfin = {
  enable = true;
  openFirewall = true;
};
```

**Tip**: Create a dedicated folder (e.g.: `/Data`) owned by the Unix group `jellyfin` organizing your content inside it.

### [navidrome](https://www.navidrome.org/)

navidrome is a Web UI (with compatible mobile apps) that streams your music files.

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
