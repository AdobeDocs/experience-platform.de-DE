---
title: Demandbase People-Verbindung
description: Verwenden Sie dieses Ziel, um Ihre Zielgruppen zu aktivieren und sie mit Demandbase-Drittanbieterdaten für andere nachgelagerte Anwendungsfälle in Marketing und Vertrieb anzureichern.
source-git-commit: df2cb1edbf998082fca961e6d9bb567a1ad3b7e6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 33%

---


# Demandbase People-Verbindung {#demandbase-people}

Aktivieren Sie Profile für Ihre Demandbase-Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung.

>[!IMPORTANT]
>
>Verwenden Sie für B2B-Anwendungsfälle, bei denen Sie [Account-Zielgruppen aktivieren](../../ui/activate-account-audiences.md), stattdessen den [Demandbase](demandbase.md)-Ziel-Connector.

## Anwendungsfall {#use-case}

Marketing-Experten können Adobe Real-Time CDP verwenden, um eine Liste von Erstanbieterkontakten zu erstellen und in Demandbase zu aktivieren, um eine optimierte und koordinierte Interaktion über die Demand-Side-Plattform (DSP) und andere Kanäle wie LinkedIn zu ermöglichen.

Dieser Ansatz ermöglicht es Marketing-Experten, die Ausgaben für Kampagnen bekannten Personen zu priorisieren, die von ihrem eigenen CRM- oder Marketing-Automatisierungssystem bezogen werden, um sicherzustellen, dass sich Marketing-Maßnahmen auf hochwertige Interessenten konzentrieren.

Nach der Aktivierung optimiert Demandbase die Bereitstellung von Anzeigen und verfeinert Zielgruppenbestimmungsstrategien, um die Interaktion, Reichweite und Konversionsraten zu maximieren, was letztendlich die Kampagneneffizienz verbessert.

## Unterstützte Identitäten {#supported-identities}

Die [!DNL Demandbase People]-Verbindung unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | Nur-Text-E-Mail-Adressen | Die [!DNL Demandbase People]-Verbindung unterstützt nur E-Mail-Adressen im Klartext. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-and-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|--------------|-----------|---------------------------|
| Exporttyp | Zielgruppenexport | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im Ziel *Demandbase* verwendet werden. |
| Häufigkeit | Streaming | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Um Zielgruppen in die Demandbase zu exportieren, benötigen Sie Folgendes:

1. Ein Demandbase-Konto.
2. Ein Demandbase-API-Token. Sie können in Demandbase ein API-Token mit Ihrem Benutzer generieren. Um ein Token zu generieren, navigieren Sie zu [Mein Profil > API-Token](https://web.demandbase.com/o/ad/at) nachdem Sie sich bei Ihrem Demandbase-Konto angemeldet haben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Bearer-Token hinzufügen](../../assets/catalog/advertising/demandbase-people/bearer-token.png)

* **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren. Unter [Voraussetzungen](#prerequisites) finden Sie Informationen zum Abrufen des Tokens.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Fügen Sie Informationen über die Zielverbindung hinzu](../../assets/catalog/advertising/demandbase-people/name-and-description.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

Jetzt können Sie Ihre Zielgruppen in Demandbase People aktivieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Zusätzliche Hinweise und wichtige Hinweise {#additional-notes}

* **Leitplanken für die Demandbase**: Wenn Sie Zielgruppen in Demandbase exportiert haben und die Exporte in Experience Platform erfolgreich sind, aber nicht alle Daten die Demandbase erreichen, haben Sie möglicherweise auf der Demandbase-Seite auf API-Einschränkungen gestoßen. Wenden Sie sich zur Klärung an sie.
* **Löschen von Listen**: Personenlisten sind eindeutig, sodass Sie keine neue Liste mit einem bereits verwendeten Namen neu erstellen können. Wenn Sie Personen aus einer Liste entfernen, sind diese nicht mehr verfügbar, aber sie werden nicht gelöscht.
* **Aktivierungszeit**: Das Laden von Daten in Demandbase unterliegt der Nachtverarbeitung.
* **Zielgruppenname**: Wenn eine Konto-Zielgruppe mit demselben Namen zuvor für Demandbase aktiviert wurde, können Sie sie nicht über einen anderen Datenfluss zum Demandbase-Ziel erneut aktivieren.
