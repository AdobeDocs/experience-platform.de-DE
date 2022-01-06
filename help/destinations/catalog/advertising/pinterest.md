---
title: Pinterest-Kundenlistenverbindung
description: Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 90aa0d16851443255dd4828e9f28330a89a12692
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---

# [!DNL Pinterest Customer List] connection

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

## Exporttyp {#export-type}

**Segmentexport** - Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im Pinterest-Kundenlisten-Ziel verwendet werden.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Pinterest Customer List] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.


### Anwendungsfall 1

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).


### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Advertiser-ID]**: Ihre Pinterest-Advertiser-ID.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Weitere Ressourcen {#additional-resources}

Beachten Sie die Informationen unter [Pinterest-Hilfeseite](https://help.pinterest.com/en/business/article/audience-targeting) für weitere Informationen.
