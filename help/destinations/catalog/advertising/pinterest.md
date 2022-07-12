---
title: Pinterest Customer List-Verbindung
description: Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 16%

---

# [!DNL Pinterest Customer List]-Verbindung

## Übersicht {#overview}

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

>[!IMPORTANT]
>
>Dieses Ziel wurde vom Pinterest-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an https://help.pinterest.com/en/contact.

## Voraussetzungen {#prerequisites}

* Der Benutzer muss sich mit einem Pinterest-Konto authentifizieren, das Zugriff auf das Advertiser-Konto hat, dem er eine Zielgruppe hinzufügen möchte. Details zur Freigabe von Advertiser-Konten finden Sie [here](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Insbesondere benötigt der Benutzer die Zugriffsebene &quot;Zielgruppe&quot;.
* Details zu Identitätsformaten der Kundenliste finden Sie hier . [here](https://help.pinterest.com/en/business/article/audience-targeting).

## Unterstützte Identitäten {#supported-identities}

Die [!DNL Pinterest Customer List] Das Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Weitere Informationen [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

Im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Ordnen Sie die gewünschten Identitäten des Zielaktivierungs-Workflows dem Zielfeld zu. *pinterest_audience*. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Ordnen Sie die *GAID* Quell-Identitäts-Namespace zum Zielidentitätsfeld *pinterest_audience*. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst. |
| IDFA | [!DNL Apple ID for Advertisers] | Ordnen Sie die *IDFA* Quell-Identitäts-Namespace zum Zielidentitätsfeld *pinterest_audience*. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst. |
| E-MAIL | E-Mail-Adressen (Klartext oder Hash mit dem SHA256-Algorithmus) | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. <br> Ordnen Sie die *Email* oder *Email_LC_SHA256* Quell-Identitäts-Namespace zum Zielidentitätsfeld *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im Pinterest-Ziel der Kundenliste verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Pinterest Customer List] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Advertiser-ID]**: Ihre Pinterest-Advertiser-ID.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Weitere Ressourcen {#additional-resources}

Beachten Sie die Informationen unter [Pinterest-Hilfeseite](https://help.pinterest.com/en/business/article/audience-targeting) für weitere Informationen.
