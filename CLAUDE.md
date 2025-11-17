# CLAUDE.md - VSCode Theme Development Guide

## Repository Overview

This repository contains **claude-vscode-theme**, a dark color theme for Visual Studio Code. The theme provides a comprehensive color scheme optimized for code readability and visual consistency across all VSCode UI elements.

### Purpose
- Provide a custom dark theme for VSCode
- Define consistent colors for syntax highlighting across multiple programming languages
- Configure UI element colors for the entire VSCode interface

## Repository Structure

```
claude-vscode-theme/
├── README.md              # Project documentation
├── claude-dark.json       # Main theme configuration file
├── CLAUDE.md             # This file - AI assistant guide
└── .git/                 # Git version control
```

## File Descriptions

### claude-dark.json
**Type:** VSCode Color Theme Configuration
**Format:** JSON
**Size:** ~53KB
**Purpose:** Complete theme definition file

This is the core file of the repository containing two main sections:

1. **`colors` object (lines 4-901):** Defines colors for ~800+ VSCode UI elements including:
   - Activity bar, sidebar, editor, terminal
   - Status bar, title bar, panels
   - Buttons, dropdowns, inputs, menus
   - Debug UI, notifications, badges
   - Git decorations, diff editor
   - Many elements are commented out (prefixed with `//`)

2. **`tokenColors` array (lines 902-1479):** Defines syntax highlighting rules including:
   - Scope-based color assignments
   - Font styles (bold, italic, underline)
   - Language-specific token colors
   - Support for: JavaScript, TypeScript, Python, Java, C/C++, CSS, HTML, Markdown, etc.

### Color Palette

The theme uses a consistent dark color palette:

**Primary Colors:**
- Background: `#1f1f1f` (editor), `#181818` (sidebar/activity bar)
- Foreground: `#cccccc` (default text)
- Accent: `#0078d4` (focus/active elements)
- Borders: `#2b2b2b`, `#3c3c3c`

**Syntax Colors:**
- Keywords: `#569CD6` (blue)
- Strings: `#CE9178` (orange)
- Comments: `#6A9955` (green)
- Functions: `#DCDCAA` (yellow)
- Variables: `#9CDCFE` (light blue)
- Types/Classes: `#4EC9B0` (teal)
- Numbers: `#B5CEA8` (light green)
- Control keywords: `#CE92A4` (pink)

**Status Colors:**
- Error: `#f85149`, `#f14c4c`
- Warning: `#cca700`
- Info: `#3794ff`
- Success/Added: `#2ea043`, `#81b88b`
- Deleted: `#f85149`, `#c74e39`
- Modified: `#0078d4`, `#e2c08d`

## Development Workflows

### Modifying the Theme

When making changes to `claude-dark.json`:

1. **Maintain JSON validity:** The file must be valid JSON
2. **Use proper color format:** All colors use hex format (`#RRGGBB` or `#RRGGBBAA` with alpha)
3. **Follow VSCode schema:** Reference `vscode://schemas/color-theme` schema
4. **Test changes:** Load the theme in VSCode to verify changes

### Adding New Colors

To add or modify UI element colors:

```json
{
  "colors": {
    "element.name": "#HEXCOLOR"
  }
}
```

