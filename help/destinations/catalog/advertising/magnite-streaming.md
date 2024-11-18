---
title: Echtzeit-Zielverbindung vergrößern
description: Verwenden Sie dieses Ziel, um Adobe CDP-Zielgruppen in Echtzeit an die Magnite-Streaming-Plattform zu übermitteln.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 4e08a14b-6800-41e1-95a5-826a6241144d
source-git-commit: da05db9376893bdbe8f0aa291f19a507e4a73d4f
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 31%

---

# Magnite: Echtzeit-Zielverbindung

## Übersicht {#overview}

Mit den Zielen [!DNL Magnite: Real-Time] und [Magnite: Batch](/help/destinations/catalog/advertising/magnite-batch.md) in Adobe Experience Platform können Sie Zielgruppen für Targeting und Aktivierung auf der Magnite-Streaming-Plattform zuordnen und exportieren.

Die Aktivierung von Zielgruppen für die Plattform [!DNL Magnite Streaming] ist ein zweistufiger Prozess, für den Sie sowohl das Magnite-Format als auch das Magnite-Ziel verwenden müssen: Echtzeit- und Magnite: Batch-Ziele.

Um Ihre Zielgruppen für [!DNL Magnite Streaming] zu aktivieren, müssen Sie:

* Aktivieren Sie die Zielgruppen für das Ziel [!DNL Magnite: Real-Time] , wie auf dieser Seite dargestellt.
* Aktivieren Sie dieselbe Zielgruppe auf dem Magnite: Batch-Ziel. Das Ziel [!DNL Magnite: Batch] ist eine obligatorische Komponente. Wenn Sie die Zielgruppe nicht am Batch-Ziel [!DNL Magnite Streaming] aktivieren, wird die Integration fehlgeschlagen und Ihre Zielgruppen werden nicht aktiviert.

Hinweis: Bei Verwendung des Echtzeit-Ziels erhält [!DNL Magnite Streaming] Zielgruppen in Echtzeit. Magnite kann jedoch nur Echtzeitzielgruppen temporär auf ihrer Plattform speichern. Diese werden innerhalb weniger Tage aus dem System entfernt. Wenn Sie daher das Ziel Magnite: Echtzeit verwenden möchten, müssen Sie *auch* das Ziel Magnite: Batch verwenden. Jede Zielgruppe, die Sie für das Echtzeit-Ziel aktivieren, müssen Sie auch für das Batch-Ziel aktivieren.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Magnite]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen kontaktieren Sie diese bitte direkt unter `adobe-tech@magnite.com`.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Magnite: Real-Time]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Aktivierung und Zielgruppenbestimmung {#activation-and-targeting}

Durch diese Integration mit Magnite können Kunden ihre CDP-Zielgruppen von Adobe Experience Platform an Magnite für das Anzeigen-Targeting übergeben. Zielgruppen können in Magnite sowohl für positives Targeting als auch für negatives Targeting (Unterdrückung) ausgewählt werden.

## Voraussetzungen {#prerequisites}

Um die [!DNL Magnite] -Ziele in Adobe Experience Platform zu verwenden, müssen Sie zunächst über ein [!DNL Magnite Streaming] -Konto verfügen. Wenn Sie über ein [!DNL Magnite Streaming] -Konto verfügen, wenden Sie sich an Ihren [!DNL Magnite] -Kundenbetreuer, um Anmeldeinformationen für den Zugriff auf [!DNL Magnite's] -Ziele zu erhalten.
Wenn Sie kein [!DNL Magnite Streaming] -Konto haben, wenden Sie sich an adobe-tech@magnite.com

## Unterstützte Identitäten {#supported-identities}

Das Ziel [!DNL Magnite: Real-Time] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Eine eindeutige Kennung für ein Gerät oder eine Identität. Wir akzeptieren jede Geräte-ID und Erstanbieter-ID unabhängig vom Typ. | Zu den von Magnite unterstützten Identitätstypen gehören u. a. PPUID, GAID, IDFA und TV-Geräte-IDs. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Magnite: Real-Time]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Nicht ausgefüllte Zielkonfigurationsauth-Felder](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Benutzername]**: Der Benutzername, den Sie von [!DNL Magnite] erhalten haben.
* **[!UICONTROL Passwort]**: Das Passwort, das Ihnen von [!DNL Magnite] bereitgestellt wird.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Ihr Firmenname]**: Ihr Name für den Kunden/das Unternehmen. Es stehen nur unterstützte [!DNL Magnite Streaming] -Clients zur Auswahl zur Verfügung.

