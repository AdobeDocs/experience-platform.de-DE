---
title: Demandbase-Verbindung
description: Verwenden Sie dieses Ziel, um Ihre Zielgruppen für Account-Based Marketing (ABM) zu aktivieren. Werben Sie über die B2B-Demand Side Platform (DSP) von DemandBase an relevante Personen und Rollen in Ihren Zielkonten. Target-Konten können auch mit Demandbase-Drittanbieterdaten angereichert werden, um sie für andere nachgelagerte Anwendungsfälle in Marketing und Vertrieb nutzen zu können.
badgeB2B: label="B2B Edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
source-git-commit: 92abae6bc63c13f1103364ae82cc9c04459ce00f
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 26%

---


# Demandbase-Verbindung {#demandbase}

>[!AVAILABILITY]
>
>>Die Funktion zum Aktivieren von Kontozielgruppen für das Demandbase-Ziel ist für Unternehmen verfügbar, die die Editionen [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) von Real-time Customer Data Platform erwerben.

Aktivieren Sie Profile für Ihre Demandbase-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung, basierend auf [Konto-Zielgruppen](/help/segmentation/ui/account-audiences.md) .

## Anwendungsfall {#use-case}

Verwenden Sie dieses Ziel, um Ihre Zielgruppen für Account-Based Marketing (ABM) zu aktivieren. Werben Sie über die B2B-Demand Side Platform (DSP) von DemandBase an relevante Personen und Rollen in Ihren Zielkonten. Target-Konten können auch mit Demandbase-Drittanbieterdaten angereichert werden, um sie für andere nachgelagerte Anwendungsfälle in Marketing und Vertrieb nutzen zu können.

Nutzen Sie beispielsweise die DSP von Demandbase, um bestimmte Rollen oder Rollen innerhalb wichtiger Konten für die wichtigsten Interessenten-Generierung auszuwählen, oder erstellen und erweitern Sie Einkaufsgruppen. Verwenden Sie das Demandbase-Ziel, um andere Anwendungsfälle zu untersuchen und Ihre Konten effektiv zu erreichen.

Mit dieser Integration können Sie das Website-Erlebnis auch mithilfe der Echtzeit-Kontodatensuche personalisieren, um die Interaktion zu optimieren.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-and-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|--------------|-----------|---------------------------|
| Exporttyp | Zielgruppenexport | Alle Zielgruppenmitglieder werden mit Schlüsselkennungen wie Name, Telefonnummer und mehr exportiert. |
| Häufigkeit | Streaming | &quot;Always-on&quot;-API-basierte Verbindungen. Aktualisierungen werden unmittelbar nach Profiländerungen nachgelagert gesendet. |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Um Kontozielgruppen in Demandbase zu exportieren, benötigen Sie Folgendes:

1. Ein Demandbase-Konto.
2. Ein Demandbase-API-Token. Sie können mit Ihrem Benutzer in Demandbase ein API-Token generieren. Um ein Token zu generieren, navigieren Sie nach der Anmeldung bei Ihrem Demandbase-Konto zu [Mein Profil > API-Token](https://web.demandbase.com/o/ad/at) .

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Bearer-Token hinzufügen](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Trägertoken]**: Füllen Sie das Trägertoken aus, um sich beim Ziel zu authentifizieren. Informationen zum Abrufen des Tokens finden Sie unter [Voraussetzungen](#prerequisites) .

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Informationen zur Zielverbindung hinzufügen](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Entitätstyp]**: Wählen Sie **[!UICONTROL Konto]** als Entitätstyp aus.

Jetzt können Sie Ihre Zielgruppen in Demandbase aktivieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Kontozielgruppen für dieses Ziel finden Sie unter [Aktivieren von Kontozielgruppen](/help/destinations/ui/activate-account-audiences.md) .

## Zusätzliche Hinweise und wichtige Hinweise {#additional-notes}

* Wenn eine Zielgruppe mit demselben Namen zuvor in Demandbase aktiviert wurde, können Sie sie nicht erneut über einen anderen Datenfluss zum Demandbase-Ziel aktivieren.
* Wenn Sie Zielgruppen in Demandbase exportiert haben und die Exporte erfolgreich sind, aber nicht alle Daten Demandbase erreichen, ist möglicherweise auf der Demandbase-Seite eine API-Drosselung aufgetreten. Wenden Sie sich zur Klarstellung an sie.
