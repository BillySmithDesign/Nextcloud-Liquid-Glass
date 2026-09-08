# Nextcloud Liquid Glass

A macOS / iOS-inspired custom CSS theme for Nextcloud, focused on a cleaner Finder-like Files experience, translucent glass surfaces, softer controls, and a more polished Dashboard.

## Features

- Dark-first macOS / iOS-inspired Liquid Glass styling
- Finder-like Files interface
- Softer sidebars, toolbars, buttons, inputs, modals, and popovers
- Dashboard glass-card styling
- Light-mode support
- Mobile-friendly visual refinements
- Avoids forcing Nextcloud's core Files grid/table layouts
- Avoids overriding core scroll containers

## Requirements

- A working Nextcloud installation
- Administrator access
- The **Custom CSS** app enabled in Nextcloud

## Install

1. In Nextcloud, open **Apps**.
2. Search for and enable **Custom CSS**.
3. Open **Administration settings → Theming → Custom CSS**.
4. Copy the contents of `nextcloud-liquid-glass.css` into the Custom CSS field.
5. Save, then hard-refresh the browser (`Cmd + Shift + R` on macOS or `Ctrl + Shift + R` on Windows/Linux).

## Important

Nextcloud's frontend classes can change between releases. This theme intentionally avoids structural overrides such as forced `display`, `grid-template-columns`, `table-layout`, fixed file-column widths, or core `overflow` rules, because those can break the Files interface and responsive layouts.

If a Nextcloud update changes component class names, some cosmetic rules may stop applying until the selectors are updated.

## Recovery if CSS breaks the UI

If the Custom CSS makes a page difficult to use, clear the custom CSS from the command line inside the Nextcloud container.

Example for a Docker container named `nextcloud`:

```bash
docker exec -u www-data nextcloud php occ config:app:set theming_customcss customcss --value=""
```

Then hard-refresh the browser.

If your container uses a different name, replace `nextcloud` with that container name.

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
- Dashboard greeting, weather chip, widgets and empty states
- Light-mode appearance

## Screenshots

Screenshots are welcome in `screenshots/` to show the Files, Dashboard and Settings views. Pull requests for selector fixes across different Nextcloud versions are also welcome.

## Compatibility

This project was developed against a modern Docker-based Nextcloud installation. Exact appearance may vary by Nextcloud version, enabled apps, browser, and theme settings.

## Contributing

Issues and pull requests are welcome. When reporting a visual problem, please include:

- Nextcloud version
- Browser and version
- Screenshot
- The page/app affected
- Any relevant element/class name from browser developer tools

## License

MIT License. See `LICENSE`.

## Disclaimer

This is an unofficial community theme and is not affiliated with or endorsed by Nextcloud, Apple, or their respective product-design teams.
