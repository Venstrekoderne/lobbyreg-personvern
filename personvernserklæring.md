# Her finner du full oversikt over alle persondata som behandles eller er planlagt behandlet i Lobbyreg.no

Alle data skal ha info om:

- **Hva** slags data det er
- **Grunnlag** for å behandle
- Når og hvordan de **behandles**
- Når og hvordan de **lagres**
- Når og hvordan de **slettes**

Alle data er sortert etter hvem dataene omhandler

# Formål med lobbyregisteret og datainnsamlingen

Formålet med å samle inn disse dataene er å lage en nettside og et tilhørende API hvor befolkningen i Norge har tilgang til å se hvilke organisasjoner og lobbyister Stortingsrepresentantene møter med, hvor hyppig de møtes, og i grove trekk hva de har snakket om. Målet er å gi åpenhet rundt lobbyisme og med det både forebygge lobbyisme som ikke tåler dagens lys, og vise at "god lobbyisme" - det at folk og organisasjoner tar kontakt med politikere for å overbevise eller fortelle om sine synspunkter - er i det store og det hele en god ting. 

Vi mener at befolkningen har en rett til innsyn i prosessene som leder frem til at en politiker tar et valg, og vi tror at åpenhet om møtene politikerene har hatt også vil gi aktører som ikke har fått presentert sin side av saken en mulighet til å invitere til et møte. 

# Data vi behandler og lagrer

## Data om Stortingsrepresentantene og deres rådgivere

### Representantenes møter som ikke skal vises i lobbyregisteret

For å enklere hente informasjon ut til lobbyregisteret kan representanten koble på sine kalendre. 

Om representanten gjør dette, enten selv eller gjennom en rådgiver, så **vil** vi lagre: 

- En unik ID per møte i kalenderen, også møter som ikke skal i lobbyregisteret.
  -  **Hvorfor:** ID-en er satt av kalendertjenesten representanten bruker, og lagres for å kunne filtrere ut hvilke møter som allerede er behnadlet og lagt til eller valgt bort for lobbyregisteret. 

Vi lagrer ikke, og behandler heller ikke på våre servere, annen informasjon enn en unik ID om møter som ikke skal vises i lobbyregisteret. All behandling av disse skjer på "klienten" - altså lokalt på PC-en eller mobilen til den som legger inn informasjonen.

### Påloggingsinformasjon til representantens kalender

For å enklere hente ut informasjon til lobbyregisteret kan representanten koble på sine kalendre. 

Om representanten gjør dette, enten selv eller gjennom en rådgiver, så **kan** vi lagre: 

- En ende-til-ende kryptert `token` som gir lesetilgang til kalenderen til representanten
  - **Hvorfor**: For å kunne koble seg på kalenderen og hente ut informasjon som gjør det enklere å fylle ut informasjon til lobbyregisteret
  
Denne `token`en vil aldri bli dekryptert på våre servere, og kan derfor ikke brukes av oss eller en angriper som får kontroll på serveren. Den vil krypteres basert på et passord som ikke lagres server-side, og som representanten eller rådgiveren vil måtte skrive inn for å starte import fra sin kalender på en ny nettleser eller datamaskin.

En dekryptert Token kan bli lagret i representantens egen nettleser for å forenkle så man ikke må skrive inn passordet hver gang.

### Representantenes og lobbyistenes møter

Ingen møter legges i lobbyregisteret uten at representanten eller en rådgiver for representanten har lagt dem inn selv. Generelt lagrer vi ikke informasjon om møter som er hemmeligstemplet eller møter med varslere.

Informasjon vi **kan** lagre om representantens møter (ikke all informasjon vil lagres om alle møter):

