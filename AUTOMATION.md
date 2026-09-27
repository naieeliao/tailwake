# Automate wakes

[← Tailwake home](README.md) · [Instructions](INSTRUCTIONS.md) · [Support Development](SUPPORT.md) · [Privacy Policy](PRIVACY.md) · [Terms of Use](TERMS.md)

Tailwake sets up a **Wake PC** action in Siri and Shortcuts for every saved PC, so you can wake one without opening the app — by voice, on a schedule, or from another shortcut.

## Wake a PC by voice

Say **“Tailwake” followed by the PC's name** — for example, “Hey Siri, Tailwake Desktop” — to wake it.

## Create a daily wake automation

This walks through waking a saved PC — named “Desktop” here — automatically every morning at 8:00 AM, using the Shortcuts app's Personal Automations. Substitute your own PC's name and time.

1. Open **Shortcuts** and go to the **Automation** tab.

   <img src="images/guide-automation-01-empty.png" alt="The Shortcuts app's empty Automation tab, with a New Automation button." width="320">

2. Tap **New Automation**, then choose **Time of Day**.

   <img src="images/guide-automation-02-trigger-picker.png" alt="The Personal Automation trigger picker, with Time of Day at the top." width="320">

3. Set the time to **8:00 AM**, keep **Repeat** set to Daily, then tap **Next**.

   <img src="images/guide-automation-03-time-8am.png" alt="The Time of Day trigger set to 8:00 AM, repeating daily." width="320">

4. Scroll down to find **Tailwake** among your installed apps.

   <img src="images/guide-automation-05-browse-apps.png" alt="Scrolling the Add Action app list down to Tailwake." width="320">

5. Tap **Tailwake**, then tap **Wake PC…**.

   <img src="images/guide-automation-06-tailwake-actions.png" alt="Tailwake's actions: Your PCs and Wake PC." width="320">

6. Choose the PC to wake — **Desktop**, for this example.

   <img src="images/guide-automation-07-pick-pc.png" alt="The PC picker listing every saved PC." width="320">

7. The automation is ready.

   <img src="images/guide-automation-08-created.png" alt="The finished automation: at 8:00 AM daily, Wake PC." width="320">

By default, the automation is set to **Run After Confirmation**, so iOS asks before it wakes the PC each morning. To run it silently, open the automation, tap the **Automation** row at the top, and switch it to **Run Immediately**.

For relay-wake limits, subscriptions, and optional tips, see [Support Development](SUPPORT.md).
