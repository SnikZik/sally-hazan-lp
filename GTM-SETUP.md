# Tracking setup for the landing page

**Live URL (uPress, static files, no WordPress): https://newbeginning.ussl.co.il/** – files uploaded via uPress File Manager (index.html, images/, robots.txt Disallow all). GitHub Pages disabled 2026-09-22; the repo stays the source.

**Live IDs (created 2026-09-22 under snir@snirdote.co.il):**
- GTM container: `GTM-MPC98BFH` (account 6378284856 / container 264875867) – version 2 live
- GA4: account 409046099, property 555387541 "newbeginning landing", stream 15825147542, Measurement ID `G-S4CTBM95T6`
- Google Ads: account "מורן" CID 311-885-1656 (Snir's choice, 2026-09-22). Conversion ID `AW-18402126771`
  - NB - Lead form → label `_mjQCOztqYEdELPX6MZE` (event generate_lead)
  - NB - Click to call → label `RR-OCO_tqYEdELPX6MZE` (event click_call)
  - NB - WhatsApp click → label `a1ekCPLtqYEdELPX6MZE` (event click_whatsapp)
  - Remarketing tag (all pages) + 3 conversion tags imported from `tracking/gtm_import_ads.json` – GTM version 3 live
  - Audience segment: "NB - מבקרי דף הנחיתה 540 יום" (page URL contains sally-hazan-lp, 540 days) in Audience manager
- Import file for the GTM tags: `tracking/gtm_container_import.json`

Page pushes these dataLayer events (see the script at the bottom of index.html):

| event            | when                                  | params                          |
|------------------|---------------------------------------|---------------------------------|
| generate_lead    | any of the 3 forms submitted (opens WhatsApp) | lead_method, form_id    |
| click_call       | any tel: link clicked                 | link_id                         |
| click_whatsapp   | any wa.me link clicked                | link_id                         |

## 1. GTM container
Done. `GTM-MPC98BFH` is in index.html (NB_CONFIG + noscript iframe).

## 2. Tags to create inside GTM
1. **GA4 Configuration** – Measurement ID G-XXXXXXX, trigger: All Pages.
2. **GA4 Event** ×3 – event names generate_lead / click_call / click_whatsapp, trigger: Custom Event with the same name. Mark generate_lead + click_call as key events in GA4.
3. **Google Ads Conversion Tracking** ×3 – conversion ID + label from Google Ads (conversion actions: "Lead form", "Click to call", "WhatsApp click"), triggers as above.
4. **Google Ads Remarketing** – conversion ID only, trigger: All Pages. Then in Google Ads → Audience manager → "All visitors" (30/90/540 days) for the display campaign.
5. **Conversion Linker** – trigger: All Pages.

## 3. Verify
GTM Preview → open the page → click call / WhatsApp / submit form → events appear in Tag Assistant and GA4 DebugView.
