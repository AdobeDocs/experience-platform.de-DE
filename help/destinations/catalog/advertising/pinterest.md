---
title: Pinterest Customer List-Verbindung
description: Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 8a48ce4185f8044b8563d0435dcec17030b90830
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 43%

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

Die [!DNL Pinterest Customer List] Das Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

Im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Ordnen Sie die gewünschten Identitäten des Zielaktivierungs-Workflows dem Zielfeld zu. *pinterest_audience*. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Ordnen Sie die *GAID* Quell-Identitäts-Namespace zum Zielidentitätsfeld *pinterest_audience*. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst. |
| IDFA | [!DNL Apple ID for Advertisers] | Ordnen Sie die *IDFA* Quell-Identitäts-Namespace zum Zielidentitätsfeld *pinterest_audience*. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst. |
| E-MAIL | E-Mail-Adressen (Klartext oder Hash mit dem SHA256-Algorithmus) | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. <br> Ordnen Sie die *Email* oder *Email_LC_SHA256* Quell-Identitäts-Namespace zum Zielidentitätsfeld *pinterest_audience*. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im Pinterest-Ziel der Kundenliste verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Pinterest Customer List] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Anzeigen-Konto-ID]**: Ihre Pinterest-Advertiser-ID.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie unter [Pinterest-Hilfeseite](https://help.pinterest.com/en/business/article/audience-targeting) für weitere Informationen.

+++ Änderungsprotokoll anzeigen


| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| November 2023 | Funktions- und Dokumentationsaktualisierung | Das Pinterest-Ziel in Real-Time CDP verwendet jetzt die v5 Advertiser-API. |

{style="table-layout:auto"}


+++
