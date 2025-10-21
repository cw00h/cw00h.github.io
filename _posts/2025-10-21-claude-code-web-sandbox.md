---
title: Peeking Inside *Claude Code on the Web*'s Sandbox
date: 2025-10-21
permalink: /posts/2025/10/claude-code-web-sandbox/
tags:
  - Agent Security
published: true
---


## TL;DR

1. Investigating the sandbox inside ***Claude Code on the Web*** was surprisingly easy. I did not need jailbreaks or prompt injection. Claude executed inspection commands and generated code for me on request.
2. The environment is strongly sandboxed. Evidence points to a gVisor backed container running under a VM, with a PID 1 init-like binary called `process_api` which is responsible for resource management.

---

## 1 Motivation

***Claude Code on the Web*** [was released yesterday](https://www.anthropic.com/news/claude-code-on-the-web), with documentation [here](https://docs.claude.com/en/docs/claude-code/claude-code-on-the-web). 

Since it now runs code inside its own server, I was curious about its attack surface, especially around potential prompt injection abuse. I wanted to understand what kind of sandbox it runs in.

---

## 2 How I investigated the sandbox

*Claude Code on the Web* **accepts natural language only**. It does not give you a raw interactive shell from the web client. The model executes bash commands indirectly through an agent layer, which limits control over output or interactivity. 

To perform proper system enumeration, I wanted to run shell commands directly inside the container. I adjusted the environment so it could communicate with my machine and tried several approaches.

1) **SSH server running inside the container**: listeners never stayed open — inbound traffic was blocked.  
2) **Basic Reverse Shell**: TCP handshakes to my host timed out; It looked like only HTTP worked through a proxy.  
3) **HTTP reverse shell**: success.

After trying several approaches, I succesfully built an HTTP reverse shell to run commands inside the container. 

<img src="/images/posts/2025-10-21-claude-code-web-sandbox/2025-10-21_19-51.png" class="align-center" width="500">

During this process, what surprised me most was how willingly Claude executed inspection commands and summarized outputs. I did **not need any jailbreak or prompt injection** to get system information. Claude Code simply executed the system inspection commands I asked for, and when I requested a reverse shell in natural language, it generated the server and client Python code and assisted debugging until the HTTP reverse shell worked.

<img src="/images/posts/2025-10-21-claude-code-web-sandbox/2025-10-21_19-40.png" class="align-center" width="600">


---

## 3 What's inside *Claude Code on the Web*’s sandbox

Once I could execute commands freely, the system's structure became clear. In fact, even during this investigation, Claude Code gave me a big helping hand by executing system inspection commands and summarizing the results.

### 3.1 Docker container confirmed

Running `ls -al /` revealed a `.dockerenv` file, the usual marker that the environment is containerized.

<img src="/images/posts/2025-10-21-claude-code-web-sandbox/2025-10-21_19-12.png" class="align-center" width="500">

### 3.2 gVisor user-space kernel

When I printed `dmesg` out:

<img src="/images/posts/2025-10-21-claude-code-web-sandbox/2025-10-21_19-53.png" class="align-center" width="500">

`dmesg` contained lines metioning **gVisor**.

This confirms the container runs under **gVisor (runsc)**, which intercepts syscalls in userspace rather than delegating them to the host kernel — strong isolation against kernel-level escape attempts.

### 3.3 Underlying VM: Google Compute Engine

`cat /sys/class/dmi/id/product_name` returned `Google Compute Engine`.

<img src="/images/posts/2025-10-21-claude-code-web-sandbox/2025-10-21_19-57.png" class="align-center" width="700">

This implies the container runs inside a GCE VM, likely orchestrated by Anthropic’s internal infrastructure.

### 3.4 Process supervisor: `process_api`

I also have found out about the supervisor process inside the container.

<img src="/images/posts/2025-10-21-claude-code-web-sandbox/2025-10-21_19-57_1.png" class="align-center" width="900">

`process_api` is the **PID 1 supervisor**. The binary file of this process is located at `/process_api`.
I guess it enforces cgroups, monitors OOM, and exposes an internal WebSocket/HTTP interface to spawn or attach to subprocesses.
It is effectively an in-container init system plus API layer that mediates all execution.

### 3.5 Network and capability restrictions

* Outbound connections only work over authenticated HTTP(S) via a proxy; It looked like raw TCP (including SSH) was blocked.
* Capabilities like `CAP_SYS_ADMIN` and `CAP_NET_ADMIN` are absent.
* `/sys` and device nodes are read-only.
* Root filesystem is mounted via `9p` with remote caching — consistent with ephemeral workspace mounts.
* There was no seccomp profile found (usually at `/proc/self/seccomp`), likely because gVisor handles syscall filtering.

These restrictions together indicate deliberate containment beyond Docker defaults.

---

## 4. What this tells us

**Architecture overview**

```
Google Compute Engine VM
 └── Docker container
      └── gVisor runsc (user-space kernel)
           └── process_api (PID 1 supervisor)
```

Each layer adds isolation:

* VM boundary isolates workloads at the hypervisor level.
* gVisor intercepts syscalls, preventing direct kernel access.
* process_api manages resource and process boundaries inside the container.
* HTTP-only egress ensures predictable, auditable outbound traffic.

This combination makes the sandbox notably resilient. Any realistic escape would likely need a vulnerability in **gVisor** or **process_api**.

---

## 5. What surprised me

Claude Code on the Web turned out to be *too cooperative*. I expected to fight against guardrails or rely on prompt injection, but instead, Claude willingly executed inspection commands, analyzed their output, and helped me build the reverse shell scripts.

So while I did set up an HTTP reverse shell for completeness, it quickly became unnecessary — Claude itself acted as an investigative assistant inside its own sandbox.

---

## 6. Next steps

Next, I plan to examine the sandbox of the newly released **[Claude Code CLI's Sandbox](https://docs.claude.com/en/docs/claude-code/sandboxing)**, which likely runs in a different isolation model. (Open source research preview is [here](https://github.com/anthropic-experimental/sandbox-runtime).)
If I find anything interesting, I'll share it in a follow-up post.

If you have found any error or have additional insights, please let me know with a email to `00cwooh@snu.ac.kr`. Thank you!