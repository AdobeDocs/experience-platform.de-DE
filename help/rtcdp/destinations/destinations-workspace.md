---
title: Arbeitsbereich „Ziele“
seo-title: Arbeitsbereich „Ziele“
description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
seo-description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# Arbeitsbereich „Ziele“ {#destinations-workspace}

Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option **Ziele**, um auf den Arbeitsbereich „Ziele“ zuzugreifen.

Der Arbeitsbereich „Ziele“ besteht aus vier Bereichen: **Katalog**, **Durchsuchen**, **Konten** und **Datenflüsse**. Diese werden in den folgenden Abschnitten beschrieben.

![Zielüberblick](/help/rtcdp/destinations/assets/destinations-overview.png)

## Katalog {#catalog}

The **[!UICONTROL Catalog]** tab displays a list of all destinations offered by Adobe, that you can send data to. Wählen Sie ein Ziel im Katalog aus, um die rechte Leiste zu öffnen. Hier können Sie eine Verbindung zum Ziel herstellen (**Ziel verbinden**) oder genauere Informationen zu den einzelnen Zielen erhalten, indem Sie die Dokumentation anzeigen (**Dokumentation anzeigen**).

![Optionen im Zielkatalog](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Weiterführende Informationen zu Zielkategorien sowie Informationen zu einzelnen Zielen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md).

## Durchsuchen {#browse}

The **[!UICONTROL Browse]** tab displays the destinations with which you have established a connection. Ziele mit aktiviertem Umschalter legen das Ziel auf „aktiv“ fest und umgekehrt. Sie können auch jene Ziele, bei denen Daten fließen, anzeigen, indem Sie **Segmente > Durchsuchen** wählen und ein zu prüfendes Segment auswählen. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte „Durchsuchen“ verfügbar sind:

![Registerkarte „Durchsuchen“](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beschreibung |
---------|----------
| Zielname | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. |
| Ziel | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| Erstellt | Datum und Uhrzeit (UTC) der Erstellung des Aktivierungsflusses zum Ziel. |
| Verbindungstyp | *Nur für E-Mail-Marketing-Ziele*. Stellt den Verbindungstyp zu Ihrem Speicher-Bucket dar. Dabei kann es sich um S3 oder FTP handeln. |
| Benutzername | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| Segmente | Die Zahl der Segmente, die für dieses Ziel aktiviert werden. |
| Status | `Active` oder `Inactive`. Gibt an, ob für dieses Ziel derzeit Daten aktiviert sind. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste anzuzeigen.

![Auf Zielzeile klicken](/help/rtcdp/destinations/assets/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen zu den für dieses Ziel aktivierten Segmenten anzuzeigen. Click **[!UICONTROL Edit activation]** to modify or add to the segments that are being sent to this destination.

## Konten {#accounts}

In the **[!UICONTROL Accounts]** tab, you can learn more about the connections that you have established with various destinations. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

![Registerkarte „Konten“](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beschreibung |
---------|----------
| Plattform | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| Benutzername | Der Benutzername, den Sie im [Zielverbindungsassistenten](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination) ausgewählt haben. |
| Flüsse | Gibt die Zahl der eindeutigen erfolgreich verbundenen Zielflüsse mit grundlegenden Informationen an, die für ein Ziel erstellt wurden. |
| Autorisiert | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |

## Datenflüsse {#data-flows}

The **[!UICONTROL Data flows]** tab displays a graphic representation of the activation flows that you have set up in the Real-time Customer Data Platform.

![Datenflüsse1](/help/rtcdp/destinations/assets/data-flows1.png)

Select any of the destinations displayed on the page and press **[!UICONTROL View flows]** to see information on all the data flows you have set up for each destination.

![Datenflüsse2](/help/rtcdp/destinations/assets/data-flows2.png)