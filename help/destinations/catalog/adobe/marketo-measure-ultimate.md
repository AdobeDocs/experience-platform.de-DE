---
title: Marketo Measure Ultimate-Ziel
description: Erfahren Sie, wie Sie Daten mit dem Marketo Measure Ultimate-Ziel verbinden und aktivieren.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 36%

---

# Marketo Measure Ultimate-Ziel {#mmu-destination}

## Übersicht {#overview}

Marketo Measure (ehemals Bizible) bietet Marketing-Experten Einblicke, welche Marketing-Maßnahmen am effektivsten sind, um Umsätze zu steigern und den ROI für ihr Unternehmen zu maximieren. Marketo Measure ist eine Marketing-Attributionslösung, die die Kanalleistung automatisch verfolgt und in Berichten aufzeigt. So erhalten Sie Einblicke in die Kanäle, die die Kundeninteraktion am meisten fördern, und können Ihre Marketingausgaben entsprechend optimieren.

Das Ziel ermöglicht den B2B-Datenfluss (Business-to-Business) von Adobe Experience Platform nach Marketo Measure. Die Karte steht nur Marketo Measure Ultimate-Kunden zur Verfügung.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Marketo Measure-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können. Diese Integration:

* erfüllt die komplexen Anforderungen an Daten und Leistungsberichte großer Unternehmen.
* Ermöglicht die Berichterstellung für die B2B-Attribution mit mehreren CRM- und Marketing-Automatisierungssystemen.
* Erleichtert die Einbindung von Offline-Kontaktpunktdaten von Drittanbietern.

## Voraussetzungen {#prerequisites}

Beachten Sie die folgenden Voraussetzungen für das Marketo Measure-Ziel:

* Experience Platform Sandbox-Zuordnung sollte vom Administrator auf der Seite mit den Marketo Measure-Einstellungen abgeschlossen werden. Ohne die Sandbox-Zuordnung können Sie den Workflow zum Herstellen einer Verbindung zum Ziel zum Speichern und Aktivieren von Daten nicht abschließen.
* Nur Datensätze von B2B-XDM-Klassen können exportiert werden (siehe z. B. die Klassen &quot;XDM Business Account&quot;und &quot;XDM Business Opportunity&quot;). Sie können nicht mehrere Datensätze derselben B2B-XDM-Klasse für eine bestimmte Datenquelle einbringen.
* Jeder Datensatz kann nur in einem Datenfluss zum Marketo Measure-Ziel enthalten sein.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Datensatzexport]** | Sie exportieren Rohdatensätze, die nicht nach Zielgruppeninteressen oder Qualifikationen gruppiert oder strukturiert sind. Weitere Informationen zu [Datensatzexporten](/help/destinations/destination-types.md#dataset-export-destinations). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Dieses Batch-Ziel exportiert alle zwei Stunden Dateien in die Marketo Measure-Plattform. Erfahren Sie mehr über [Planen von Datensatzexporten](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele in Datensätzen verwalten und aktivieren]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die im folgenden Abschnitt aufgelisteten Felder aus.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

![Der Workflow Mit Ziel verbinden für das Marketo Measure-Ziel.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Exportieren von Datensätzen in dieses Ziel {#export-datasets}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Datensatzziele verwalten und aktivieren]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Ausführliche Anweisungen zum Exportieren von Datensätzen in dieses Ziel finden Sie im Tutorial [Datensätze exportieren](/help/destinations/ui/export-datasets.md) .

## Überprüfen des Datenexports {#exported-data}

Um einen erfolgreichen Datensatzexport zu überprüfen, können Sie überprüfen, ob Ihr Datensatz erfolgreich zu Ihrem [Snowflake-Data Warehouse](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html) gelangt ist.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
