# industriepc_lbulic_msimov_soezturk_gsina

## Schritt 1
Doku finden, sich über die einzelnen Karten informieren INPUT OUTPUT für Lampe & Button (Button = Input, Lampe = Output). 
herausgefunden dass karten -> EL2004 und EL 2008 output sind und EL1008 1104 und 1104 für input sind

## Schritt 2
Den IndustriePC über LAN (weil WLAN zu instabil für Industrie) verbinden, dabei hat LAN kabel nicht funktioniert und 
Verbindung fehlgeschlagen -> näcshtes mal gutes lan kabel benutzen

## Schritt 3
IP Adresse ermitteln mittels ```addr show```

## Schritt 4
Erstellen einer Authdatei <br>
```sudo nano /etc/apt/auth.conf.d/bhf.conf```

## Schritt 5
Twincat installieren
´´´sudo apt update``` <br>
```sudo apt install tc31-xar-um```ad.beckhoff.com/download/document/ipc/embedded-pc/embedded-pc-cx/Beckhoff_RT_Linux_de.pdf/embedded-pc-cx/Beckho
