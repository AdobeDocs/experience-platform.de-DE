---
title: Konfigurierbare und allgemeine Exporteinstellungen in Zielen
description: Erfahren Sie, welche Exporteinstellungen in Zielen auf Zielebene konfigurierbar sind und welche fest eingestellt sind und nicht bearbeitet werden können.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: 47197b745bebb6564d912d9dc045593bc076ae2a
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 92%

---

# Konfigurierbare und allgemeine Exporteinstellungen in Zielen

Hinsichtlich des Exportverhaltens für Experience Platform-Ziele müssen Sie drei separate Ebenen berücksichtigen, auf denen Konfigurationen funktionieren.

* Auf der ersten Ebene sind bestimmte Einstellungen im Zusammenhang mit dem Verhalten beim Profilexport und den Konfigurationseinstellungen allen Zielen, die zu einem Zieltyp gehören, gemein. Diese Einstellungen beziehen sich darauf, welche Trigger ein Zielexport ist und was in einem Export enthalten ist und von Zielentwicklern oder Real-Time CDP-Benutzern nicht bearbeitet werden kann.
* Auf zweiter Ebene können bestimmte Einstellungen vom Zielentwickler-Team beim Authoring von Zielen mit Destination SDK auf Zielebene angepasst werden.
* Auf dritter Ebene gibt es Konfigurationseinstellungen, die Real-Time CDP-Benutzer in den Aktivierungs-Workflows festlegen können.

