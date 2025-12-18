Protokoll

Projekt: industriepc_lbulic_msimov_soezturk_gsina

Schritt 1 – Dokumentation & Hardwareanalyse

Zunächst wurde die vorhandene Dokumentation der Beckhoff-Hardware recherchiert und studiert. Ziel war es, die eingesetzten I/O-Karten zu identifizieren und deren Funktion (Input / Output) festzulegen.

Ergebnis:
	•	Output-Karten (Ausgänge):
	•	EL2004
	•	EL2008
	•	Input-Karten (Eingänge):
	•	EL1008
	•	EL1104
	•	EL1104

Dabei wurde festgelegt:
	•	Button (Taster) → Input
	•	Lampe → Output

Diese Zuordnung ist notwendig für das spätere Hardware-Mapping in TwinCAT.

⸻

Schritt 2 – Verbindung des Industrie-PCs

Der Industrie-PC wurde über LAN mit dem Netzwerk verbunden, da WLAN für industrielle Anwendungen als zu instabil gilt.

Problem:
	•	Das verwendete LAN-Kabel funktionierte nicht korrekt
	•	Die Netzwerkverbindung konnte nicht hergestellt werden

Maßnahme:
	•	Für zukünftige Versuche wird ein geprüftes, funktionsfähiges LAN-Kabel verwendet

⸻

Schritt 3 – Ermitteln der IP-Adresse

Nach der Netzwerkverbindung wurde versucht, die IP-Adresse des Industrie-PCs zu ermitteln.

Verwendeter Befehl:

ip addr show

Dieser Befehl listet alle Netzwerkinterfaces inklusive der zugewiesenen IP-Adressen auf.

⸻

Schritt 4 – Erstellen der Authentifizierungsdatei

Für den Zugriff auf Beckhoff-Paketquellen wurde eine Authentifizierungsdatei angelegt.

Befehl:

sudo nano /etc/apt/auth.conf.d/bhf.conf

In dieser Datei werden die Zugangsdaten für die Beckhoff-Repositorys hinterlegt.

⸻

Schritt 5 – Installation von TwinCAT (XAR)

Nach der Vorbereitung wurde TwinCAT Runtime unter Linux installiert.

Befehle:

sudo apt update
sudo apt install tc31-xar-um

Zusätzlich wurde die offizielle Beckhoff-Dokumentation verwendet:
Beckhoff_RT_Linux_de.pdf (Embedded PC CX)

⸻

Schritt 6 – SPS-Programmierung (TwinCAT)

Ziel des Programms ist es, mit einem Taster eine Lampe zu toggeln.
Bei jeder steigenden Flanke (Taster wird gedrückt) ändert die Lampe ihren Zustand (Ein/Aus).

Funktionsprinzip
	•	Der Taster wird als digitale Eingangsvariable gemappt
	•	Die Lampe wird als digitale Ausgangsvariable gemappt
	•	Ein R_TRIG-Baustein erkennt die steigende Flanke
	•	Bei erkannter Flanke wird der Zustand der Lampe invertiert

SPS-Code (Structured Text)

PROGRAM MAIN
VAR
    // Hardware-Variablen (Namen bleiben für das Mapping erhalten)
    bKnopf  AT %I* : BOOL; 
    bLampe  AT %Q* : BOOL;
    
    // Instanz zur Erkennung der steigenden Flanke
    fbTasterFlanke : R_TRIG;
END_VAR

// Aktuellen Zustand des Tasters an den Flankenerkennungs-Baustein übergeben
fbTasterFlanke(CLK := bKnopf);

// Wenn eine positive Flanke erkannt wurde
IF fbTasterFlanke.Q THEN
    // Lampenzustand umschalten
    bLampe := NOT bLampe;
END_IF


⸻

Ergebnis
	•	Die Hardware-Zuordnung (Input / Output) wurde erfolgreich analysiert
	•	TwinCAT wurde unter Linux installiert
	•	Ein funktionales SPS-Programm zur Taster-Lampenschaltung wurde erstellt
	•	Die Logik arbeitet flankengetriggert und verhindert Mehrfachschaltungen beim Gedrückthalten des Tasters

⸻
