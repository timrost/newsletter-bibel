# Runbook (Master) v2: Newsletter – **DOI · Impressum · Tracking** (DE/EU)
**Stand:** 2025-09-04

Ergänzt v1 um **Mailbox‑Provider‑Pflichten** (Gmail/Yahoo) und Verweise.

## 0) Setup
- ESP mit AV‑Vertrag; VVT‑Eintrag „Newsletter“.
- Datenschutzerklärung: Abschnitt Newsletter (Art. 13 DSGVO).

## 1) Einwilligung einsammeln
- Einwilligungstext (Zweck, Widerruf, Link Datenschutz).
- Anmeldung **loggen**: Zeitpunkt, IP/Hash, Quelle, Einwilligungstext‑Version.

## 2) Double‑Opt‑In (DOI)
- DOI‑Mail **ohne Werbung** (OLG München 29 U 1682/12).  
- Klick → **Consent‑Record** (Zeit, Token, Textversion).  
- **Nachweis** (Art. 7 Abs. 1 DSGVO); BGH I ZR 164/09 (Telefonwerbung).

## 3) Abmelden / Widerspruch
- Abmeldelink in jeder E‑Mail, **sofort wirksam**.  
- **Header**: `List-Unsubscribe` (RFC 2369) **und** `List-Unsubscribe-Post: List-Unsubscribe=One-Click` (RFC 8058).

> **Mailbox‑Provider‑Pflichten (Gmail/Yahoo, Bulk‑Sender ≥5 000/d):**
> - **One‑Click** erforderlich (RFC 8058 / Header).  
> - **Unsubscribes innerhalb von 2 Tagen** umsetzen.  
> - **SPF + DKIM** bestehen **und** **DMARC** veröffentlichen (**p≥none**).  
> Quellen: Google Admin Help / Blog; Yahoo Best Practices.

**Header‑Beispiel:**  
```
List-Unsubscribe: <mailto:unsubscribe@example.com?subject=unsubscribe>,
 <https://example.com/u/abc123>
List-Unsubscribe-Post: List-Unsubscribe=One-Click
```

## 4) Impressum (§ 5 DDG)
- Anbieterkennzeichnung im Footer **oder** klar verlinkt.

## 5) Tracking & Zählpixel (§ 25 TDDDG + DSGVO)
- **Vorherige Einwilligung**; Ausnahmen nur „unbedingt erforderlich“.  
- EU/DE‑Empfänger → Pixel **default off**; nur bei Consent aktivieren; Consent‑Logs pflegen.  
- BfDI‑Hinweis: Zählpixel erfordern § 25‑Einwilligung; **DSGVO** anwendbar.

## 6) Betrieb & Kontrollen
- **Monatlich:** DOI‑Logs, Abmelde‑SLA, Pixel‑Consent‑Quote.  
- **Quartalsweise:** Rechtstexte, Deliverability (SPF/DKIM/DMARC).  
- **Vor Versand:** Inhalt/Links/Impressum/Header – Testinbox.

---

## Verweise (Auswahl)
- Google Admin Help – Sender Guidelines: https://support.google.com/a/answer/81126  
- Google Admin Help – FAQ (One‑Click/Fristen): https://support.google.com/a/answer/14229414  
- Google Blog (2‑Tage‑Pflicht): https://blog.google/products/gmail/gmail-security-authentication-spam-protection/  
- Yahoo – Best Practices (DMARC, One‑Click, **Honor within 2 days**): https://senders.yahooinc.com/best-practices/  
- RFC 2369: https://www.ietf.org/rfc/rfc2369.txt · RFC 8058: https://datatracker.ietf.org/doc/html/rfc8058  
- DSGVO (EUR‑Lex): https://eur-lex.europa.eu/eli/reg/2016/679/oj  
- UWG § 7: https://www.gesetze-im-internet.de/uwg_2004/__7.html · DDG § 5: https://www.gesetze-im-internet.de/ddg/__5.html · TDDDG § 25: https://www.gesetze-im-internet.de/ttdsg/__25.html  
- BGH I ZR 164/09: https://juris.bundesgerichtshof.de/cgi-bin/rechtsprechung/document.py?Art=en&Gericht=bgh&anz=1&nr=57082&pos=0  
- OLG München 29 U 1682/12: https://medien-internet-und-recht.de/volltext.php?mir_dok_id=2427  
- BfDI Zählpixel: https://www.bfdi.bund.de/DE/Buerger/Inhalte/Telemedien/Z%C3%A4hlpixel.html  
- DSK‑OH Digitale Dienste (11/2024): https://www.datenschutzkonferenz-online.de/media/oh/OH_Digitale_Dienste.pdf
