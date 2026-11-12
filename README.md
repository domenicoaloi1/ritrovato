# if-found

Lost-and-found pages for the NFC tags on your things, hosted for free on GitHub Pages.

> **Status:** early version, not yet tested end to end on real phones and tags. Check your own pages and tags before relying on them.

Stick an NFC tag on your keys, backpack or bike. Whoever finds it holds their phone near the tag, a web page opens, and the page tells them how to reach you. The finder needs no app and no account. You need no server, no paid service and no code: the setup is done in the browser, and the tags are written with a free phone app.

It is not a tracker: it only helps if someone finds your item and contacts you. See [Good to know](#good-to-know).

## Why a web page?

Many people write a plain text record on their tags ("If found, call…"). Many phones, including iPhones and Pixels, **do not show text records** unless an NFC app is installed, so the finder sees nothing. A **URL record** is different: phones open it in the browser on their own. This template gives every item its own page to put in that URL record.

## What the finder sees

One page per item, for example `https://<username>.github.io/if-found/keys`:

- "You found: Keys", with an optional description and your first name;
- your message for that item, or a default one;
- your contacts, in the order you choose: email, phone call, WhatsApp, or a web form. Email and WhatsApp open with a message already written for them;
- every address and number is also shown as text, in case a button does not work on their phone.

Pages are in English or Italian, look right in light and dark mode, and work without JavaScript. They load nothing from other websites and ask search engines not to list them.

`https://<username>.github.io/if-found/` shows a generic page with your contacts. So does any address that does not match an item, for example a typo or a tag you wrote before adding its item. A finder never gets a blank page.

## Privacy first: read this before you start

This repository has to be public: on a free GitHub account, Pages only works with public repositories (on paid plans the repository can be private, but the pages are still public). So:

- **Everything you put in this repository is public, forever.** That includes its history: deleting a line later does not remove it from past versions.
- **Never put** your home address, your full name, children's details (name, school, class) or health conditions in the settings or in any item.
- **Email:** use a dedicated alias you can throw away if it gets spam, not your main address. A Gmail `+tag` address does not help, because it reveals your main address. The page asks search engines not to list it, but spam bots ignore that.
- **Phone:** a number you publish stays public. With WhatsApp, the finder also sees your WhatsApp name (choose a neutral one) and, depending on your privacy settings, your profile photo.
- **Your commit email:** every change you save records an email address, and creating your copy already saves one. **Before you create your copy**, open your account settings (profile picture → **Settings → Emails**, or https://github.com/settings/emails) and turn on **Keep my email addresses private** (and **Block command line pushes that expose my email**). GitHub then uses a `…@users.noreply.github.com` address for your commits.
- **Your username** is part of every address, so the finder can read it: if it contains your name or surname, the finder learns it. Decide if you are comfortable with that before you write your tags (changing it later breaks them). The rest of the address is up to you: make it look trustworthy, not suspicious (see [step 1](#1-create-your-copy)).
- **Your GitHub profile** (`github.com/<username>`) is one click away from the address. A real profile can reassure the finder, but check what it shows in **Settings → Public profile** and leave out anything you would not tell a stranger, such as your location.
- **If you saved something private by mistake**, editing it out is not enough, because it stays in the history. Delete the repository, create a new copy with the same name, turn on Pages again (step 2) and add back your settings and items: your tags keep working. Copies that others made in the meantime may still have it.
- **Organisations** (a school, a club, a small business): use an account or organisation that belongs to the group, not a volunteer's personal account.

## What you need

- A GitHub account. The steps below use GitHub Pages; for other hosts, see [Good to know](#good-to-know).
- NFC tags from the NXP **NTAG21x** family, sold as stickers, key fobs or cards. **NTAG213** is the minimum and is enough for one address and a short text; **NTAG215** and **NTAG216** have more room. Avoid **MIFARE Classic** tags (often sold as "1K" or "S50"): iPhones and many Android phones cannot read them. Not sure what you have? In NFC Tools, tap **Read** and hold the tag to the phone: the **Tag type** line tells you. If the phone does not read it at all (with NFC on), it is probably not an NTAG.
- On metal (a water bottle, a laptop, an aluminium or steel bike frame) use **anti-metal** tags: ordinary ones do not work there. On a carbon frame, test first. For things used outdoors, prefer sealed, waterproof tags (epoxy or PVC key fobs).
- An Android phone or an iPhone with the free **NFC Tools** app, to write the tags.
- Optional: a small label for each tag (see [Add a label](#add-a-label)).

## Set up

Everything below happens on github.com, in the browser.

### 1. Create your copy

1. First, make your commit email private (see [Privacy first](#privacy-first-read-this-before-you-start)). Then, on this repository's page, click **Use this template → Create a new repository**. This is better than a fork: you get a clean copy that is fully yours.
2. Name it `if-found`, or choose another name. The name becomes part of every address and the finder reads it, so prefer a calm word that explains itself, for example `found` or the same word in your language (for things that travel abroad, English is understood more widely). The whole address should look simple and trustworthy to a stranger. Choose it once: renaming later breaks your tags (see [Things that break your tags](#things-that-break-your-tags)). The examples below use `if-found`: if you chose another name, use yours instead.
3. Choose **Public** and click **Create repository**.

### 2. Turn on GitHub Pages

1. In your new repository, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**, then choose the branch `main` and the folder `/ (root)`, and click **Save**.
3. Open the **Actions** tab. GitHub Pages builds the site with GitHub Actions, so if you see a button to enable workflows, enable them.

After a few minutes, `https://<username>.github.io/if-found/` shows the example page. A **"This page is not fully set up yet"** warning is normal at this point: it stays until you replace the example contacts.

### 3. Add your settings

Open `_data/settings.yml`, click the pencil icon to edit it, and click **Commit changes** when you are done (keep **Commit directly to the `main` branch** selected, or the site will not change). The comments in the file explain each line:

| Setting | What it does |
|---|---|
| `language` | Language of the page: `"en"` or `"it"`. |
| `owner_name` | Optional. Your first name or a nickname, shown as "This belongs to …". Leave `""` to hide it. |
| `default_message` | Shown on the generic page and on items without their own message. |
| `contacts` | How the finder can reach you, in order of preference. The first one gets the most visible button. |

Contact types:

| `type` | Field | Example |
|---|---|---|
| `email` | `address` | `"lost-keys-4821@example.org"` |
| `phone` | `number` | `"+<country code> <number>"`, spaces are fine |
| `whatsapp` | `number` | `"+<country code> <number>"`, spaces are fine |
| `form` | `action` | `"https://formspree.io/f/…"`, see [Using a form](#using-a-form) |

Keep the indentation exactly as it is, and put values in `"quotes"`, phone numbers especially: without quotes, a number that does not start with `+` can come out wrong. A contact that still has its example value is never shown to the finder.

If a quick answer matters (a pet, a person who may need help), put `phone` or `whatsapp` first: an email or a form can take hours to be read.

### 4. Add your items

Each file in the `_items/` folder is one item, and its file name is the item's address: `_items/keys.md` becomes `https://<username>.github.io/if-found/keys`.

- Start by editing the example `_items/keys.md` for your first item, or delete it: otherwise `/keys` stays online with the example text.
- To add an item, open `_items/keys.md`, copy its content, then use **Add file → Create new file** in the `_items/` folder and give it a new name ending in `.md`, for example `backpack.md`.
- The file must start with a `---` line, and the item's fields end at a second `---` line. Without them the page is not created (the file is published as plain text), and the address shows the generic page.
- Between the two `---` lines: `title` (the item's name, in `"quotes"`, shown to the finder and used in the email subject) and an optional `description` (to help the finder recognise it, never personal details). Write "Blue backpack", not "Sofia's backpack".
- Below the second `---` line: an optional message for this item only. Leave it empty to use `default_message`.
- Replacing an item (a new ball, a new set of keys)? Keep the same file name and change only `title` and `description`: the old tag, or a new one with the same address, keeps working.
- A tag you give to someone else still leads to your page: the finder contacts you, not them. For their own contacts, they need their own copy of this template.

Choosing the file name:

- Use only lowercase letters `a`–`z` (no accents), digits and hyphens, and keep it short: it has to fit on the tag. A plain word like `keys` or `backpack` reads naturally in the address. Anyone can guess a word, though, and try `/backpack` to see if you have one. If you would rather not show which items you own, use a code instead: a short one like `k7` hides the word but is easy to find by trying, a longer random one like `k7q2xm` is hard to guess.
- Many similar items: add a number, for example `ball-07` or `bib-12`.
- For a pet, use a generic word like `dog`, not its name, and do not use its name in `title` either: a stranger who knows the name can call the pet.
- Never name an item `index` or `404`: those names are taken.
- Never write `{{` or `{%` in a message: they break the site update, or the text around them disappears.

### 5. Check your pages

After every change:

1. Open the **Actions** tab and wait for the latest run to finish (usually a minute or two). A green check means the site is updated.
2. Open the item's address and check that it shows what you expect. If it still shows the old version, reload it after a few minutes.

**If the run shows a red cross, the update failed and the old version of the site stays online**, old contacts included. GitHub usually also emails you when a run fails. To read the error, open the failed run, click the **build** job and open the **Build with Jekyll** step: near the end, a line with `Error` or `Exception` names the file with the mistake (in `_items/` or `_data/`) and usually the line. Most often it is a YAML mistake: a missing quote, a wrong indentation, or a tab instead of spaces.

## Write the NFC tag

In **NFC Tools**:

1. Open **Write → Add a record → URL / URI**.
2. Make sure the prefix box says `https://` (not `https://www.`) and type only the rest of the item's address, for example `<username>.github.io/if-found/keys`: all lowercase, with no `/` at the end. The tag then holds `https://<username>.github.io/if-found/keys`.
3. Optional: add a **Text** record **after** the URL, with a short fallback such as "If found: lost-keys-4821@example.org". It is for phones that read tags with an NFC app; it is public like everything else. An NTAG213 has room for about 90 characters of it, fewer with a long address or with accented letters; an NTAG215 or NTAG216 has room for much more.
4. Tap **Write** and hold the tag against the phone.

**Test before you lock or seal anything.** Try the tag with an iPhone and with an Android phone, and check that the right page opens:

- **iPhone** (XS and newer): hold the tag near the top of the phone, with the screen on, and tap the notification that appears. An iPhone uses **only the first URL record** on a tag, so keep the URL first. It does not read tags if it has not been unlocked at least once since it was turned on.
- **Android**: NFC must be on (Settings), and the screen unlocked. Hold the tag near the back of the phone. Recent Android versions show a notification that you tap to open the link.

Only when it works on both, you can **lock** the tag (NFC Tools: **Other → Lock tag**) so nobody can overwrite it. **Locking cannot be undone**: a locked tag can never be rewritten, not even by you.

**Sealing is not locking.** A tag glued under a cover or sealed in plastic or resin can still be rewritten by anyone with an NFC app. If you seal a tag: test, seal, **test again**, then lock (you can lock it through the cover). The cover, its thickness or nearby metal can stop the phone from reading it, so the step that cannot be undone comes last.

Only want your phone number on the tag, without a website? Write a **Phone number** record (a `tel:` link) instead of a URL. Android offers to call it; check that it works on an iPhone too before relying on it.

## Add a label

Many people do not know what NFC is, even if they pay with their phone every day. A small label tells the finder that the tag is there for them. These are only suggestions:

- Keep it short and calm, and say where to hold the phone and what happens next, for example "Found it? Hold your phone here to contact the owner", or in Italian "Trovato? Avvicina qui il telefono per contattare il proprietario".
- On small surfaces (a helmet, a bottle cap) a shorter text works: "Found? Phone here" / "Trovato? Telefono qui". For things that travel abroad, write it in English, or in both languages with English first. A small phone icon helps; avoid the contactless payment symbol.
- Put it on the tag itself (the back of a key fob) or on the item, next to the tag.
- Never write your name, a child's name, your address or your phone number on it. Your contacts belong on the page, where you can change them. The name of a club or an organisation is fine and can reassure the finder, but not a school's name on a child's things.
- Avoid words that sound like a scam or put pressure on the finder, such as "scan to verify", "pay" or "reward".
- On things exposed to rain, sweat or washing, a paper label may last only a few weeks: use a durable one (laminated label-maker tape, engraving, or text printed on the fob) and check it now and then.

## Things that break your tags

The address on your tags must keep working for years. These changes break it **on every tag at once**:

- renaming the repository;
- changing your GitHub username;
- making the repository private, or turning off GitHub Pages.

Renaming or deleting an item file breaks only that item's address. The tag then shows the generic page, which still has your contacts.

## Using a form

A `form` contact lets the finder write to you without seeing your email address. It uses an external service: for example [Formspree](https://formspree.io), which has a free plan. Create a form there, copy its endpoint (`https://formspree.io/f/…`) into `action`, and confirm your email with the service.

The message goes through that service, so its rules and its privacy policy apply. After sending, the finder sees the service's own page, which may include an anti-spam check. If you limit the form to your website's address in the service's settings, check that messages still arrive. **Send yourself a test message from your phone** before relying on the form.

## Adding a language

The fixed texts of the page are in `_data/strings.yml`, one block per language. Copy the `en` block, change its key (for example `fr`), translate the values, and set `language: "fr"` in `_data/settings.yml`. Keep the `{title}`, `{id}` and `{owner}` placeholders as they are. Keep every line of the block: a missing line leaves an empty text or button on the page, or makes the update fail.

## Good to know

- **It does not solve losing things on its own.** It only works when someone finds the item, notices the tag, has a phone that reads it and decides to contact you. It is not a GPS tracker, not a Bluetooth tracker (like an AirTag or a Galaxy SmartTag) and not an alarm: it locates nothing and warns no one. It can complement them, not replace them.
- **For a pet or a person who may need help, it is only a backup.** Keep the main solutions: a microchip and an engraved ID tag for a pet, a tracker or the arrangements you already have for a person.
- **This is not an emergency system.** If someone needs help, call your local emergency number (112 in Europe).
- The pages themselves collect nothing: no tracking, no statistics, no location. You only learn that someone found your item when they write to you. GitHub, which hosts the pages, logs visitors' IP addresses for security, as most websites do; you cannot see them.
- From time to time, check that your contacts still work. An old alias or a changed number makes every tag useless.
- **Other hosts.** GitHub Pages is the only setup described here. The pages are a standard Jekyll site whose code does not depend on GitHub, so other static hosts that can build Jekyll should work too, as long as they serve `keys.html` at `/keys` and `404.html` for unknown addresses. You will need to add your own build settings (a `Gemfile` and `jekyll build`). Choose your host before writing your tags: moving later changes every address, so every tag would need rewriting, unless you use a domain of your own and keep it renewed.
- You only edit `_data/settings.yml` and the files in `_items/` (and `_data/strings.yml` to add a language). The other files make the pages work: `_layouts/`, `_includes/`, `_config.yml`, `index.html` and `404.html`.

## License

[MIT](LICENSE). This project comes with no promise of maintenance or support.
