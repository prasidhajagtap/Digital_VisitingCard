# Digital Visiting Card

Everything is in one file: `index.html`.

- Opening the page shows the card.
- Tapping the **name** turns the card over (smooth flip) to show the QR code on its back. Tapping the card turns it back.
- The other person points their phone camera at it and taps **Add to Contacts**.
  The contact is stored inside the QR code (vCard), so no app, login or internet is needed on their side.

## Where the details come from

SharePoint only. The card shows the logged-in user's details (Azure login), read from the portal page's hidden fields.
There is no demo data: outside a portal page the card shows "Could not read your login details…".

## Download for SharePoint

Latest file (this branch):
https://raw.githubusercontent.com/prasidhajagtap/Digital_VisitingCard/claude/eloquent-babbage-nd6nh0/index.html
(open the link, then Save As `index.html`; or on GitHub open `index.html` → "Download raw file").

Portal hidden fields used (found by class first, e.g. `class="hdnBuUnitDesc"`, then by id/name ending):

| Card field | Hidden field |
|---|---|
| Name | `hdnName` (if empty: made from the email, e.g. `prasidha.jagtap@…` → "Prasidha Jagtap") |
| Email | `hdnCurrentUserEmail` |
| Business | `hdnBusinessDesc` |
| Office address | `hdnBuUnitDesc` |
| Designation, Contact number | Master data — **not connected yet** (hidden until then) |

`hdnPoornataId` is read only to look up master data later. It is never shown and never put in the QR.
No photo is used.

The portal may fill these fields a little after the page loads, so the card checks every 400 ms for up to 6 s.
If nothing is found it shows "Could not read your login details…" with a **Try again** button.

## UAT test (onehruat.poornata.com)

1. Upload `index.html` to the portal, e.g. `/Style Library/VisitingCard/index.html`.
2. On a portal page where the hidden fields exist (the same kind of page used for Geo attendance, e.g. `TestingText.aspx`),
   add a **Page Viewer** web part pointing to that `index.html`.
3. Sign in with Azure login and open the page. Check:
   - name, email, business and office address are yours;
   - designation and phone are hidden;
   - tapping the name shows the QR, and a phone scan offers "Add to Contacts" with the same details.
4. Also test: open the page signed out / on a page without the fields → error message and "Try again".

## Connect master data later

In `VC_CONFIG.masterData.url`, set the address of the master data service, for example
`https://…/employee/{id}` — `{id}` is replaced with the Poornata ID. It must return JSON:
`{ "designation": "...", "phone": "..." }`. Nothing else needs to change.


## Notes

- Design: brand red `#CB2129` gradient with gold accents, gentle animations (off when the device asks for reduced motion).
- QR codes are made in the browser with qrcode-generator 1.4.4 by Kazuhiko Arase (MIT License), embedded in the page.
- GitHub Pages cannot show a real card (it has no portal login); use SharePoint for testing.
