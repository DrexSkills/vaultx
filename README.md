# VaultX

Your privacy. Your files. Your rules.

**Live site:** https://drexskills.github.io/vaultx/

A private vault for photos, videos, documents, notes and web links, backed by Supabase.

## How it works
- No sign-up or login. On first open you create a 4-digit passcode; behind the scenes the browser gets a private anonymous Supabase session.
- Everything is encrypted in your browser with AES-256 (key derived from your passcode with PBKDF2) **before** it's uploaded. Supabase only stores scrambled data.
- Files go to a private Supabase Storage bucket (`vaultx`); notes, links and file details go to the `vaultx_items` table.
- Row-level security means each account can only read its own rows and files.
- Your vault is tied to the browser you created it in. Clearing that browser's site data removes access.

## Features
- Passcode lock screen
- Hide photos, videos, documents, notes and links (files up to 50 MB)
- Fake error screen (tap the sad face 5 times to get in)
- Auto-lock after 1, 5 or 15 minutes
- Change passcode (re-encrypts everything)
- Erase vault

## Supabase setup (already done)
- Tables: `vaultx_profiles`, `vaultx_items` (RLS on)
- Function: `vaultx_rekey` (atomic passcode change)
- Storage bucket: `vaultx` (private, per-user folders)

Required: in the Supabase dashboard, turn on **Authentication → Sign In / Providers → Allow anonymous sign-ins**.

## Notes
- There is no passcode recovery. If you forget it, you can only erase the vault.
- The key in `index.html` is Supabase's public (anon) key. It's safe to publish; access is protected by row-level security.
