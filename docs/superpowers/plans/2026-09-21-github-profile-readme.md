# GitHub Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a clean, blue-accent GitHub profile README that introduces Denz as an aspiring software developer in Singapore and highlights selected public projects.

**Architecture:** Keep the profile dependency-free: one GitHub-flavored Markdown document and two theme-specific SVG header assets selected with `<picture>`. All project copy is maintained directly in the README, and verification uses built-in PowerShell, XML parsing, Git, and GitHub's public endpoints.

**Tech Stack:** GitHub-flavored Markdown, supported inline HTML, SVG 1.1, PowerShell, Git

**Spec:** `docs/superpowers/specs/2026-09-21-github-profile-readme-design.md`

## Global Constraints

- The repository must remain a public profile repository named exactly `asurazxz` with a non-empty root `README.md`.
- Software engineering must be the clear focus within the first screen.
- Use a blue-accent editorial style that supports GitHub light and dark themes.
- Use no JavaScript, build process, runtime dependency, third-party statistics service, visitor counter, trophy card, or animated typing effect.
- Describe Resilience and Eventus accurately without implying that group work was completed individually.
- Present photography only as a secondary creative hobby.
- The README must remain understandable when images are unavailable.

## Review Focus

- GitHub dark-theme selection must resolve `assets/header-dark.svg`; the light/default fallback must resolve `assets/header-light.svg`.
- Both SVGs must parse as XML and expose the same meaningful title, description, and visible copy.
- All local image paths and public repository links must resolve without redirects to missing resources.
- Project wording must identify collaborative work and avoid unsupported claims of expertise or ownership.
- The README's headings and text must remain coherent if the `<picture>` block is not rendered, and the image must provide complete descriptive alternative text.

---

### Task 1: Point the Checkout at the Profile Repository

**Files:**
- Modify: `.git/config` through `git remote set-url`

**Interfaces:**
- Consumes: the existing `origin` remote and the renamed public repository at `https://github.com/asurazxz/asurazxz.git`
- Produces: an `origin` remote whose fetch and push URLs both target the profile repository

- [ ] **Step 1: Record the failing configuration check**

Run:

```powershell
$expected = 'https://github.com/asurazxz/asurazxz.git'
$actual = git remote get-url origin
if ($actual -ne $expected) { throw "origin is '$actual'; expected '$expected'" }
```

Expected: FAIL because `origin` still targets `asurazxz.github.io.git`.

- [ ] **Step 2: Update the remote URL**

Run:

```powershell
git remote set-url origin https://github.com/asurazxz/asurazxz.git
```

- [ ] **Step 3: Verify local configuration and remote reachability**

Run:

```powershell
$expected = 'https://github.com/asurazxz/asurazxz.git'
$actual = git remote get-url origin
if ($actual -ne $expected) { throw "origin is '$actual'; expected '$expected'" }
git ls-remote --exit-code origin HEAD
```

Expected: the URL check passes and `git ls-remote` prints the current `HEAD` hash.

---

### Task 2: Create the Theme-Aware Editorial Header

**Files:**
- Create: `assets/header-light.svg`
- Create: `assets/header-dark.svg`

**Interfaces:**
- Consumes: the approved identity copy and blue visual system from the specification
- Produces: two 1200×360 SVG images with identical semantic content and theme-specific colors

- [ ] **Step 1: Run the asset contract before the files exist**

Run:

```powershell
$paths = @('assets/header-light.svg', 'assets/header-dark.svg')
foreach ($path in $paths) {
  if (-not (Test-Path -LiteralPath $path)) { throw "Missing $path" }
  [xml]$svg = Get-Content -LiteralPath $path -Raw
  if ($svg.svg.viewBox -ne '0 0 1200 360') { throw "$path has the wrong viewBox" }
}
```

Expected: FAIL with `Missing assets/header-light.svg`.

- [ ] **Step 2: Create the light header**

