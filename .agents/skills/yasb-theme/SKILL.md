---
name: yasb-theme
description: Create, edit, and review this repository's YASB bar widgets, YAML configuration, and Sass styles. Use for YASB theme changes, default-setting cleanup, stylesheet compilation, and committing completed changes.
---

# YASB Theme Workflow

## Sources and files

- Consult https://docs.yasb.dev/latest for the relevant widget options, defaults, callbacks, and supported style selectors before making changes. Follow the relevant widget documentation rather than guessing names or defaults.
- Edit bar and widget configuration in `ctn/config.yaml`.
- Edit styles in `style.sass`, using its existing indented Sass syntax and conventions.
- Treat `ctn/styles.css` as generated output; do not edit it directly.
- Paths and commands below are relative to the repository root.

## Keep configuration and styles in sync

- When adding a widget to the configuration, add its matching styles to `style.sass` in the same change. Reuse shared rules where appropriate instead of duplicating declarations.
- Match selectors to the widget's documented classes and configured custom classes. Cover relevant labels, icons, states, and popups used by the widget.
- Keep YAML and Sass minimal, readable, and consistent with the surrounding code. Avoid unrelated reformatting or cleanup.
- Omit optional settings whose values equal documented defaults. Remove redundant default settings in the configuration you touch only after verifying that omission preserves behavior. Keep required fields and intentional overrides.
- If documentation is unavailable or a default is uncertain, retain the setting and report the uncertainty rather than guessing.
- Remove obsolete widget-specific styles when removing a widget, but preserve rules still shared by other widgets.

## Compile and validate

- After every completed Sass edit, compile from the repository root:

  ```sh
  sass --no-source-map style.sass ctn/styles.css
  ```

- `compile_auto.cmd` runs Sass in watch mode. Use the one-shot command above for agent work; do not start a persistent watcher.
- If Sass is unavailable or compilation fails, report the blocker. Do not claim the CSS is current or commit a broken or uncompiled style change as complete.
- Review the diff for consistent widget references and selectors, verified default removal, and unintended changes. Run applicable available validation. Distinguish successful compilation from visual verification in YASB; do not claim a runtime check unless performed.

## Commit completed work

- Check Git status before editing and preserve existing user changes.
- After successful validation, commit the completed task unless the user explicitly requests no commit. Include both Sass source and generated CSS when styles change.
- Stage only files or hunks belonging to the task; do not include unrelated user edits. Review the staged diff before committing.
- Use a short, imperative, capitalized commit subject, ideally at most 50 characters, without terminal punctuation. Add a body only when it provides useful context, wrapped at 72 characters.
- Do not push or create branches unless requested. Report any validation or commit blocker instead of implying success.