**Important:** Refer to [VSCode Theme Color Reference](https://code.visualstudio.com/api/references/theme-color) for valid color keys.

### Adding New Token Colors

To add syntax highlighting for new scopes:

```json
{
  "tokenColors": [
    {
      "scope": ["scope.name", "another.scope"],
      "settings": {
        "foreground": "#HEXCOLOR",
        "fontStyle": "bold|italic|underline"
      }
    }
  ]
}
```

### Testing the Theme

**Method 1: Development Mode**
1. Copy `claude-dark.json` to `~/.vscode/extensions/theme-name/themes/`
2. Create `package.json` with theme contribution
3. Reload VSCode
4. Select theme from Color Theme picker

**Method 2: Quick Test**
1. Open Command Palette (Ctrl+Shift+P / Cmd+Shift+P)
2. Run "Developer: Inspect Editor Tokens and Scopes"
3. Verify token scopes and colors

## VSCode Theme Conventions

### Theme File Structure

```json
{
  "$schema": "vscode://schemas/color-theme",
  "type": "dark",
  "colors": { /* UI colors */ },
  "tokenColors": [ /* Syntax highlighting */ ]
}
```

### Commented Colors

Many colors in this theme are commented out (lines 146-900). These represent:
- Optional color customizations
- Advanced/rarely used UI elements
- Alternative color choices for future iterations

**Note:** Commented colors use `//` prefix but remain in JSON structure for reference.

### Scope Naming

Syntax scopes follow TextMate grammar conventions:
- `comment` - Comments
- `string` - String literals
- `keyword` - Language keywords
- `variable` - Variables
- `entity.name.function` - Function names
- `entity.name.type` - Type/class names
- `storage.type` - Type declarations
- `support.function` - Built-in functions

## Common Tasks for AI Assistants

### Task 1: Modify a Specific Color

**Request:** "Change the editor background to a darker shade"

**Steps:**
1. Read `claude-dark.json`
2. Find `"editor.background"` in `colors` object
3. Update hex value (e.g., `#1a1a1a` instead of `#1f1f1f`)
4. Commit changes

### Task 2: Add Syntax Highlighting for New Language

**Request:** "Add support for Rust syntax highlighting"

**Steps:**
1. Research Rust TextMate scopes
2. Add new entries to `tokenColors` array
3. Map Rust-specific scopes to appropriate colors
4. Test with Rust code samples

### Task 3: Adjust Color Consistency

**Request:** "Make all blue colors more vibrant"

**Steps:**
1. Search for all blue hex values (e.g., `#0078d4`, `#569CD6`)
2. Adjust to brighter variants
3. Ensure contrast ratios remain accessible
4. Test across different UI elements

### Task 4: Uncomment Optional Colors

**Request:** "Enable all available color customizations"

**Steps:**
1. Find commented color definitions (lines with `//`)
2. Remove `//` prefix
3. Ensure JSON remains valid
4. Test theme appearance

### Task 5: Export Theme as Extension

**Request:** "Package this as a VSCode extension"

**Steps:**
1. Create `package.json` with extension metadata
2. Add theme contribution point
3. Create README with screenshots
4. Package with `vsce`

## Best Practices for AI Assistants

### When Modifying This Repository

1. **Always validate JSON:** Use JSON validator before committing
2. **Preserve formatting:** Maintain consistent indentation (tabs)
3. **Test color contrast:** Ensure WCAG AA compliance for accessibility
4. **Document changes:** Add clear commit messages explaining color changes
5. **Check cross-platform:** Colors may render differently on macOS/Windows/Linux

### Color Selection Guidelines

1. **Maintain contrast ratios:**
   - Text on background: minimum 4.5:1
   - Large text: minimum 3:1
   - UI components: minimum 3:1

2. **Use semantic colors:**
   - Red for errors/deletions
   - Green for success/additions
   - Yellow/orange for warnings
   - Blue for information

3. **Consider color blindness:**
   - Don't rely solely on color for meaning
   - Use different shades/brightness levels
   - Test with color blindness simulators

### Git Workflow

**Branch naming:** Follow pattern `claude/theme-update-[feature]`

**Commit messages:**
- `feat: add new color for [element]`
- `fix: correct contrast ratio for [element]`
- `style: adjust [color] brightness`
- `docs: update theme documentation`

**Before committing:**
1. Validate JSON syntax
2. Test theme in VSCode
3. Check for unintended color changes
4. Review diff carefully

## Known Issues and Limitations

1. **Commented colors:** Many advanced UI colors are commented out and not active
2. **Schema compliance:** Ensure all color keys match VSCode's current API version
3. **Deprecated keys:** Some color keys may be deprecated in future VSCode versions

## Useful VSCode Commands

- `Developer: Inspect Editor Tokens and Scopes` - See token scopes at cursor
- `Developer: Generate Color Theme From Current Settings` - Export current colors
- `Preferences: Color Theme` - Switch between themes
- `Developer: Reload Window` - Reload after theme changes

## External Resources

- [VSCode Theme Color Reference](https://code.visualstudio.com/api/references/theme-color)
- [VSCode Theme Guide](https://code.visualstudio.com/api/extension-guides/color-theme)
- [TextMate Scope Naming](https://macromates.com/manual/en/language_grammars#naming_conventions)
- [Color Contrast Checker](https://webaim.org/resources/contrastchecker/)

## Development Setup

This repository requires no build process or dependencies. To work on the theme:

1. Clone the repository
2. Edit `claude-dark.json` directly
3. Test in VSCode (see Testing section)
4. Commit changes following git workflow

## Contact and Contribution

When contributing to this repository:
- Keep changes focused and atomic
- Test thoroughly before committing
- Document any breaking changes
- Follow existing code style (JSON formatting)

---

**Last Updated:** 2025-11-17
**Theme Version:** Initial development
**VSCode Compatibility:** 1.60+
