---
title: PubMatic Connect
description: PubMatic maximiert den Kundenwert durch die Bereitstellung der programmatischen Digital Marketing Supply Chain der Zukunft. PubMatic Connect kombiniert Plattformtechnologie und dedizierten Service, um die Art und Weise, wie Inventar und Daten gepackt und transagiert werden, zu verbessern.
last-substantial-update: 2023-12-14T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 42%

---

# PubMatic Connect-Ziel {#pubmatic-connect}

## Übersicht {#overview}

Nutzen Sie [!DNL PubMatic Connect], um den Kundenwert zu maximieren, indem Sie die programmatische Digital-Marketing-Lieferkette der Zukunft bereitstellen. [!DNL PubMatic Connect] kombiniert Plattformtechnologie und dedizierten Service, um die Art und Weise zu verbessern, wie Inventar und Daten gepackt und verarbeitet werden.

Verwenden Sie dieses Ziel, um Zielgruppendaten an die [!DNL PubMatic Connect]-Plattform zu senden.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL PubMatic]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an `support@pubmatic.com`.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL PubMatic Connect]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Ansprechen von Benutzern auf mobilen, Web- und Videoüberwachungsplattformen {#targeting}

Herausgeber oder Datenanbieter möchten Zielgruppen von Adobe Experience Platform an [!DNL PubMatic Connect] senden, um Benutzende auf mobilen, Web- und TV-Plattformen mithilfe einer großen Anzahl von Kennungen anzusprechen.

## Voraussetzungen {#prerequisites}

Wenden Sie sich an Ihren [!DNL PubMatic] Account Manager, um sicherzustellen, dass Ihr Konto richtig konfiguriert ist und das Onboarding von Zielgruppensegmenten unterstützt. Er wird auch sicherstellen, dass Sie über alle relevanten Details verfügen, um dieses Ziel zu verwenden und Sie während der Einrichtung zu unterstützen.

## Unterstützte Identitäten {#supported-identities}

[!DNL PubMatic Connect] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
| --------------- | ------ | --- |
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform ([-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
| --- | --- | --- |
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder sonstiges), die im PubMatic Connect -Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector die Aktualisierung nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
> Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Authentifizierung](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Zieldetails](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
- **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
- **[!UICONTROL Datenpartner-ID]**: Die Datenpartner-ID, die in Ihrem [!DNL PubMatic]-Konto für diese Integration eingerichtet wurde.
- **[!UICONTROL Standard-Ländercode]**: Der standardmäßige Ländercode, der auf alle Identitäten angewendet werden soll, wenn im Profil keine angegeben ist.
- **[!UICONTROL Konto-ID]**: Ihre [!DNL PubMatic Connect] Konto-ID.
- **[!UICONTROL Kontotyp]**: Der Kontotyp Ihres [!DNL PubMatic] Platform-Kontos. Wenden Sie sich an Ihren [!DNL PubMatic] Account Manager, wenn Sie Fragen haben, für die Sie sich entscheiden können. Folgende Optionen sind verfügbar:
   - [!UICONTROL PUBLISHER]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL KÄUFER]

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
> - Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>
> - Zum Exportieren _Identitäten_ benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](../../assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Auswahl der Quellfelder:

- Wählen Sie eine Kennung aus (normalerweise Namespaces wie IDFA oder einen benutzerdefinierten ID-Namespace).

Auswählen der Zielfelder:

- Wenden Sie sich an Ihren [!DNL PubMatic] Account Manager, um Informationen darüber zu erhalten, welcher UID-Typ in diesem Schritt korrekt sein wird.
- Wählen Sie die Nummer des [!DNL PubMatic UID] aus, die der im ersten Schritt ausgewählten Kennung entspricht.

![Zuordnen von Attributen und Identitäten](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Über die [!DNL PubMatic] Benutzeroberfläche können Sie überprüfen, ob die Daten korrekt gepusht wurden und ob die Segmente verfügbar sind. Es kann bis zu 24 Stunden dauern, nachdem Daten per Push an die [!DNL PubMatic]-Benutzeroberfläche gesendet wurden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
