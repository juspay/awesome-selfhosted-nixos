# awesome-selfhosted-nixos

This repository catalogs various services that can be self-hosted on [NixOS](https://nixos.asia/en/nixos-tutorial), providing users with an effective initial configuration to start with. The objective is to promote the simplest methods for replacing various proprietary services using a machine running NixOS.

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

navidrome is a Web UI (with compatible mobile apps) that streams your music files, providing a self-hosted alternative to Spotify.

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

## File management

### [Syncthing](https://syncthing.net/)

Like Dropbox, but OSS and better. We use home-manager because this way it works on both Linux & macOS.

Once activated, go to http://localhost:8384 to access the Syncthing GUI.

```nix
# Add this to your home-manager config
{
  services.syncthing = {
    enable = true;

    # Optional: Configure settings
    settings = {
      gui = {
        theme = "dark";
        insecureAdminAccess = false;
      };
      options = {
        urAccepted = -1; # Disable usage reporting
        crashReportingEnabled = false;
        announceEnabled = true;
        localAnnounceEnabled = true;
        relaysEnabled = true;
      };
    };
  };
}
```
