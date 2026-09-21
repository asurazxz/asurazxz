# GitHub Profile README Design

## Purpose

Create a public GitHub profile README for `asurazxz` that introduces Denz as an aspiring software developer in Singapore. The profile should communicate curiosity, active exploration across software engineering, and personality through real project work rather than presenting a conventional resume.

## Success Criteria

- The README appears correctly on the `asurazxz` GitHub profile.
- Software engineering is the clear focus within the first screen.
- Selected public projects are described accurately and link to their repositories.
- Photography appears only as a secondary personal interest.
- The presentation feels clean, sleek, and editorial in both GitHub light and dark themes.
- The profile remains useful if custom images fail to load.
- The repository has no runtime or third-party statistics dependencies.

## Content Structure

### Editorial Header

Open with the name “Denz” and the description “aspiring software developer in Singapore.” Add one concise supporting line about exploring software engineering by building practical products.

### Currently Exploring

Describe an intentionally broad learning direction without claiming a premature specialization. Emphasize full-stack web development, product-focused engineering, reliable systems, and learning through hands-on projects.

### Selected Work

Feature two software projects:

1. **Resilience** — the primary project. Describe it as a mobile-first finance-planning PWA for Singapore platform workers. Mention its relevant technologies: React, TypeScript, FastAPI, PostgreSQL, Supabase, and optional Gemini assistance.
2. **Eventus** — an event-management platform built with Node.js, Express, MongoDB, and EJS.

End this section with a link to browse all public repositories. Project descriptions must stay concise and must not imply that group work was completed individually.

### Tools and Technologies

Show a restrained, grouped list covering languages, frontend, backend, and data technologies demonstrated by the selected repositories. Avoid a large badge wall and avoid implying mastery.

### Beyond Code

Include one sentence describing photography as a creative side hobby. Link to the `photography-portfolio` repository without presenting it as a primary software-engineering project.

### Footer

Close with a simple invitation to explore the repositories. Do not include visitor counters, generic activity statistics, trophy cards, or other decorative metrics.

## Visual System

Use a blue-accent editorial style.

- **Light theme:** warm off-white background, deep navy text, and cobalt-blue accents.
- **Dark theme:** near-black navy background, soft white text, and brighter blue accents.
- **Typography:** modern sans-serif styling with a subtle monospace detail.
- **Composition:** generous spacing, short sections, thin dividers, and a compact project layout.
- **Restraint:** no animated typing, oversized badge collections, or distracting decoration.

Create separate light and dark header SVGs and select them with GitHub-supported `<picture>` markup. The SVGs must use strong contrast and legible type. The README must supply descriptive alternative text, and no meaning may depend on color alone.

## Repository Structure

```text
README.md
assets/
  header-light.svg
  header-dark.svg
docs/superpowers/specs/
  2026-09-21-github-profile-readme-design.md
```

The implementation should use GitHub-flavored Markdown and only the small amount of supported HTML needed for the theme-aware header and project layout. Project data will be maintained directly in the README. No JavaScript, build process, dynamic statistics service, or runtime dependency is required.

## Repository Configuration

The GitHub repository has been renamed to `asurazxz`, matching the account name. During implementation, update the local `origin` remote from `asurazxz/asurazxz.github.io.git` to `asurazxz/asurazxz.git`.

## Verification

- Confirm `origin` points to the renamed repository.
- Validate the syntax of both SVG assets.
- Confirm all local image paths resolve from the README.
- Confirm all repository and profile links are reachable.
- Review the Markdown hierarchy and supported HTML structure.
- Inspect the header in representative light and dark contexts.
- Confirm the README remains understandable with images unavailable.
- Review claims against the public repository documentation for Resilience, Eventus, and the photography portfolio.

## Out of Scope

- A GitHub Pages website
- Automated repository discovery
- Dynamic contribution or language statistics
- Contact forms or private contact details
- A detailed resume, employment history, or fixed engineering specialization