Create `assets/header-light.svg` with this complete content:

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="360" viewBox="0 0 1200 360" role="img" aria-labelledby="title description">
  <title id="title">Denz — aspiring software developer in Singapore</title>
  <desc id="description">A clean blue editorial banner introducing Denz and an interest in building useful, dependable software.</desc>
  <rect width="1200" height="360" rx="28" fill="#F7F9FC"/>
  <path d="M0 28A28 28 0 0 1 28 0h1144a28 28 0 0 1 28 28v304a28 28 0 0 1-28 28H28A28 28 0 0 1 0 332V28Z" fill="none" stroke="#D7E1F4"/>
  <circle cx="1080" cy="74" r="136" fill="#E8F0FF"/>
  <circle cx="1080" cy="74" r="78" fill="#D8E6FF"/>
  <path d="M928 282h188" stroke="#2563EB" stroke-width="4" stroke-linecap="round"/>
  <path d="M1068 266l48 16-48 16" fill="none" stroke="#2563EB" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
  <text x="82" y="82" fill="#2563EB" font-family="ui-monospace, SFMono-Regular, Menlo, Consolas, monospace" font-size="18" font-weight="700" letter-spacing="4">HELLO, I’M</text>
  <text x="78" y="190" fill="#10213D" font-family="Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, sans-serif" font-size="104" font-weight="750" letter-spacing="-5">Denz.</text>
  <text x="82" y="240" fill="#41526D" font-family="Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, sans-serif" font-size="24" font-weight="600">Aspiring software developer · Singapore</text>
  <text x="82" y="294" fill="#66758C" font-family="Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, sans-serif" font-size="19">Exploring software engineering by building useful, dependable products.</text>
</svg>
```

- [ ] **Step 3: Create the dark header**

Create `assets/header-dark.svg` with this complete content:

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="360" viewBox="0 0 1200 360" role="img" aria-labelledby="title description">
  <title id="title">Denz — aspiring software developer in Singapore</title>
  <desc id="description">A clean blue editorial banner introducing Denz and an interest in building useful, dependable software.</desc>
  <rect width="1200" height="360" rx="28" fill="#0B1220"/>
  <path d="M0 28A28 28 0 0 1 28 0h1144a28 28 0 0 1 28 28v304a28 28 0 0 1-28 28H28A28 28 0 0 1 0 332V28Z" fill="none" stroke="#22314D"/>
  <circle cx="1080" cy="74" r="136" fill="#101F3D"/>
  <circle cx="1080" cy="74" r="78" fill="#152B55"/>
  <path d="M928 282h188" stroke="#60A5FA" stroke-width="4" stroke-linecap="round"/>
  <path d="M1068 266l48 16-48 16" fill="none" stroke="#60A5FA" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
  <text x="82" y="82" fill="#60A5FA" font-family="ui-monospace, SFMono-Regular, Menlo, Consolas, monospace" font-size="18" font-weight="700" letter-spacing="4">HELLO, I’M</text>
  <text x="78" y="190" fill="#F2F6FC" font-family="Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, sans-serif" font-size="104" font-weight="750" letter-spacing="-5">Denz.</text>
  <text x="82" y="240" fill="#C7D2E3" font-family="Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, sans-serif" font-size="24" font-weight="600">Aspiring software developer · Singapore</text>
  <text x="82" y="294" fill="#91A1BA" font-family="Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, sans-serif" font-size="19">Exploring software engineering by building useful, dependable products.</text>
</svg>
```

- [ ] **Step 4: Validate structure, semantic parity, and required contrast colors**

Run:

