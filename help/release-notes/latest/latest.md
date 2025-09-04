---
title: Adobe Experience Platform – Versionshinweise August 2025
description: Versionshinweise August 2025 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 24%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: Mittwoch, 19. August 2025**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [Katalog-Service](#catalog-service)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweise zur Streaming-Durchsatzkapazität | Drei neue Warnhinweise ermöglichen es Benutzenden, Warnhinweise zu abonnieren und zu konfigurieren, um die Leistung der Streaming-Durchsatzkapazität proaktiv zu verwalten und zu überwachen. Zu den neuen Warnhinweisen gehören Fälle, in denen der Streaming-Durchsatz 80 % bzw. 90 % erreicht oder die Kapazitätsbeschränkungen überschreitet. Weitere Informationen finden Sie im Handbuch [Kapazitätswarnungsregeln](../../observability/alerts/rules.md#capacity). |

Weitere Informationen zu Warnhinweisen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Katalog-Service {#catalog-service}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle in Experience Platform aufgenommenen Daten werden als Dateien und Ordner im Data Lake gespeichert. Catalog speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Datenaufbewahrung für das Echtzeit-Kundenprofil | Sie können **nur** die Datenaufbewahrungsdauer für das Echtzeit-Kundenprofil einmal alle 30 Tage aktualisieren. |

Weitere Informationen zum Katalog-Service finden Sie im Abschnitt [Übersicht über den Katalog-Service](../../catalog/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

>[!IMPORTANT]
>
>**Erweiterung des Datensatzexport-Zeitplans**
>
>Wenn in Ihrem Unternehmen Datenflüsse für den Datensatzexport vor November 2024 erstellt wurden, funktionieren diese Datenflüsse ab **1. September 2025**. Wenn Sie die Datenflüsse benötigen, um nach dem 1. September 2025 weiterhin Daten zu exportieren, müssen Sie ihre Zeitpläne für jedes Ziel erweitern, an das Sie Datensätze exportieren, indem Sie die Schritte in [diesem Handbuch](../../destinations/ui/dataset-expiration-update.md) befolgen.

>[!IMPORTANT]
>
>**Aktualisierung der IP-Zulassungsliste für API-basierte Ziele erforderlich**
>
>Aufgrund von Upgrades der Exportmodul-Engine für Streaming-Ziele müssen Unternehmen, die [IP-](../../destinations/catalog/streaming/ip-address-allow-list.md)Zulassungsliste auf die Zulassungsliste setzten) für API-basierte Ziele verwenden, die folgenden IP-Adressen zu ihren -**hinzufügen (vor dem 15. September 2025**:
>
>**Erforderliche IP-Adressen:**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**Diese Änderung gilt für die folgenden Zieltypen:**
>
>- [Exportziele für Streaming-Zielgruppen](../../destinations/destination-types.md#streaming-destinations) ([Pega CDH RealTime Audience](/help/destinations/catalog/personalization/pega-v2.md), API-basierte Integrationen mit [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) und [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Öffentliche oder private Ziele, die über [Destination SDK erstellt ](../../destinations/destination-sdk/getting-started.md)
>
>**Aktion erforderlich:** Wenn Sie mit Adobe an API-basierten Streaming-Zielen gearbeitet haben, müssen Sie die oben genannten IP-Adressen zu Ihrer Zulassungsliste auf die Zulassungsliste setzte hinzufügen, um einen unterbrechungsfreien Datenfluss zu Ihren API-basierten Zielen sicherzustellen.

**Neue Ziele**

| Ziel | Beschreibung |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Verwenden Sie das [!DNL Acxiom Real ID Audience Connection]-Ziel, um Zielgruppen mit [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/)-Technologie zu erweitern und Zielgruppen für mehrere Plattformen zu aktivieren, z. B. [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr. |

**Aktualisierte Ziele**

| Ziel | Beschreibung |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) internes Upgrade | Seit dem 11. August 2025 haben Sie im Zielkatalog für einen kurzen Zeitraum möglicherweise zwei **[!DNL Microsoft Bing]** nebeneinander gesehen. Dies ist auf ein internes Upgrade des Ziel-Service zurückzuführen. Der bestehende **[!DNL Microsoft Bing]**-Ziel-Connector wurde in **[!UICONTROL (veraltet) Microsoft Bing]** umbenannt, und es **[!UICONTROL jetzt eine neue Karte mit dem Namen]** Microsoft Bing verfügbar. <br> Das Upgrade wurde abgeschlossen und die veraltete Karte wurde aus dem Zielkatalog entfernt. Verwenden Sie die **[!UICONTROL Microsoft Bing]**-Verbindung im Katalog für neue Aktivierungsdatenflüsse. Wenn Sie aktive Datenflüsse zum **[!UICONTROL (veraltet) Microsoft Bing]**-Ziel hatten, werden diese automatisch aktualisiert, sodass keine Aktion erforderlich ist. <br><br>Wenn Sie Datenflüsse über die [Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) erstellen, müssen Sie Ihre [!DNL flow spec ID] und [!DNL connection spec ID] auf die folgenden Werte aktualisieren:<ul><li>Flussspezifikations-ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Verbindungsspezifikations-ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Nach diesem Upgrade kann es zu einem **Rückgang der Anzahl aktivierter Profile** in Ihren Datenflüssen zu [!DNL Microsoft Bing] kommen. Dieser Rückgang wird durch die Einführung der **ECID-Zuordnungsanforderung** für alle Aktivierungen auf dieser Zielplattform verursacht. |
| Details zur Authentifizierungsgültigkeit für Ziele von [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) und [LinkedIn übereinstimmende Zielgruppen](../../destinations/catalog/social/linkedin-b2b.md) | Informationen zum Authentifizierungsablauf für [!DNL LinkedIn] Ziele sind jetzt direkt in der Experience Platform-Benutzeroberfläche sichtbar, sodass Sie sehen können, wann Ihre Authentifizierung abläuft und erneuert wird, bevor sie zu Unterbrechungen Ihrer Datenflüsse führt. Sie können das Ablaufdatum Ihres Tokens über die Spalte **[!UICONTROL Account-Ablaufdatum]** entweder auf den Registerkarten **[[!UICONTROL Konten]](../../destinations/ui/destinations-workspace.md#accounts)** oder **[[!UICONTROL Durchsuchen]](../../destinations/ui/destinations-workspace.md#browse)** überwachen. |

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserte Such-, Filter- und Tagging-Funktionen für Ziele | Verbessern Sie Ihren Zielverwaltungs-Workflow mit erweiterten Such-, Filter- und Tagging-Funktionen auf den Registerkarten [Durchsuchen](../../destinations/ui/destinations-workspace.md#browse) und [Konten](../../destinations/ui/destinations-workspace.md#accounts). <br> Sie können jetzt nach bestimmten Datenflüssen und Konten nach Namen suchen, nach verschiedenen Kriterien wie Zielplattform, Status und Datum filtern und benutzerdefinierte Tags erstellen, um Ihre Ziele zu organisieren. Die Spaltensortierung ist auch für Schlüsselfelder wie die letzte Datenflusslaufzeit verfügbar, was die Identifizierung und Verwaltung Ihrer Zielverbindungen erleichtert. <br> ![Animierte Demonstration der Suche nach einem Ziel-Datenfluss auf der Registerkarte Durchsuchen](../../destinations/assets/ui/workspace/search.gif) |


## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Modellbasierte Schemata | Vereinfachen Sie Ihre Datenmodellierung mit modellbasierten Schemata. Sie können jetzt Schemas einfacher mit umfassenden Beispielen und Anleitungen erstellen. Diese Funktion steht derzeit Lizenzinhabern von Campaign Orchestration zur Verfügung und wird auf Kunden von Data Distiller bei GA ausgeweitet, was die Datenmodellierung zugänglicher und effizienter macht. |

Weitere Informationen finden Sie in der [XDM-Übersicht](../../xdm/home.md).

<!--

## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## Sandboxes {#sandboxes}

Experience Platform wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Deduplizierung des Abhängigkeitsobjekts im importierenden Workflow | Sandbox-Tools verwenden jetzt vorhandene Objekte immer wieder, wenn Objekte mit demselben Namen erkannt werden, um eine Vermehrung von Objekten zu vermeiden. Diese Änderung gilt für die folgenden Objekte: <ul><li>Schema</li><li>Feldergruppe</li><li>Zielgruppe</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Weitere Informationen finden Sie im [Handbuch zu Objekten, die für Sandbox-Tools unterstützt werden](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Gesamte Sandbox-Unterstützung für die Paketfreigabe zwischen Organisationen | Die Sandbox-Tools unterstützen jetzt **gesamte Sandbox**-Eingabe für die gemeinsame Nutzung von Organisations-Packages. Sie können jetzt sowohl ganze Sandbox- als auch Multi-Objekt-Pakete in allen Organisationen freigeben. Weitere Informationen finden Sie im [Handbuch zu Objekten, die für Sandbox-Tools unterstützt werden](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zielgruppenschätzungen | Zielgruppenschätzungen werden jetzt als **Bereich“ angezeigt** der auf dem Konfidenzintervall der Sampling-Daten basiert. Weitere Informationen zu Schätzungen finden Sie im [Segment Builder-Handbuch](/help/segmentation/ui/segment-builder.md#audience-properties). |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit der [!DNL Oracle NetSuite]-Quelle | Die [!DNL Oracle NetSuite] ist jetzt allgemein verfügbar. Sie können jetzt Ihr [!DNL Oracle NetSuite]-Konto mit Experience Platform verbinden, um Aktivitäts- und Entitätsdaten für eine einheitliche Analyse und Aktivierung aufzunehmen. Weitere Informationen finden Sie in der [[!DNL Oracle NetSuite] Übersicht](../../sources/connectors/marketing-automation/oracle-netsuite.md). |
| Allgemeine Verfügbarkeit der [!DNL PathFactory]-Quelle | Die [!DNL PathFactory] ist jetzt allgemein verfügbar. Sie können Ihr [!DNL PathFactory]-Konto mit Experience Platform verbinden, um Besucher-, Sitzungs- und Seitenansichtsdaten für eine einheitliche Analyse und Aktivierung aufzunehmen. Weitere Informationen finden Sie in der [[!DNL PathFactory] Übersicht](../../sources/connectors/marketing-automation/pathfactory.md). |
| Allgemeine Verfügbarkeit der [!DNL Stripe]-Quelle | Die [!DNL Stripe] ist jetzt allgemein verfügbar. Sie können Ihr [!DNL Stripe] mit Experience Platform verbinden, um Zahlungs- und Transaktionsdaten für eine einheitliche Analyse und Aktivierung aufzunehmen. Weitere Informationen finden Sie in der [[!DNL Stripe] Übersicht](../../sources/connectors/payments/stripe.md). |
| Erweiterte Authentifizierung für [!DNL Azure Blob Storage] | Sie können jetzt die auf Service-Prinzipalen basierende Authentifizierung verwenden, um Ihre [!DNL Azure Blob Storage] mit Experience Platform zu verbinden. Verwenden Sie die auf Service-Prinzipalen basierende Authentifizierung für erhöhte Sicherheit, einfachere Rotation der Anmeldeinformationen und eine granularere Zugriffssteuerung für Ihr Konto. Weitere Informationen finden Sie in der [[!DNL Azure Blob Storage] Übersicht](../../sources/connectors/cloud-storage/blob.md). |

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

<!---

| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

| Enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination  | The enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination is an upgraded version of the existing [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector. This new connector brings profile sync capabilities in addition to the existing audience sync capabilities from the legacy connector, providing a tighter integration with [!DNL Marketo Engage]. <br> The [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector will be deprecated in **March 2026**. To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** destination, review the following key points and required actions: <ul><li>All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.</li><li> **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../destinations/ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.</li></ul>|

-->

