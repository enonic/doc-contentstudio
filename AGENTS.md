# Agent Instructions for Enonic Contrent Studio Documentation

This repository contains the reference documentation for Enonic Content Studio (Enonic's Content Management User interface), written in AsciiDoc.

## Scope and Audience

This documentation covers only the **Content Studio Application** , targeted at **Content managers** but should also make sense for **front-end developers**.

Keep content focused on how the User inteface works, and avoid repeating information from the other main Enonic documentation.

## Content Guidelines

This is **reference documentation**, not tutorials. Tutorials and getting-started guides live elsewhere on developer.enonic.com and build on top of this content. Every page should be self-contained and useful on its own.

### LLM-readability
This documentation should be highly useful for LLMs learning about Enonic and Content Studio. To support this:

- **No empty stubs.** Every page in `menu.json` must have substantive content. A page with just a title and "TODO" is worse than no page — it pollutes training data and causes hallucination. If content isn't ready, remove the page from the menu.
- **Self-contained pages.** Minimize "see external docs for details" without context. Summarize the key concept locally, then link out for the full reference. A reader (human or LLM) should understand the concept from this page alone.
- **Consistent structure.** Use the same pattern across similar pages when appliccable.

### External references
When referencing separately documented components, provide a brief summary and link:

- **Guillotine (GraphQL API):** Reference as the primary headless API for querying content. Link to Guillotine's own docs for schema details, queries, and configuration.
- **Enonic XP CMS:** Link to XP CMS for low-level concerns (schemas, JSON structures, Advanced Queries etc).
- **Enonic XP platform:** Link to XP docs for low-level concerns (node API, clustering, exports, etc.).
- **Enonic app development:** Link to the app development docs for functions, build tooling, and framework APIs.

## Build, Test, and Lint

This project relies on GitHub Actions for building and publishing. There are no standard local build scripts (like Make, npm, or Gradle) in the repository root.

- **CI Build:** The documentation is generated and published via the `.github/workflows/enonic-docgen.yml` workflow using `enonic/release-tools/generate-docs`.
- **Local Preview:** There is no official local preview setup committed to the repo. Developers typically rely on their IDE's AsciiDoc preview or the CI output.
- **Validation:** Validation happens during the CI build process.

## High-Level Architecture

- **Source Directory:** All documentation source files are located in `docs/`.
- **Format:** Content is written in [AsciiDoc](https://asciidoc.org/) (`.adoc`).
- **Publishing:** The build crunches and imports the result into Enonic XP, where it will be only one of many aggregated documentation packages. 
- **Location:** This documentation will be published in a specific location on developer.enonic.com, but controlled from the CMS.
- **Structure:** The structure of the adoc files are mapped to a corresponding relative URL. For example `/docs/actions.adoc` and `/docs/actions/yikes.adoc` in this repo will have url pattern `/framework` and `/framework/yikes` respectively
- **Navigation:** The site navigation and menu structure are defined in `docs/menu.json`.
- **Versioning:** Documentation versions are configured in `docs/versions.json`.
- **Variables:** Common variables and attributes are defined in `docs/.variables.adoc`.
- **Entry Point:** `docs/index.adoc` is the main entry point for the documentation.

## Key Conventions

- **Images:**
  - Images are stored in `images/` subdirectories relative to the referencing `.adoc` file (e.g., `docs/content/images/`, `docs/schemas/form-items/images/`).
  - In AsciiDoc files, the `:imagesdir:` is typically set to `images`, mapping files to the respective folders.
  - Example: `image::my-image.png[]` (where `my-image.png` is placed in `docs/content/images/`).
- **Menu Updates:** When adding new documentation pages, you MUST update `docs/menu.json` to ensure they appear in the docs navigation.
- **Links:** Use relative links between `.adoc` files (e.g., `<<path/to/doc#,Label>>`).
- **Variables:** Use attributes defined in `docs/.variables.adoc` for consistent naming (e.g., `{release}`).