```powershell
$light = [xml](Get-Content -LiteralPath 'assets/header-light.svg' -Raw)
$dark = [xml](Get-Content -LiteralPath 'assets/header-dark.svg' -Raw)
foreach ($entry in @(@('light', $light), @('dark', $dark))) {
  $name = $entry[0]
  $svg = $entry[1].svg
  if ($svg.viewBox -ne '0 0 1200 360') { throw "$name viewBox mismatch" }
  if ($svg.role -ne 'img') { throw "$name role mismatch" }
  if ($svg.'aria-labelledby' -ne 'title description') { throw "$name accessible label mismatch" }
}
if ($light.svg.title -ne $dark.svg.title) { throw 'Theme titles differ' }
if ($light.svg.desc -ne $dark.svg.desc) { throw 'Theme descriptions differ' }
$lightRaw = Get-Content -LiteralPath 'assets/header-light.svg' -Raw
$darkRaw = Get-Content -LiteralPath 'assets/header-dark.svg' -Raw
if ($lightRaw -notmatch '#10213D' -or $lightRaw -notmatch '#2563EB') { throw 'Light palette incomplete' }
if ($darkRaw -notmatch '#F2F6FC' -or $darkRaw -notmatch '#60A5FA') { throw 'Dark palette incomplete' }
```

Expected: PASS with no output.

- [ ] **Step 5: Commit the header assets**

```powershell
git add -- assets/header-light.svg assets/header-dark.svg
git commit -m "feat: add theme-aware profile header"
```

---

### Task 3: Write the Editorial Profile README

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: `assets/header-light.svg`, `assets/header-dark.svg`, and the verified public repository descriptions
- Produces: the complete profile content rendered by GitHub at `https://github.com/asurazxz`

- [ ] **Step 1: Run the README content contract against the existing one-line file**

Run:

```powershell
$readme = Get-Content -LiteralPath 'README.md' -Raw
$required = @(
  'assets/header-light.svg',
  'assets/header-dark.svg',
  '## Building to learn',
  '## Selected work',
  'https://github.com/asurazxz/Resilience',
  'https://github.com/asurazxz/Eventus',
  '## Tools I’ve worked with',
  '## Beyond code'
)
foreach ($value in $required) {
  if (-not $readme.Contains($value)) { throw "README missing: $value" }
}
```

Expected: FAIL because the current README contains only the old repository title.

- [ ] **Step 2: Replace the README with the approved editorial content**

Write this complete content to `README.md`:

```markdown
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/header-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/header-light.svg">
  <img alt="Denz — aspiring software developer in Singapore. Exploring software engineering by building useful, dependable products." src="./assets/header-light.svg" width="100%">
</picture>

## Building to learn

I’m Denz, an aspiring software developer in Singapore. I’m exploring software engineering broadly by turning ideas into practical products, learning how the interface, application logic, and data layer fit together along the way.

Right now, I’m interested in:

- building thoughtful full-stack web experiences;
- making product decisions around real user needs; and
- understanding the reliable systems behind polished interfaces.

## Selected work

<table>
  <tr>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/asurazxz/Resilience">Resilience</a></h3>
      <p>A team-built, mobile-first finance-planning PWA designed around the variable weekly income of Singapore platform workers.</p>
      <p><code>React</code> <code>TypeScript</code> <code>FastAPI</code> <code>PostgreSQL</code> <code>Supabase</code></p>
    </td>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/asurazxz/Eventus">Eventus</a></h3>
      <p>A collaborative event-management platform built as an SMU web application development project.</p>
      <p><code>Node.js</code> <code>Express</code> <code>MongoDB</code> <code>EJS</code></p>
    </td>
  </tr>
</table>

→ [Browse all public repositories](https://github.com/asurazxz?tab=repositories)

## Tools I’ve worked with

| Area | Technologies |
| --- | --- |
| Languages | TypeScript, JavaScript, Python, SQL, HTML & CSS |
| Frontend | React, Vite, Tailwind CSS, EJS |
| Backend | Node.js, Express, FastAPI |
| Data | PostgreSQL, MongoDB, Supabase |

## Beyond code

Photography is a creative side hobby of mine—I’m also experimenting with how to present that work through a [small editorial portfolio](https://github.com/asurazxz/photography-portfolio).

---

<sub>Still exploring, still building. Take a look around the repositories to see what I’m learning next.</sub>
```

- [ ] **Step 3: Verify content, fallback semantics, and honest attribution**

Run:

