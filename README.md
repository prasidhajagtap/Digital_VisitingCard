# Digital Visiting Card

Live: https://prasidhajagtap.github.io/Digital_VisitingCard/

Everything is in one file: `index.html`.

- Opening the link shows the card.
- Tapping the **name** shows a QR code.
- The other person points their phone camera at it and taps **Add to Contacts**.
  The contact is stored inside the QR code (vCard), so no app or internet is needed on their side.

## Change the details

In `index.html`, edit the `VC_CONFIG` block (name, designation, business, phone, email, address) and push to `main`.
GitHub Pages updates the site in about a minute.

Tip: use plain English letters where possible. Some phones show special symbols wrongly when saving a contact from a QR code.

## Notes

- Design: brand red `#CB2129` gradient with gold accents. Logo is embedded in the page.
- QR codes are made in the browser with qrcode-generator 1.4.4 by Kazuhiko Arase (MIT License), embedded in the page.
- Hosting: Settings → Pages → Deploy from a branch → `main`, folder `/ (root)`.
