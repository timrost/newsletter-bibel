# ADR‑0004: Bild‑Policy (Newsletter & Web) – DE/EU
**Status:** Proposed · **Datum:** 2025-09-04 · **Geltung:** Newsletter, Website, Social‑Tiles · **Kein Rechtsrat**

## 1. Ziel & Scope
Diese Policy regelt **Beschaffung, Einsatz, Nachweise und Kennzeichnungen** von Bildern (Fotos, Grafiken, Logos) in
- redaktionellen Beiträgen (Teaser/Bildkacheln) und
- Marketing‑/Newsletter‑Mails (Header/Teaser/Thumbnails).

Sie berücksichtigt UrhG (inkl. **§§ 87f–87h**, **§ 51** Zitatrecht, **§ 59** Panoramafreiheit, **§ 72** Lichtbilder), das **Recht am eigenen Bild** (KunstUrhG **§§ 22/23**), sowie DSGVO‑Bezüge bei personenbezogenen Fotos.

## 2. Grundsätze
1) **Lizenz vor Nutzung**: Nur Bilder mit **klarer Nutzungsberechtigung** (eigene Werke, Stock‑Lizenz, CC mit zulässigen Bedingungen, Presse‑Kit/Offizielle Freigaben).  
2) **Personenfotos**: Nur mit **Einwilligung/Model Release** oder gesetzlicher Ausnahme (KUG § 23) – besonders streng bei **Minderjährigen**.  
3) **Keine riskanten „Web‑Funde“**: Kein Hotlink/Screenshot fremder Seiten, keine „Google‑Bildersuche“-Übernahmen.  
4) **Einbettung/Framing**: Nur, wenn **rechtmäßig veröffentlicht** **und** keine **Schutzmaßnahmen** umgangen werden; keine Links auf **offensichtlich rechtswidrige** Quellen.  
5) **Dokumentation**: Für jedes Bild gibt es einen **License‑Record** (Quelle, Rechtekette, Bedingungen, Ablage/Beleg).

## 3. Erlaubte Quellen (mit Muss‑Checks)
**A) Eigene Produktion**  
- Erlaubt, wenn Fotograf/Design im Projekt oder übertragen.  
- **Bei Personen**: Einwilligung/Release (inkl. Zweck „Newsletter/Web“), Widerrufsweg dokumentiert.

**B) Stock‑/Agentur‑Lizenzen (editorial/commercial)**  
- Nur mit **passender Lizenzart** (Newsletter = idR **commercial use**).  
- **Verbote** der Lizenz beachten (z. B. sensibler Kontext, Logos, Model‑Endorsement).  
- **Ablage**: Lizenz‑PDF/Bestellbeleg + Lizenztext.

**C) Creative‑Commons**  
- **Keine NC/ND** für Newsletter‑/Marketing‑Kontexte (riskant).  
- **CC BY/CC BY‑SA** nur mit **korrekter Attribution** (Urheber, Titel/Quelle, Lizenz‑Link) und ggf. **Share‑Alike** beachten.  
- Attribution im Alt‑Text/Credit‑Zeile bzw. Bildnachweis‑Seite hinterlegen.

**D) Offizielle Presse‑/Behördenfotos**  
- Nur, wenn Nutzungsrechte **schriftlich** (Website „Presse“, Open‑Data/Open‑Gov‑Lizenz, E‑Mail‑Freigabe) belegt sind; **Auflagen** (Namensnennung, Bearbeitungsverbote) einhalten.

**Nicht zulässig**: Social‑Media‑Reposts als Bilddownload; **Screenshots** von Webseiten/Streams; Hotlinking fremder Bild‑CDNs.

## 4. Personenfotos: KUG/DSGVO
- **Grundsatz (§ 22 KUG)**: Veröffentlichung nur **mit Einwilligung** der abgebildeten Person(en).  
- **Ausnahmen (§ 23 KUG)**: Personen der Zeitgeschichte, **Versammlungen/Aufzüge**, Beiwerk etc.; stets **Interessenabwägung**.  
- **Newsletter/Marketing**: i. d. R. **Einwilligung** nötig (DSGVO **Art. 6(1)(a)** oder **berechtigte Interessen** **Art. 6(1)(f)** mit Widerspruchsmöglichkeit – **Vorsicht**).  
- **Minderjährige**: Einwilligung Erziehungsberechtigte; sensibler Kontext vermeiden.  
- **Ihre Rechte**: Entfernen auf Verlangen ermöglichen; Lösch‑/Widerspruchswege im Impressum/Datenschutz nennen.

