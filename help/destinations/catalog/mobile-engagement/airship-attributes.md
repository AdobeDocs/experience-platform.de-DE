---
keywords: Luftschiffsattribute;Luftschiffsziel
title: Airship Attributes-Verbindung
description: Nahtlose Weitergabe von Adobe-Zielgruppendaten an Airship als Zielgruppenattribute für Targeting innerhalb von Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 31%

---

# [!DNL Airship Attributes]-Verbindung {#airship-attributes-destination}

## Übersicht {#overview}

[!DNL Airship] ist die führende Plattform für Kundeninteraktionen, mit der Sie Ihren Benutzern in allen Phasen des Kundenlebenszyklus sinnvolle, personalisierte Omnichannel-Nachrichten bereitstellen können.

Diese Integration übergibt Adobe-Profildaten an [!DNL Airship] as [Attribute](https://docs.airship.com/guides/audience/attributes/) für Targeting oder Aktivierung.

Weitere Informationen zu [!DNL Airship], siehe [Dokumente für die Luftfahrt](https://docs.airship.com).

>[!TIP]
>
>Diese Ziel-Connector- und Dokumentationsseite wird von der [!DNL Airship] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre Zielgruppen an senden können [!DNL Airship]müssen Sie:

* Attribute in Ihren [!DNL Airship] Projekt.
* Generieren Sie ein Trägertoken zur Authentifizierung.

>[!TIP]
>
>Erstellen Sie eine [!DNL Airship] Konto über [dieser Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) wenn Sie noch nicht fertig sind.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten entsprechend Ihrer Feldzuordnung. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Attribute aktivieren {#enable-attributes}

Adobe Experience Platform-Profilattribute ähneln [!DNL Airship] -Attribute und können in Platform mithilfe des unten beschriebenen Zuordnungstools einfach miteinander zugeordnet werden.

[!DNL Airship] -Projekte haben mehrere vordefinierte und standardmäßige Attribute. Wenn Sie über ein benutzerdefiniertes Attribut verfügen, müssen Sie es in [!DNL Airship] zuerst. Siehe [Einrichten und Verwalten von Attributen](https://docs.airship.com/tutorials/audience/attributes/) für Details.

## Bearer-Token generieren {#bearer-token}

Navigieren Sie zu **[!UICONTROL Einstellungen]** &quot; **[!UICONTROL APIs und Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen **[!UICONTROL Token]** im Menü links.

Klicks **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token ein, z. B. &quot;Adobe-Attributziel&quot;und wählen Sie &quot;Zugriff auf alle&quot;für die.

Klicks **[!UICONTROL Token erstellen]** und speichern Sie die Angaben als vertraulich.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Airship Attributes] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Nutzen Sie in Adobe Experience Platform erfasste Profildaten zur Personalisierung der Nachricht und Rich-Content in einem beliebigen von [!DNL Airship]der Kanäle. Beispiel: [!DNL Experience Platform] Profildaten zum Festlegen von Standortattributen in [!DNL Airship]. Dadurch kann eine Hotelmarke für jeden Benutzer ein Bild für den nächstgelegenen Hotelstandort anzeigen.

### Anwendungsfall 2

Nutzen von Attributen aus Adobe Experience Platform zur weiteren Anreicherung [!DNL Airship] Profile und deren Kombination mit SDK oder [!DNL Airship] Prognosedaten. Ein Einzelhändler kann beispielsweise eine Zielgruppe mit Treuestatus und Standortdaten (Attribute aus Platform) erstellen und [!DNL Airship] Daten abwandern, um Nachrichten mit hoher Zielgruppenbestimmung an Benutzer mit dem Gold-Treuestatus zu senden, die in Las Vegas, NV leben und eine hohe Wahrscheinlichkeit für Abwanderungen haben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Trägertoken]**: das Trägertoken, das Sie aus dem [!DNL Airship] Dashboard.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domäne]**: Wählen Sie entweder ein US- oder EU-Rechenzentrum aus, je nachdem, welche [!DNL Airship] -Rechenzentrum gilt für dieses Ziel.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] -Attribute können entweder für einen Kanal festgelegt werden, der die Geräteinstanz darstellt, z. B. iPhone, oder für einen benannten Benutzer, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ungehasht) verwenden, wählen Sie das E-Mail-Feld in Ihrem **[!UICONTROL Quellattribute]** und zugeordnet werden [!DNL Airship] benannter Benutzer in der rechten Spalte unter **[!UICONTROL Target-Identitäten]**, wie unten dargestellt.

![Zuordnung von benannten Benutzern](../../assets/catalog/mobile-engagement/airship/mapping.png)

Bei Kennungen, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, müssen Sie basierend auf der Quelle dem entsprechenden Kanal zuordnen. Die folgenden Abbildungen zeigen, wie zwei Zuordnungen erstellt werden:

* IDFA iOS Advertising-ID an eine [!DNL Airship] iOS-Kanal
* Adobe `fullName` Attribut [!DNL Airship] Attribut &quot;Vollständiger Name&quot;

>[!NOTE]
>
>Verwenden Sie den benutzerfreundlichen Namen, der im [!DNL Airship] Dashboard bei der Auswahl des Zielfelds für Ihre Zuordnung.

**Zuordnungsidentität**

Quellfeld auswählen:

![Verbindung zu Airship-Attributen herstellen](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Zielgruppenfeld auswählen:

![Verbindung zu Airship-Attributen herstellen](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Zuordnungsattribut**

Quellattribut auswählen:

![Quellfeld auswählen](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Zielattribut auswählen:

![Zielgruppenfeld auswählen](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Überprüfung der Zuordnung:

![Kanalzuordnung](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](../../../data-governance/home.md).
