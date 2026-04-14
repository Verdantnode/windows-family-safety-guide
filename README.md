# Windows 11 + Microsoft Family Safety: clean setup guide

A no-BS guide for getting Microsoft Family Safety working on a fresh Windows 11 install without wrecking the setup by hardening privacy too early.

I wrote this after spending way too long fighting a fresh install with basically no useful official guidance. Family Safety is slow, stateful, and easy to break if you poke at it before Microsoft finishes syncing everything.

## What this guide is for

- New Windows 11 installs
- One organizer account
- Child accounts already invited and accepted
- Devices that refuse to show up, duplicate entries, or delayed sync

## Read this first

This is not a same-day setup. New installs can take several hours and sometimes up to 24-48 hours before everything shows up consistently.

Do not restart the whole process because one screen is still empty. In this setup, waiting is often the right move.

## Critical rules

### During setup, do this

- Say yes to required privacy, diagnostics, and account prompts.
- Allow Microsoft account sync and background services.
- Leave Windows defaults alone until Family Safety is working.

### During setup, do not do this

- O&O ShutUp10 / ShutUp11
- Debloat scripts
- Registry or Group Policy privacy hardening
- Telemetry blockers
- "Disable call-home" tools

Family Safety depends on Microsoft account sync, device registration, and encryption-related services. Hardening privacy too early can break setup without obvious errors.

## Setup flow

### 1. Install Windows 11

- Do a clean install.
- Sign in with the organizer's Microsoft account during setup.
- Finish setup completely.
- Do not add family members yet.

### 2. Confirm the organizer account

Open **Settings > Accounts > Your info** and confirm:

- You are signed in with a Microsoft account
- The account type is Administrator

### 3. Verify the organizer on this device

Open **Settings > Accounts > Windows Backup**.

If you see:

- "Verify your identity"
- "Sync isn't available"

Click **Verify**, complete MFA, then turn sync on.

Checkpoint:

- No verification warnings remain
- Sync stays enabled after closing Settings

This step fixes a large share of "nothing shows up" problems.

### 4. Confirm device registration

Open:

https://account.microsoft.com/devices

This PC must appear under the organizer account. If it does not, stop here and wait. Family Safety will not behave correctly until it does.

**Important:** do not use **Add device** on this page for a Family Safety setup. It usually does not help unless the PC is an actual Microsoft device already tied to the account.

### 5. Let encryption finish if it is running

Open **Settings > Privacy & security > Device encryption**.

If encryption is in progress, it can take hours. During that time, registration and Family Safety can lag.

Do not sign out, remove accounts, or reconfigure the device while encryption is still running.

### 6. Confirm the family group on the web

On any device, signed in as the organizer, open:

https://account.microsoft.com/family

Confirm:

- Organizer is listed as organizer
- Child accounts are listed correctly
- Any duplicate child entries from earlier attempts are cleaned up
- The right invitation has already been accepted

If this is not correct, fix it here first.

### 7. Add the child locally

On the PC, signed in as the organizer, open **Settings > Accounts > Family & other users**.

The child should already be listed under Your family.

If the child is listed:

- Click the entry
- Click **Allow sign-in**
- Restart the PC

If the child is not listed:

**Do not enter the email address.**

Entering the email here sends a new invitation, creates duplicate entries, and can break the device link.

If the child is not listed, go back to the verification steps and wait longer.

### 8. First login as the child

- Switch user
- Sign in as the child
- Stay online
- Let setup finish completely
- Do not switch users midway

This login creates the device, child, and family link.

### 9. Force backend sync

From the organizer account on a PC or phone:

https://family.microsoft.com

Turn **Activity reporting** on for the child. Turning **Screen Time** on briefly can also help.

### 10. Wait

It can still take hours, sometimes until the next day, for:

- The device to appear under the child
- Controls to become editable

That is normal on a brand-new device.

## After it works

Once all of the following are true:

- The device appears under the organizer
- The device appears under the child in Family Safety
- Screen Time and Activity reporting work

You can harden privacy, reduce telemetry, disable ads, and remove default apps carefully.

Do not break Microsoft account sync or security services afterward.

## Common failure signals

| Symptom | Likely cause |
| --- | --- |
| Windows asks for the child's email again | Organizer account is not fully verified or synced on this PC |
| Child appears twice in Family Safety | The email was re-entered instead of allowing sign-in |
| Child can log in, but the device never shows | Organizer verification or encryption had not completed |

## Short version

- This is a slow, stateful setup.
- Verification and sync on the organizer device are mandatory.
- Do not harden privacy during setup.
- Never re-enter the child's email locally.
- Waiting is often the correct fix.

## Feedback

This is not really designed for real families. The bigger problem is that I have to be fully signed in on all of these devices, and they all have to live as my devices in my Microsoft account.

- There is no clear official guide for fresh installs.
- The setup path should warn people not to start on the child's account first.
- For 4 kids, that means 8 child devices plus my own devices all tied back to my account.
- The PIN setup is fine for one or two kids, but it scales badly once you have a full house.
- Using the same PIN everywhere is the only practical way to keep this from becoming unmanageable.
- A child should not be one recovered login away from getting into a fully signed-in, 2FA-capable parent account and undoing all of this.

What Windows should have:

- A dedicated **family installer** mode for setting up a child's device
- A **reinstall for child** option for new or reset PCs
- A management account that is a sub-account instead of the parent's main account
- Better guardrails around device setup, PINs, and account switching
