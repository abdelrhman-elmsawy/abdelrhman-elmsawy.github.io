# Portfolio audit — 2026-10-03

## Repository structure
The main branch contains the expected portfolio HTML, supporting CSS, assets, PDFs, SEO files, manifest, and workflows.

## Static integrity checks
- index.html has doctype, html/head/body closures.
- index.html has one phase5.css stylesheet reference.
- Navbar is fixed.
- Duplicate HTML IDs were not found.
- Local src/href references resolved against the repository tree.

## Issues found and isolated on audit branch
1. index.html references an optional #copyEmail element, but no such element exists. The handler is already guarded by `if(copyEmailBtn)`, so this is harmless dead code.
2. index.html calls `closeCert()` from the Escape-key handler, but no `closeCert` function is declared. This is guarded on the audit branch with `typeof closeCert === "function"`, eliminating the runtime error when Escape is pressed.

## Phase 5 stylesheet review
The stylesheet is valid plain CSS in structure, but selectors such as `.project-card`, `.skill-card`, and `.cert-card` do not match the actual main-page classes (`.project`, `.skill-group`, `.training`). Those rules are currently inert rather than breaking the page.

## Workflows
`.github/workflows/enable-phase5.yml` intentionally modifies index.html on pushes to main. It should be treated as a one-time migration workflow, not as a permanent recurring build step.

## Verification boundary
A true browser runtime test, HTML validator, CSS parser, and PDF/image decode test were not available through the connected GitHub API alone. The repository-level/static checks above are verified from the current main tree.
