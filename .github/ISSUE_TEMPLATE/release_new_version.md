---
name: 'For maintainers: Release a new version'
about: This is the Developer-only template which we use for tracking the process of future releases.
title: 'Prepare Release 3.y.z'
labels: release
assignees: ''
---

**Target timeline**
Feature freeze / Start of translation process: <!-- Add a date, usually about 6-8 weeks from the last release, e.g. 2021-04-20 -->
Approximate release date: <!-- Usually 2-3 weeks after starting translations, e.g. 2021-05-04 -->

**Checklist**
- [ ] Assign this issue to the release shepherd who is in charge of managing this checklist
- [ ] Create a milestone and add all relevant issues
- [ ] Ensure that all issues/PR targeted for this release are done by checking the milestone
- [ ] Declare a code freeze. PRs can still be worked on and may get reviewed, but must not be merged unless agreed explicitly.
- [ ] Create at least one beta release
- [ ] Get feedback on the stability of the beta release
- [ ] Website translations
  - [ ] Create new branch `translate3_y_z` based on branch `release`
  - [ ] Squash-merge `changes` into `translate3_y_z`
  - [ ] Ping translators. Translators should open PRs with their changes against the `translate3_y_z` branch (?) and reference this issue ("Add German translations for 3.y.z")
  - [ ] Wait for all PRs to be merged
  - [ ] Merge `translate3_y_z` into release
- [ ] App installer translations
  - [ ] Ping translators
  - [ ] Review PRs, <details><summary>Checklist for the PRs</summary>
    ```
    - [ ] Translator listed in the `src/util.cpp` **optionally add link to PR or code**
    - [ ] Looks consistent
    - [ ] Passes `tools/check-wininstaller-translations.sh`
    ```
    </details>
  - [ ] Wait for all PRs to be merged
- [ ] App translations
  - [ ] Generate `.ts` files in master via `lupdate`
  - [ ] Ping translators. Translators do their work using `linguist` and submit PRs with their changes against master. Get the list of translators from `src/utils.cpp` (some grep/sed would be nice; last one per language is the active one).
  - [ ] Review PRs, <details><summary>Checklist for the PRs</summary>
     ```
     - [ ] Translator listed in the `src/util.cpp` **optionally add link to PR or code**
     - [ ] Punctuation and spacing consistent
     - [ ] Signal words consistent ("ASIO", "Buffer")
     - [ ] No untranslated strings (`grep unfinished -5 src/res/translation/translation_$TRANSLTION*.ts`)
     - [ ] Only a single `.ts` file checked in
     ```
     </details>
  - [ ] Wait for all PRs to be merged
  - [ ] Generate `.qm` files via `lrelease Jamulus.pro`
- [ ] Tag a release candidate
- [ ] Draft an announcement, include all contributors via `tools/get_release_contributors.py`
- [ ] Update the version number in `Jamulus.pro` and add the release date to the Changelog header and commit
- [ ] Tag this commit as `r3_y_z`
- [ ] Wait for the build to complete
- [ ] Prepare `Jamulus.pro` (`dev` suffix) and ChangeLog (add a header) for the next release
- [ ] Do a smoke test for Windows/Mac/Linux -- Do the binaries start/connect properly?
- [ ] Upload the artifacts to SourceForge and link latest
- [ ] Trigger the update notification by updating the both Update Check Servers with the new version
- [ ] Announce the new release with a summary of changes (+ link to the changelog for details) and a link to the download page
  - [ ] On Github discussions in the Announcements section. Lock the announcement thread.
  - [ ] On Facebook in the group "Jamulus (official group)"
- [ ] Update download links on the website (start page, per-platform pages + translations)
- [ ] Create a milestone for the next minor release
- [ ] Update [this checklist](https://github.com/jamulussoftware/jamulus/blob/master/.github/ISSUE_TEMPLATE/release_new_version.md) with any improvements which were found
