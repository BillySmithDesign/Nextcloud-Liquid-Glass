# Nextcloud Liquid Glass

A macOS / iOS-inspired custom CSS theme for Nextcloud, focused on a cleaner Finder-like Files experience, translucent glass surfaces, softer controls, and a more polished Dashboard.

## Features

- Dark-first macOS / iOS-inspired Liquid Glass styling
- Finder-like Files interface
- Softer sidebars, toolbars, buttons, inputs, modals, and popovers
- Refined glass-card Dashboard styling
- Nextcloud 34.x Dashboard panel override for `.panels > .panel`
- Finder-like Dashboard recommendation/activity rows
- Light-mode support
- Mobile-friendly visual refinements
- Avoids forcing Nextcloud's core Files grid/table layouts
- Avoids overriding core scroll containers

## Requirements

- A working Nextcloud installation
- Administrator access
- The **Custom CSS** app enabled in Nextcloud

## Install

### Browser method

1. In Nextcloud, open **Apps**.
2. Search for and enable **Custom CSS**.
3. Open **Administration settings → Theming → Custom CSS**.
4. Copy the contents of `nextcloud-liquid-glass.css` into the Custom CSS field.
5. For Nextcloud 34.x, append `nextcloud-34-dashboard-fix.css` after the base stylesheet.
6. Save, then hard-refresh the browser (`Cmd + Shift + R` on macOS or `Ctrl + Shift + R` on Windows/Linux).

### Docker / OCC method

On some Nextcloud builds the browser Custom CSS editor may remain stuck on **Saving…** for larger stylesheets. In that case, apply the theme through `occ` instead.

```bash
curl -fsSL https://raw.githubusercontent.com/BillySmithDesign/Nextcloud-Liquid-Glass/main/nextcloud-liquid-glass.css -o /tmp/nextcloud-liquid-glass.css
curl -fsSL https://raw.githubusercontent.com/BillySmithDesign/Nextcloud-Liquid-Glass/main/nextcloud-34-dashboard-fix.css -o /tmp/nextcloud-34-dashboard-fix.css
cat /tmp/nextcloud-liquid-glass.css /tmp/nextcloud-34-dashboard-fix.css > /tmp/nextcloud-liquid-glass-final.css

docker exec -u www-data nextcloud php occ config:app:set theming_customcss customcss --value="$(cat /tmp/nextcloud-liquid-glass-final.css)"
```

Then hard-refresh the browser.

If your container uses a different name, replace `nextcloud` with that container name.

## Optional: remove folder README / Rich Workspace headers

Nextcloud can display a folder `Readme.md` as a large Rich Workspace panel at the top of Files. To disable those panels globally:

```bash
docker exec -u www-data nextcloud php occ config:app:set text workspace_available --value=0
```

This does not delete Markdown files; it only removes the automatic folder-top workspace preview.

## Important

Nextcloud's frontend classes can change between releases. This theme intentionally avoids structural overrides such as forced `display`, `grid-template-columns`, `table-layout`, fixed file-column widths, or core `overflow` rules, because those can break the Files interface and responsive layouts.

The Nextcloud 34.x Dashboard currently uses Vue-scoped component attributes in addition to `.panels > .panel`. The compatibility override therefore includes both a generic selector and the currently observed scoped selector. If a future Nextcloud release regenerates the Vue scope ID, the generic selector should remain the preferred fallback.

## Recovery if CSS breaks the UI

Clear the custom CSS from the command line inside the Nextcloud container:

```bash
docker exec -u www-data nextcloud php occ config:app:set theming_customcss customcss --value=""
```

Then hard-refresh the browser.

## What this theme changes

The stylesheet focuses on visual styling:

- Global header and unified search
- Left navigation sidebar
- Files toolbar, file rows, metadata and actions
- Inputs, buttons and focus states
- Settings cards
- Modals and menus
- Right sidebar
- Scrollbar appearance
- Dashboard greeting and weather chip
- Dashboard glass panels, widgets, recommendation/activity rows and empty states
- Light-mode appearance

## Files in this repo

- `nextcloud-liquid-glass.css` — base theme
- `nextcloud-34-dashboard-fix.css` — Nextcloud 34.x Dashboard compatibility + final glass refinements
- `README.md` — installation, recovery and compatibility notes

## Screenshots

Screenshots are welcome in `screenshots/` to show the Files, Dashboard and Settings views. Pull requests for selector fixes across different Nextcloud versions are also welcome.

## Compatibility

This project was developed against a modern Docker-based Nextcloud installation and tested with Nextcloud 34.x Dashboard markup. Exact appearance may vary by Nextcloud version, enabled apps, browser, and theme settings.

## Contributing

Issues and pull requests are welcome. When reporting a visual problem, please include:

- Nextcloud version
- Browser and version
- Screenshot
- The page/app affected
- Any relevant element/class name from browser developer tools

## License

Apache License 2.0. See `LICENSE`.

## Disclaimer

This is an unofficial community theme and is not affiliated with or endorsed by Nextcloud, Apple, or their respective product-design teams.