```powershell
$readme = Get-Content -LiteralPath 'README.md' -Raw
$required = @(
  'media="(prefers-color-scheme: dark)"',
  'assets/header-dark.svg',
  'assets/header-light.svg',
  '## Building to learn',
  '## Selected work',
  'team-built',
  'collaborative',
  '## Tools I’ve worked with',
  '## Beyond code'
)
foreach ($value in $required) {
  if (-not $readme.Contains($value)) { throw "README missing: $value" }
}
if ($readme -match 'visitor|troph|github-readme-stats|typing-svg') { throw 'Disallowed decorative dependency found' }
$alt = [regex]::Match($readme, '<img alt="([^"]+)"').Groups[1].Value
if ($alt -notmatch 'aspiring software developer in Singapore') { throw 'Fallback alt text is incomplete' }
```

Expected: PASS with no output.

- [ ] **Step 4: Verify every local asset and public repository target**

Run:

```powershell
$readme = Get-Content -LiteralPath 'README.md' -Raw
$localAssets = [regex]::Matches($readme, '(?:src|srcset)="\./([^"]+)"') | ForEach-Object { $_.Groups[1].Value } | Sort-Object -Unique
foreach ($asset in $localAssets) {
  if (-not (Test-Path -LiteralPath $asset)) { throw "Missing local asset: $asset" }
}
$repos = @('Resilience', 'Eventus', 'photography-portfolio')
foreach ($repo in $repos) {
  git ls-remote --exit-code "https://github.com/asurazxz/$repo.git" HEAD | Out-Null
  if ($LASTEXITCODE -ne 0) { throw "Repository unavailable: $repo" }
}
```

Expected: PASS with no output.

- [ ] **Step 5: Commit the README**

```powershell
git add -- README.md
git commit -m "feat: publish editorial GitHub profile"
```

---

### Task 4: Perform Final Profile Verification

**Files:**
- Verify: `README.md`
- Verify: `assets/header-light.svg`
- Verify: `assets/header-dark.svg`
- Verify: `docs/superpowers/specs/2026-09-21-github-profile-readme-design.md`

**Interfaces:**
- Consumes: the complete profile implementation from Tasks 1–3
- Produces: a clean, committed branch ready to push to GitHub

- [ ] **Step 1: Run the complete structural verification**

Run:

```powershell
$ErrorActionPreference = 'Stop'
$expectedRemote = 'https://github.com/asurazxz/asurazxz.git'
if ((git remote get-url origin) -ne $expectedRemote) { throw 'origin mismatch' }
[xml]$light = Get-Content -LiteralPath 'assets/header-light.svg' -Raw
[xml]$dark = Get-Content -LiteralPath 'assets/header-dark.svg' -Raw
if ($light.svg.viewBox -ne $dark.svg.viewBox) { throw 'Theme dimensions differ' }
$readme = Get-Content -LiteralPath 'README.md' -Raw
if ($readme.Length -lt 1000) { throw 'README is unexpectedly short' }
if (-not $readme.Contains('<picture>') -or -not $readme.Contains('</picture>')) { throw 'Theme picture block is incomplete' }
git diff --check
if ($LASTEXITCODE -ne 0) { throw 'Whitespace validation failed' }
```

Expected: PASS with no output.

- [ ] **Step 2: Inspect both headers as rendered images**

Open `assets/header-light.svg` and `assets/header-dark.svg` with the workspace image viewer. Confirm that neither image clips the name, role, location, supporting sentence, arrow, or rounded border at 1200×360.

- [ ] **Step 3: Review the README without its image block**

Temporarily reason from the content beginning at `## Building to learn`. Confirm that it independently identifies Denz, location, development stage, current interests, collaborative project context, tools, and photography hobby. Do not modify the file for this check.

- [ ] **Step 4: Confirm repository state and recent commits**

Run:

```powershell
git status --short
git log -4 --oneline --decorate
```

Expected: no uncommitted implementation changes. The recent history includes the design, plan, header, and README commits.

- [ ] **Step 5: Report the completed local implementation**

Report the final commit hash, verification results, and the fact that the branch is ready to push. Do not push unless the user explicitly requests publication.
