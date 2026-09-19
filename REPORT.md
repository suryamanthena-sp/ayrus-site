# Ayrus site — report

## Status per part

**One-page site (six sections, inline CSS, no backend, no build step): DONE**
- evidence: `index.html` written; headless Chrome rendered it at 1440x900 and at a true 390px viewport.
- evidence: `innerW=390 scrollW=390` (no horizontal overflow on phone), captured from `file://.../md.html` in a 390px iframe.

**Images folder built from the present pictures: DONE**
- evidence: `ls -la /Users/surya/Downloads/kit/images` -> `logo.jpeg`, `logo-dark.jpeg`, `profile.jpeg`, `speaking.jpeg`, `shot-1.jpeg`.
- `working` is absent from the picture folder, so section five is built without it (no gap).

**Contact links real and tappable: DONE**
- evidence: `grep -o 'href="[^"]*"' index.html` printed exactly:
  - `https://cal.com/suryaprakash-m-andfwl/discovery-call` (header, hero, contact — 3 places)
  - `https://wa.me/919876543210?text=Hi%20Ayrus%2C%20I%20would%20like%20to%20talk%20about%20the%20monthly%20MIS%20service.`
  - `mailto:support@ayrusai.com?subject=Ayrus%20-%20monthly%20MIS%20enquiry`

**Picture attributes: DONE**
- evidence: every `<img>` carries `width`, `height` and `alt`; sizes read with `sips -g pixelWidth -g pixelHeight`.

**GitHub repository created and pushed: BLOCKED**
- evidence: `gh auth status` -> `You are not logged into any GitHub hosts. To log in, run: gh auth login`
- evidence: `gh repo create ayrus-site --public --source=. --remote=origin --push` ->
  `To get started with GitHub CLI, please run:  gh auth login` /
  `Alternatively, populate the GH_TOKEN environment variable with a GitHub API authentication token.`
- The site is committed locally on branch `main` (commit `a9b4602`), ready to push.
- To unblock: run `gh auth login`, then `gh repo create ayrus-site --public --source=. --remote=origin --push` from `/Users/surya/Downloads/kit`, or import the local folder on Vercel directly.

## What broke and how I fixed it

1. No `images/` folder at the given location, and the pictures were named differently. Listed the folder, then created `images/` and copied the five files under the brief's names. Confirmed with the member which file is the dark-background logo.
2. First hero used a half-width image column; the landscape speaking photo was cropped to a narrow slice and the speaker was cut out. Rebuilt the hero as a full-width first-screen photo with the headline on a cream panel behind it.
3. Anchor-based screenshots came back blank because `scroll-behavior:smooth` left the headless scroll mid-animation. Removed it.
4. `sips` crop offsets were unreliable for slicing a tall capture, so I sliced with a small wrapper page instead.
5. Headless Chrome on macOS clamps the window to ~500px wide, so the first phone capture looked cut off. Re-measured at a true 390px viewport in an iframe: `innerW=390 scrollW=390`, no overflow.

## Claims ledger

| Claim | Proof |
|---|---|
| Six sections in the required order | `grep -n 'id=' index.html`; rendered screenshots |
| Price written once, on its own line under the cards | `grep -c "60,000" index.html` -> `1` |
| Business name spelled `Ayrus` | `grep -o -i 'ayrus[a-z]*' index.html` -> `Ayrus` only (plus the name `AyrusAI` and the email domain `ayrusai`, both given by the member) |
| Icons are inline SVG, no emoji | three `<svg>` elements in the cards; `grep` for emoji -> none |
| Phone layout has no sideways scroll | `innerW=390 scrollW=390` |
| Page is live on the internet | UNVERIFIED — not deployed; the member imports the repo on Vercel |
| GitHub repository link | BLOCKED — `gh auth status` reports not logged in |

Slots left for the member to fill: none. Every quote, number, offer and timeline on the page comes from the saved niche, problem, solution, price and the member's answers. The client quote in section two is the problem statement the member gave, written in the client's voice, and is unattributed because no client was named.

## What I would tell the next person

- The logo pair: `Logo White.jpeg` is for the cream page (header) and `Logo Dark.jpeg` is for the dark footer. Both are square tiles with their own background, so they sit as small badges rather than cut-out marks.
- `shot1-6.jpeg` is one portrait picture (1792x2400), not six. It runs as the single full-width band between the problem section and the cards. It carries the Ayrus logo on the laptop screen; the band crop favours the person, so that logo is only partly visible.
- To publish: run `gh auth login`, then from `/Users/surya/Downloads/kit` run `gh repo create ayrus-site --public --source=. --remote=origin --push`.
