# Arc's URLBar for Zen

An Arc-inspired addressbar layout for Zen Browser, built on [Kostiantyn Kugot's original Blended Addressbar](https://github.com/kkugot/blended-addressbar). The original mod supplies the page-aware colors, browser frame, split-view controls, bookmarks behavior, and loading indicators. This fork adds optional ways to display the address in Zen's top toolbar.

![Blended Addressbar preview](https://raw.githubusercontent.com/igeag/blended-addressbar/main/marketplace-preview.png)

*Preview of the original mod; the fork's toolbar options are configured in Sine. Arc is a visual reference, and this project is not affiliated with Arc or The Browser Company.*

## Added in this fork

| Option | What it does | Default |
| --- | --- | --- |
| Domain-only address | Shows the hostname, such as `github.com`, while the top addressbar is idle. The full URL remains available for editing and copying. | Off |
| Centered address | Centers the idle address label in the browser window when space allows. | Off |
| Compact top toolbar | Shortens the **entire** top navigation toolbar, including its buttons. Choose Original, Compact (36px), or Extra compact (32px). | Compact |
| Content-sized address field | When either address-display option is on, the idle clickable field fits its label and keeps Copy URL close. The native editor returns when you focus the addressbar. | Automatic with either option |
| Zoom reset button | When the compact top addressbar is active and page zoom differs from 100%, Zen's native zoom percentage sits just beyond the field beside the site-data menu. Click it to reset zoom. | Automatic with either address-display option |

The sidebar also closes into Compact Mode with a 220ms eased animation. This follows the system's reduced-motion setting and preserves Zen's native opening and hover behavior.

The toolbar changes were made to bring Zen's top bar closer to Arc's compact appearance. The domain-only and centered options can be enabled separately in Sine. Zen's floating search bar keeps its native behavior.

## Features from the original mod

- Addressbar colors that follow the active page in dual-toolbar layouts, with matching text and icon contrast.
- Optional window tint with adjustable strength.
- A browser frame with adjustable corner radius, spacing, and shadow strength. Corner shape follows Zen's settings.
- Split view with a 1.5pt inset focus ring in Zen's accent color. The page and ring share squircle clipping, with rounded outer corners and square divider corners.
- Browser sidebars share the panes’ outer-corner clipping, with a passive inner highlight in split view and no thick active-pane border. In single-tab dual-toolbar mode, the sidebar has a full-height column; the addressbar and bookmarks stay above the webpage. Native compact toolbar autohide is preserved.
- A bookmarks bar in Only Sidebar mode that appears on hover or stays visible.
- Compact address and reload/stop controls above each dual-toolbar split pane, with independent colors and loading glow. The shared toolbar and bookmarks row are hidden during split view.
- Three loading indicators: Progress bar, URL bar glow, and Window edge. You can also keep Zen's native loader.

## Installation

1. Install [Sine](https://github.com/CosmoCreeper/Sine#installation) and restart Zen.
2. In Sine settings, install the mod from the repository `igeag/blended-addressbar`.
3. If installing from this GitHub repository, turn on Sine's **Enable installing JS from unofficial sources** setting (`sine.allow-unsafe-js`) and restart Zen. This setting permits JavaScript from all unofficial Sine sources, so enable it only if you trust the mods you have installed. Without it, Sine loads the CSS (including toolbar height) but skips the script required for domain-only and centered address text.
4. Enable **Blended Addressbar** and open its Sine settings. The **Addressbar Display** section contains this fork's domain, centering, and top-toolbar height options; the other sections contain the original mod's frame, tint, and loading settings.

## Compatibility

Supported Zen layouts: **Only Sidebar**, **Sidebar and Top Toolbar**, and **Collapsed Sidebar**. The new address display and toolbar-height options apply to Zen's top toolbar; Only Sidebar keeps its native sidebar addressbar while the original frame, window tint, split view, compact mode, and loading bar remain supported. Visual validation is still recommended after Zen updates because browser chrome selectors can change.

## Split addresses

In dual-toolbar layouts, each split pane shows a field styled like the native addressbar, with copy URL, site settings/extensions and reload/stop controls. Click the address, or focus it with Tab and press Enter, to select that pane and open Zen’s real editor over the field. Cmd/Ctrl+L opens that same editor over the selected pane. Suggestions, paste, selection and navigation remain native. Hover to see the full URL. Reload/stop controls its own pane without changing the selected tab.

Page and system light/dark changes update all visible split fields without switching tabs.

These rows share the page’s clipping boundary and reserve the native field height plus 6px above the page. The original collapsed addressbar is hidden while split fields are active; its DOM stays in place and its editor is positioned over the selected field. The shared toolbar row and bookmarks toolbar are hidden in this mode, even when bookmarks are set to always show. Both return on exit without changing Zen’s settings. Rows are removed outside split view, in Only Sidebar, and in fullscreen; Glance overlays are excluded.

## Preferences

Change these settings in Sine. The preference names below also identify them in `about:config`.

### Addressbar display

- `uc.blended-addressbar.domain-only`: show only the hostname (for example, `github.com`) while the addressbar is idle; disabled by default. Focusing the field reveals Zen's normal full URL for editing. Split-pane address labels also hide their path.
- `uc.blended-addressbar.center-text`: center the idle address label in the browser window where the field has room; disabled by default. Each split-pane address label centers within its own field.
- `uc.blended-addressbar.toolbar-height`: choose Original, Compact (36px), or Extra compact (32px) for the whole top navigation toolbar, including its buttons. Compact is the default. This replaces the earlier addressbar-field height setting.

The domain-only setting applies to HTTP and HTTPS pages. Other page types keep Zen's native label. The display settings leave the underlying URL, copy actions, and address editing unchanged.
In the top toolbar, the idle addressbar fits the displayed label and keeps Copy URL beside it. Focusing the addressbar restores Zen's full-width editor.
When that compact address display is active, the native zoom reset button moves outside the URL field to avoid covering the domain. It returns to its original location when the compact display is off.

### Window tint

- `uc.blended-addressbar.window-tint.enabled`: tint the browser window with active page colors while preserving Zen's existing icon and text colors.
- `uc.blended-addressbar.window-tint.strength`: tint strength as a percentage from `0` to `100`; defaults to `25`.

Page colors are always remembered in memory while browsing. They are not saved across browser restarts.

### Split focus

The active pane’s inset highlight appears over 260ms and disappears over 90ms. System reduced-motion settings disable these transitions.

### Browser frame

Corner shape follows Zen's `layout.css.corner-shape.enabled` setting and `--zen-squircle-value`. The mod controls the radius. Split-page clipping uses Zen's curvature value, and the focus ring inherits the page's shape.

- `uc.blended-addressbar.frame-radius`: outer browser frame corner radius as a CSS length, such as `8px` or `0`. Defaults to `14px`.
- `uc.blended-addressbar.frame-radius.disabled`: remove browser frame rounding without changing the configured radius; disabled by default.
- `uc.blended-addressbar.frame-gap`: spacing around the browser frame, between split panes and beside an open sidebar, as a CSS length such as `5px` or `0`. Defaults to `var(--zen-element-separation)`, following Zen’s native spacing. Explicit saved values are preserved.
- `uc.blended-addressbar.frame-padding.disabled`: remove the browser frame padding and the visible split/sidebar gaps. Resize handles retain a small invisible hit area.
- `uc.blended-addressbar.addressbar-bookmarks-separator.disabled`: remove the separator between the addressbar and visible bookmarks bar; in Only Sidebar, remove the bookmarks bar's bottom separator.
- `uc.blended-addressbar.single-toolbar.bookmarks-always-visible`: keep bookmarks visible in Only Sidebar instead of revealing them on top-edge hover; disabled by default.
- `uc.blended-addressbar.frame-shadow`: choose the browser frame shadow preset: standard, minimal, or medium. Minimal adds a 0.5pt white inner highlight and a black outer shadow, both at 15% opacity, with a 0.5pt outer edge.

### Loading indicator

- `uc.loadbar.mode`: choose Default, Progress bar, URL bar glow, or Window edge. Default keeps Zen's native loader; the mod defaults to URL bar glow.
- `uc.loadbar.color`: fallback loadbar color when no page or header color is available.
- `uc.loadbar.focus-color`: use the browser focus color for Progress bar, URL bar glow, and Window edge instead of the header foreground; enabled by default.
- `uc.loadbar.iridescent`: add a subtle color shift to the moving URL bar glow; disabled by default. System reduced-motion settings disable the animation and progress transitions.
- `uc.loadbar.height`: loading bar thickness for all custom loadbar styles.
- `uc.loadbar.opacity`: loading bar body opacity and glow intensity for all custom loadbar styles.
- `uc.loadbar.roundedcorner`: enable right-side rounded corners for Progress bar, URL bar glow, and Window edge.
- `uc.loadbar.shadow`: enable shadow for Progress bar and Window edge.

URL bar glow adds a soft gradient across the whole field, a moving bright tip and a gently breathing progress line while loading. Rendered page colors update as they paint during loading. Reduced-motion settings disable the breathing animation. It follows each browser’s loading progress, with an estimate when progress is unavailable and a short completion fade. It uses the existing focus color setting, or the local header foreground when that setting is off.

## License

[MIT](https://github.com/igeag/blended-addressbar/blob/main/LICENSE).

## Credits

**Original creator and author:** [Kostiantyn Kugot (@kkugot)](https://github.com/kkugot), who created [Blended Addressbar](https://github.com/kkugot/blended-addressbar) and its core features. This repository is an independent fork adding the Arc-inspired toolbar display options above. The original MIT copyright notice is preserved in [LICENSE](LICENSE).

The sampler adapts ideas from [caezium/zen-page-tint](https://github.com/caezium/zen-page-tint), especially the `requestAnimationFrame` scheduling pattern, persistent content sampler, and bounded page-color cache.

The moving glow and per-pane address controls take design inspiration from [z1n-k/zia](https://github.com/z1n-k/zia). This implementation keeps Zen’s native editor and uses the mod’s own color and layout helpers.

