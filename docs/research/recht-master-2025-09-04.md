# Recht & Compliance (DE/EU) – **Masterfassung** (v2, 2025-09-04)
> **Hinweis:** Keine Rechtsberatung. Rechtslage/Guidance regelmäßig prüfen.

Diese v2 ergänzt v1 um **verlinkte Primärquellen** und kleine Klarstellungen (TDM/Presserecht).

---

## 1) Normen & Geltungsbereich (DE/EU)

- **DSGVO** – Art. 7 (**Nachweis**), Art. 13 (**Informationspflichten**), Art. 21 (**Widerspruch/Direktwerbung**).  
  → EUR‑Lex: Art. 7, 13, 21 (VO 2016/679).  
- **UWG § 7** – E‑Mail‑Werbung & **Bestandskundenprivileg** (Abs. 3).  
- **DDG § 5** – Anbieterkennzeichnung/Impressum.  
- **TDDDG § 25** – Zugriff/Speicherung in **Endeinrichtungen** (Cookies/SDK/**Zählpixel**) nur mit **Einwilligung**, Ausnahmen „unbedingt erforderlich“.  
- **UrhG §§ 87f–87h** – Leistungsschutzrecht Presseverleger (Ausnahme: **einzelne Wörter/kleinste Textausschnitte**).  
- **UrhG §§ 44b/60d** & **DSM‑RL Art. 3/4** – Text‑&‑Data‑Mining; **Opt‑out** (Art. 4) beachten.

---

## 2) E‑Mail‑Werbung & Einwilligung

Grundsatz: Werbung per E‑Mail **nur mit Einwilligung** (§ 7 Abs. 2 Nr. 3 UWG i. V. m. Art. 6 Abs. 1 a DSGVO).  
**Bestandskunden (§ 7 Abs. 3 UWG)** greift **nur**, wenn **alle 4 Voraussetzungen** erfüllt sind: Verkauf, **eigene ähnliche** Produkte, **kein Widerspruch**, **Hinweis** bei Erhebung und jeder Nutzung.  
**Widerspruch (Art. 21 DSGVO):** Direktwerbung nach Widerspruch **zu unterlassen**.

---

## 3) Double‑Opt‑In (DOI) & Nachweis

- **Art. 7 Abs. 1 DSGVO**: Verantwortliche müssen **Einwilligungen belegen**.  
- **BGH, 10.02.2011 – I ZR 164/09:** DOI **grundsätzlich geeignet** (Telefonwerbung).  
- **OLG München, 27.09.2012 – 29 U 1682/12:** **Werbliche** DOI‑Bestätigung unzulässig → Bestätigungsmail **rein funktional**.

Empfohlene **Logfelder**: Zeitpunkt Anmeldung, IP/Hash, Quelle/Referrer, DOI‑Mail‑Zeit, Bestätigung (Zeit/Token), **Fassung des Einwilligungstextes**.

---

## 4) Impressum & Datenschutz (Art. 13 DSGVO; § 5 DDG)

- Vollständige Anbieterkennzeichnung im Footer **oder** klar verlinkt.  
- Art. 13 DSGVO **bei Anmeldung**: Zwecke, Rechtsgrundlagen, Empfänger, Speicherdauer/Kriterien, Drittland, Widerruf/Widerspruch, Beschwerderecht.

---

## 5) Tracking/Pixel (TDDDG § 25 + DSGVO)

- **Zugriffe auf Endgeräte** (inkl. **Zählpixel**) erfordern **vorherige Einwilligung** (§ 25 Abs. 1 TDDDG); **Ausnahmen** nur „unbedingt erforderlich“ (§ 25 Abs. 2).  
- **BfDI**: Zählpixel benötigen **§ 25‑Einwilligung**; zusätzlich **DSGVO** anwendbar.  
- **DSK‑OH 11/2024**: Konkretisiert Consent‑Anforderungen bei digitalen Diensten.

---

## 6) Abmelden & List‑Unsubscribe (RFC 2369/8058)

- **Abmeldung/Widerruf jederzeit** (Art. 7 Abs. 3; Art. 21 DSGVO; § 7 UWG).  
- **Mailbox‑Provider (Gmail/Yahoo)**: One‑Click‑Unsubscribe (RFC 8058) **und** **48 h** zum Umsetzen; ≥ 5 000/d Bulk‑Sender zusätzlich **DMARC (p≥none)** + SPF/DKIM.

**Header‑Beispiel:**  
```
List-Unsubscribe: <mailto:unsubscribe@example.com?subject=unsubscribe>,
 <https://example.com/u/abc123>
List-Unsubscribe-Post: List-Unsubscribe=One-Click
```

---

## 7) Urheberrecht: Snippets & TDM

- **Presseverlegerrecht (§§ 87f–87h UrhG):** Lizenz nötig, **außer** „einzelne Wörter/kleinste Textausschnitte“. → **sehr knappe** Teaser + Link.  
- **TDM (DSM‑RL Art. 3/4; § 44b/§ 60d UrhG):** **Lawful access**; **maschinelles Opt‑out** (Art. 4) respektieren; Forschung (§ 60d) privilegiert.

---

## 8) Mustertexte (Kurzvorlagen)

**Einwilligung (neben Eingabefeld):**  
> „Ich möchte den Newsletter von … per E‑Mail erhalten … Widerruf jederzeit … Hinweise (Art. 13 DSGVO) in der Datenschutzerklärung.“

**DOI‑Bestätigung (ohne Werbung):**  
> Betreff: „Bitte bestätigen Sie Ihre Newsletter‑Anmeldung“ …

**Footer‑Block:**  
> {{Unternehmen}} · {{Adresse}} · {{Kontakt}} · [Impressum](#) · [Datenschutz](#) · [Abmelden](#)

---

## 9) Checkliste

- [ ] Einwilligungstext & **Nachweis** (Art. 7/13 DSGVO)  
- [ ] DOI‑Mail **ohne Werbung**; Logs vollständig  
- [ ] **Impressum** nach § 5 DDG  
- [ ] **Pixel** nur mit § 25 TDDDG‑Einwilligung  
- [ ] **List‑Unsubscribe** (RFC 2369/8058) + **48 h**  
- [ ] **TDM‑Opt‑out** geprüft

---

## Verlinkte Primärquellen
- **DSGVO** (EUR‑Lex): https://eur-lex.europa.eu/eli/reg/2016/679/oj  (Art. 7/13/21)  
- **UWG § 7**: https://www.gesetze-im-internet.de/uwg_2004/__7.html  
- **DDG § 5**: https://www.gesetze-im-internet.de/ddg/__5.html  
- **TDDDG § 25**: https://www.gesetze-im-internet.de/ttdsg/__25.html  
- **BfDI – Zählpixel**: https://www.bfdi.bund.de/DE/Buerger/Inhalte/Telemedien/Z%C3%A4hlpixel.html  
- **DSK‑OH Digitale Dienste (11/2024)**: https://www.datenschutzkonferenz-online.de/media/oh/OH_Digitale_Dienste.pdf  
- **RFC 2369 (List‑Unsubscribe)**: https://www.ietf.org/rfc/rfc2369.txt  
- **RFC 8058 (One‑Click)**: https://datatracker.ietf.org/doc/html/rfc8058  
- **BGH I ZR 164/09 (DOI Nachweis)**: https://juris.bundesgerichtshof.de/cgi-bin/rechtsprechung/document.py?Art=en&Gericht=bgh&anz=1&nr=57082&pos=0  
- **OLG München 29 U 1682/12 (DOI‑Bestätigung)**: https://medien-internet-und-recht.de/volltext.php?mir_dok_id=2427  
- **UrhG § 44b / § 60d**: https://www.gesetze-im-internet.de/urhg/__44b.html · https://www.gesetze-im-internet.de/urhg/__60d.html  
- **UrhG §§ 87f–87h**: https://www.gesetze-im-internet.de/urhg/__87f.html  
- **DSM‑RL (EU 2019/790)**: https://eur-lex.europa.eu/eli/dir/2019/790/oj
