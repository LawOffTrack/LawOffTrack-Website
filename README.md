# Law Off Track — deploy guide

This folder is the whole site:

- `index.html` — the site itself (design, layout, all the interactive bits)
- `content/posts.json` — **every post lives here.** This is the only file
  you'll ever need to touch to add or edit a post.
- `admin/` — a real, password-protected editing panel at **yoursite.com/admin**
  where you fill in a form instead of touching code at all.
- `images/uploads/` — where images you upload through the admin panel land.

No build step, no dependencies to install — just get this folder onto
GitHub and Netlify.

## Step 1 — Put it on GitHub (no command line needed)

1. Go to [github.com](https://github.com) and sign in (or create a free account).
2. Click the **+** in the top-right corner → **New repository**.
3. Name it `law-off-track` (or anything you like), set it to **Public**, and
   click **Create repository**.
4. On the new repo's page, click **uploading an existing file**.
5. Drag the **entire contents** of this folder in — `index.html`, the
   `content` folder, the `admin` folder, and the `images` folder — then
   click **Commit changes**.

   (If GitHub's uploader won't accept empty folders, that's fine — the
   `images/uploads` folder will be created automatically the first time you
   upload an image through the admin panel.)

## Step 2 — Put it live on Netlify

1. Go to [netlify.com](https://netlify.com) and sign up / log in — "sign up
   with GitHub" is easiest since you already have one.
2. Click **Add new site → Import an existing project**.
3. Choose **GitHub**, authorize Netlify, and select the `law-off-track`
   repository from Step 1.
4. Leave the build settings blank (there's nothing to build). Click **Deploy**.
5. Netlify gives you a live URL immediately (something like
   `random-name-123.netlify.app`), and from now on, every change you save on
   GitHub — by hand or through the admin panel — redeploys automatically
   within a minute or two.

## Step 3 — Turn on the admin panel (`/admin`)

The `/admin` page needs two things switched on in Netlify, both free,
one-time, a few clicks each:

1. In your Netlify site dashboard, go to **Identity** (left sidebar) and
   click **Enable Identity**.
2. Still under Identity, click **Settings and usage**, scroll to
   **Registration**, and set it to **Invite only** (so random people can't
   sign themselves up).
3. Scroll down to **Services → Git Gateway** and click **Enable Git
   Gateway**. This is what lets the admin panel commit your edits to GitHub
   on your behalf, without you ever touching GitHub directly.
4. Back on the **Identity** tab, click **Invite users**, and invite your own
   email address. You'll get an email with a link — click it, set a
   password, and that's your login for `/admin` from now on.

Once that's done, go to `yoursite.netlify.app/admin` (or, once your domain
is connected, `lawofftrack.com/admin`), log in with the email and password
from step 4, and you'll see an editor.

## Step 4 — Connect your own domain (the only paid part)

1. Buy your domain from any registrar (Namecheap, GoDaddy, etc).
2. In Netlify: **Site configuration → Domain management → Add a domain**,
   type your domain, and follow Netlify's instructions — it will tell you
   exactly which DNS records to add at your registrar (usually one A record
   or a CNAME, and Netlify auto-issues a free HTTPS certificate).
3. DNS changes can take a few minutes to a few hours to take effect.
4. Once your domain is live, `lawofftrack.com/admin` is your admin panel —
   no separate address to remember.

## Adding and editing posts — the easy way, via `/admin`

This is the workflow you'll use day to day, once Step 3 is done:

1. Go to `lawofftrack.com/admin` and log in.
2. You'll see **Case Files (Posts) → All Posts**, and inside it a list of
   every post.
3. **To add a post:** click the green **Add** button on the "Posts" list,
   fill in the fields (title, a short URL slug like `my-new-post`, date,
   whether it's featured, an optional image, tags, an excerpt, and the body
   — written and formatted like a normal document, no HTML needed), then
   click **Publish** in the top right.
4. **To edit a post:** click it in the list, change what you like, **Publish**.
5. **To feature a post:** open it, tick **Featured**. Only tick this on one
   post at a time — it becomes the large hero card at the top of the page.
   Untick it on the old featured post first (or after).
6. **To add an image:** in a post's editor, click into the **Image** field
   and either drag a file in or click to browse. It's stored in
   `images/uploads` automatically.
7. **To reorder or remove a post:** on the "Posts" list, drag entries by
   their handle to reorder, or open one and use the trash icon to delete it.
8. Whatever you do, the moment you click **Publish**, it's committed to
   GitHub and Netlify redeploys — live within a minute or two, nothing else
   to click.

### If you'd rather skip the admin panel

You can still edit `content/posts.json` directly on GitHub (click the
pencil icon on the file, edit the JSON, commit) — each post is one object
inside the `"posts"` array, in the same shape the admin panel produces. The
admin panel is just a friendlier way to edit the same file, so either
approach is safe to mix and match.

## What was migrated

All 6 posts from lawofftrack.weebly.com plus your About and Contact page
text, now built into `index.html` directly (About and Contact are sections
of the site itself, reachable from the nav — no separate pages to keep in
sync). Since the Weebly dashboard login wasn't accessible, everything was
pulled from the public blog pages, so it's worth a quick read-through of
each post once the site is live, just to confirm nothing looks off.

## A note on the Contact form and comments

Since this is a free static site with no server, the Contact form and each
post's comment box work by opening the visitor's own email app with the
message pre-filled, addressed to your inbox — there's no database and
nothing for you to manage. WhatsApp and LinkedIn share buttons on each post
work the same simple way, just opening those apps/sites with the link
pre-filled.
