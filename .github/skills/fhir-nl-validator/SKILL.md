---
name: fhir-nl-validator
description: "Valideer FHIR Implementation Guides (llms.md) en individuele profielen (StructureDefinitions) tegen de 9 Nederlandse Validatiecriteria van de FHIR Beheerraad."
argument-hint: "[profiel_naam]"
user-invocable: true
disable-model-invocation: false
---

# FHIR-NL Profile Validator & Auditor

Dit is een specialistische workspace-skill voor het auditen en valideren van Nederlandse FHIR-conformance-artefacten (profielen en Implementation Guides) aan de hand van de 9 Validatiecriteria van de FHIR Beheerraad (versie november 2020).

## Wanneer te gebruiken
- Toetsen van een specifiek Nederlands FHIR-profiel (StructureDefinition).
- Auditen van een volledige Implementation Guide (zoals `llms.md` of `llms-full.txt`).
- Controleren of de FHIR-artefacten correct aansluiten op de onderliggende Nictiz Zorginformatiebouwstenen (zibs).

## Stappenplan voor de Agent

### 1. Inhoudelijke Match-Controle (Cruciaal)
Bij het beoordelen van elk afzonderlijk profiel of geselecteerde resource, voer verplicht de volgende analyse uit op de `StructureDefinition.description` of geselecteerde elementen:
1. **zib-Match**:
   - Welke specifieke Zorginformatiebouwsteen (zib) of functionele use case wordt geclaimd in de `description`?
   - Komen de in de tekst genoemde zib-concepten exact overeen met de aanwezige `StructureDefinition.mapping` elementen (bijv. `identity` als `zib-problem-v3.2`)?
2. **FHIR Resource-Type Match**:
   - Controleer `StructureDefinition.type` en `baseDefinition`.
   - **Inhoudelijke toets**: Is dit gekozen FHIR resource-type functioneel en logisch passend bij de zib/use case uit de `description`?
   - *Rapporteer een FAIL/WARN bij een verkeerde keuze (bijv. een zib Aandoening/Problem die op een `Observation` is gemapped in plaats van een `Condition`).*

### 2. Toetsing aan de 9 Validatiecriteria
Controleer elk element systematisch tegen de volgende criteria:
1. **Aanduiding van relevante sectoren/domeinen**: Use cases, scenario's en FHIR CapabilityStatements (endpoints + operaties) moeten helder zijn beschreven.
2. **Generiek karakter van profielen**: Vlag profielen die specifiek voor leveranciers, regio's of beroepsgroepen zijn ingericht zonder dat hier een wettelijke grondslag voor is.
3. **Beheerprocedure & Complete documentatie**: Elk artefact moet `.publisher` en `.contact` hebben. Er moet een duidelijke beheerparagraaf zijn (e-mail, issue tracker, stuurgroep).
4. **FHIR Core (RESTful) correct toegepast**: RESTful uitwisseling is de norm ("comply or explain").
5. **Relatie met Zorginformatiebouwstenen (zibs) & Inhoudelijke Match**: Bevat het profiel expliciete zib-mappings? Matchen de zib, de `description` en het gekregen FHIR resource-type inhoudelijk 1-op-1 met elkaar?
6. **Relatie met reeds gevalideerde profielen**: Controleer of het profiel correct afgeleid is van bestaande Nederlandse profielen (zoals `nl-core-` of `zib-` profielen) in plaats van direct vanaf FHIR Core.
7. **Correct gebruik van terminologie- en codestelsels**: Worden de in de zib voorgeschreven ValueSets/codestelsels (SNOMED CT, LOINC, LCR) gebruikt? Vermijd lokale/propriëtaire codesets.
8. **Geen dubbele of overbodige extensies**: Controleer of gemaakte extensies niet al in FHIR Core of landelijk beschikbaar zijn.
9. **Voldoende en dekkende voorbeelden**: Elk profiel moet minimaal één valide voorbeeld-resource hebben dat de specificaties dekt.

---

## Rapportage Format

Wanneer een validatie wordt gevraagd, koppel je ALTIJD terug in de volgende structuur:

### 📌 Validatierapport: [Naam van de IG / Profiel]

**Eindoordeel**: ✅ PASSED / ⚠️ WARNINGS / ❌ FAILED

#### 1. Inhoudelijke Match Analyse (`description` vs. zib & resource)
- **Geclaimde zib in description**: ...
- **Gekozen FHIR Resource Type**: ...
- **Match Status**: 🟢 Logisch & Correct / 🔴 Mismatch
- **Zib-Mapping Aanwezig**: Ja/Nee (Identificatie: ...)

#### 2. Criterium Overzicht
| # | Criterium | Status | Specifieke Bevinding |
|---|---|---|---|
| 1 | Sectoren/Domeinen | PASS/WARN/FAIL | ... |
| 2 | Generiek Karakter | PASS/WARN/FAIL | ... |
| 3 | Beheer & Metadata | PASS/WARN/FAIL | ... |
| 4 | RESTful Paradigma | PASS/WARN/FAIL | ... |
| 5 | Relatie met zibs | PASS/WARN/FAIL | ... |
| 6 | Overerving/Base | PASS/WARN/FAIL | ... |
| 7 | Terminologie | PASS/WARN/FAIL | ... |
| 8 | Extensies | PASS/WARN/FAIL | ... |
| 9 | Voorbeelden | PASS/WARN/FAIL | ... |

#### 3. Gedetailleerde Bevindingen & Actiepunten
- [Concrete verbetervoorstellen en inhoudelijke gaps]
