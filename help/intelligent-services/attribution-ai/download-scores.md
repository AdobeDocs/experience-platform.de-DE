---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: Zugreifen auf Ergebnisse in Attribution AI
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 689b4c7a96856e1167ee435a6740fed006136256

---


# Zugreifen auf Ergebnisse in Attribution AI

>[!IMPORTANT] Weitere Informationen zu Rohdaten-Downloads für den Massenexport von Daten erhalten Sie unter attributionai-support@adobe.com.

Der Zugriff auf Ergebnisse für Attribution AI erfolgt über Snowflake. Derzeit müssen Sie den Adobe-Support unter attributionai-support@adobe.com per E-Mail senden, um die Anmeldeinformationen für Ihr Reader-Konto für Snowflake einzurichten und zu erhalten.

Nachdem der Adobe-Support Ihre Anforderung verarbeitet hat, erhalten Sie eine URL für das Reader-Konto für Snowflake und die entsprechenden Anmeldeinformationen unten:

- Schneeflocken-URL
- Benutzername
- Kennwort

>[!NOTE] Das Reader-Konto dient zum Abfragen der Daten mit SQL-Clients, Arbeitsblatt- und BI-Lösungen, die JDBC Connector unterstützen.

Sobald Sie über Ihre Anmeldeinformationen und Ihre URL verfügen, können Sie die Modelltabellen entweder im Rohformat, nach Touchpoint-Datum oder Konvertierungsdatum aggregieren.

## Schema im Schneeflocken finden

Melden Sie sich mit den angegebenen Anmeldeinformationen bei Snowflake an. Klicken Sie im linken oberen Navigationsbereich auf die Registerkarte **Arbeitsblätter** und navigieren Sie dann im linken Bereich zu Ihrem Datenbankverzeichnis.

![Arbeitsblätter und Navigation](./images/download-scores/edited_snowflake_1.png)

Klicken Sie dann in der oberen rechten Ecke des Bildschirms auf Schema **** auswählen. Vergewissern Sie sich, dass im angezeigten Popup die richtige Datenbank ausgewählt ist. Klicken Sie anschließend auf das Dropdownmenü *Schema* und wählen Sie eines der aufgelisteten Schema aus. Sie können direkt aus den unter dem ausgewählten Schema aufgelisteten Ergebnistabellen Abfragen auswählen.

![Schema suchen](./images/download-scores/edited_snowflake_2.png)

## Herunterladen von Rohwerten

Weitere Informationen zu Rohdaten-Downloads erhalten Sie unter attributionai-support@adobe.com.

## Verbinden von PowerBI mit Snowflake (optional)

Mit Ihren Snowflake-Anmeldeinformationen können Sie eine Verbindung zwischen PowerBI Desktop- und Snowflake-Datenbanken herstellen.

Geben Sie zunächst unter dem Feld *Server* Ihre Snowflake-URL ein. Geben Sie als Nächstes unter *Warehouse*&quot;XSMALL&quot;ein. Geben Sie dann Ihren Benutzernamen und Ihr Passwort ein.

![Beispiel von POWERBI](./images/download-scores/powerbi-snowflake.png)

Nachdem die Verbindung hergestellt wurde, wählen Sie Ihre Snowflake-Datenbank aus und wählen Sie dann das entsprechende Schema aus. Sie können jetzt alle Tabellen laden.

Nachdem Sie Ihr Schema ausgewählt haben, werden Tabellen mit Ihren Zuordnungswerten angezeigt.

| Tabelle | Beschreibung |
| ----- | ----------- |
| APP_{APP_ID} | Rohzuordnungsergebnis. |
| APP_{APP_ID}_BY_CONV_DATE | Rohzuordnungswert, aggregiert auf der Ebene des Konvertierungsdatums. |
| APP_{APP_ID}_BY_TP_DATE | Rohzuordnungswert, aggregiert auf der Touchpoint-Datumsebene. |

## Nächste Schritte

In diesem Dokument werden die Schritte beschrieben, die für die Abfrage von Daten und den Zugriff auf Ergebnisse für Attribution AI erforderlich sind. Sie können jetzt auch weiterhin die anderen angebotenen [Intelligent Services](../home.md) und Handbücher durchsuchen.