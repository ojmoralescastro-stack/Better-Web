# Better Web

Better Web is a digital services company that builds clean, professional websites and modern chatbots. This repository is its interactive website: a giant pulsing logo on a black screen that, when clicked, reveals five sections radiating outward like rays of light.

It is a **static site** (plain HTML, CSS and JavaScript). There is no build step, no backend and no API key.

## 1. Website structure

- **Home:** the Better Web logo, very large and pulsing. Click it to open the radial menu.
- **Radial menu:** five white labels connected to the logo by thin rays.
- **Contact Us:** Gmail and WhatsApp buttons.
- **Chat:** a guided conversation with selectable options that ends with Gmail and WhatsApp buttons.
- **Website Creation:** service copy plus two layered website screenshots with an arrow to switch between them.
- **Chatbot Creation:** service copy decorated with white and light-blue glowing diamonds.
- **About Us:** calm text over a field of faint stars, with a small logo at the bottom.

## 2. Technologies

Semantic HTML5, modern CSS, vanilla JavaScript (ES modules). No frameworks, no dependencies, no analytics, no cookies.

## 3. Project structure

```
/
├── index.html
├── README.md
├── .gitignore
├── robots.txt
├── sitemap.xml
├── _headers              (security headers used by Cloudflare Pages)
├── assets/images/
│   ├── logo.png
│   ├── website-1.png
│   └── website-2.png
├── css/main.css
└── js/
    ├── main.js           (starts everything)
    ├── navigation.js     (home, menu and section views, back arrow, Escape key)
    ├── radial-menu.js    (places the five labels and rays around the logo)
    ├── website-showcase.js
    ├── chatbot.js
    ├── contact.js        (Gmail and WhatsApp links)
    └── animations.js     (diamonds and stars)
```

## 4. The three images

Put them in `assets/images/` with these exact names:

| File | What it is | Where it is used |
|------|-----------|------------------|
| `logo.png` | The official Better Web logo | Home screen, About Us (small), browser icon |
| `website-1.png` | Screenshot of the Olas y Olivos site | Website Creation only |
| `website-2.png` | Screenshot of the Sintli House site | Website Creation only |

The screenshots are not used anywhere else.

## 5. How the radial menu works

Clicking the logo shrinks it and places the five labels on an ellipse around it. `radial-menu.js` calculates each label's position and the length and angle of its ray from the screen size, so the layout adapts to phones, tablets and desktops. Clicking the logo again, or pressing `Esc`, closes the menu. Inside a section, the back arrow returns to the menu and the menu button (top right) jumps to any section.

## 6. How the Chat works

The Chat is a predefined decision flow in `js/chatbot.js`. It asks "What do you need?" and continues with relevant questions (website type and goal, chatbot channel and task, timing). It shows no prices, calls no AI service and stores nothing; restarting or closing the page clears it. To change the questions, edit the `STEPS` object at the top of `chatbot.js`.

## 7. How Gmail works

The Gmail button is a standard `mailto:` link to `betterwebdotcom@gmail.com`, so it opens the visitor's email app with a new message. At the end of the Chat, the subject and the visitor's selected answers are pre-filled.

## 8. How WhatsApp works

The WhatsApp button opens `https://wa.me/` followed by the number in international format. The number is only inside the link; it is never shown as text on the page. At the end of the Chat, the selected answers are pre-filled as the message. To change the number or the email, edit the two constants at the top of `js/contact.js` and the two links inside the `<template>` at the bottom of `index.html`.

## 9. Run it locally

JavaScript modules do not work when you double-click `index.html`, so use a tiny local server:

```
python3 -m http.server 8000
```

Then open http://localhost:8000. (Any other static server also works.)

## 10. Upload to GitHub

1. Create an account at github.com and click **New repository**. Name it (for example `better-web`) and click **Create repository**.
2. On the new repository page, click **uploading an existing file**.
3. Drag in everything inside the project folder (including the `assets`, `css` and `js` folders and the hidden `.gitignore`), then click **Commit changes**.

## 11. Deploy with Cloudflare Pages

1. Log in at dash.cloudflare.com and open **Workers & Pages**, then **Create** and **Pages**, then **Connect to Git**.
2. Authorize GitHub and pick your repository.
3. Use these settings: **Framework preset:** None. **Build command:** leave empty (no build step). **Build output directory:** `/` (the root of the repository).
4. Click **Save and Deploy**. Cloudflare gives you a free `*.pages.dev` address. You can add your own domain later under **Custom domains**.

## 12. Update the website later

Edit a file on GitHub (pencil icon) or upload a new version, then commit. Cloudflare Pages redeploys automatically within a minute or two. After you get your real domain, replace `YOUR-DOMAIN.example` in `index.html`, `robots.txt` and `sitemap.xml`.

## 13. Security practices

- No API keys, passwords or secrets anywhere; `.gitignore` excludes `.env` files and `node_modules`.
- No external scripts, fonts or trackers. Everything loads from the same site.
- Strict Content Security Policy (in `index.html` and `_headers`) plus headers such as `X-Content-Type-Options`, `X-Frame-Options` and `Referrer-Policy`.
- The Chat builds its content with `textContent`, never `innerHTML`, so visitor choices cannot inject code.
- Only the visitor's own email app or WhatsApp receives what they choose to send. This reduces risk; no website can be guaranteed unhackable.

## 14. Accessibility practices

Semantic headings, keyboard access to the logo, menu, Chat options and screenshot arrow, visible focus outlines, ARIA labels on icon buttons, alt text on the screenshots, decorative elements hidden from screen readers, and support for `prefers-reduced-motion`.

## 15. Troubleshooting

- **Blank page or nothing happens when opened locally:** you opened the file directly. Use the local server in section 9.
- **Images missing:** check the three file names and the `assets/images/` folder (names are case-sensitive).
- **Changes not showing after deploy:** wait for the Cloudflare build to finish, then hard refresh (Ctrl+Shift+R).
- **Gmail does nothing:** the visitor has no default email app; this is a browser setting.
- **WhatsApp does not open:** WhatsApp (app or web) must be available on the device.
