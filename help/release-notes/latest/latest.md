---
title: Adobe Experience Platform – Versionshinweise Februar 2026
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2026.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 05c9a99132d1385f9ec043bb667a72304b17a9b5
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 32%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/latest)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Versionsdatum: Mittwoch, 17. Februar 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [Ziele](#destinations)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)
- [Experience-Datenmodell (XDM)](#xdm)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Alerts] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Slack] Integration für Warnhinweise für Kunden | Sie können jetzt kundenorientierte Warnhinweise an [!DNL Slack] senden. Folgen Sie [&#x200B; Schritt-für-Schritt-Tutorial](../../observability/alerts/slack-integration.md) um die [!DNL Slack]-Integration einzurichten und Warnhinweise direkt in Ihrem [!DNL Slack]-Arbeitsbereich zu erhalten. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [[!DNL Snowflake] Batch](../../destinations/catalog/warehouses/snowflake-batch.md) allgemein verfügbar | Das [!DNL Snowflake] Batch-Ziel ist jetzt allgemein verfügbar. Real-Time CDP-Kunden auf der ganzen Welt können diesen Connector jetzt verwenden, um Daten in ihre Snowflake-Konten zu aktivieren, ohne die Daten physisch kopieren zu müssen. Alle Einschränkungen aus der eingeschränkten Version wurden aufgehoben (Verfügbarkeit nur für Kunden in den USA, Unterstützung für Zielgruppen, die nur zur standardmäßigen Zusammenführungsrichtlinie gehören). |

{style="table-layout:auto"}

**Fehlerbehebungen und Verbesserungen**

| Fehlerbehebung | Beschreibung |
| --- | --- |
| Warnhinweis für fehlgeschlagene Aktivierung überschritten | Die Zielwarnung „Fehlgeschlagene Aktivierungsrate“ wird jetzt korrekt für den Schwellenwert verwendet, den Sie beim Bewerten und Senden des Warnhinweises konfigurieren. Zuvor wurde der Warnhinweis mit einer Fehlerrate von 1 % ausgelöst, unabhängig vom konfigurierten Prozentsatz. Siehe [Standardmäßige Warnhinweisregeln](../../observability/alerts/rules.md#destinations) für weitere Informationen zu diesem Warnhinweis. |
| Berichte zu ausgeschlossenen Identitäten bei Google Customer Match | Es wurde ein Fehler in der Zählungslogik übersprungener Datensätze behoben, der dazu führte, dass für Google-Ziele zum Kundenabgleich überhöhte Werte für ausgeschlossene Profile angezeigt wurden. Das Aktivierungs- und Exportverhalten war nicht betroffen, nur die gemeldeten Zahlen waren falsch. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../../destinations/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Bearbeitbare API-Zielgruppen | Sie können jetzt Zielgruppen bearbeiten, die entweder mit der Segmentierungs-Service-API oder mit der Audience Agent in Segment Builder erstellt wurden. **Hinweis:** Zielgruppen, die Zeitreihendaten enthalten, **derzeit nicht** Segment Builder bearbeitet werden können. |
| Aktualisierung der Gültigkeit externer Zielgruppendaten | Sie können die Segmentierungs-Service-API verwenden, um den Datenablauf Ihrer externen Audiences zu verlängern. Weitere Informationen finden Sie im [API-Handbuch für externe Zielgruppen](/help/segmentation/api/external-audiences.md#extend-data-expiration). |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| Unterstützung des Unity-Katalogs [!DNL Databricks] Quell-Connector | Der [!DNL Databricks]-Quell-Connector unterstützt jetzt den Unity-Katalog. Lesen Sie die aktualisierte [[!DNL Databricks]](../../sources/connectors/databases/databricks.md)-Dokumentation , um zu erfahren, wie Sie beim Konfigurieren Ihrer Quellverbindung den Unity-Katalog verwenden. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

| Funktion | Beschreibung |
| --- | --- |
| Eingeschränkte Bearbeitung für Schemata mit Datensätzen | Bearbeitungsvorgänge, die zu grundlegenden Änderungen führen, sind jetzt eingeschränkt, sobald ein Datensatz für ein Schema vorhanden ist. Wenn ein Datensatz zugeordnet ist, können Sie Felder nicht mehr umbenennen oder löschen, Felddatentypen oder -formate ändern, Identitätsdeskriptoren ändern, verwandte Felder zum Entfernen vorhandener Felder verwalten oder die zugewiesene Klasse ändern. Additive Änderungen und das Verwerfen von Feldern werden weiterhin unterstützt. |

Weitere Informationen finden Sie in der [XDM-Übersicht](../../xdm/home.md).

