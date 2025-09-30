---
title: Demandbase-Verbindung
description: Verwenden Sie dieses Ziel, um Ihre Konto-Zielgruppen für Account-Based Marketing-Anwendungsfälle (ABM) zu aktivieren. Werben Sie über die B2B-Demand Side Platform (DSP) von DemandBase für relevante Personas und Rollen in Ihren Zielkonten. Zielkonten können auch mit Demandbase-Drittanbieterdaten für andere nachgelagerte Anwendungsfälle in Marketing und Vertrieb angereichert werden.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P-Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 39012e2308af57af7c9193bdc4894f8f2e358606
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 25%

---

# Demandbase-Verbindung {#demandbase}

>[!AVAILABILITY]
>
>Die Funktion zum Aktivieren von Account-Zielgruppen für das Demandbase-Ziel ist für Unternehmen verfügbar, die die [Business-to](/help/rtcdp/overview.md#rtcdp-b2b)- und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-Editionen von Real-Time Customer Data Platform erwerben.

Aktivieren Sie Profile für Ihre Demandbase-Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung, basierend auf [Account-Zielgruppen](/help/segmentation/types/account-audiences.md) .

## Anwendungsfall {#use-case}

Verwenden Sie dieses Ziel, um Ihre Konto-Zielgruppen für Account-Based Marketing-Anwendungsfälle (ABM) zu aktivieren. Werben Sie über die B2B-Demand Side Platform (DSP) von DemandBase für relevante Personas und Rollen in Ihren Zielkonten. Zielkonten können auch mit Demandbase-Drittanbieterdaten für andere nachgelagerte Anwendungsfälle in Marketing und Vertrieb angereichert werden.

Nutzen Sie beispielsweise die Ad-Tech-DSP von Demandbase, um bestimmte Rollen oder Personas innerhalb von Schlüsselkonten für die Top-of-funnel-Lead-Generierung anzusprechen, oder erstellen und erweitern Sie Einkaufsgruppen. Verwenden Sie das Demandbase-Ziel, um andere Anwendungsfälle zu erkunden, um Ihre Konten effektiv anzusprechen.

Mit dieser Integration können Sie das Website-Erlebnis auch personalisieren, indem Sie die Suche nach Kontoinformationen in Echtzeit verwenden, um die Interaktion zu optimieren.

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
| Exporttyp | Zielgruppenexport | Alle Mitglieder der Zielgruppe werden mit Schlüsselkennungen wie Name, Telefonnummer und mehr exportiert. |
| Häufigkeit | Streaming | „Always-on“-API-basierte Verbindungen. Aktualisierungen werden nachgelagert sofort nach Profiländerungen gesendet. |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Um Konto-Zielgruppen in die Demandbase zu exportieren, benötigen Sie Folgendes:

1. Ein Demandbase-Konto.
2. Ein Demandbase-API-Token. Sie können in Demandbase ein API-Token mit Ihrem Benutzer generieren. Um ein Token zu generieren, navigieren Sie zu [Mein Profil > API-Token](https://web.demandbase.com/o/ad/at) nachdem Sie sich bei Ihrem Demandbase-Konto angemeldet haben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Bearer-Token hinzufügen](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren. Unter [Voraussetzungen](#prerequisites) finden Sie Informationen zum Abrufen des Tokens.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Fügen Sie Informationen über die Zielverbindung hinzu](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Entitätstyp]**: Wählen Sie **[!UICONTROL Konto]** als Entitätstyp aus.

Jetzt können Sie Ihre Zielgruppen in Demandbase aktivieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [ Aktivieren von Konto-Zielgruppen für ](/help/destinations/ui/activate-account-audiences.md) Ziel finden Sie unter „Aktivieren von Konto-Zielgruppen“.

### Obligatorische Zuordnungen {#mandatory-mappings}

Beim Aktivieren von Zielgruppen für das [!DNL Demandbase] müssen Sie die folgenden obligatorischen Feldzuordnungen im Zuordnungsschritt konfigurieren:

| Quellfeld | Zielfeld | Beschreibung |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | Der Name des Kontos |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | Die E-Mail-Domain des Unternehmenskontos |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | Die primäre Kennung für das Konto |

![Demandbase-Zuordnungen](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

Diese Zuordnungen sind erforderlich, damit das Ziel ordnungsgemäß funktioniert, und müssen konfiguriert werden, bevor Sie mit dem Aktivierungs-Workflow fortfahren können.

## Zusätzliche Hinweise und wichtige Hinweise {#additional-notes}

* Wenn eine Konto-Zielgruppe mit demselben Namen zuvor für Demandbase aktiviert wurde, können Sie sie nicht über einen anderen Datenfluss zum Demandbase-Ziel erneut aktivieren.
* Wenn Sie Zielgruppen in die Demandbase exportiert haben und die Exporte in Experience Platform erfolgreich sind, aber nicht alle Daten die Demandbase erreichen, kann es zu API-Einschränkungen auf der Demandbase gekommen sein. Wenden Sie sich zur Klärung an sie.
