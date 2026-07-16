---
title: codex cli 连按 Esc 后对话信息丢失
status: published
date: 2026-07-08
summary: 
---
codex 连按 Esc 后会编辑历史信息，即使没编辑，最新对话信息也可能会丢失，非常坑爹。
在 .codex/sessions 里找到会话源文件，删掉文件末尾的 thread_rolled_back 整行即可恢复。
