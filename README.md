npm 5.1.0-1
========
npm@5 package for Arch Linux.

```bash
wget https://github.com/simnalamburt/arch.npm/releases/download/v5.1.0-1/npm-5.1.0-1-any.pkg.tar.xz
sudo pacman -U npm-5.1.0-1-any.pkg.tar.xz
```

Use [`makepkg`](https://www.archlinux.org/pacman/makepkg.8.html) to build the
package manually.

```bash
makepkg -si
```

<br>

#### Current status
I sent an email to [Felix Yan](https://github.com/felixonmars) asking for the
patch to be merged and waiting for a reply.

#### References
- [What is holding npm5 back in the repos? - /r/archlinux](https://www.reddit.com/r/archlinux/comments/6ijx48/what_is_holding_npm5_back_in_the_repos/djdvsd8/)
