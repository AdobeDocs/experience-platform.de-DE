---
title: Pinterest Customer List-Verbindung
description: Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 1b35687350dbbcebfc86acc90852d86870292142
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 37%

---

# [!DNL Pinterest Customer List]-Verbindung

## Übersicht {#overview}

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

>[!IMPORTANT]
>
>Dieses Ziel wurde vom Pinterest-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an https://help.pinterest.com/en/contact.

## Voraussetzungen {#prerequisites}

* Der Benutzer muss sich mit einem Pinterest-Konto authentifizieren, das Zugriff auf das Advertiser-Konto hat, dem er eine Zielgruppe hinzufügen möchte. Details zum Freigeben von Advertiser-Konten finden Sie [hier](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Insbesondere benötigt der Benutzer die Zugriffsebenen „Zielgruppe“.
* Details zu Identitätsformaten der Kundenliste finden Sie [hier](https://help.pinterest.com/en/business/article/audience-targeting).

## Unterstützte Identitäten {#supported-identities}

Das [!DNL Pinterest Customer List]-Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

Ordnen Sie [ Schritt ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Zielaktivierung die gewünschten Identitäten dem Zielfeld zu (*_audience*. Identitäten werden bei der Datenaufnahme in Pinterest unterschieden und aufgelöst.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Ordnen Sie den Quell *Identity-Namespace* GAID“ dem Zielidentitätsfeld (*_audience)*. |
| IDFA | [!DNL Apple ID for Advertisers] | Ordnen Sie *Quell* Identity-Namespace von IDFA dem Zielidentitätsfeld (*_audience)*. |
| E-MAIL | E-Mail-Adressen (Klartext oder Hash mit dem SHA256-Algorithmus) | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. <br> Ordnen Sie den Quell *Identity*-Namespace oder *Email_LC_SHA256* dem Zielidentitätsfeld (*_audience)*. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im Ziel der Pinterest-Kundenliste verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Pinterest Customer List]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Anwendungsfall 1

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Werbekonto-ID]**: Ihre Pinterest Advertiser-ID.

### Authentifizierungsdaten aktualisieren {#refresh-authentication-credentials}

Pinterest-Token laufen alle 30 Tage ab. Sie können das Ablaufdatum Ihres Tokens über die Spalte **[!UICONTROL Account-Ablaufdatum]** entweder auf den Registerkarten **[[!UICONTROL Konten]](../../ui/destinations-workspace.md#accounts)** oder **[[!UICONTROL Durchsuchen]](../../ui/destinations-workspace.md#browse)** überwachen.

Sobald das Token abgelaufen ist, funktionieren Datenexporte an das Ziel nicht mehr. Um dies zu verhindern, authentifizieren Sie sich erneut, indem Sie die folgenden Schritte ausführen:

1. Navigieren Sie **[!UICONTROL Ziele]** > **[!UICONTROL Konten]**
2. (Optional) Verwenden Sie die verfügbaren Filter auf der Seite, um nur Pinterest-Konten anzuzeigen.
   ![Filtern, um nur Pinterest-Konten anzuzeigen](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-filters.png)
3. Wählen Sie das Konto aus, das Sie aktualisieren möchten, klicken Sie auf das Auslassungszeichen und wählen Sie **[!UICONTROL Details bearbeiten]**.
   ![Wählen Sie das Steuerelement „Details bearbeiten“](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-edit-details.png)
4. Wählen Sie im modalen Fenster die Option **[!UICONTROL OAuth erneut]** und authentifizieren Sie sich erneut mit Ihren Pinterest-Anmeldeinformationen.
   ![Modales Fenster mit Option „OAuth erneut verbinden“](/help/destinations/assets/catalog/advertising/pinterest-customer-list/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Ihre Authentifizierungsdaten werden aktualisiert und ihre Gültigkeitsdauer wird auf 30 Tage zurückgesetzt.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie auf der Seite zum [Pinterest](https://help.pinterest.com/en/business/article/audience-targeting)Hilfezentrum .

+++ Änderungsprotokoll anzeigen


| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| November 2023 | Funktions- und Dokumentationsaktualisierung | Das Pinterest-Ziel in Real-Time CDP verwendet jetzt die Advertiser-API v5. |

{style="table-layout:auto"}


+++