## 5. Panoramafreiheit & Orte
- **Öffentlicher Raum (§ 59 UrhG)**: Dauerhaft öffentliche Werke (Bauwerke/Skulpturen) dürfen abgebildet werden; **Innenräume/Hausrecht** gesondert.  
- **Museen/Privatgelände**: Fotografieren oft **nur privat**; Veröffentlichung kann am **Hausrecht** scheitern → vorher Genehmigung einholen.  
- **Ephemere Kunst** (z. B. verhüllte Objekte) fällt **nicht** unter § 59.

## 6. Zitat & Thumbnails
- **Bildzitat (§ 51 UrhG)**: Nur **ausnahmsweise**, wenn **Belegfunktion** im **eigenen** Werk (Auseinandersetzung) – **keine** bloße Illustration/Eyecandy.  
- **Thumbnails/Previews**: Eigene oder lizenzierte Vorschaubilder verwenden; **keine** fremden Thumbs kopieren.

## 7. Linking/Embedding (EU‑Rechtsprechung)
- **Framing** rechtmäßig veröffentlichter Inhalte kann zulässig sein; **unzulässig**, wenn **wirksame Schutzmaßnahmen** gegen Framing umgangen würden (**VG Bild‑Kunst, C‑392/19**).  
- **Linking** auf **rechtswidrig** hochgeladene Inhalte ist riskant; **Kommerziell Handelnde** müssen prüfen – sonst **öffentliche Wiedergabe** (**GS Media, C‑160/15**).

## 8. TDM & Opt‑out (KI/Training)
- **EU‑Urheberrecht (DSM‑RL 2019/790)**: TDM ist für Unternehmen **nur zulässig**, wenn **kein Opt‑out** besteht (maschinenlesbar).  
- **Policy**: Für **Bilder** kein eigenständiges TDM; ggf. **Opt‑out** strikt respektieren (robots/meta‑Tags/Terms).

## 9. Operative Umsetzung (DoR & Nachweise)
**Metadaten je Bild (im CMS/Repo):**  
`source_url`, `source_type` (own|stock|cc|press), `license_name`, `license_uri`, `credit_text`, `has_model_release` (bool), `restrictions` (string), `reviewer`, `review_date`.  
**Review‑Gate:** Kein Versand/Go‑Live ohne vollständigen **License‑Record**.  
**Fallback:** Wenn ungeklärt → **kein Bild** oder eigenes **Icon/Pattern**.

## 10. Beispiele (Kurz)
- **OK**: Stadt‑Pressefoto mit schriftlicher Freigabe + Credit.  
- **OK**: Eigene Aufnahme eines Platzes (außen) – Personen nur als Beiwerk.  
- **Nicht OK**: Screenshot aus Zeitungsartikel als Newsletter‑Bild.  
- **Nicht OK**: Instagram‑Foto herunterladen und einbetten (ohne Lizenz).

---

## Quellen (Primärtexte & Urteile)
- **KUG § 22/§ 23 (Recht am eigenen Bild)** – gesetze‑im‑internet.de  
- **UrhG § 51 (Zitat)** · **§ 59 (Panoramafreiheit)** · **§ 72 (Lichtbilder)** – gesetze‑im‑internet.de  
- **CJEU C‑392/19 – VG Bild‑Kunst / SPK (Framing & Schutzmaßnahmen)** – CURIA/EUR‑Lex  
- **CJEU C‑160/15 – GS Media (Linking auf rechtswidrige Inhalte)** – CURIA  
- **DSM‑Richtlinie 2019/790 (Art. 3/4 TDM; Opt‑out)** – EUR‑Lex  
- **Creative Commons (CC BY/ND – Attribution/ND‑Verbot)** – creativecommons.org

