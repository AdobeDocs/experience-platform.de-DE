---
title: Pinterest-Kundenlistenverbindung
description: Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 5%

---

# [!DNL Pinterest Customer List] connection

## Übersicht {#overview}

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

>[!IMPORTANT]
>
>Dieses Ziel wurde vom Pinterest-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an https://help.pinterest.com/en/contact.

## Voraussetzungen {#prerequisites}

* Der Benutzer muss sich mit einem Pinterest-Konto authentifizieren, das Zugriff auf das Advertiser-Konto hat, dem er eine Zielgruppe hinzufügen möchte. Details zur Freigabe von Advertiser-Konten finden Sie [hier](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Insbesondere benötigt der Benutzer die Zugriffsebene &quot;Zielgruppe&quot;.
* Details zu Identitätsformaten der Kundenliste finden Sie [hier](https://help.pinterest.com/en/business/article/audience-targeting).


## Unterstützte Identitäten {#supported-identities}

Das [!DNL Pinterest Customer List]-Ziel unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erfahren Sie mehr über [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

Ordnen Sie im Schritt [Zuordnen](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Zielaktivierungs-Workflows die gewünschten Identitäten dem Zielfeld *pinterest_audience* zu. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Ordnen Sie den Quell-Identitäts-Namespace *GAID* dem Zielidentitätsfeld *pinterest_audience* zu. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst. |
| IDFA | [!DNL Apple ID for Advertisers] | Ordnen Sie den Quell-Identitäts-Namespace *IDFA* dem Zielidentitätsfeld *pinterest_audience* zu. Identitäten werden bei der Datenerfassung in Pinterest identifiziert und aufgelöst. |
| E-MAIL | E-Mail-Adressen (Klartext oder Hash mit dem SHA256-Algorithmus) | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. <br> Ordnen Sie den  ** E-Mail- *E-Mail_LC_SHA256* -Quell-Identitäts-Namespace dem Zielidentitätsfeld  *pinterest_audience* zu. |

{style=&quot;table-layout:auto&quot;}

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im Pinterest-Kundenlisten-Ziel verwendet werden.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das [!DNL Pinterest Customer List]-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.


### Anwendungsfall 1

Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.



### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre Pinterest-Konto-ID.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) .

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie auf der [Pinterest Help Center-Seite](https://help.pinterest.com/en/business/article/audience-targeting) .
