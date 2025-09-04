# Runbook (Master): Newsletter – **DOI · Impressum · Tracking** (DE/EU)
**Phase 1 – Doku** · **Stand:** 2025-09-04

Dieses Runbook ergänzt das bestehende Versand‑How‑to und konzentriert sich auf **Compliance‑Schritte** (DOI, Abmelden, Impressum, Tracking).

## 0) Setup
- ESP mit AV‑Vertrag; VVT‑Eintrag „Newsletter“.
- Datenschutzerklärung: Abschnitt Newsletter (Art. 13 DSGVO).

## 1) Einwilligung einsammeln
- Einwilligungstext mit Zweck, Widerruf, Link Datenschutz.  
- Anmeldung **loggen**: Zeitpunkt, IP/Hash, Quelle, Einwilligungstext‑Version.

## 2) Double‑Opt‑In (DOI)
- DOI‑Mail **ohne Werbung** (OLG München 29 U 1682/12).  
- Klick → **Consent‑Record** (Zeit, Token, Textversion).  
- **Nachweis** (Art. 7 Abs. 1 DSGVO); BGH I ZR 164/09 zur Eignung von DOI (Telefonwerbung).

## 3) Abmelden / Widerspruch
- Abmeldelink in jeder E‑Mail, **sofort wirksam**.  
- **Header setzen**: `List-Unsubscribe` (RFC 2369) **und** `List-Unsubscribe-Post: List-Unsubscribe=One-Click` (RFC 8058).  
- **Mailbox‑Fristen**: Abmeldungen **≤ 48 h** umsetzen (Gmail/Yahoo‑Vorgaben).

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
- BfDI‑Hinweis: Zählpixel erfordert § 25‑Einwilligung; **DSGVO** anwendbar.

## 6) Betrieb & Kontrollen
- **Monatlich:** DOI‑Logs, Abmelde‑SLA, Pixel‑Consent‑Quote.  
- **Quartalsweise:** Rechtstexte, Deliverability (SPF/DKIM/DMARC).  
- **Vor Versand:** Inhalt/Links/Impressum/Header – Testinbox.

---

### Quellen (Kurzüberblick)
DSGVO Art. 7/13/21 · UWG § 7 · DDG § 5 · TDDDG § 25 · BfDI (Zählpixel) · DSK‑OH (2024) · RFC 2369/8058 · BGH/OLG DOI
