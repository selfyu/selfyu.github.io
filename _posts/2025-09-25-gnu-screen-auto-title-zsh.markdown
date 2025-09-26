---
layout: post
title:  "MacOS zsh GNU screen auto set title to current folder name"
date:   2025-09-25 22:25:03 +0800
categories: screen zsh
---

add to .zshrc

```
function set-screen-title() {
  # 把当前路径写到 screen 的窗口 title
  echo -ne "\033k${PWD##*/}\033\\"
}

autoload -Uz add-zsh-hook
add-zsh-hook precmd set-screen-title
```

.screenrc

```
hardstatus on
hardstatus alwayslastline
defscrollback 4096
#caption always "%{.bW}%-w%45>%{.rY}%n %t%{-}%+w %-0<"
caption always "%{.15;25}%-w%45>%{.3;1}%n %t%{-}%+w %-0<"
#hardstatus string "%=%{..G} %H(%l) %{..Y} %Y/%m/%d %c:%s "
hardstatus string "%=%{..G} %H %{..Y} %Y/%m/%d %c %s"

##escape ^Kk

bindkey ^[, prev
bindkey ^[. next
bindkey ^y  number -1

bind w windowlist
bind ^w windowlist
```



