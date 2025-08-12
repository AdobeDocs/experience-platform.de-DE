---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: a26ad18b1e44b3198db9e8a36ad3749ed8a0afa2
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 18%

---

# Hinweise zu Vorabversionen von Adobe Experience Platform

>[!IMPORTANT]
>
>Dieses Dokument ist als **Vorschau** der Versionshinweise für den aktuellen Monat gedacht. Release-Elemente können sich ändern und in der endgültigen Version hinzugefügt oder entfernt werden.

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: August 2025**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Warnhinweise zur Streaming-Durchsatzkapazität | Drei neue Warnhinweise ermöglichen es Benutzenden, Warnhinweise zu abonnieren und zu konfigurieren, um die Leistung der Streaming-Durchsatzkapazität proaktiv zu verwalten und zu überwachen. Zu den neuen Warnhinweisen gehören Fälle, in denen der Streaming-Durchsatz 80 % bzw. 90 % erreicht oder die Kapazitätsbeschränkungen überschreitet. Weitere Informationen finden Sie im Handbuch [Kapazitätswarnungsregeln](../observability/alerts/rules.md#capacity). |

Weitere Informationen zu Warnhinweisen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../observability/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| --- | --- |
| [!DNL Acxiom Real ID Audience] | Verwenden Sie das [!DNL Acxiom Real ID Audience Connection] Ziel, um Zielgruppen mit [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/)-Technologie zu erweitern und Zielgruppen für mehrere Plattformen zu aktivieren, z. B. [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr. |


**Aktualisierte Ziele**

| Ziel | Beschreibung |
| --- | --- |
| Details zum Authentifizierungsablauf für [!DNL LinkedIn] Ziele | Machen Sie sich keine Gedanken mehr über abgelaufene Anmeldedaten. Informationen zum Kontoablauf sind jetzt direkt in der Experience Platform-Benutzeroberfläche sichtbar, sodass Sie sehen können, wann Ihre [!DNL LinkedIn]-Authentifizierung abläuft und erneuert wird, bevor sie zu Unterbrechungen Ihrer Datenflüsse führt. |
| Verschlüsselungsunterstützung für [!DNL Data Landing Zone] Ziele | Schützen Sie Ihre exportierten Daten mit Verschlüsselung. Sie können jetzt RSA-formatierte öffentliche Schlüssel anhängen, um Ihre exportierten Dateien zu verschlüsseln, sodass Sie dasselbe Sicherheitsniveau erhalten, das andere Cloud-Speicherziele für Ihre vertraulichen Informationen bieten. |
| [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) internes Upgrade | Ab dem 11. August 2025 können Sie im Zielkatalog zwei **[!DNL Microsoft Bing]** nebeneinander sehen. Dies ist auf ein internes Upgrade des Ziel-Service zurückzuführen. Der bestehende **[!DNL Microsoft Bing]**-Ziel-Connector wurde in **[!UICONTROL (veraltet) Microsoft Bing]** umbenannt, und es **[!UICONTROL jetzt eine neue Karte mit dem Namen]** Microsoft Bing verfügbar. Verwenden Sie die neue **[!UICONTROL Microsoft Bing]**-Verbindung im Katalog für neue Aktivierungsdatenflüsse. Wenn Sie aktive Datenflüsse zum **[!UICONTROL (veraltet) Microsoft Bing]**-Ziel haben, werden diese automatisch aktualisiert, sodass keine Aktion erforderlich ist. <br><br>Wenn Sie Datenflüsse über die [Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) erstellen, müssen Sie Ihre [!DNL flow spec ID] und [!DNL connection spec ID] auf die folgenden Werte aktualisieren:<ul><li>Flussspezifikations-ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Verbindungsspezifikations-ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Nach diesem Upgrade kann es zu einem **Rückgang der Anzahl aktivierter Profile** in Ihren Datenflüssen zu [!DNL Microsoft Bing] kommen. Dieser Rückgang wird durch die Einführung der **ECID-Zuordnungsanforderung** für alle Aktivierungen auf dieser Zielplattform verursacht. |
| Zusätzliche Kennungen für [!DNL Amazon Ads] Ziele | Das Amazon Ads-Ziel unterstützt jetzt neue Identitäten (`firstName`, `lastName`, `street`, `city`, `state`, `zip`, `country`). Diese Felder sollen die Übereinstimmungsraten der Zielgruppen verbessern und werden im Klartext mit optionalem SHA256-Hashing übergeben. |
| Konsolidierung [!DNL Marketo] Zielkarten | Vereinfachen Sie die Einrichtung Ihres [!DNL Marketo] Ziels mit unserer einheitlichen Zielkarte. Wir haben [!DNL Marketo] V2- und V3-Karten in einer optimierten Option zusammengefasst, sodass Sie leichter das richtige Ziel auswählen und schnell loslegen können. |

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Erweitern der Zeitpläne für den Datensatzexport für Datenflüsse, die vor November 2024 erstellt wurden | Wenn in Ihrem Unternehmen Datenflüsse für den Datensatzexport vor November 2024 erstellt wurden, funktionieren diese Datenflüsse ab dem 1. September 2025 nicht mehr. Wenn Sie die Datenflüsse benötigen, um nach dem 1. September 2025 weiterhin Daten zu exportieren, müssen Sie ihre Zeitpläne für jedes Ziel erweitern, an das Sie Datensätze exportieren, indem Sie die Schritte in [diesem Handbuch](../destinations/ui/dataset-expiration-update.md) befolgen. |
| Verbesserte Such-, Filter- und Tagging-Funktionen für Ziele | Verbessern Sie Ihren Zielverwaltungs-Workflow mit erweiterten Such-, Filter- und Tagging-Funktionen auf den Registerkarten Durchsuchen und Konten . Sie können jetzt nach bestimmten Datenflüssen und Konten nach Namen suchen, nach verschiedenen Kriterien wie Zielplattform, Status und Datum filtern und benutzerdefinierte Tags erstellen, um Ihre Ziele zu organisieren. Die Spaltensortierung ist auch für Schlüsselfelder wie die letzte Datenflusslaufzeit verfügbar, was die Identifizierung und Verwaltung Ihrer Zielverbindungen erleichtert. |

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Modellbasierte Schemata | Vereinfachen Sie Ihre Datenmodellierung mit modellbasierten Schemata. Sie können jetzt Schemas einfacher mit umfassenden Beispielen und Anleitungen erstellen. Diese Funktion steht derzeit Lizenzinhabern von Campaign Orchestration zur Verfügung und wird auf Kunden von Data Distiller bei GA ausgeweitet, was die Datenmodellierung zugänglicher und effizienter macht. |

Weitere Informationen finden Sie in der [XDM-Übersicht](../xdm/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zielgruppenschätzungen | Zielgruppenschätzungen werden jetzt automatisch in Segment Builder generiert. Dieser Wert wird bei jeder Änderung der Zielgruppe aktualisiert und entspricht immer den neuesten Zielgruppenregeln. |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für [!BADGE Beta]{type=Informative} Azure Private Link in der Benutzeroberfläche | Schützen Sie Ihre Daten mit privaten Netzwerkverbindungen. Sie können jetzt private Endpunkte erstellen und Datenflüsse einrichten, die das öffentliche Internet umgehen, sodass die Sicherheit und Netzwerkisolierung für Ihre sensiblen Daten verbessert wird. |
| Aktualisierungen der [!DNL Marketo]-Dokumentation | Verschaffen Sie sich einen vollständigen Überblick darüber, wie Ihre [!DNL Marketo] transformiert werden, wenn sie in Experience Platform eintreten. Alle Feldzuordnungen enthalten jetzt detaillierte Erläuterungen zu Datenumwandlungen, sodass Sie genau verstehen können, wie Ihre `PersonID` `leadID` wird und `eventType` `activityType` wird. |
| Unterstützung für die Authentifizierung des Service-Prinzipals für [!DNL Azure Blob Storage] | Sie können jetzt Ihr [!DNL Azure Blob Storage]-Konto mit Experience Platform verbinden, indem Sie die Authentifizierung als Service-Prinzipal durchführen. |

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
