# Tmux Cheat Sheet

## Session Management

| Command / Shortcut | Description |
|--------------------|-------------|
| `tmux new -s <name>` | Create a new named session |
| `tmux a` | Attach to the most recently used session |
| `tmux attach -t <session-name-or-id>` | Attach to a specific session |
| `Ctrl + B`, `D` | Detach from the current session |
| `tmux ls` | List all active sessions |
| `tmux kill-session` | Kill the current session |
| `tmux kill-session -t <session-name>` | Kill a specific session |

---

## Window Management

| Shortcut | Description |
|----------|-------------|
| `Ctrl + B`, `C` | Create a new window |
| `Ctrl + B`, `N` | Switch to the next window |
| `Ctrl + B`, `P` | Switch to the previous window |
| `Ctrl + B`, `W` | Show a visual list of windows |
| `Ctrl + B`, `<window-number>` | Jump directly to a window (0–9) |

---

## Pane (Split Window) Management

| Shortcut | Description |
|----------|-------------|
| `Ctrl + B`, `%` | Split pane vertically (left/right) |
| `Ctrl + B`, `"` | Split pane horizontally (top/bottom) |

---

## Pane Navigation

| Shortcut | Description |
|----------|-------------|
| `Ctrl + B`, `←` | Move to the left pane |
| `Ctrl + B`, `→` | Move to the right pane |
| `Ctrl + B`, `↑` | Move to the pane above |
| `Ctrl + B`, `↓` | Move to the pane below |

---

## Pane Selection

| Shortcut | Description |
|----------|-------------|
| `Ctrl + B`, `Q` | Display pane numbers |
| `Ctrl + B`, `Q`, `<number>` | Jump to the selected pane |

---

## Pane Resize

| Shortcut | Description |
|----------|-------------|
| `Ctrl + B`, `Alt + ←` | Resize pane left |
| `Ctrl + B`, `Alt + →` | Resize pane right |
| `Ctrl + B`, `Alt + ↑` | Resize pane upward |
| `Ctrl + B`, `Alt + ↓` | Resize pane downward |

---

## Quick Reference

| Action | Command / Shortcut |
|--------|--------------------|
| Create session | `tmux new -s <name>` |
| Attach to latest session | `tmux a` |
| Attach to named session | `tmux attach -t <name>` |
| List sessions | `tmux ls` |
| Detach session | `Ctrl + B`, `D` |
| Kill current session | `tmux kill-session` |
| Kill named session | `tmux kill-session -t <name>` |
| New window | `Ctrl + B`, `C` |
| Next window | `Ctrl + B`, `N` |
| Previous window | `Ctrl + B`, `P` |
| List windows | `Ctrl + B`, `W` |
| Jump to window | `Ctrl + B`, `<window-number>` |
| Split vertically | `Ctrl + B`, `%` |
| Split horizontally | `Ctrl + B`, `"` |
| Move between panes | `Ctrl + B`, `← ↑ ↓ →` |
| Show pane numbers | `Ctrl + B`, `Q` |
| Jump to pane | `Ctrl + B`, `Q`, `<number>` |
| Resize pane | `Ctrl + B`, `Alt + ← ↑ ↓ →` |
