Searched for files matching `**/*InformRelativesRequest*`, 4 matches

Read [](file:///home/michael/eclipse-workspace/fhir-nl/pzp-stu3-1.0.0-rc3/StructureDefinition-ACP-InformRelativesRequest.ai.md)

Read [](file:///home/michael/eclipse-workspace/fhir-nl/pzp-stu3-1.0.0-rc3/CommunicationRequest-ACP-InformRelativesRequest-Pat1.ai.md)

### 📌 Validatierapport: ACP Inform Relatives Request (`StructureDefinition-ACP-InformRelativesRequest`)

**Eindoordeel**: ⚠️ WARNINGS

---

#### 1. Inhoudelijke Match Analyse (`description` vs. zib & resource)
- **Geclaimde zib in description**: Dit profiel is gemapped op het element **"Bespreken met naasten"** (concept ID `187` in de `pall-izppz-zib2017` dataset), met de functionele vraag: *"Heeft u patiënt geïnformeerd over de eigen verantwoordelijkheid om deze behandelafspraken met naasten te bespreken?"*.
- **Gekozen FHIR Resource Type**: `CommunicationRequest`.
- **Match Status**: 🔴 **Mismatch in beschrijvende teksten** (Zie toelichting bij de bevindingen).
- **Zib-Mapping Aanwezig**: Ja (Identificatie: `pall-izppz-zib2017`, gekoppeld aan ID `187`).

---

#### 2. Criterium Overzicht

| # | Criterium | Status | Specifieke Bevinding |
|---|---|---|---|
| 1 | **Sectoren/Domeinen** | **PASS** | De use case ligt binnen Proactieve Zorgplanning (PZP). De specifieke zoekquery (`GET [base]/CommunicationRequest?patient=Patient/[id]&category=http://snomed.info/sct\|223449006`) is opgenomen in data-exchange.md. |
| 2 | **Generiek Karakter** | **PASS** | Dit profiel is generiek van aard en herbergt geen leverancier- of regiospecifieke restricties. |
| 3 | **Beheer & Metadata** | **PASS** | Metadata op resource-niveau is correct ingevuld (`publisher: IKNL`, `contact` met url, `version: 1.0.0-rc3`). |
| 4 | **RESTful Paradigma** | **PASS** | RESTful-uitwisseling is gewaarborgd en volledig gedocumenteerd in de transactiegids. |
| 5 | **Relatie met zibs** | **PASS** | Correcte en traceerbare mappings op elementniveau naar de zib-concepten van `pall-izppz-zib2017`. |
| 6 | **Overerving/Base** | **PASS** | Afgeleid van de FHIR Core basis `http://hl7.org/fhir/StructureDefinition/CommunicationRequest` (wat logisch is, aangezien er in zib2017 geen specifieke basis voor dit concept bestaat). |
| 7 | **Terminologie** | **PASS** | Gebruikt correct de internationale SNOMED CT-codes: op `.category` wordt code `223449006` ("adviseren om iemand te informeren") afgedwongen; op `.reasonCode` de code `713603004` ("advance care planning"). |
| 8 | **Extensies** | **PASS** | Er is alleen hergebruik van de landelijk geaccepteerde Nictiz-extensie `practitionerrole-reference` op de agent. Geen overbodige extensies gedefinieerd. |
| 9 | **Voorbeelden** | **PASS** | Er zijn 3 uitstekende, consistente patiëntvoorbeelden aanwezig (zoals `ACP-InformRelativesRequest-Pat1`) die de specificaties foutloos weerspiegelen. |

---

#### 3. Gedetailleerde Bevindingen & Actiepunten

1. **Inhoudelijke mismatch in de metadata (`description`):**
   - **Bevinding**: Uit de changelog.md (issue #63) blijkt dat dit profiel herontworpen is van een `Communication` (gebeurtenis) naar een `CommunicationRequest` (verzoek/advies). De technical details (`type` en `baseDefinition`) zijn hierop correct aangepast. 
   - **Fout**: De `description` van de StructureDefinition is echter **niet** mee-geüpdatet en bevat nog de oude teksten:
     * *"Communication events that have taken place in context of Advance Care Planning. Based on Communication resource."*
   - **Gevolg**: Dit zorgt voor verwarring, omdat het profiel nu technisch een `CommunicationRequest` (aanvraag/verzoek) is, maar de tekst beweert dat het een reeds plaatsgevonden gebeurtenis (`Communication` event) is.
   - **Actiepunt (Cruciaal)**: Pas de `description` van de `StructureDefinition` aan naar bijvoorbeeld: 
     * *"Request or recommendation made to the patient in the context of Advance Care Planning to inform their relatives about treatment agreements. Based on CommunicationRequest resource."*

2. **Kwaliteitsverbetering in RC3**:
   - **Bevinding**: Uit de changelog (issue #157) blijkt dat de kardinaliteiten van `.subject`, `.requester.agent` en `.sender` zijn aangescherpt van optioneel naar verplicht (`1..1`). 
   - **Evaluatie**: Dit is een zeer sterke verbetering voor de betrouwbaarheid van de gegevens. Een aanvraag/advies heeft in de Nederlandse zorgpraktijk immers pas waarde als onomstotelijk vaststaat *wie* het advies heeft gegeven (`requester`), *aan wie* (`subject`) en *wie* de verzender is. Dit krijgt een compliment voor de datakwaliteit.