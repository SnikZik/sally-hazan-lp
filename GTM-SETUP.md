# Tracking setup for the landing page

Page pushes these dataLayer events (see the script at the bottom of index.html):

| event            | when                                  | params                          |
|------------------|---------------------------------------|---------------------------------|
| generate_lead    | any of the 3 forms submitted (opens WhatsApp) | lead_method, form_id    |
| click_call       | any tel: link clicked                 | link_id                         |
| click_whatsapp   | any wa.me link clicked                | link_id                         |

## 1. GTM container
Replace `GTM-XXXXXXX` in index.html (2 places: NB_CONFIG and the noscript iframe).

## 2. Tags to create inside GTM
1. **GA4 Configuration** – Measurement ID G-XXXXXXX, trigger: All Pages.
2. **GA4 Event** ×3 – event names generate_lead / click_call / click_whatsapp, trigger: Custom Event with the same name. Mark generate_lead + click_call as key events in GA4.
3. **Google Ads Conversion Tracking** ×3 – conversion ID + label from Google Ads (conversion actions: "Lead form", "Click to call", "WhatsApp click"), triggers as above.
4. **Google Ads Remarketing** – conversion ID only, trigger: All Pages. Then in Google Ads → Audience manager → "All visitors" (30/90/540 days) for the display campaign.
5. **Conversion Linker** – trigger: All Pages.

## 3. Verify
GTM Preview → open the page → click call / WhatsApp / submit form → events appear in Tag Assistant and GA4 DebugView.
