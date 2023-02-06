---
title: Konfigurierbare und allgemeine Exporteinstellungen in Zielen
description: Erfahren Sie, welche Exporteinstellungen in Zielen auf Zielebene konfigurierbar sind und die fest eingestellt sind und nicht bearbeitet werden können.
source-git-commit: 04322d10a88b27d5641ab9474c8387945aab9982
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---


# Konfigurierbare und allgemeine Exporteinstellungen in Zielen

Wenn Sie über das Exportverhalten für Experience Platform-Ziele nachdenken, müssen Sie drei separate Ebenen berücksichtigen, auf denen Konfigurationen funktionieren.

* Auf der ersten Ebene sind einige Einstellungen im Zusammenhang mit dem Profil-Exportverhalten und den Konfigurationseinstellungen für alle Ziele, die zu einem Zieltyp gehören, üblich. Diese Einstellungen beziehen sich darauf, welche Trigger ein Zielexport hat und was in einem Export enthalten ist und von Zielentwicklern oder Echtzeit-CDP-Benutzern nicht bearbeitet werden kann.
* Auf zweiter Ebene können einige Einstellungen vom Zielentwickler beim Authoring von Zielen mit Destination SDK auf Zielebene angepasst werden.
* Auf dritter Ebene gibt es Konfigurationseinstellungen, die von Benutzern der Echtzeit-Kundendatenplattform in den Aktivierungs-Workflows festgelegt werden können.

![Abbildung der Wechselwirkung zwischen allgemeinen und konfigurierbaren Exporteinstellungen für Ziele](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Auf dieser Seite werden alle gängigen und konfigurierbaren Exporteinstellungen für Ziele auf den drei oben beschriebenen Ebenen beschrieben oder mit diesen verlinkt.

## Allgemeine Exporteinstellungen für Zieltypen {#common-settings-across-destination-types}

Das Verhalten beim Zielexport ist bei allen Zielen, die zu einem Zieltyp gehören, in Bezug auf *Was Trigger ein Zielexport?* und *was in den Zielexporten enthalten ist*. Zielexporte werden durch Benachrichtigungen ausgelöst, die der Zieldienst vom [Upstream-Echtzeit-Kundenprofildienst](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Was in den Zielexporten enthalten ist, variiert geringfügig zwischen den Zieltypen. Mehr über [Allgemeine Exportverhaltensmuster pro Zieltyp](/help/destinations/how-destinations-work/profile-export-behavior.md). Diese Einstellungen können nicht von Zielentwicklern oder Echtzeit-CDP-Benutzern bearbeitet werden.

## Anpassbare Exporteinstellungen nach Ziel-Entwicklern {#customizable-settings-by-destination-developers}

Zielentwickler können [Destination SDK](/help/destinations/destination-sdk/overview.md) , um benutzerdefinierte oder produktionalisierte (private oder öffentliche) Ziele zu erstellen. Destination SDK bietet Entwicklern eine große Flexibilität bei der Konfiguration von Zielen basierend auf den nachgelagerten Funktionen ihrer API-Endpunkte und Dateiempfangssysteme. Basierend auf den nachgelagerten Funktionen stehen den Zielentwicklern beim Konfigurieren eines Ziels mit Destination SDK die folgenden Konfigurationsoptionen zur Verfügung:

* Bestimmen Sie, welche Attribute und Identitäten aus Experience Platform zum Ziel exportiert werden können. Bestimmen Sie auch, welche Identitäten für ihre Ziele für einen erfolgreichen Datenexport erforderlich sind.
* Legen Sie eine Aggregationsrichtlinie fest, die bestimmt, wie lange die Experience Platform beim Aggregieren von HTTP-Nachrichten warten soll, die an API-Integrationen gesendet werden. Ziel-Entwickler können verschiedene Aggregattypen konfigurieren, um zu bestimmen, wie viele Profile in ausgehenden HTTP-Nachrichten enthalten sein sollen und wie lange die Experience Platform warten soll, bis die HTTP-Nachricht gesendet wird. Weitere Informationen zu [Konfigurationsoptionen für Aggregationsrichtlinien](/help/destinations/destination-sdk/destination-configuration.md#aggregation) für Zielentwickler in der Dokumentation zur Destination SDK verfügbar.
* Bestimmen Sie, ob HTTP-Nachrichtenexporte Profile enthalten sollen, die sich für Segmente qualifizieren, die aus Segmenten entfernt werden oder beides.
* Legen Sie fest, welche Konfigurationen für Dateinamen und Dateiformatierung Benutzern beim Exportieren von Dateien zur Verfügung stehen sollen.

## Von Benutzern anpassbare Einstellungen auf der Datenflussebene {#settings-on-dataflow-level}

Neben den nicht bearbeitbaren Einstellungen, die vom Zieltyp und den vom Zielentwickler konfigurierten Einstellungen abhängen, gibt es bestimmte Exporteinstellungen, die Benutzer im Aktivierungs-Workflow konfigurieren können. Diese Einstellungen beziehen sich auf den Exportplan für einen bestimmten Datenfluss zu einem Ziel, die Attribute und Identitätsfelder, die in einen Datenfluss exportiert werden sollen, oder die Dateiformatierungsoptionen für exportierte Dateien.

Die Einstellungen, die Benutzern beim Herstellen einer Verbindung zu einem Ziel zur Verfügung stehen, hängen davon ab, wie das Ziel vom Zielentwickler konfiguriert wurde und welche Einstellungen den Benutzern zur Verfügung gestellt wurden.

Beispiel: für [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations)kann ein Zielentwickler konfigurieren, welche Identitäten sein Ziel akzeptiert und nur diese Identitäten dem Benutzer in [Zuordnungsschritt des Aktivierungs-Workflows](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), wie unten dargestellt:

![Bildschirmaufzeichnung der Identitätsauswahl für das Zielfeld im Zuordnungsschritt des Aktivierungs-Workflows. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Entsprechend gilt für [dateibasierte Ziele](/help/destinations/destination-types.md#file-based), kann der Zielentwickler bestimmen, [Dateinamenanhängen-Optionen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) sie für ihren Bestimmungsort verfügbar machen möchten oder [Dateiformatierungsoptionen](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) Sie möchten sie verfügbar machen und der Benutzer kann nur aus diesen Optionen auswählen, wie unten dargestellt:

![Bildschirmaufzeichnung der Dateiformatierungsoption beim Herstellen einer Verbindung zu einem dateibasierten Ziel.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Bildschirmaufzeichnung der Option &quot;Dateiname anhängen&quot;im Planungsschritt des Aktivierungs-Workflows. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Erfahren Sie mehr über die verschiedenen Optionen und Schritte, die im Aktivierungs-Workflow verfügbar sind:

* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Unternehmensziele](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportieren von Dateien On-Demand an Batch-Ziele](/help/destinations/ui/export-file-now.md)
* [(Beta) Exportieren von Datensätzen an Cloud-Speicher-Ziele](/help/destinations/ui/export-datasets.md)

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, welche Exporteinstellungen für Ziele bei allen Zieltypen gelten, welche von Entwicklern auf individueller Zielebene konfiguriert werden können und welche Einstellungen von Benutzern im Aktivierungs-Workflow bearbeitet werden können.

Für Zielentwickler können Sie [Erste Schritte](/help/destinations/destination-sdk/getting-started.md) mit Destination SDK. Benutzer, die Daten aktivieren möchten, können alle verfügbaren Ziele im Abschnitt [Katalog](/help/destinations/catalog/overview.md).