# Die RESTlichen Dinge im Internet

RESTful Web Services und die damit assoziierten Ressourcen Orientierten
Architekturen (ROA) haben in letzter Zeit viel Aufmerksamkeit erhalten. Die
Prinzipien von REST und die eingesetzten Technologien sind nicht gerade neu
sondern wurden im wesentlichen in den späten 90er Jahren und im Jahr 2000
entwickelt. Dennoch hat der Einsatz von REST bei der Entwicklung von verteilten
Systemen erst in den letzten Jahren deutlich an Fahrt aufgenommen. Viele
Unternehmen bieten heute Ihre Dienste auch über REST-Schnittstellen an,
darunter namhafte Unternehmen wie z. B. Amazon, Google, Yahoo und Dropbox. REST
wird sehr wahrscheinlich eine zentrale Rolle bei der Entwicklung des Internets
der Dinge spielen.

## Was ist REST?

Die Abkürzung REST (Link: http://en.wikipedia.org/wiki/REST) steht für
Representational State Transfer und identifiziert einen architekturellen Stil
für den Bau von verteilten Systemem. Im Kern geht es bei REST darum, bestehende
und erprobte Web-Standards wie z. B. HTTP einzusetzen und dabei eine Reihe von
Prinzipien zu beachten. Stefan Tilkov (Link: http://www.innoq.com/blog/st/) hat
diese Prinzipien wie folgt zusammengefasst:

- Gebe jedem "Ding" einen eindeutigen Identifier. Benutze URI's zur
  Indentifikation von "Dingen" in einem globalen Namensraum. Statt "Dingen"
  spricht man bei REST von Ressourcen.
- Benutze Links um "Dinge" zu referenzieren und Beziehungen zwischen den
  "Dingen" zu modellieren. Erst Links machen das Web zum Web.
- Benutze standardisierte Methoden für den Zugriff auf "Dinge". HTTP bietet
  alles was man braucht um CRUD-Operationen auszuführen - GET, PUT, POST,
  DELETE und eine Reihe anderer Methoden, die alle eine wohldefinierte Semantik
  haben. Der Einsatz standardisierte Methoden trägt wesentlich zur
  Vereinheitlichung von REST-Schnittstellen bei - hat man erst einmal Eine
  verstanden, versteht man Jede.
- Stelle mehrere, für den jeweiligen Zweck optimale Repräsentationen für
  "Dinge" bereit, wie z. B. XML, JSON oder HTML.
- Kommuniziere Zustandslos. Der Applikationszustand wird nur vom Client, der
  Zustand der "Dinge" nur vom Server verwaltet. Dieses Prinzip ist grundlegend
  für die Skalierbarkeit des heutigen Internets.

## REST und das Internet der Dinge

REST und das Internet der Dinge (und Dienstleistungen) sind wie füreinander
geschaffen. Implementierungen von REST Schnittstellen können sehr
leichtgewichtig sein - HTTP Clients und Server sind mittlerweile auch auf den
kleinsten IP-fähigen Platformen verfügbar. 

Die zentrale Abstraktion bei REST ist die Ressource (bei Service Orientierten
Architekturen ist es der Dienst). Diese Abstraktion passt perfekt in die Welt
von eingebetteten, verteilen Regelungssystemen; Sensoren, Aktoren und
Regelungssysteme und die Dienste die sie anbieten lassen sich elegant als
Ressourcen und REST-Schnittstellen modellieren.

Dies sind nur einige der Gründe warum REST für die eingebetteten System, die
wir bei Bosch bauen, attraktiv ist.

## Ein Beispiel

Hier ein (vereinfachtes) Beispiel aus der Heizungstechnik. Es illustriert, wie
eine REST-Schnittstelle mit einer JSON-Repräsentation verwendet werden kann um
eine Heizung ferzusteuern.

Frage die vorhandenen Räume ab:

	GET http://mein.haus.de/heizung/raeume 
	
liefert Status 200 (OK) 
	
	[ 
        {
            'id':'wohnzimmer', 
            'uri': 'http://mein.haus.de/heizung/raeume/wohnzimmer'
		}, 
		{ 
            'id':'bad', 
            'uri': 'http://mein.haus.de/heizung/raeume/bad' 
        } 
	]

Es werden nicht nur die Namen der Räume, sondern auch die URI's der Ressourcen,
die die Räume representieren, mitgeliefert. 

Frage die aktuelle Raumtemperatur im Wohnzimmer ab:

    GET http://mein.haus.de/heizung/raeume/wohnzimmer/temp 
	
liefert Status Code 200 (OK)

    { 
		'temp':'20.2', 
		'unit':'celsius' 
	}

Setze die Solltemperatur im Wohnzimmer auf 21 °C:

PUT http://mein.haus.de/heizung/raeume/wohnzimmer/sollTemp

mit Anhang

    { 
		'temp':'21.0' 
	}
	
liefert Status Code 204 (NO CONTENT)

Schalte die Heizung während meines Kurzurlaubs nächste Woche Wochenende
ausnahmsweise auf Frostbetrieb:

    POST http://mein.haus.de/heizung/heizplan/ausnahmen

mit Anhang		

	{ 
		'start':'2012-10-19T18:00', 
		'end':'2012-10-21T21:00',
		'modus': 'frost' 
	} 
	
liefert Status Code 201 (CREATED) 
	
	http://mein.haus.de/heizung/heizplan/ausnahmen/12

## Erfahrung bei Bosch

Ich habe in meiner Arbeit für die Bosch-interne FusionX Community mehrere
REST-Schnittstellen für verschiedene Domänen wie z. B. Heizungstechnik und
Fahrzeugtechnik entwickelt. Diese Schnittstellen haben wir erfolgreich in
mobilen Endgeräten und Browsern eingesetzt. Bosch Thermotechnik hat auf Basis
einer unserer Schnittstellen ein [Internet-Gateway](http://www.junkers.com/de/de/produkte/datenfernmanagement/junkershome/junkershome_produkt.aspx)
entwickelt und im Programm, welches den Fernzugriff auf Bosch-Heizungen
erlaubt. Andere Geschäftseinheiten evaluieren, bzw. planen den Einsatz von
ähnlichen REST-Schnittstellen in Ihren Produkten. Alles in Allem ist REST auf
dem besten Wege zu einer Basistechnologie für Bosch zu werden.

