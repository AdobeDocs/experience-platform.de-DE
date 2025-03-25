---
keywords: Luftschiffattribute;Luftschiffziel
title: Airship Attributes-Verbindung
description: Nahtlose Übergabe von Adobe-Zielgruppendaten an Airship als Zielgruppenattribute für das Targeting in Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 453884612e787439ea58f312d8080622ee0441f7
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 28%

---

# [!DNL Airship Attributes]-Verbindung {#airship-attributes-destination}

>[!IMPORTANT]
>
>* Ab dem 25. März 2025 werden im Zielkatalog zwei [!DNL Airship Attributes] nebeneinander angezeigt. Dies ist auf ein internes Upgrade des Ziel-Service zurückzuführen. Der vorhandene [!DNL Airship Attributes]-Ziel-Connector wurde in **[!UICONTROL (veraltet) Airship Attributes]** umbenannt und eine neue Karte mit dem Namen **[!UICONTROL Airship Attributes]** ist jetzt für Sie verfügbar.
>* Verwenden Sie die **[!UICONTROL Airship Attributes]**-Verbindung im Katalog für neue Aktivierungsdatenflüsse. Wenn Sie aktive Datenflüsse zum Ziel &quot;**[!UICONTROL (veraltet) Airship Attributes]** haben, werden diese automatisch aktualisiert, sodass keine Aktion von Ihnen erforderlich ist.
>* Wenn Sie Datenflüsse über die [Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) erstellen, müssen Sie Ihre [!DNL flow spec ID] und [!DNL connection spec ID] auf die folgenden Werte aktualisieren:
>   * Flussspezifikations-ID: `a862e0be-966e-4e5a-80d3-1bb566461986`
>   * Verbindungsspezifikations-ID: `594bc002-4a47-49b7-8a98-ac0d21045502`

## Überblick {#overview}

[!DNL Airship] ist die führende Plattform für Kundeninteraktion, mit der Sie Ihren Benutzern in jeder Phase des Kundenlebenszyklus aussagekräftige, personalisierte Omni-Channel-Messaging bereitstellen können.

Durch diese Integration werden Adobe-Profildaten zum Targeting oder [ als ](https://docs.airship.com/guides/audience/attributes/) an [!DNL Airship] übergeben.

Weitere Informationen zu [!DNL Airship] finden Sie unter [Airship Docs](https://docs.airship.com).

>[!TIP]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom [!DNL Airship]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre Zielgruppen an [!DNL Airship] senden können, müssen Sie Folgendes tun:

* Aktivieren Sie Attribute in Ihrem [!DNL Airship].
* Erzeugt ein Bearer-Token zur Authentifizierung.

>[!TIP]
>
>Erstellen Sie über [diesen Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) ein [!DNL Airship]-Konto, falls noch nicht geschehen.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten, entsprechend Ihrer Feldzuordnung. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Attribute aktivieren {#enable-attributes}

Adobe Experience Platform-Profilattribute ähneln [!DNL Airship] Attributen und können mithilfe des unten auf dieser Seite gezeigten Zuordnungs-Tools einfach miteinander in Platform zugeordnet werden.

[!DNL Airship] Projekte verfügen über mehrere vordefinierte und standardmäßige Attribute. Wenn Sie über ein benutzerdefiniertes Attribut verfügen, müssen Sie es zuerst in [!DNL Airship] definieren. Weitere [ finden Sie unter „Einrichten und Verwalten ](https://docs.airship.com/tutorials/audience/attributes/) Attributen“.

## Bearer-Token generieren {#bearer-token}

Navigieren Sie **[!UICONTROL Einstellungen]**&quot; **[!UICONTROL APIs und Integrationen]** im [Airship-Dashboard](https://go.airship.com) und wählen Sie **[!UICONTROL Token]** im linken Menü aus.

Klicken Sie **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token an, z. B. „Ziel der Adobe-Attribute“, und wählen Sie „Zugriff auf alle“ für die Rolle aus.

Klicken Sie **[!UICONTROL Token erstellen]** und speichern Sie die Details als vertraulich.

## Anwendungsszenarien {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Airship Attributes]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Anwendungsfall #1

Nutzen Sie die in Adobe Experience Platform erfassten Profildaten für die Personalisierung der Nachricht und für umfangreiche Inhalte in allen Kanälen von [!DNL Airship]. Nutzen Sie beispielsweise [!DNL Experience Platform] Profildaten, um Standortattribute in [!DNL Airship] festzulegen. Dadurch kann eine Hotelmarke für jeden Benutzer ein Bild für den nächstgelegenen Hotelstandort anzeigen.

### Anwendungsfall #2

Nutzen Sie Attribute aus Adobe Experience Platform, um [!DNL Airship] Profile weiter anzureichern und mit SDK oder [!DNL Airship] Prognosedaten zu kombinieren. Ein Einzelhändler kann beispielsweise eine Zielgruppe mit Treuestatus- und Standortdaten (Attribute aus Platform) erstellen und Daten [!DNL Airship], die voraussichtlich abwandern werden, um hochgradig zielgerichtete Nachrichten an Benutzer mit dem Treuestatus „Gold“ zu senden, die in Las Vegas (NV) leben und eine hohe Abwanderungswahrscheinlichkeit haben.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Bearer-Token]**: Das Bearer-Token, das Sie aus dem [!DNL Airship]-Dashboard generiert haben.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domain]**: Wählen Sie entweder ein US- oder EU-Rechenzentrum aus, je nachdem, welches [!DNL Airship] Rechenzentrum für dieses Ziel gilt.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] können entweder auf einem Kanal, der eine Geräteinstanz darstellt, z. B. iPhone, oder einem benannten Benutzer festgelegt werden, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema E-Mail-Adressen im Klartext (ungehasht) als primäre Identität haben, wählen Sie das E-Mail-Feld in Ihren **[!UICONTROL Source-]** aus und ordnen Sie sie dem [!DNL Airship] namens Benutzer in der rechten Spalte unter **[!UICONTROL Zielidentitäten]** zu, wie unten dargestellt.

![Benannte Benutzerzuordnung](../../assets/catalog/mobile-engagement/airship/mapping.png)

Für Kennungen, die einem Kanal, d. h. einem Gerät, zugeordnet werden sollen, ordnen Sie sie dem entsprechenden Kanal basierend auf der Quelle zu. Die folgenden Bilder zeigen, wie zwei Zuordnungen erstellt werden:

* IDFA iOS Advertising-ID für einen [!DNL Airship] iOS-Kanal
* Adobe `fullName` Attribut [!DNL Airship] Attribut „Vollständiger Name“ an

>[!NOTE]
>
>Verwenden Sie den benutzerfreundlichen Namen, der im [!DNL Airship]-Dashboard angezeigt wird, wenn Sie das Zielfeld für Ihre Attributzuordnung auswählen.

**Identität zuordnen**

Quellfeld auswählen:

![Mit Airship-Attributen verbinden](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Zielfeld auswählen:

![Mit Airship-Attributen verbinden](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Attribut zuordnen**

Quellattribut auswählen:

![Quellfeld auswählen](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Zielattribut auswählen:

![Zielfeld auswählen](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Zuordnung überprüfen:

![Kanalzuordnung](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](../../../data-governance/home.md).
