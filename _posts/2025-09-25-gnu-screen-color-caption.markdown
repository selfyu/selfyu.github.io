---
layout: post
title:  "MacOS iTerm GNU screen in 256 color TERM caption config"
date:   2025-09-25 22:25:03 +0800
categories: github-page
---

我在Linux中没有遇到这个问题，可能是OS的区别，或者screen的区别？在MacOS中，
```
caption always "%{.bW}%-w%45>%{.rY}%n %t%{-}%+w %-0<"
```

`%{.bW} %{.rY}` 这两处配置的颜色 bwry（蓝白红黄）会失效

需要改成数字  %{.15;25} %{.3;1}


完整的 .screenrc

```
hardstatus on
hardstatus alwayslastline
defscrollback 4096
#caption always "%{.bW}%-w%45>%{.rY}%n %t%{-}%+w %-0<"
caption always "%{.15;25}%-w%45>%{.3;1}%n %t%{-}%+w %-0<"
hardstatus string "%=%{..G} %H %{..Y} %Y/%m/%d %c %s"
bindkey ^[, prev
bindkey ^[. next
bindkey ^y  number -1
bind w windowlist
bind ^w windowlist
```

终端中打印所有颜色脚本

```
#!/bin/bash

for i in {0..255}; do
  printf "\e[48;5;%sm %3s \e[0m" "$i" "$i"
  if (( (i + 1) % 16 == 0 )); then
    echo
  fi
done
```

