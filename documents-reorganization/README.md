# Reorganizing a Documents folder and cloud storage with an AI assistant

A generic write-up of the method. It contains no personal data and does not describe the owner's security setup.

## Approach

1. **Look before touching.** Read-only inventory first; check which folder Windows really uses as "Documents" (it can be redirected).
2. **Propose, then confirm.** A target structure and a plan are shown and approved before any change.
3. **Move whole folders** (instant rename on the same volume) instead of copying thousands of files.
4. **Prove nothing was lost.** Take a manifest (name | size | date) before and after; the difference must equal the intended removals.
5. **Delete reversibly.** Recycle Bin / Drive trash first; permanent deletion only on explicit request.
6. **Keep a journal.** Every move or deletion is logged in a CSV.

## Target structure

```
00_INBOX                  transit zone
01_ADMINISTRATIF          identity, housing, bank, taxes, insurance, invoices
02_TRAVAIL                CVs, contracts, companies
03_ETUDES                 schools, presentations
04_PROJETS                one folder per project
05_FINANCES               budget, savings, investments
06_PERSONNEL              hobbies, travel, photos, videos
07_LOGICIELS_ET_OUTILS    software, tools, virtual machines
99_ARCHIVES               finished items + operation journals
```

## Clean-up rules

- Exact duplicates only (same content); keep original user file over generated copies.
- Duplicates between deliberately organized folders are listed in a CSV, not deleted.
- Zero-byte files are kept (their name can be the data); project backups are kept.
- Game and app folders stay at the root.

## Case-only renames on NTFS

A direct rename to a different letter case is refused ("source equals destination"); rename via a temporary name. Windows is case-insensitive, so deleting `Name.txt` also deletes `NAME.txt`.

## Google Drive

Using a Drive connector: read-only inventory, approved plan, create folders, move files with the `parent` update, rename, and trash only superseded older versions (recoverable 30 days). Log file, Drive ID, source and destination.

## Verification habits

- A tool exiting with code 0 can still be wrong: test the property you care about.
- Make verification steps blocking (the script must stop on failure).
- Use short drive letters (`subst`) for paths over 259 characters.
- Close File Explorer windows before renaming a parent folder.
- Clear the read-only attribute before recursive deletion.
