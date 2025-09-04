# Recht & Compliance (DE/EU) – **Masterfassung** für Newsletter & KI‑Recherche
> **Stand:** 2025-09-04 · **Hinweis:** Keine Rechtsberatung. Bitte aktuellen Gesetzesstand prüfen.

Diese **Masterfassung** ist Phase‑1‑Doku für die Projekt‑Bibel (Master > Kurzfassung). Sie ergänzt die bestehende Kurzseite `research/recht.md` zunächst **ohne** sie zu überschreiben.

---

## 1) Normen & Geltungsbereich (DE/EU)

- **DSGVO** (EU 2016/679) – Art. 7 (**Nachweis** der Einwilligung), Art. 13 (**Informationspflichten**), Art. 21 (**Widerspruch**, Direktwerbung). Quellen: EUR‑Lex/OJ.  
- **UWG § 7** – E‑Mail‑Werbung & **Bestandskundenprivileg** (Abs. 3).  
- **DDG § 5** – Anbieterkennzeichnung/Impressum für **digitale Dienste**.  
- **TDDDG § 25** – Zugriff/Speicherung in **Endeinrichtungen** (Cookies/SDK/**Zählpixel**) nur mit **Einwilligung**, Ausnahmen „unbedingt erforderlich“.  
- **UrhG §§ 87f–87h** – Leistungsschutzrecht Presseverleger (Ausnahme: **einzelne Wörter/kleinste Textausschnitte**).  
- **UrhG §§ 44b/60d** & **DSM‑RL Art. 3/4** – Text‑&‑Data‑Mining (TDM); **Opt‑out** nach Art. 4 DSM für nicht‑wissenschaftliche Zwecke beachten.

> **Hinweis 2024/25**: TTDSG → **TDDDG** (Umbenennung zum 14.05.2024; inhaltlich maßgeblich bleibt § 25).

---

## 2) E‑Mail‑Werbung & Einwilligung

**Grundsatz:** Werbung per E‑Mail ist **nur mit vorheriger Einwilligung** zulässig (§ 7 Abs. 2 Nr. 3 UWG i. V. m. Art. 6 Abs. 1 a DSGVO).  
**Bestandskundenprivileg (§ 7 Abs. 3 UWG)** greift **nur**, wenn **alle 4 Voraussetzungen** erfüllt sind: (1) Adresse bei **Verkauf** erhoben, (2) **eigene ähnliche** Produkte/Dienstleistungen, (3) **kein Widerspruch**, (4) **Widerspruchshinweis** bei Erhebung **und** jeder Nutzung.

**Widerspruch (Art. 21 DSGVO):** Bei **Direktwerbung** führt Widerspruch zur **Einstellung** der Verarbeitung für diese Zwecke.

---

## 3) Double‑Opt‑In (DOI) & Nachweisfähigkeit

- **Art. 7 Abs. 1 DSGVO:** Verantwortliche müssen **Einwilligungen belegen** (Nachweislast).  
- **BGH, 10.02.2011 – I ZR 164/09:** DOI kann **geeignet** sein, eine Einwilligung (Telefonwerbung) nachzuweisen; E‑Mail gesondert bewerten.  
- **OLG München, 27.09.2012 – 29 U 1682/12:** **Werbliche** Inhalte in DOI‑Bestätigungen unzulässig → Bestätigungsmail **rein funktional** gestalten (kein Marketing).  
- **Praxis‑Logfelder:** Zeitpunkt Anmeldung, IP/Hash, Quelle/Referrer, DOI‑Mail‑Zeit, Bestätigung (Zeit/Token), **Fassung des Einwilligungstextes**.

---

## 4) Impressum & Datenschutzinformationen

- **Impressum (§ 5 DDG)**: Vollständige Anbieterkennzeichnung **im Footer** oder **klar verlinkt**.  
- **Art. 13 DSGVO**: Bei Erhebung der E‑Mail‑Adresse – Zwecke, Rechtsgrundlagen, Empfänger, Speicherdauer/Kriterien, Drittlandübermittlungen, Widerruf/Widerspruch, Beschwerderecht.

---

## 5) Tracking/Pixel in Newslettern (TDDDG § 25 + DSGVO)

- **Zugriffe auf Endgeräte** (inkl. **Zählpixel**) erfordern **vorherige Einwilligung** (§ 25 Abs. 1 TDDDG); **Ausnahmen** nur „unbedingt erforderlich“ (§ 25 Abs. 2).  
- **BfDI (Leitseite Zählpixel):** bestätigt **Einwilligungspflicht**; zusätzlich werden personenbezogene Daten verarbeitet → **DSGVO** anwendbar.  
- **DSK‑OH „Digitale Dienste“ (2024)** konkretisiert Banner/Consent.  
**Praxis:** EU/DE‑Empfänger → Pixel **default off**; nur bei **Consent=true** aktivieren; Consent‑Logs pflegen.

---

## 6) Abmelden & **List‑Unsubscribe** (RFC 2369/8058)

- **Widerruf/Abmeldung jederzeit** (Art. 7 Abs. 3; Art. 21 DSGVO; § 7 UWG).  
- **Mailbox‑Anforderungen 2024/25:** **One‑Click** `List-Unsubscribe-Post: List-Unsubscribe=One-Click` (RFC 8058); **48 h** zum Umsetzen (Gmail/Yahoo).  

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
> „Ich möchte den Newsletter von … per E‑Mail erhalten. Ich willige in die Verarbeitung meiner E‑Mail‑Adresse zum Versand ein. Ich kann meine Einwilligung jederzeit widerrufen, z. B. über den Abmeldelink in jeder E‑Mail. Hinweise (Art. 13 DSGVO) in der Datenschutzerklärung.“

**DOI‑Bestätigung (ohne Werbung):**  
> Betreff: „Bitte bestätigen Sie Ihre Newsletter‑Anmeldung“  
> „Sie haben die Anmeldung mit {mail} angestoßen. Bitte bestätigen: {URL}. Wenn Sie sich nicht angemeldet haben, ignorieren Sie diese E‑Mail.“

**Footer‑Block:**  
> {Unternehmen} · {Adresse} · {Kontakt} · [Impressum](#) · [Datenschutz](#) · [Abmelden](#)

---

## 9) Checkliste (Audit‑fähig)

- [ ] Einwilligungstext & **Nachweis** (Art. 7/13 DSGVO)  
- [ ] DOI‑Mail **ohne Werbung**; Logs vollständig  
- [ ] **Impressum** nach § 5 DDG  
- [ ] **Pixel** nur mit § 25 TDDDG‑Einwilligung  
- [ ] **List‑Unsubscribe** (RFC 2369/8058)  
- [ ] **TDM‑Opt‑out** geprüft

---

### Primärquellen (Auszug)
- DSGVO (Art. 7/13/21) – EUR‑Lex/OJ  
- UWG § 7 – gesetze‑im‑internet.de  
- DDG § 5 – gesetze‑im‑internet.de  
- TDDDG § 25 – gesetze‑im‑internet.de  
- BfDI – Zählpixel  
- DSK‑OH „Digitale Dienste“ (2024)  
- RFC 2369 · RFC 8058  
- UrhG §§ 87f–87h · § 44b · § 60d  
- DSM‑RL (EU) 2019/790
