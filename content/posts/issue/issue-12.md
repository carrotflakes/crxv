+++
date = 2025-03-04T07:34:24Z
title = "コマンドの実行に時間がかかったとき終了を通知する"
draft = false
writer = "carrotflakes"
+++


## 概要

コマンド実行に10秒以上かかったら、コマンド終了時に何秒かかったか音声で教えてくれるようになります。

## 前提

mac で zsh を使っている。

## コード

`.zshrc` に以下を追加する。

``` sh
function timer_start {
  TIMER_START=$SECONDS
}

function timer_end {
  local duration=$(( SECONDS - TIMER_START ))
  if (( duration > 10 )); then
    say "${duration}秒かかりました"
  fi
}

autoload -Uz add-zsh-hook
add-zsh-hook preexec timer_start
add-zsh-hook precmd timer_end
```
