# WORKLOG

One line per slice: what I did -> the command I ran -> what it printed.

- Listed the project folder -> `ls -la /Users/surya/Downloads/kit` -> five JPEGs at the root, no `images/` folder.
- Held the build and asked for contact details -> (no command) -> member replied: name AyrusAI, WhatsApp +919876543210, email support@ayrusai.com, booking link https://cal.com/suryaprakash-m-andfwl/discovery-call.
- Listed the picture folder after the member moved it -> `ls -la ".../news-agent/Pictures"` -> `Logo Dark.jpeg`, `Logo White.jpeg`, `Profile Picture Sept 19 11-07.jpeg`, `Man Speaking in Meeting Room Sept 19 11 07.jpeg`, `shot1-6.jpeg`.
- Read image sizes for width/height attributes -> `sips -g pixelWidth -g pixelHeight <file>` -> logo 2048x2048, speaking 2752x1536, shot 1792x2400, profile 2048x2048.
- Built the images folder under the brief's names -> `cp` of the five files -> `logo.jpeg`, `logo-dark.jpeg`, `profile.jpeg`, `speaking.jpeg`, `shot-1.jpeg`.
- Wrote the page -> `index.html` (one file, inline CSS, no build step) -> written.
- First desktop screenshot -> headless Chrome at 1440x5400 -> hero image was a narrow half-width crop that cut the speaker out.
- Fixed the hero to a full-width first-screen photo with the headline on a cream panel -> headless Chrome at 1440x900 -> speaker, headline, one teal word, subline and button all read.
- Measured mobile viewport -> headless Chrome reported `innerW=500 scrollW=500` at `--window-size=390` -> macOS clamps Chrome's minimum window width, so the "overflow" was a cropped 500px render.
- Re-measured at a true 390px viewport in an iframe -> `innerW=390 scrollW=390` -> no horizontal overflow, phone layout correct.
- Checked links and image attributes -> `grep -o 'href="[^"]*"' index.html` and `grep -o '<img[^>]*>'` -> booking link x3, WhatsApp, mailto correct; all five images carry width, height and alt.
- Tried to publish -> `ssh -T git@github.com -> "Hi suryamanthena-sp!"; push over SSH succeeded (see REPORT.md).
- Published the repo -> `git push -u origin main` -> `* [new branch] main -> main`; `git ls-remote origin` matches local HEAD afa2619.
- Deployed and verified live -> `curl -w "HTTP %{http_code}" https://ayrusai-site.vercel.app/` -> HTTP 200; all five images HTTP 200 image/jpeg; deployment URL (-1w1gw7dmx-) returned HTTP 302 to the Vercel login.
- Member asked to remove the price -> edited index.html to drop the `.price` block and its CSS -> `grep -c "60,000\|class=\"price\"\|\.price" index.html` -> `0`.