![Abbildung der Wechselwirkung zwischen allgemeinen und konfigurierbaren Exporteinstellungen für Ziele](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Auf dieser Seite werden alle gängigen und konfigurierbaren Exporteinstellungen für Ziele auf den drei oben beschriebenen Ebenen beschrieben oder zu diesen verlinkt.

## Allgemeine Exporteinstellungen über alle Zieltypen hinweg {#common-settings-across-destination-types}

Das Verhalten beim Zielexport ist bei allen Zielen, die zu einem Zieltyp gehören, in Bezug darauf, *was einen Zielexport auslöst* und *was in den Zielexporten enthalten ist*, einheitlich. Zielexporte werden durch Benachrichtigungen ausgelöst, die der Ziel-Service vom [Upstream-Echtzeit-Kundenprofil-Service](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html#adobe-experience-platform-%26-applications-detailed-architecture-diagram) erhält.

Was in den Zielexporten enthalten ist, variiert geringfügig zwischen den Zieltypen. Erfahren Sie mehr über [allgemeine Exportverhaltensmuster nach Zieltyp](/help/destinations/how-destinations-work/profile-export-behavior.md). Diese Einstellungen können nicht von Zielentwicklern oder Real-Time CDP-Benutzern bearbeitet werden.

## Durch Zielentwicklerinnen und -entwickler anpassbare Exporteinstellungen {#customizable-settings-by-destination-developers}

Zielentwicklerinnen und -entwickler können mit [Destination SDK](/help/destinations/destination-sdk/overview.md) benutzer- oder produktdefinierte (private oder öffentliche) Ziele erstellen. Destination SDK bietet Entwickelnden eine große Flexibilität bei der Konfiguration von Zielen basierend auf den Downstream-Funktionen ihrer API-Endpunkte und Dateiempfangssysteme. Auf Grundlage der Downstream-Funktionen stehen Zielentwicklerinnen und -entwickler beim Konfigurieren eines Ziels mit Destination SDK die folgenden Konfigurationsoptionen zur Verfügung:

* Sie können bestimmen, welche Attribute und Identitäten aus Experience Platform für das Ziel exportiert werden können. Sie können auch bestimmen, welche Identitäten von ihren Zielen für einen erfolgreichen Datenexport erforderlich sind.
* Sie können eine Aggregationsrichtlinie festlegen, die bestimmt, wie lange Experience Platform beim Aggregieren von HTTP-Nachrichten warten soll, die an API-Integrationen gesendet werden. Sie können verschiedene Aggregationstypen konfigurieren, um zu bestimmen, wie viele Profile in ausgehenden HTTP-Nachrichten enthalten sein sollen und wie lange Experience Platform warten soll, bis die HTTP-Nachricht gesendet wird. Weitere Informationen zu den [Konfigurationsoptionen für Aggregationsrichtlinien](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) stehen Zielentwicklerinnen und -entwicklern in der Destination SDK-Dokumentation zur Verfügung.
* Sie können bestimmen, ob HTTP-Nachrichtenexporte Profile enthalten sollen, die sich für Segmente qualifizieren oder aus Segmenten entfernt werden oder beides.
* Sie können bestimmen, welche Dateinamens- und Dateiformatierungskonfigurationen Benutzenden beim Exportieren von Dateien zur Verfügung stehen sollen.

## Benutzerseitig anpassbare Einstellungen auf Datenflussebene {#settings-on-dataflow-level}

Neben den nicht bearbeitbaren Einstellungen, die vom Zieltyp und den vom Zielentwickler-Team konfigurierten Einstellungen abhängen, gibt es bestimmte Exporteinstellungen, die Benutzende im Aktivierungs-Workflow konfigurieren können. Diese Einstellungen beziehen sich auf den Exportzeitplan für einen bestimmten Datenfluss zu einem Ziel, die Attribute und Identitätsfelder, die in einen Datenfluss exportiert werden sollen, oder die Dateiformatierungsoptionen für exportierte Dateien.

Die Einstellungen, die Benutzenden beim Herstellen einer Zielverbindung zur Verfügung stehen, hängen davon ab, wie das Ziel vom Zielentwickler-Team konfiguriert wurde und welche Einstellungen den Benutzenden zur Verfügung gestellt wurden.

Beispiel: Für [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations) kann ein Zielentwickler-Team konfigurieren, welche Identitäten vom Ziel akzeptiert werden. Nur diese Identitäten werden dann den Benutzenden im [Zuordnungsschritt des Aktivierungs-Workflows](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) angezeigt, wie unten dargestellt:

![Bildschirmaufzeichnung der Identitätsauswahl für das Zielfeld im Zuordnungsschritt des Aktivierungs-Workflows. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Entsprechend kann das Zielentwickler-Team für [dateibasierte Ziele](/help/destinations/destination-types.md#file-based) bestimmen, welche [Optionen zum Anhängen von Dateinamen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) für das Ziel bzw. welche [Optionen zum Formatieren von Dateien](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) verfügbar gemacht werden sollen. Die Benutzenden können dann nur aus diesen Optionen auswählen, wie unten dargestellt:

![Bildschirmaufzeichnung der Dateiformatierungsoption beim Verbinden mit einem dateibasierten Ziel.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Bildschirmaufzeichnung der Option zum Anhängen von Dateinamen im Planungsschritt des Aktivierungs-Workflows. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Die folgenden verschiedenen Optionen und Schritte sind im Aktivierungs-Workflow verfügbar:

* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Unternehmensziele ](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportieren von Dateien nach Bedarf an Batch-Ziele](/help/destinations/ui/export-file-now.md)
* [Exportieren von Datensätzen an Cloud-Speicher-Ziele](/help/destinations/ui/export-datasets.md)

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, welche Exporteinstellungen für Ziele bei allen Zieltypen häufig sind, welche von Entwicklerinnen und Entwicklern auf individueller Zielebene konfiguriert werden können und welche Einstellungen von Benutzenden im Aktivierungs-Workflow bearbeitet werden können.

Ausführliche Informationen zum allgemeinen Exportverhalten für verschiedene Zieltypen [finden Sie hier](/help/destinations/how-destinations-work/profile-export-behavior.md).

[in dieser Anleitung](/help/destinations/destination-sdk/getting-started.md) für Zielentwicklerinnen und -entwickler finden Sie Informationen zu den ersten Schritten mit Destination SDK. Wenn Sie Daten aktivieren möchten, finden Sie alle verfügbaren Ziele im [Katalog](/help/destinations/catalog/overview.md).
