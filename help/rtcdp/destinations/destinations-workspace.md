---
title: Zielarbeitsbereich
seo-title: Zielarbeitsbereich
description: Wählen Sie in der Adobe Echtzeit-Kundendatenplattform in der linken Navigationsleiste die Option Ziele, um auf den Zielarbeitsbereich zuzugreifen.
seo-description: Wählen Sie in der Adobe Echtzeit-Kundendatenplattform in der linken Navigationsleiste die Option Ziele, um auf den Zielarbeitsbereich zuzugreifen.
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# Zielarbeitsbereich {#destinations-workspace}

Wählen Sie in der Adobe Echtzeit-Kundendatenplattform in der linken Navigationsleiste &quot; **Ziele** &quot;aus, um auf den Arbeitsbereich &quot;Ziele&quot;zuzugreifen.

Der Arbeitsbereich &quot;Ziele&quot;besteht aus vier Bereichen: **Katalog**, **Durchsuchen**, **Konten** und **Datenfluss**, die in den folgenden Abschnitten beschrieben werden.

![Ziele-Übersicht](/help/rtcdp/destinations/assets/destinations-overview.png)

## Katalog {#catalog}

Auf der Registerkarte &quot; **[!UICONTROL Katalog]** &quot;wird eine Liste aller von Adobe angebotenen Ziele angezeigt, an die Sie Daten senden können. Wählen Sie ein Ziel im Katalog aus, um die rechte Leiste zu öffnen. Hier können Sie eine Verbindung zum Ziel (**Connect-Ziel**) herstellen oder detailliertere Informationen zu den einzelnen Zielen erhalten, indem Sie sich die Dokumentation ansehen (Dokumentation **anzeigen**).

![Optionen des Zielkatalogs](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Weitere Informationen zu Zielkategorien und Informationen zu den einzelnen Zielen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md).

## Durchsuchen {#browse}

Auf der Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;werden die Ziele angezeigt, zu denen Sie eine Verbindung hergestellt haben. Ziele mit aktiviertem Umschalter legen das Ziel auf &quot;aktiv&quot;und umgekehrt fest. Sie können auch die Ziele, an denen Daten fließen, anzeigen, indem Sie **Segmente > Durchsuchen** auswählen und ein zu prüfendes Segment auswählen. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte &quot;Durchsuchen&quot;bereitgestellt werden:

![Registerkarte &quot;Durchsuchen&quot;](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beschreibung |
---------|----------
| Zielname | Der Name, den Sie für die Aktivierung angegeben haben, fließt zu diesem Ziel. |
| Ziel | Die Zielplattform, die Sie für den Aktivierungsablauf ausgewählt haben. |
| Erstellt | Datum und Uhrzeit der Erstellung des Aktivierungsablaufs zum Ziel. |
| Verbindungstyp | *Nur* für E-Mail-Marketing-Ziele. Stellt den Verbindungstyp zu Ihrem Speicherbehälter dar. Kann S3 oder FTP sein. |
| Benutzername | Die Kontoanmeldeinformationen, die Sie für den Zielfluss ausgewählt haben. |
| Segmente | Die Anzahl der Segmente, die für dieses Ziel aktiviert werden. |
| Status | `Active` oder `Inactive`. Gibt an, ob Daten derzeit für dieses Ziel aktiviert werden. Informationen zum Bearbeiten des Status finden Sie unter Aktivierung [deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste anzuzeigen.

![Klickziel-Zeile](/help/rtcdp/destinations/assets/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen zu den für dieses Ziel aktivierten Segmenten anzuzeigen. Klicken Sie auf Aktivierung **[!UICONTROL bearbeiten]** , um die Segmente zu ändern oder hinzuzufügen, die an dieses Ziel gesendet werden.

## Konten {#accounts}

Auf der Registerkarte &quot; **[!UICONTROL Konten]** &quot;erfahren Sie mehr über die Verbindungen, die Sie mit verschiedenen Zielen hergestellt haben. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

![Registerkarte &quot;Konten&quot;](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beschreibung |
---------|----------
| Plattform | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| Benutzername | Der Benutzername, den Sie im [Verbindungsziel-Assistenten](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)ausgewählt haben. |
| Abläufe | Stellt die Anzahl der eindeutigen erfolgreichen Zielflüsse dar, die mit grundlegenden Informationen verknüpft sind, die für ein Ziel erstellt wurden. |
| Autorisiert | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |

## Datenflüsse {#data-flows}

Auf der Registerkarte &quot; **[!UICONTROL Datenflüsse]** &quot;wird eine grafische Darstellung der Aktivierungsflüsse angezeigt, die Sie auf der Echtzeit-Datenplattform eingerichtet haben.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Wählen Sie eines der Ziele aus, die auf der Seite angezeigt werden, und drücken Sie die **[!UICONTROL Eingabetaste]** , um Informationen zu allen Datenflüssen anzuzeigen, die Sie für jedes Ziel eingerichtet haben.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)