>[!NOTE]
>
>Der Unternehmensname muss eine Zeichenfolge sein, die mit dem Namen des Amazon S3-Bereitstellungsbuckets übereinstimmt, den Sie mit Magnite konfiguriert und im Schritt [Für Ziel authentifizieren](#authenticate) eingerichtet haben. Zu den unterstützten Zeichen gehören &quot;a-z&quot;, &quot;A-Z&quot;, &quot;0-9&quot;, &quot;-&quot;(Bindestrich) oder &quot;_&quot;(Unterstrich).

![ Felder für die Zielkonfigurationsauth ](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Wählen Sie danach die Schaltfläche **[!UICONTROL Erstellen]** aus.

![Optionale Governance-Richtlinie und Durchsetzungsaktionen](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

Nachdem die Zielverbindung erstellt wurde, können Sie mit dem Aktivierungsfluss für die Zielgruppe fortfahren. Im folgenden Abschnitt wird erläutert, wie Sie Zielgruppen mithilfe des Echtzeit-Ziels aktivieren können.

### Zuordnen von Attributen und Identitäten {#map}

Der nächste Schritt besteht in der Zuordnung der Quell-IDs zur Magnite-Geräte-ID.

* Sie können so viele Zuordnungen wie nötig hinzufügen, indem Sie **[!UICONTROL Neue Zuordnung hinzufügen]** auswählen.

In diesem Beispiel, das das Echtzeit-Ziel verwendet, wird eine Zeile angezeigt, die eine generische deviceId-Quellkennung enthält, die dem Zielfeld Magnite device_id zugeordnet ist. Wenn Sie mit den Zuordnungen arbeiten, wählen Sie [!UICONTROL Weiter] aus.

![Ordnen Sie die gewünschten Datenfelder dem Feld device_ID zu](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Stellen Sie sicher, dass die Zuordnungs-IDs für alle aktivierten Zielgruppen festgelegt sind, oder legen Sie KEINE fest, wenn keine Zuordnungs-ID vorhanden ist.

![Stellen Sie sicher, dass die Zuordnungs-IDs für alle aktivierten Zielgruppen festgelegt sind, oder legen Sie KEINE fest, wenn keine Zuordnungs-ID vorhanden ist](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Jetzt müssen Sie für jede Zielgruppe ein Startdatum (obligatorisch), ein Enddatum (optional) und eine Zuordnungs-ID konfigurieren.

**Zuordnungs-ID**

* Verwenden Sie das Feld **[!UICONTROL Zuordnungs-ID]** , wenn eine Zielgruppe über eine bereits vorhandene Segment-ID verfügt, die Magnite zuvor bekannt war.

* Um einer Zielgruppe eine **[!UICONTROL Zuordnungs-ID]** hinzuzufügen, wählen Sie jede einzelne Zielgruppenzeile aus und geben Sie Daten in die rechte Spalte ein (siehe Abbildung oben). Wenn Sie keine Zuordnungs-ID hinzufügen möchten, geben Sie KEINE in das Feld Zuordnungs-ID ein.

Wählen Sie **[!UICONTROL Weiter]** aus und schließen Sie den Aktivierungsfluss ab.

![Wählen Sie den nächsten aus und schließen Sie den Aktivierungsfluss ab.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach dem Hochladen Ihrer Zielgruppen können Sie mit den folgenden Schritten überprüfen, ob Ihre Zielgruppen korrekt erstellt und hochgeladen wurden:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Nach der Aufnahme werden Zielgruppen voraussichtlich innerhalb weniger Minuten in [!DNL Magnite Streaming] angezeigt und können auf einen Deal angewendet werden. Sie können dies bestätigen, indem Sie nach der Segment-ID suchen, die während der Aktivierungsschritte in der Adobe Experience Platform freigegeben wurde.

## Dieselben Zielgruppen über das [!DNL Magnite: Batch]Ziel aktivieren

Zielgruppen, die mit [!DNL Magnite Streaming] über das Echtzeit-Ziel freigegeben werden, müssen auch über das Magnite: Batch-Ziel freigegeben werden. Wenn die Segmentnamen in der Benutzeroberfläche von [!DNL Magnite Streaming] korrekt konfiguriert sind, werden sie entsprechend den Segmentnamen aktualisiert, die nach der täglichen Aktualisierung in Adobe Experience Platform verwendet werden.

Wenn für Ihre Integration kein Batch-Ziel konfiguriert wurde, richten Sie es jetzt über das Dokument Magnite: Batch-Ziel ein.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Hilfedokumentation finden Sie im [Magnite Help Center](https://help.magnite.com/help).
