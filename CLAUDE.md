# CLAUDE.md

This file provides SuiteCRM-specific guidance for this assignment workspace.

## Project Context

- Target codebase: `Fixthis/SuiteCRM`
- Product: SuiteCRM 7.15.x (PHP CRM platform)
- Feature target: custom dashboard widget (dashlet)
- Assignment phases: V1.0 exploration, V1.1 rules tuning, V1.2 feature delivery

## Verified Stack

- Language: PHP 8.1+
- Package manager: Composer
- Backend framework style: SugarCRM/SuiteCRM module architecture
- Template layer: Smarty template files (`*.tpl`) in many dashlets
- Test tooling in repo: PHPUnit and Codeception (from `composer.json`)

## Architecture Map (High Level)

- Front controller and entry points: `index.php`, `Api/`, multiple legacy entry scripts.
- Core framework: `include/`, `data/`, `modules/`, `service/`.
- Module implementation: `modules/<ModuleName>/...`.
- Customization-safe extensions: `custom/`.
- Dashlet framework core: `include/Dashlets/`.
- Dashlet rebuild utility: `modules/Administration/RebuildDashlets.php`.

## Dashlet Patterns To Follow

- Existing dashlets are under `modules/*/Dashlets/<DashletName>/`.
- Typical files:
	- `<DashletName>.php` (class, usually extends `DashletGeneric`)
	- `<DashletName>.meta.php` (registration metadata in `$dashletMeta`)
	- `<DashletName>.data.php` (search fields and columns in `$dashletData`)
	- optional `*.tpl` and `*.js`
- For custom work, prefer `custom/modules/<ModuleName>/Dashlets/<DashletName>/` to avoid core-file edits.

## Local Commands

```bash
# from Fixthis/SuiteCRM
composer install

# run phpunit (after env setup)
vendor/bin/phpunit

# run codeception suite (if configured locally)
vendor/bin/codecept run
```

Note: Full SuiteCRM test execution may require DB/app configuration; record any constraints in `writeup.md`.

## Scoped Rules (V1.1)

Rule 1
- Scope: `SuiteCRM/modules/*/Dashlets/**/*.php` and `SuiteCRM/custom/modules/*/Dashlets/**/*.php`
- Requirement: Follow existing dashlet structure (`.php`, `.meta.php`, `.data.php`) and naming patterns.

Rule 2
- Scope: `SuiteCRM/custom/**`
- Requirement: New feature code should go in `custom/` whenever possible; avoid editing core framework files under `include/` or base module files unless unavoidable.

Rule 3
- Scope: `SuiteCRM/**/*.php`
- Requirement: Preserve SuiteCRM legacy conventions used nearby (array style, globals where framework requires them, entry-point guards, translation helpers).

Rule 4
- Scope: `SuiteCRM/tests/**` and feature files touched in `SuiteCRM/custom/**`
- Requirement: Add verification first (or alongside minimal test harness) before implementation changes; record failing-to-passing evidence.

## Feature Delivery Protocol

1. Write acceptance criteria for the custom dashlet in Given/When/Then.
2. Add failing verification (test or reproducible check steps) first.
3. Implement dashlet in `custom/modules/.../Dashlets/...`.
4. Rebuild dashlet cache and verify widget appears in Add Dashlets dialog.
5. Run feasible tests and capture no-regression evidence.

## Gotchas

- Dashlets may not be recognized until cache rebuild.
- SuiteCRM has legacy and modernized PHP mixed together; nearest-neighbor style is safer than broad refactors.
- Environment-dependent tests can fail without full SuiteCRM runtime config.