- 🗺️ Upresist sted (F.eks. "Stortinget", "Virtuelt" eller "Vestland fylke")
  - **Hvorfor**: For å kunne gi befolkningen informasjon om hvor representanten har flest møter, uten å lagre detaljert informasjon om hvor møtedeltakerne var på et gitt tidspunkt.
  - **Begrensninger**: Vi lagrer ikke strukturert nøyaktig informasjon, som adresse eller kommune - for å beskytte personvernet til de som deltar. Vi anser ikke det som viktig informasjon for å oppnå formålet med lobbyregisteret. Det kan allikevel være nyttig å vise hvor mange møter som skjer på Stortinget, vs møter som skjer utenfor Stortinget, og vi lagrer derfor informasjon om dette.

- 📆 Dato, _ikke tid_ (F.eks. "Fredag 24. mars 2022)
  - **Hvorfor**: For å kunne gi befolkningen informasjon om når møtene skjedde, så de enklere kan sees i sammenheng, uten å lagre informasjon ned på time eller minutt om når møtedeltakerne møttes.
  - **Begrensinger**: Vi lagrer ikke tidspunkt, kun dato. Vi viser ikke offentlig møter som er i fremtiden for å beskytte sikkerheten til de involverte, selv om de kan lagres i forkant om representatene legger dem inn.

- 🧔 Lobbyisten:
  - Lobbyistens kategori (f.eks. "Oljenæring" eller "Fagforening" eller "Miljøbevegelsen")
    - **Hvorfor**: For å kunne lage statistikk over hva slags representant oftest møter med.
  - Hvem man er der på vegne av: 
    - Organisasjonens navn, om man er der på vegne av en organisasjon, f.eks. "NHO" eller "LO"):
      - **Hvorfor**: Dette er kjernen av lobbyregisteret. Hvilke organisasjoner forsøker påvirke politikerene?  Vi mener vi har en legitim interesse til å lagre disse dataene.
      - **Begrensinger**: Vi lagrer ikke navn på hvem som deltok for lobbyister som kommer som organisasjon, da det ikke trengs for å oppnå formålet og vil offentlig knytte deres navn til arbeidsgiver.
    - Privatpersoners navn, om man er der som privatperson (f.eks. "Ola Nordmann"):
      - **Hvorfor**: Dette er kjernen av lobbyregisteret. Hvilke personer forsøker påvirke politikerene?  Vi mener vi har en legitim interesse til å lagre disse dataene.
      - **Begrensinger**: Vi lagrer kun navn om det ikke er en mindre personlig måte å identifisere lobbyisten på. Normalt vil de fleste være der på vegne av en organisasjon.

- Deltakere fra Stortingspartiene:
  - Navn og partitilhørlighet på alle Stortingsrepresentanter i møtet
    - **Hvorfor**: Dette er kjernen av lobbyregisteret. Hvilke representanter møter med hvem? Vi mener vi har en legitim interesse til å lagre disse dataene.
  - Rådgivere i møtet, samt hvilken representant de er rådgiver for, evt partitilhørlighet om de ikke er knyttet til en enkeltrepresentant
    - **Hvorfor**: Rådgivere er ofte stedfortredere for representantene. Vi ønsker lagre hvilken representant de er der for.
    - **Begrensinger**: Vi lagrer ikke navn på rådgivere, da det ikke trengs for å oppnå formålet og vil offentlig knytte deres partitilhørlighet til navn.

- Møtets tema (f.eks. "Møte om laksenæringens vilkår")
  - **Hvorfor**: For å kunne gi kontekst til hvorfor møtet skjedde. 
  - **Begrensinger**: Dette skrives av representanten eller representantens rådgiver. 


### Representantene og rådgivernes brukerkontoer i lobbyregisteret

Vi lagrer e-post og navn på alle brukere som har innlogging. Disse knyttes til møtene i lobbyregisteret de har rett til å administrere, typisk sine egne.

## Data om besøkende til nettsiden

Det lagres per dags dato ikke persondata om besøkende til nettsiden. 

Det er sannsynlig at vi i fremtiden vil lagre anonyme bruksdata som hvilke funksjoner som brukes, f.eks. hvilke ord besøkende søker på. I så fall vil denne seksjonen fylles ut med mer informasjon om nøyaktig hva som samles og lagres.
