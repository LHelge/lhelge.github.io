---
title: Run persistent Claude Code sessions on a headless server
slug: claude-code-tmux
author: LHelge
created: 2026-07-04
description: "Setting up an always-on Arch box so I can drive Claude Code with remote control while I'm away from the laptop."
image: /static/blog/server.png
tags: 
  - Claude
  - Development
  - Homelab
---

I've really enjoyed working with Anthropic's models ever since Opus 4.5. They read
between the lines and get my intent, and Opus, now Fable too, is genuinely good at my
weapon of choice, *Rust*. **Fable 5** came and went fast in June: available for only a
few days before the US government applied export restrictions on it. Now it's back for a
week as part of my Claude Max subscription, and I have a long list of things I'd like to
throw at it.

The catch: it's vacation season here in Sweden, I have a trip planned, and I don't want
to bring the laptop. I've used Claude Code's `/remote-control` feature for a while. It's
a great way to keep an eye on a session while you're out and about, but you still need a
computer running somewhere to host it. We've all seen the 3D-printed brackets that keep
a MacBook lid from closing.

I have a small HP server at home running some homelab stuff, and I'll occasionally SSH
in to do development. The problem is that a plain SSH session dies the moment the
connection drops. For everyday work I reach for
[zellij](https://github.com/zellij-org/zellij). I find the UX nicer, the keybindings
more discoverable and the defaults friendlier. But I couldn't get a zellij session to
stay alive across a disconnect (could be me, could be how its server attaches to the
session), so for this I switched to [tmux](https://github.com/tmux/tmux), which
daemonizes itself and just kept running. After some trial and error I landed on a setup
that works great for my use case, so here's a writeup for the next time I need it.

# The always-on dev machine

First you need a machine that's always on. That could be a cloud-hosted VPS, an old box
in the basement, or in my case a [Proxmox](https://www.proxmox.com/en/) VM on my home
server.

> [!TIP]
> Since I'll be doing Rust development, which is notoriously slow to compile, I gave the
> VM a decent number of CPU cores, plenty of memory, and a fast NVMe SSD for the system
> disk. A Raspberry Pi 3 from the junk bin wouldn't cut it. Giving the agent a fast loop
> to recompile and run the full test suite makes for a much better experience, *even
> remotely*.

I spun up the VM, installed a headless [Arch Linux](https://archlinux.org/), added my
SSH key, and set it up with a nice Zsh shell and a [starship](https://starship.rs/)
prompt. Then I installed the terminal tools I use day to day: Rust, Node, Python, git,
gh-cli, helix, ripgrep, zellij, Claude Code, and of course tmux.

## Easy things to forget

- Generate a new SSH key and add it to GitHub, Codeberg, GitLab, or wherever you keep
  your projects.
- Set the global git config for `user.name` and `user.email`.
- Authenticate the gh-cli with `gh auth login` if you want Claude to open PRs for you.

# Long live the session

Because tmux daemonizes its own server, a detached session already survives logging out
of SSH, or even outright killing the connection from your client. That was the whole
reason I switched to it.

There's still one systemd wrinkle worth knowing about: some distros are configured to
reap a user's leftover processes on logout (the `KillUserProcesses` setting in
`logind.conf`; Arch leaves it off by default). To keep the setup robust no matter how a
box is configured, I enable lingering for my user:

```bash
sudo loginctl enable-linger $USER
```

Lingering lets a user's services and processes keep running without an active login
session, exactly the state I'm after here. On my Arch box tmux survives without it, but
it's cheap insurance for a machine I want to leave running and rely on while I'm away.

# SSH straight into tmux

You could SSH into the machine and run `tmux attach` every time, but wouldn't it be
nicer to SSH straight into your tmux session? Here's how I have my `~/.ssh/config` set
up:

```
Host dev-claude
    RequestTTY yes
    RemoteCommand zsh -l -c "tmux new -A -s claude"

Host dev dev-claude
    HostName 10.10.1.123
    User lhelge
    IdentityFile ~/.ssh/id_ed25519
```

Now `ssh dev-claude` drops me directly into the `claude` session, creating it if it
doesn't exist yet (`tmux new -A`), while plain `ssh dev` still gives me a normal shell.

> [!NOTE]
> I generally just [WireGuard](https://www.wireguard.com/) into my home network and
> connect straight to SSH. If you don't have that, you could put an externally reachable
> jump host in front and add a `ProxyJump` to the config, or use something like
> [Tailscale](https://tailscale.com/), though I haven't tested that setup myself.

That's it. Laptop stays home, the session stays alive, and Fable keeps chewing through
my backlog while I'm away.
