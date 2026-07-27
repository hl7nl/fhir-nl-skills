## Validatie criteria

De validatie criteria (november 2020) zijn onder meer:

1. Aanduiding van relevante sectoren/domeinen voor de profielen
Uit de documentatie moet blijken voor welke use cases en in welke domeinen/sectoren de FHIR conformance artefacten zijn bedoeld.
Hieronder vallen use cases, scenario’s en FHIR CapabilityStatements. Deze laatste bevatten de endpoints en de bewerkingen die daar mogelijk zijn.
Use cases en scenario’s kun je op allerlei manier maken. Hierin standaardiseren we niet, maar de producten moeten wel met generieke tooling inzichtelijk zijn, zoals een browser, Office, etc.
2. Beoordeling of profielen voldoende generiek zijn
Profielen die specifiek zijn voor bepaalde leveranciers (bijv. vanwege vertalingen), sectoren, beroepsgroepen of specifiek zijn voor een regionale use case, doch afwijken van de internationale FHIR-Core specificaties, hebben weinig relevantie voor validatie door de FHIR Beheerraad/Beheerteam, tenzij sprake is van wettelijke verplichtingen
3. Beheerprocedure, complete documentatie
De FHIR conformance artefacten moeten worden beheerd. Vermeld moet worden door wie en op welke wijze de voor validatie aangeboden FHIR profielen worden beheerd en onderhouden. HL7 Nederland beheert geen gevalideerde FHIR-NL profielen, doch verwijst hiernaar via een register waarin o.m. de eigenaren worden vermeld
De wijze waarop beheer wordt gedaan (e-mail, stuurgroep, tooling, etc.) mag verschillen. Algemeen moet je ergens vragen kunnen stellen en mogelijkheid voor updates open houden.
Alle artefacten moeten markeringen hebben op basis waarvan je het beheerproces kunt vinden. Bijvoorbeeld StructureDefinition.publisher en .contact
4. FHIR Core (RESTful?) correct toegepast
Niet alleen de inhoud van de resources moet interoperabel zijn, maar ook de wijze van beschikbaarstelling c.q. uitwisseling. Het FHIR RESTful paradigma levert internationaal de meeste implementers, testservers, tooling op. We zien RESTful dan ook als “comply or explain”.
5. Relatie met Zorginformatiebouwstenen
Registratie aan de Bron heeft samen met een steeds groter aantal de zorgpartijen gezien dat als je functioneel geen overeenstemming hebt over bepaalde concepten, je daar bij technische uitwisseling last van krijgt. Het resultaat zijn de Zorginformatiebouwstenen (zibs), welke worden beheerd door het zibCentrum van Nictiz. Bij ieder FHIR profiel moet de relatie naar deze zibs zijn gelegd zodat ook geïdentificeerd kan worden welke gaps er mogelijk nog in de zibs zitten. Daarmee versterken ze elkaar.
6. Relatie met reeds gevalideerde profielen
Met minder profielen kunnen werken, houdt dingen eenvoudig. Soms is echter niet uit te sluiten dat er iets nieuws nodig is. Als dat 1 element t.o.v. een bestaand profiel is, dan is afleiding van het bestaande profiel een optie. Naarmate de tijd vordert is de verwachting dat het aantal volledig nieuwe profielen afneemt.
7. Correct gebruik van terminologie- en codestelsels 
In eerste instantie worden de te hanteren terminologie- en codestelsels aangegeven in de zibs. Waar van toepassing moet deze zijn toegepast, of moet een mapping zijn gedefinieerd.
Voor elementen die nog niet bestaan in zibs moeten algemeen binnen de context erkende terminologiestelsels zijn gebruikt. Gebruik van lokale terminologie of betaalde terminologie waarvoor geldige alternatieven bestaan moet worden vermeden.
8. Geen extensies waarvoor reeds elementen bestaan, Geen extensies waarvoor reeds extensies bestaan
Extensies zijn prettig voor als het niet anders kan, maar maken implementatie ook ingewikkelder. Extensies zullen altijd worden gecontroleerd op bestaan in de FHIR Core specificatie. Merk op dat hier ook al veel extensies worden voor-gedefinieerd. Ook deze hebben de voorkeur boven eigen definitie. Tenslotte mag een extensie ook geen bestaande Nederlandse extensie functioneel of technisch dupliceren
9. Voldoende en dekkende voorbeelden
Extreem belangrijk zijn voorbeelden. Dit is het eerste waar mensen op bouwen om in fase 2 pas te kijken naar de volledige documentatie. Voorbeelden maken soms abstracte specificaties helder en er moeten dus ook dekkende voorbeelden zijn waarbij ieder stukje specificatie wordt geraakt. Dat mag best verspreid over meerdere voorbeelden cumulatief het geval zijn als de use case dat rechtvaardigt.