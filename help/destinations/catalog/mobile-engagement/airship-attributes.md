---
keywords: Luftschiffsattribute;Luftschiffsziel
title: Airship Attributes-Verbindung
description: Nahtlose Weitergabe von Adobe-Zielgruppendaten an Airship als Zielgruppenattribute für das Targeting innerhalb von Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 8%

---

# [!DNL Airship Attributes]-Verbindung {#airship-attributes-destination}

## Übersicht {#overview}

[!DNL Airship] ist die führende Plattform für Kundeninteraktionen, mit der Sie Ihren Benutzern in allen Phasen des Kundenlebenszyklus sinnvolle, personalisierte Omnichannel-Nachrichten bereitstellen können.

Diese Integration übergibt Adobe-Profildaten an [!DNL Airship] as [Attribute](https://docs.airship.com/guides/audience/attributes/) für Targeting oder Aktivierung.

Weitere Informationen finden Sie unter [!DNL Airship], siehe [Dokumente für die Luftfahrt](https://docs.airship.com).

>[!TIP]
>
>Diese Dokumentationsseite wurde von der [!DNL Airship] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre Zielgruppensegmente an senden können [!DNL Airship]müssen Sie:

* Attribute in Ihren [!DNL Airship] Projekt.
* Generieren Sie ein Trägertoken zur Authentifizierung.

>[!TIP]
>
>Erstellen Sie eine [!DNL Airship] Konto über [dieser Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) wenn Sie noch nicht fertig sind.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten, entsprechend Ihrer Feldzuordnung. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Attribute aktivieren {#enable-attributes}

Adobe Experience Platform-Profilattribute ähneln [!DNL Airship] -Attribute und können in Platform mithilfe des unten beschriebenen Zuordnungstools einfach miteinander zugeordnet werden.

[!DNL Airship] -Projekte haben mehrere vordefinierte und standardmäßige Attribute. Wenn Sie über ein benutzerdefiniertes Attribut verfügen, müssen Sie es in [!DNL Airship] zuerst. Siehe [Einrichten und Verwalten von Attributen](https://docs.airship.com/tutorials/audience/attributes/) für Details.

## Bearer-Token generieren {#bearer-token}

Navigieren Sie zu **[!UICONTROL Einstellungen]** &quot; **[!UICONTROL APIs und Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen Sie **[!UICONTROL Token]** im Menü links.

Klicken **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token ein, z. B. &quot;Adobe Attributes Destination&quot;und wählen Sie &quot;All Access&quot;für die  aus.

Klicken **[!UICONTROL Token erstellen]** und speichern Sie die Angaben als vertraulich.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Airship Attributes] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Nutzen Sie in Adobe Experience Platform erfasste Profildaten zur Personalisierung der Nachricht und Rich-Content in einem beliebigen von [!DNL Airship]der Kanäle. Beispiel: [!DNL Experience Platform] Profildaten zum Festlegen von Standortattributen in [!DNL Airship]. Dadurch kann eine Hotelmarke für jeden Benutzer ein Bild für den nächstgelegenen Hotelstandort anzeigen.

### Anwendungsfall 2

Nutzen von Attributen aus Adobe Experience Platform zur weiteren Anreicherung [!DNL Airship] Profile und deren Kombination mit SDK oder [!DNL Airship] Prognosedaten. Ein Einzelhändler kann beispielsweise ein Segment mit Treuestatus und Standortdaten (Attribute aus Platform) erstellen und [!DNL Airship] Daten abwandern, um Nachrichten mit hoher Zielgruppenbestimmung an Benutzer mit dem Gold-Treuestatus zu senden, die in Las Vegas, NV leben und eine hohe Wahrscheinlichkeit für Abwanderungen haben.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### An Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

* **[!UICONTROL Trägertoken]**: das Trägertoken, das Sie aus dem [!DNL Airship] Dashboard.

### Zieldetails ausfüllen {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domäne]**: Wählen Sie entweder ein US- oder EU-Rechenzentrum aus, je nachdem, welche [!DNL Airship] -Rechenzentrum gilt für dieses Ziel.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] -Attribute können entweder für einen Kanal festgelegt werden, der die Geräteinstanz darstellt, z. B. iPhone, oder für einen benannten Benutzer, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ungehasht) verwenden, wählen Sie das E-Mail-Feld in Ihrem **[!UICONTROL Quellattribute]** und zugeordnet werden [!DNL Airship] benannter Benutzer in der rechten Spalte unter **[!UICONTROL Target-Identitäten]**, wie unten dargestellt.

![Zuordnung von benannten Benutzern](../../assets/catalog/mobile-engagement/airship/mapping.png)

Bei Kennungen, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, müssen Sie basierend auf der Quelle dem entsprechenden Kanal zuordnen. Die folgenden Abbildungen zeigen, wie zwei Zuordnungen erstellt werden:

* IDFA iOS Advertising-ID an eine [!DNL Airship] iOS-Kanal
* Adobe `fullName` Attribut [!DNL Airship] Attribut &quot;Vollständiger Name&quot;

>[!NOTE]
>
>Verwenden Sie den benutzerfreundlichen Namen, der im [!DNL Airship] Dashboard bei der Auswahl des Zielfelds für Ihr Attribut-Mapping.

**Zuordnungsidentität**

Quellfeld auswählen:

![Verbindung zu Airship-Attributen herstellen](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Zielgruppenfeld auswählen:

![Verbindung zu Airship-Attributen herstellen](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Zuordnungsattribut**

Quellattribut auswählen:

![Quellfeld auswählen](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Wählen Sie das Zielattribut aus:

![Zielgruppenfeld auswählen](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Überprüfung der Zuordnung:

![Kanalzuordnung](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](../../../data-governance/home.md).
