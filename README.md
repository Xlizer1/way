```
# Generic Hyprland configuration - works on any fresh Arch install
# See https://wiki.hyprland.org/Configuring/Monitors/

# Monitor configuration - auto-detect (works on any setup)
monitor = ,preferred,auto,1
# For multiple monitors, Hyprland will auto-arrange them
# You can customize this later for specific setups

# Set programs that you use
$terminal = kitty
$fileManager = thunar
$menu = wofi --show drun

# Environment variables for Wayland compatibility
env = XCURSOR_SIZE,24
env = QT_QPA_PLATFORMTHEME,qt5ct
env = GDK_BACKEND,wayland,x11
env = QT_QPA_PLATFORM,wayland;xcb
env = CLUTTER_BACKEND,wayland
env = XDG_CURRENT_DESKTOP,Hyprland
env = XDG_SESSION_TYPE,wayland
env = XDG_SESSION_DESKTOP,Hyprland

# Input configuration
input {
    kb_layout = us
    kb_variant =
    kb_model =
    kb_options =
    kb_rules =
    follow_mouse = 1
    
    touchpad {
        natural_scroll = true
    }
    
    sensitivity = 0 # -1.0 - 1.0, 0 means no modification.
    
    # Gaming optimization (optional)
    accel_profile = flat
    force_no_accel = true
}

# General window behavior
general {
    gaps_in = 5
    gaps_out = 10
    border_size = 2
    col.active_border = rgba(33ccffee) rgba(00ff99ee) 45deg
    col.inactive_border = rgba(595959aa)
    layout = dwindle
    
    # Performance optimizations
    allow_tearing = true
    no_focus_fallback = true
}

# Visual effects
decoration {
    rounding = 5
    
    blur {
        enabled = true
        size = 3
        passes = 1
        new_optimizations = true
        ignore_opacity = true
        xray = false
        popups = false
    }
    
    drop_shadow = true
    shadow_range = 4
    shadow_render_power = 3
    col.shadow = rgba(1a1a1aee)
}

# Animations
animations {
    enabled = true
    bezier = myBezier, 0.05, 0.9, 0.1, 1.05
    animation = windows, 1, 7, myBezier
    animation = windowsOut, 1, 7, default, popin 80%
    animation = border, 1, 10, default
    animation = borderangle, 1, 8, default
    animation = fade, 1, 7, default
    animation = workspaces, 1, 6, default
}

# Layout configurations
dwindle {
    pseudotile = true
    preserve_split = true
}

master {
    new_is_master = true
}

gestures {
    workspace_swipe = true
}

# Performance and behavior settings
misc {
    disable_hyprland_logo = true
    disable_splash_rendering = true
    vfr = true
    vrr = 1
    mouse_move_enables_dpms = true
    enable_swallow = false
    focus_on_activate = true
}

# Basic transparency (comment out if you want fully opaque windows)
windowrulev2 = opacity 0.95 0.90,class:^(kitty)$
windowrulev2 = opacity 0.98 0.95,class:^(thunar)$
# Keep media players fully opaque
windowrulev2 = opacity 1.0 1.0,class:^(mpv)$
windowrulev2 = opacity 1.0 1.0,fullscreen:1

# ============================================================================
# KEYBINDINGS WITH COMMENTS
# ============================================================================

# Application shortcuts
bind = SUPER, RETURN, exec, $terminal                    # Super + Enter: Open terminal
bind = SUPER, E, exec, $fileManager                      # Super + E: Open file manager
bind = SUPER, SPACE, exec, $menu                         # Super + Space: Open application launcher

# Window management
bind = SUPER, Q, killactive,                             # Super + Q: Close active window
bind = SUPER, V, togglefloating,                         # Super + V: Toggle floating mode
bind = SUPER, P, pseudo,                                 # Super + P: Enable pseudo-tiling
bind = SUPER, S, togglesplit,                            # Super + S: Toggle split direction
bind = SUPER, F, fullscreen, 0                          # Super + F: Toggle fullscreen
bind = SUPER, M, fullscreen, 1                          # Super + M: Toggle maximize

# Session management
bind = SUPER SHIFT, Q, exit,                             # Super + Shift + Q: Exit Hyprland

# Focus movement
bind = SUPER, left, movefocus, l                         # Super + Left: Move focus left
bind = SUPER, right, movefocus, r                        # Super + Right: Move focus right
bind = SUPER, up, movefocus, u                           # Super + Up: Move focus up
bind = SUPER, down, movefocus, d                         # Super + Down: Move focus down

# Window movement
bind = SUPER SHIFT, left, movewindow, l                  # Super + Shift + Left: Move window left
bind = SUPER SHIFT, right, movewindow, r                 # Super + Shift + Right: Move window right
bind = SUPER SHIFT, up, movewindow, u                    # Super + Shift + Up: Move window up
bind = SUPER SHIFT, down, movewindow, d                  # Super + Shift + Down: Move window down

# Window resizing
bind = SUPER ALT, left, resizeactive, -20 0              # Super + Alt + Left: Resize narrower
bind = SUPER ALT, right, resizeactive, 20 0              # Super + Alt + Right: Resize wider
bind = SUPER ALT, up, resizeactive, 0 -20                # Super + Alt + Up: Resize shorter
bind = SUPER ALT, down, resizeactive, 0 20               # Super + Alt + Down: Resize taller

# Workspace switching
bind = SUPER, 1, workspace, 1                            # Super + 1-0: Switch to workspace 1-10
bind = SUPER, 2, workspace, 2
bind = SUPER, 3, workspace, 3
bind = SUPER, 4, workspace, 4
bind = SUPER, 5, workspace, 5
bind = SUPER, 6, workspace, 6
bind = SUPER, 7, workspace, 7
bind = SUPER, 8, workspace, 8
bind = SUPER, 9, workspace, 9
bind = SUPER, 0, workspace, 10

# Move windows to workspaces
bind = SUPER SHIFT, 1, movetoworkspace, 1                # Super + Shift + 1-0: Move window to workspace 1-10
bind = SUPER SHIFT, 2, movetoworkspace, 2
bind = SUPER SHIFT, 3, movetoworkspace, 3
bind = SUPER SHIFT, 4, movetoworkspace, 4
bind = SUPER SHIFT, 5, movetoworkspace, 5
bind = SUPER SHIFT, 6, movetoworkspace, 6
bind = SUPER SHIFT, 7, movetoworkspace, 7
bind = SUPER SHIFT, 8, movetoworkspace, 8
bind = SUPER SHIFT, 9, movetoworkspace, 9
bind = SUPER SHIFT, 0, movetoworkspace, 10

# Special workspace (scratchpad)
bind = SUPER, grave, togglespecialworkspace, magic       # Super + `: Toggle scratchpad
bind = SUPER SHIFT, grave, movetoworkspace, special:magic # Super + Shift + `: Move to scratchpad

