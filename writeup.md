# writeup.md

## V1.0 - Exploration and Understanding

### Architecture Map

- Entry points:
   - Legacy web entry scripts like `index.php` and other root entry files.
   - API-related code under `Api/`.
- Core modules:
   - `include/` for framework utilities, including dashlet base classes.
   - `modules/` for business modules and many built-in dashlets.
   - `custom/` for customization-safe extensions.
- Data flow:
   - Request enters an entry point, routes through Suite/Sugar framework layers, then module classes/beans fetch and render data.
- Persistence layer:
   - Bean and framework-managed DB access patterns in module/domain code.
- Test organization:
   - PHPUnit and Codeception dependencies present in `composer.json`.
   - Test directories present under `tests/`.

### Exploration Log

- Date:
   - 2026-05-05
- Commands used:
   - Repository clone
   - Path search for dashlet-related files
   - Reads of representative dashlet source files and metadata
- Files inspected:
   - `SuiteCRM/composer.json`
   - `SuiteCRM/include/Dashlets/Dashlet.php` (path discovered)
   - `SuiteCRM/modules/Accounts/Dashlets/MyAccountsDashlet/MyAccountsDashlet.php`
   - `SuiteCRM/modules/Accounts/Dashlets/MyAccountsDashlet/MyAccountsDashlet.meta.php`
   - `SuiteCRM/modules/Accounts/Dashlets/MyAccountsDashlet/MyAccountsDashlet.data.php`
   - `SuiteCRM/modules/Administration/RebuildDashlets.php`
- Key findings:
   - Dashlets follow a strong file naming convention with class/meta/data triplets.
   - `DashletGeneric` is a common base for module listing-style dashlets.
   - Rebuilding dashlet cache is part of registration/visibility workflow.
   - Composer requires PHP 8.1+ and includes PHPUnit/Codeception in dev dependencies.

### Conventions Observed

- Naming conventions:
   - Dashlet class/folder/file names are aligned (e.g., `MyAccountsDashlet`).
   - Metadata arrays use framework globals (`$dashletMeta`, `$dashletData`).
- Layering conventions:
   - UI configuration and metadata are separated from class logic.
   - Framework extension points are strongly path-based.
- Error handling conventions:
   - Entry-point guard pattern (`if (!defined('sugarEntry') || !sugarEntry) die(...)`).
- Test patterns:
   - Existing test frameworks are PHPUnit and Codeception.
   - For assignment scope, include reproducible verification evidence if full runtime tests are environment-constrained.

## V1.1 - Rules and Context Tuning

### Initial Rules Added

1. Scope: `SuiteCRM/modules/*/Dashlets/**/*.php`, `SuiteCRM/custom/modules/*/Dashlets/**/*.php`
   Rule: Follow the class/meta/data file triplet and naming conventions used by existing dashlets.
2. Scope: `SuiteCRM/custom/**`
   Rule: Place new feature code in `custom/` first; avoid direct core edits under `include/` unless required.
3. Scope: `SuiteCRM/**/*.php`
   Rule: Preserve local coding style and framework-required patterns (entry guards, globals, translation helpers).

### Validation Task

- Prompt used:
   - "Create a new SuiteCRM custom dashlet by copying nearest-neighbor structure from existing module dashlets."
- Agent output summary:
   - Produced plan using class/meta/data files and `custom/modules/.../Dashlets/...` target path.
- What matched conventions:
   - Correct dashlet triplet structure.
   - Correct preference for customization-safe location.
- What did not match:
   - Did not initially include explicit cache rebuild verification step.

### Refinements

- Change made:
   - Added explicit rule/step requiring dashlet cache rebuild and post-add-dialog verification.
- Why:
   - Without rebuild, feature can appear broken even when files are correct.
- Outcome:
   - Instructions now better match real SuiteCRM operational behavior.

## V1.2 - Feature Addition

### Feature Specification

- Feature name:
   - Open Opportunities Summary Dashlet
- User story:
   - As a sales user, I want a dashboard widget that shows open opportunities assigned to me so I can quickly prioritize active deals.
- Acceptance criteria:
   - Given I am logged into SuiteCRM with opportunities assigned to me
   - When I add "Open Opportunities Summary" from the Add Dashlets dialog
   - Then the widget appears on my home dashboard with open opportunities and key fields (name, amount, close date, sales stage)
   - Given there are no matching opportunities
   - When the dashlet renders
   - Then it shows an empty-state message instead of failing
   - Given the dashlet files are installed in `custom/modules/.../Dashlets/...`
   - When admin rebuilds dashlet cache
   - Then the new dashlet is discoverable in the dashlet picker

### Test-First Timeline

- Failing tests added:
   - Pending
- Implementation pass:
   - Pending
- Refactor pass:
   - Pending

### Regression Verification

- Full suite command:
   - `vendor/bin/phpunit` (plus selective suite as environment allows)
- Result:
   - Pending environment setup
- Notes:
   - Full SuiteCRM test execution can require DB/application config.

## Evidence

- Links to key commits:
   - Pending
- Before/after examples of improved agent output:
   - Pending
