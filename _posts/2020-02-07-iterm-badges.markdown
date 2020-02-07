---
layout: post
title:  "Set iTerm badges from command line"
summary: "How to set iTerm badges, a.k.a. headings from your command line"
date:   2020-02-07 20:00:00
categories: iterm
tags: [iterm, mac, shell]
---

When working with multiple terminal windows, it is sometimes useful to have some kind of heading that indicates what each terminal contains. During our last showcase, we used this to let the audience know what each of our three terminal windows is showing.

![iterm badges](/assets/images/iterm/iterm-badges.png)

Here is a short tutorial on how to set this up, so that you can set the badge easily from the command line. We assume that you are using [iTerm](https://iterm2.com/) on a Mac.

1. Install the [iTerm shell integration](https://iterm2.com/documentation-shell-integration.html) - if you are using bash, here is all you need to run

   ```bash
   curl -L https://iterm2.com/shell_integration/install_shell_integration.sh | bash
   ```

   this will add some includes into your `~/.bash_profile`. The website contains explanations for other shells as well (e.g. `zsh`)

2. Add the following function to your `~/.bash_profile` (or `~/.zshrc`)

   ```bash
   function iterm2_print_user_vars() {
       iterm2_set_user_var badge $badge
   }
   ```

   thereby you set a iTerm user var `badge` that reads the content from the `$badge` shell variable.

3. reload your shell profile via

   ```bash
   source ~/.bash_profile
   ```

3. In your iTerm profile settings, set `\(user.badge)`

   ![iTerm profile settings for the badge](/assets/images/iterm/iterm-badge-settings.png)

5. You can now set your badge in your terminal via

   ```bash
   export badge='hello badge'
   ```

   ![set badge in terminal](/assets/images/iterm/iterm-badge.png)

Have fun!

## Further References

* https://technology.customink.com/blog/2016/07/18/how-to-add-badges-to-iterm2/
