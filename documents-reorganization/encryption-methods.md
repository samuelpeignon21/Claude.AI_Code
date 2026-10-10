# Document encryption methods used

Generic description of the methods. No passphrases, recovery keys, vault names or file contents are recorded here.

## Options considered (Windows 11 Home)

| Option | Verdict |
|---|---|
| EFS (built-in folder encryption) | Not available on Home |
| BitLocker / Device Encryption | Whole-disk only; protects against device theft, no per-folder password |
| **AES-256 zip archive** | Used for the cloud-upload copy |
| **Cryptomator** | Used for the local, day-to-day folder |
| VeraCrypt | Fixed-size container, poor fit for cloud sync, needs admin rights |

## Method A: AES-256 zip archives (upload copy)

A separate copy of the tree is prepared outside Documents; originals are never modified. Each sensitive folder is replaced, in the copy only, by `NAME_CHIFFRE/NAME.zip` plus a note saying the folder is encrypted (the note never contains the passphrase).

Tool: `tar` (bsdtar, built into Windows 10/11), no install needed. Archives open with 7-Zip or WinRAR.

```powershell
tar -a -c -f NAME.zip --options "zip:encryption=aes256,hdrcharset=UTF-8" --passphrase "<passphrase>" -C <parent> <folder>
```

Notes:
- Several options go in **one** comma-separated `--options`; a second `--options` flag overrides the first and silently drops the encryption.
- `hdrcharset=UTF-8` keeps accents and characters such as `€` in file names.
- A passphrase on the command line is visible to other local processes; for real use prefer a tool that prompts for it.
- Use a long passphrase (several random words); archive strength is only as good as the passphrase.
- Long paths (>259 chars): map a short drive letter with `subst` before archiving and extracting.

### Blocking verification for every archive

1. Extract **without** passphrase: 0 readable files.
2. Extract **with** the passphrase: same relative names and sizes; SHA-256 on a random sample of 150-200 files.
3. Extract with a **wrong** passphrase: no file may have the original SHA-256.

Only when all three pass is the clear-text copy removed from the upload folder.

## Method B: Cryptomator vault (local use)

- Free, open source, per-file encryption (AES-256); the vault is a normal folder of encrypted files, so it is cloud-friendly.
- Unlocked, it mounts as a drive letter; locked, only encrypted names and data are visible.
- Create the vault, choose a strong password, store the **recovery key outside the computer**.
- Copy files in, verify by SHA-256, then move the clear originals to the Recycle Bin (recoverable) and empty it only when satisfied.
- Never edit files inside the vault's own folder (`masterkey`, `vault.cryptomator`, `d/`).
- Back up the vault folder (still encrypted) with the upload copy.

### What recovery needs

1. The complete vault folder (master key file, vault config, `d` directory),
2. the password **or** the recovery key,
3. Cryptomator on the new machine ("open existing vault").

Without 1 or 2 the data is unrecoverable. Do a restore test: download, open, read a file.

## Choosing between them

| Need | Method |
|---|---|
| Files used often, on this PC | Cryptomator |
| Cold copy to upload / archive | AES-256 zip |
| Protection if the laptop is stolen | BitLocker / Device Encryption, in addition |

Remember that a sync client uploads whatever is in the synced folders: only data inside a vault or an encrypted archive stays unreadable for the provider.
