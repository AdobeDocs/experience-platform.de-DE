---
title: Adobe Experience Platform - Versionshinweise - Februar 2022
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2022.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 53%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 7. März 2022**

>[!NOTE]
>
>Diese Version wurde vom ursprünglichen Datum des 23. Februar auf den 7. März verschoben.

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards] durch die Sie wichtige Einblicke in die Daten Ihres Unternehmens anzeigen können, wie sie bei täglichen Momentaufnahmen erfasst werden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Widgets für Standardziele | Mit den folgenden Standard-Widgets können Sie verschiedene Metriken im Zusammenhang mit Ihren Zielen visualisieren.<ul><li>Kürzlich aktivierte Segmente nach Ziel. Dieses Widget zeigt die fünf am häufigsten aktivierten Segmente in absteigender Reihenfolge entsprechend dem ausgewählten Ziel an.</li><li>Trend der Zielgruppengröße. Dieses Widget zeigt die Beziehung der Profilanzahl über einen bestimmten Zeitraum für ein Segment, das diesem Zielkonto zugeordnet wurde.</li><li>Nicht zugeordnete Segmente nach Identität. Dieses Widget listet die fünf am häufigsten nicht zugeordneten Segmente nach absteigender Identitätsanzahl für ein bestimmtes Ziel und eine bestimmte Identität auf.</li><li>Zugeordnete Segmente nach Identität. Dieses Widget listet die fünf am häufigsten zugeordneten Segmente auf. Die Reihenfolge von Segmenten variiert von hoch bis niedrig entsprechend der jeweiligen Anzahl der Quell-IDs, die mit der im Dropdown-Menü des Widgets ausgewählten Ziel-ID übereinstimmen.</li><li>Allgemeine Zielgruppen. Dieses Widget bietet eine Liste der fünf wichtigsten Segmente, die für das am oberen Seitenrand ausgewählte Zielkonto aktiviert wurden, sowie das im Widget-Dropdown-Menü ausgewählte Ziel.</li></ul> Weitere Informationen zu den verfügbaren Standard-Widgets finden Sie im Abschnitt [Dashboard-Dokumentation zu Zielen.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

Weitere Informationen zu [!DNL Dashboards] finden Sie in der [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie an Adobe oder andere Ziele weitergegeben, transformiert und verteilt werden können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserter UI-Workflow für die Konfiguration von Datenströmen | Der Workflow zum Erstellen eines neuen Datenstroms in der Datenerfassungs-UI wurde aktualisiert. Beim Hinzufügen von Services zu einem Datenstrom werden nur die Services, auf die Sie Zugriff haben, in die Optionsliste aufgenommen. Weitere Informationen finden Sie in der Anleitung zum [Konfigurieren eines Datenstroms](../../edge/datastreams/overview.md). |
| Datenvorbereitung für die Datenerfassung | Wenn Sie das Adobe Experience Platform Web SDK verwenden, können Sie jetzt Datenvorlagenfunktionen verwenden, um Ihre Daten Server-seitig dem Experience-Datenmodell (XDM) zuzuordnen. Weitere Informationen finden Sie im Abschnitt [Datenvorbereitung für die Datenerfassung](../../edge/datastreams/data-prep.md) im Leitfaden zu den Datenströmen. |
| IDs von Erstanbieter-Geräten | Sie können jetzt Ihre eigenen Geräte-IDs beim Erfassen von Kundendaten mit dem Platform Web SDK an das Adobe Experience Platform Edge Network senden, um eine Problemumgehung für aktuelle Browser-Beschränkungen bei Cookie-Lebenszyklen von Drittanbietern zu bieten. Weitere Informationen finden Sie im Leitfaden zu [IDs von Erstanbieter-Geräten](../../edge/identity/first-party-device-ids.md). |

Weitere Informationen zur Datenerfassung in Platform finden Sie in der [Übersicht zur Datenerfassung](../../rtcdp-connections/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| (Beta) Destination SDK-Unterstützung für dateibasierte Ziele | [Destination SDK-Unterstützung für dateibasierte Ziele](../../destinations/destination-sdk/file-based-destination-configuration.md) befindet sich derzeit in der privaten Beta-Phase und steht nur einer ausgewählten Anzahl von Partnern und Kunden zur Verfügung. Die Funktionalität und die zugehörige Dokumentation können sich vor der Veröffentlichung der allgemeinen Verfügbarkeit ändern.<br><br>Wenden Sie sich an Ihren Kundenbetreuer, um zu erfahren, wie Sie auf die Funktion zugreifen können. Adobe-interne Kundenbetreuer sollten sich an die Produkt- und Engineering-Teams der Experience Platform-Ziele wenden, um unterstützte Anwendungsfälle zu besprechen. <br><br> In der Beta-Phase der Destination SDK-Unterstützung für dateibasierte Ziele können Beta-Partner und -Kunden die [Destination SDK der Experience Platform](/help/destinations/destination-sdk/overview.md) um private Ziele zu erstellen, um von der folgenden Funktion zu profitieren: <ul><li>Erstellen Sie ein dateibasiertes (Batch-)Ziel über Amazon S3, SFTP-Server, Azure Blob, Azure Data Lake Storage, Data Landing Zone Storage.</li><li>Konfigurieren und legen Sie die standardmäßigen Zeitplanungs- und Frequenzoptionen für Dateiexporte fest.</li><li>Konfigurieren und legen Sie Optionen zum Formatieren der exportierten CSV-Dateien fest (Trennzeichen, Escape-Zeichen und andere Optionen).</li><li>Möglichkeit zum Festlegen und Bearbeiten benutzerdefinierter Dateikopfzeilen.</li><li>Möglichkeit zum Empfang von Ereignisbenachrichtigungen über den Export von Dateien und Segmenten.</li><li>Möglichkeit, zusätzliche Dateitypen wie CSV, TSV, JSON, Parquet zu exportieren.</li></ul>  <br>Lesen Sie für die ersten Schritte mit der neuen Funktion [(Beta) Verwenden Sie Destination SDK, um ein dateibasiertes Ziel zu konfigurieren.](../../destinations/destination-sdk/file-based-destination-configuration.md). <br><br> Die Funktion zum Erstellen privater oder produktiver *Streaming* Ziele mithilfe von Destination SDK sind bereits für alle Experience Platform-Kunden und -Partner verfügbar. Lesen Sie das Handbuch zum [Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels](/help/destinations/destination-sdk/configure-destination-instructions.md) für Details. |

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Mit dem [!DNL Identity Service] von Adobe Experience Platform erhalten Sie einen besseren Überblick über Ihre Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend zusammenführen und so wirkungsvolle, persönliche digitale Erlebnisse in Echtzeit bereitstellen können.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Berechtigung für `view-identity-graph` | Sie können jetzt die Berechtigung `view-identity-graph` verwenden, um zu steuern, ob Benutzer in Ihrer Organisation Identitätsdiagrammdaten anzeigen können. Benutzern ohne diese Berechtigung wird der Zugriff auf den Identitätsdiagramm-Viewer in der UI oder beim Zugriff auf [!DNL Identity Service]-APIs, die Identitäten zurückgeben, untersagt. Weitere Informationen zu Berechtigungen finden Sie in der [Übersicht zur Zugriffskontrolle](../../access-control/home.md). |

Weitere allgemeine Informationen zum [!DNL Identity Service] finden Sie unter [Identity Service – Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).