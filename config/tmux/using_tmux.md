# 🖥️ Tmux Cheat Sheet

### 🚀 Session Management

| Command | Description |
|---------|-------------|
| `tmux` | Start a new session |
| `tmux new -s <session-name>` | Create a new named session |
| `tmux ls` | List all sessions |
| `tmux list-sessions` | List all sessions (verbose) |
| `tmux a` | Attach to last session |
| `tmux attach` | Attach to last session |
| `tmux attach -t <session-name>` | Attach to specific session |
| `tmux a -t <session-name>` | Attach to specific session (short) |
| `tmux kill-session -t <session-name>` | Kill specific session |
| `tmux kill-server` | Kill all sessions |
| `tmux rename-session -t <old> <new>` | Rename a session |
| `C-b d` | 🔌 Detach from current session |
| `C-b D` | 🔌 Choose which session to detach from |
| `C-b $` | ✏️ Rename current session |
| `C-b s` | 📋 List all sessions (interactive) |
| `C-b (` | ⬅️ Switch to previous session |
| `C-b )` | ➡️ Switch to next session |

---

### 🪟 Windows Management

| Keybinding | Description |
|------------|-------------|
| `C-b c` | ➕ Create new window |
| `C-b n` | ➡️ Move to **n**ext window |
| `C-b p` | ⬅️ Move to **p**revious window |
| `C-b 0-9` | 🔢 Jump to window number 0-9 |
| `C-b w` | 📋 List all windows (interactive) |
| `C-b ,` | ✏️ Rename current window |
| `C-b &` | ❌ Close current window (with confirmation) |
| `C-b l` | 🔄 Toggle to last active window |
| `C-b f` | 🔍 Find window by name |

---

### 📐 Panes Management

| Keybinding | Description |
|------------|-------------|
| `C-b "` | ➖ Split pane **horizontally** (top/bottom) |
| `C-b %` | ➗ Split pane **vertically** (left/right) |
| `C-b <arrow keys>` | 🧭 Move to pane in arrow direction |
| `C-b h/j/k/l` | 🧭 Move to pane (Vim style - custom binding) |
| `C-b o` | 🔄 Cycle through panes |
| `C-b ;` | ↩️ Toggle to last active pane |
| `C-b q` | 🔢 Show pane numbers (press number to jump) |
| `C-b Ctrl+<arrow>` | 📏 Resize pane (hold Ctrl, press arrow multiple times) |
| `C-b Alt+<arrow>` | 📏 Resize pane in larger steps |
| `C-b z` | 🔍 Toggle pane **zoom** (full screen) |
| `C-b x` | ❌ Close current pane (with confirmation) |
| `C-b !` | 🪟 Convert pane to window |
| `C-b {` | ⬅️ Swap pane with previous |
| `C-b }` | ➡️ Swap pane with next |
| `C-b Space` | 🔄 Cycle through pane layouts |
| `C-b Ctrl+o` | 🔃 Rotate panes |
| `exit` or `Ctrl+d` | 🚪 Exit current pane |

---

### ⚙️ Configuration & Help

| Keybinding | Description |
|------------|-------------|
| `C-b ?` | ❓ Show all key bindings |
| `C-b :` | ⌨️ Enter command prompt |
| `C-b t` | 🕐 Display clock |
| `C-b r` | 🔄 Reload config (custom binding) |
| `tmux source-file ~/.tmux.conf` | Reload Tmux configuration |
| `tmux show-options -g` | Show global options |
| `tmux list-keys` | List all key bindings |
| `tmux info` | Show session info |

---

### 🔌 Tmux Plugin Manager (TPM)
```bash
# Clone TPM
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

**Add to `~/.tmux.conf`:**
```bash
# List of plugins
set -g @plugin 'tmux-plugins/tpm'

# Initialize TPM (keep at bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

**Plugin Management**
| Keybinding | Description |
|------------|-------------|
| `C-b I` | 📦 **I**nstall plugins (capital I) |
| `C-b U` | 🔄 **U**pdate plugins |
| `C-b Alt+u` | 🗑️ Uninstall plugins not in config |
