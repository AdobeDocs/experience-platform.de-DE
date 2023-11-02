---
title: Adobe Experience Platform – Versionshinweise Februar 2022
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2022.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 99%

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

Adobe Experience Platform bietet mehrere [!DNL dashboards], mit denen Sie wichtige Einblicke in die Daten Ihrer Organisation erhalten, die in täglichen Snapshots erfasst werden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Widgets für Standardziele | Mit den folgenden Standard-Widgets können Sie verschiedene Metriken im Zusammenhang mit Ihren Zielen visualisieren.<ul><li>Kürzlich aktivierte Segmente nach Ziel. Dieses Widget zeigt die fünf am häufigsten aktivierten Segmente in absteigender Reihenfolge für das ausgewählte Ziel an.</li><li>Trend der Zielgruppengröße. Dieses Widget stellt die Entwicklung der Profilanzahl über einen bestimmten Zeitraum für ein Segment dar, das diesem Zielkonto zugeordnet wurde.</li><li>Nicht zugeordnete Segmente nach Identität. Dieses Widget listet die fünf häufigsten nicht zugeordneten Segmente auf, die nach absteigender Identitätsanzahl für ein bestimmtes Ziel und eine bestimmte Identität angeordnet werden.</li><li>Zugeordnete Segmente nach Identität. Dieses Widget listet die fünf am häufigsten zugeordneten Segmente auf. Die Reihenfolge der Segmente entspricht der jeweiligen Anzahl der Quell-IDs von hoch bis niedrig, die mit der im Dropdown-Menü des Widgets ausgewählten Ziel-ID übereinstimmen.</li><li>Häufige Zielgruppen. Dieses Widget bietet eine Liste der fünf wichtigsten Segmente, die für das am oberen Seitenrand ausgewählte Zielkonto aktiviert wurden, sowie das im Widget-Dropdown-Menü ausgewählte Ziel.</li></ul> Weitere Informationen zu den verfügbaren Standard-Widgets finden Sie in der [Dokumentation zum Ziele-Dashboard](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets). |

Weitere Informationen zu [!DNL Dashboards] finden Sie in der [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie an Adobe oder andere Ziele weitergegeben, transformiert und verteilt werden können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserter UI-Workflow für die Konfiguration von Datenströmen | Der Workflow zum Erstellen eines neuen Datenstroms in der Datenerfassungs-UI wurde aktualisiert. Beim Hinzufügen von Services zu einem Datenstrom werden nur die Services, auf die Sie Zugriff haben, in die Optionsliste aufgenommen. Weitere Informationen finden Sie in der Anleitung zum [Konfigurieren eines Datenstroms](../../datastreams/overview.md). |
| Datenvorbereitung für die Datenerfassung | Wenn Sie das Adobe Experience Platform Web SDK verwenden, können Sie jetzt Datenvorlagenfunktionen verwenden, um Ihre Daten Server-seitig dem Experience-Datenmodell (XDM) zuzuordnen. Weitere Informationen finden Sie im Abschnitt [Datenvorbereitung für die Datenerfassung](../../datastreams/data-prep.md) im Leitfaden zu den Datenströmen. |
| IDs von Erstanbieter-Geräten | Sie können jetzt Ihre eigenen Geräte-IDs beim Erfassen von Kundendaten mit dem Platform Web SDK an das Adobe Experience Platform Edge Network senden, um eine Problemumgehung für aktuelle Browser-Beschränkungen bei Cookie-Lebenszyklen von Drittanbietern zu bieten. Weitere Informationen finden Sie im Leitfaden zu [IDs von Erstanbieter-Geräten](../../edge/identity/first-party-device-ids.md). |

Weitere Informationen zur Datenerfassung in Platform finden Sie in der [Übersicht zur Datenerfassung](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| (Beta) Destination SDK-Unterstützung für dateibasierte Ziele | Die [Destination SDK-Unterstützung für dateibasierte Ziele](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) befindet sich derzeit in der privaten Beta-Phase und steht nur einer ausgewählten Anzahl von Partnern und Kundinnen bzw. Kunden zur Verfügung. Die Funktionalität und die zugehörige Dokumentation können sich vor der Veröffentlichung zur allgemeinen Verfügbarkeit ändern.<br><br>Wenden Sie sich an die Adobe-Kundenbetreuung, um zu erfahren, wie Sie auf die Funktion zugreifen können. Adobe-internes Kundenbetreuungspersonal sollte sich an die Produkt- und Engineering-Teams für Experience Platform-Ziele wenden, um unterstützte Anwendungsfälle zu besprechen. <br><br> In der Beta-Phase der Destination SDK-Unterstützung für dateibasierte Ziele können Beta-Partner sowie -Kundinnen und -Kunden das [Experience Platform Destination SDK](../../destinations/destination-sdk/overview.md) verwenden, um private Ziele zu erstellen, die von den folgenden Funktionen profitieren: <ul><li>Erstellen eines dateibasierten (Batch-)Ziels über Amazon S3, SFTP-Server, Azure Blob, Azure Data Lake Storage, Data Landing Zone-Speicher.</li><li>Konfigurieren und Festlegen von standardmäßigen Zeitplanungs- und Frequenzoptionen für Dateiexporte.</li><li>Konfigurieren und Festlegen von Optionen zum Formatieren der exportierten CSV-Dateien (Trennzeichen, Escape-Zeichen und andere Optionen).</li><li>Möglichkeit zum Festlegen und Bearbeiten benutzerdefinierter Dateikopfzeilen.</li><li>Möglichkeit zum Empfang von Ereignisbenachrichtigungen über den Export von Dateien und Segmenten.</li><li>Möglichkeit, zusätzliche Dateitypen wie CSV, TSV, JSON, Parquet zu exportieren.</li></ul>  <br>Lesen Sie für die ersten Schritte mit den neuen Funktionen [(Beta) Verwenden von Destination SDK, um ein dateibasiertes Ziel zu konfigurieren](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> Die Funktion zum Erstellen privater oder produktbezogener *Streaming*-Ziele mithilfe von Destination SDK ist bereits für alle Experience Platform-Kundinnen und -Kunden sowie -Partner verfügbar. Lesen Sie das Handbuch zum [Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels](../../destinations/destination-sdk/guides/configure-destination-instructions.md) für Details. |

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihrer Kundinnen und Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Mit dem [!DNL Identity Service] von Adobe Experience Platform erhalten Sie einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend zusammenführen und so wirkungsvolle, persönliche digitale Erlebnisse in Echtzeit bereitstellen können.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Berechtigung für `view-identity-graph` | Sie können jetzt die Berechtigung `view-identity-graph` verwenden, um zu steuern, ob Benutzerinnen und Benutzer in Ihrer Organisation Identitätsdiagrammdaten anzeigen können. Benutzerinnen und Benutzern ohne diese Berechtigung wird der Zugriff auf den Identitätsdiagramm-Viewer in der Benutzeroberfläche oder beim Zugriff auf [!DNL Identity Service]-APIs, die Identitäten zurückgeben, untersagt. Weitere Informationen zu Berechtigungen finden Sie in der [Übersicht zur Zugriffskontrolle](../../access-control/home.md). |

Weitere allgemeine Informationen zum [!DNL Identity Service] finden Sie unter [Identity Service – Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).