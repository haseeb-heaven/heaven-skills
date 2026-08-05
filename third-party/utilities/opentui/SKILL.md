---
name: opentui
description: >-
  Build terminal UIs with OpenTUI, a Rust-based TUI framework. Covers component creation,
  event handling, key bindings, layouts, themes, custom widgets, and debugging terminal
  interfaces. Use when building command-line applications with rich interactive interfaces.
version: 1
---

# OpenTUI

Build terminal UIs with OpenTUI — a Rust-based framework for creating rich, interactive terminal applications.

## When NOT to Use

- Simple scripts that only need stdout/stderr output — use `println!` instead
- GUI desktop applications — consider GTK, WebViews, or native GUI frameworks
- Web-based dashboards — HTML/CSS/JS is better suited for browser interfaces

## Core Components

| Component | Purpose | Example |
|-----------|---------|---------|
| **Widget** | Basic visual element (text, button, input) | `TextWidget::new("Hello")` |
| **Container** | Layout grouping (rows, columns, grids) | `Row::new().push(widget1).push(widget2)` |
| **View** | Full screen layout with state management | `MyAppView::new()` |
| **Event** | User interactions (key, mouse, tick) | `EventHandler::on_key(Key::Enter)` |

## Building a TUI Application

### Step 1: Setup Project
```toml
# Cargo.toml
[dependencies]
opentui = "0.x"
ratatui = "0.x"  # Terminal rendering backend
```

### Step 2: Create Views
```rust
use opentui::*;

struct MyApp {
    count: u32,
    message: String,
}

impl View for MyApp {
    fn render(&self, area: Rect) -> Frame {
        let mut frame = Frame::default();
        
        // Header
        frame.render_widget(Text::format!("Count: {}", self.count), area.top());
        
        // Body
        frame.render_widget(Paragraph::new(&self.message), area.middle());
        
        // Footer
        frame.render_widget(Hint::new("Press q to quit"), area.bottom());
        
        frame
    }
    
    fn handle_event(&mut self, event: Event) -> Action {
        match event {
            Event::Key(Key::Char('q')) => Action::Quit,
            Event::Key(Key::Enter) => {
                self.count += 1;
                self.message = format!("Count incremented to {}", self.count);
                Action::Redraw
            },
            _ => Action::None
        }
    }
}
```

### Step 3: Run the App
```rust
fn main() {
    let app = MyApp {
        count: 0,
        message: String::from("Welcome! Press Enter to increment."),
    };
    app.run()
}
```

## Key Bindings Reference

| Key | Default Action | Custom Binding |
|-----|---------------|----------------|
| `q` / `Ctrl+C` | Quit | `on_key(Key::Char('q'), quit)` |
| `j` / `Down` | Move down | `on_key(Key::Down, move_down)` |
| `k` / `Up` | Move up | `on_key(Key::Up, move_up)` |
| `h` / `Left` | Move left | `on_key(Key::Left, move_left)` |
| `l` / `Right` | Move right | `on_key(Key::Right, move_right)` |
| `Enter` | Select/Confirm | `on_key(Key::Enter, confirm)` |
| `Esc` | Cancel/Back | `on_key(Key::Esc, cancel)` |
| `?` | Show help | `on_key(Key::Char('?'), show_help)` |
| `:` | Command mode | `on_key(Key::Char(':'), cmd_mode)` |

## Layout Patterns

### Row Layout
```
┌─────────────┬─────────────┐
│ Left Panel   │ Right Panel  │
└─────────────┴─────────────┘
```
Use for side-by-side content (file browser + preview).

### Column Layout
```
┌──────────────────────┐
│ Header               │
├──────────────────────┤
│ Main Content         │
├──────────────────────┤
│ Footer               │
└──────────────────────┘
```
Use for standard application screens.

### Grid Layout
```
┌──────┬──────┬──────┐
│ Cell │ Cell │ Cell │
├──────┼──────┼──────┤
│ Cell │ Cell │ Cell │
└──────┴──────┴──────┘
```
Use for tables, dashboards, card views.

## Debugging Tips

1. **Terminal size issues** — Wrap rendering in `area.max(term_size())` bounds check
2. **Flickering** — Enable double-buffering (`tui.enable_alternate_screen(true)`)
3. **Slow rendering** — Profile with `criterion`; avoid allocations in render loops
4. **Input not received** — Check that terminal raw mode is enabled before event loop
5. **Unicode display** — Ensure terminal supports UTF-8; use ASCII fallback if needed

## Best Practices

1. **Keep render functions pure** — Render shouldn't modify app state directly
2. **Batch state updates** — Collect changes, apply in single tick
3. **Use lazy loading** — Don't fetch/render data until view is visible
4. **Handle resize gracefully** — Store viewport dimensions, reflow on change
5. **Test with different terminal sizes** — TUIs break at narrow widths easily