# Mouse workspace scrolling
bind = SUPER, mouse_down, workspace, e+1                 # Super + Mouse scroll: Change workspaces
bind = SUPER, mouse_up, workspace, e-1

# Focus cycling
bind = ALT, Tab, cyclenext                               # Alt + Tab: Cycle through windows
bind = ALT SHIFT, Tab, cyclenext, prev                   # Alt + Shift + Tab: Reverse cycle

# Mouse window controls
bindm = SUPER, mouse:272, movewindow                     # Super + Left click drag: Move window
bindm = SUPER, mouse:273, resizewindow                   # Super + Right click drag: Resize window

# System controls
bind = SUPER, L, exec, swaylock -f                       # Super + L: Lock screen

# Audio controls (requires pamixer)
bind = , XF86AudioRaiseVolume, exec, pamixer -i 5        # Volume up key
bind = , XF86AudioLowerVolume, exec, pamixer -d 5        # Volume down key  
bind = , XF86AudioMute, exec, pamixer -t                 # Mute key

# Brightness controls (requires brightnessctl)
bind = , XF86MonBrightnessUp, exec, brightnessctl set +5%    # Brightness up key
bind = , XF86MonBrightnessDown, exec, brightnessctl set 5%-  # Brightness down key

# Screenshot controls
bind = , Print, exec, mkdir -p ~/Pictures && grim ~/Pictures/screenshot-$(date +%Y-%m-%d_%H-%M-%S).png     # Print: Full screenshot
bind = SUPER SHIFT, S, exec, mkdir -p ~/Pictures && grim -g "$(slurp)" ~/Pictures/screenshot-$(date +%Y-%m-%d_%H-%M-%S).png   # Super + Shift + S: Area screenshot
bind = CTRL, Print, exec, grim -g "$(slurp)" - | wl-copy    # Ctrl + Print: Area screenshot to clipboard

# Waybar controls
bind = SUPER, B, exec, killall -SIGUSR1 waybar           # Super + B: Toggle waybar visibility

# ============================================================================
# STARTUP APPLICATIONS
# ============================================================================

# Essential startup applications
exec-once = waybar                                       # Status bar

# Optional startup applications (comment out if not installed)
# exec-once = dunst                                      # Notification daemon
# exec-once = swww init                                  # Wallpaper daemon
# exec-once = nm-applet --indicator                      # Network manager applet
# exec-once = blueman-applet                             # Bluetooth applet

# Clipboard history (requires cliphist)
# exec-once = wl-paste --type text --watch cliphist store
# exec-once = wl-paste --type image --watch cliphist store

# Uncomment and modify these lines for your specific setup:
# exec-once = swww img /path/to/your/wallpaper.png       # Set wallpaper
# exec-once = /usr/lib/polkit-kde-authentication-agent-1 # Authentication agent
```
