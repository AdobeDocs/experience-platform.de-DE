---
title: Magnite-Batch-Ziel
description: Verwenden Sie dieses Ziel, um Adobe CDP-Zielgruppen in Batches an die Magnite-Streaming-Plattform zu senden.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 8cc3890f-84f8-49d1-a329-322c13f9e5af
source-git-commit: 57e6dc4252c031d993592b963efc089f8427ce25
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 14%

---

# Magnite: Batch-Verbindung {#magnite-streaming-batch}

## Übersicht {#overview}

In diesem Dokument wird das Magnite: Batch-Ziel beschrieben und anhand von Beispielanwendungsfällen erhalten Sie ein besseres Verständnis, wie Sie Zielgruppen aktivieren und exportieren können.

Adobe Real-Time CDP-Zielgruppen können auf zwei Arten an die Magnite-Streaming-Plattform bereitgestellt werden - sie können einmal täglich bereitgestellt werden oder in Echtzeit bereitgestellt werden:

1. Wenn Sie Zielgruppen nur einmal pro Tag bereitstellen möchten bzw. müssen, können Sie das Magnite: Batch-Ziel verwenden, das Zielgruppen über eine tägliche S3-Batch-Dateibereitstellung für Magnite-Streaming bereitstellt. Diese Batch-Zielgruppen werden auf unbestimmte Zeit in der Magnite-Plattform gespeichert, im Gegensatz zu Echtzeit-Zielgruppen, die nur für einige Tage gespeichert werden.

2. Wenn Sie jedoch Zielgruppen häufiger bereitstellen möchten oder müssen, müssen Sie das Ziel [Echtzeit-Magnite](/help/destinations/catalog/advertising/magnite-streaming.md) verwenden. Bei Verwendung des Echtzeit-Ziels erhält Magnite Streaming Zielgruppen in Echtzeit. Magnite kann jedoch nur Echtzeitzielgruppen temporär auf ihrer Plattform speichern. Diese werden innerhalb weniger Tage aus dem System entfernt. Wenn Sie daher das Echtzeit-Ziel von Magnite verwenden möchten, müssen Sie *auch* das Ziel Magnite: Batch verwenden. Jede Zielgruppe, die Sie für das Echtzeit-Ziel aktivieren, müssen Sie auch für das Batch-Ziel aktivieren.

Zusammenfassend: Wenn Sie Adobe Real-Time CDP-Zielgruppen nur einmal täglich bereitstellen möchten, verwenden Sie das Magnite: Batch-Ziel nur und Zielgruppen werden einmal täglich bereitgestellt. Wenn Sie Adobe Real-Time CDP-Zielgruppen in Echtzeit bereitstellen möchten, verwenden Sie *sowohl* das Magnite: Batch-Ziel als auch das Magnite-Echtzeit-Ziel. Weitere Informationen erhalten Sie bei Magnite: Streaming .


Lesen Sie weiter unten, um weitere Informationen zum Magnite-Ziel zu erhalten: Batch-Ziel, wie Sie eine Verbindung herstellen und wie Sie Adobe Real-Time CDP-Zielgruppen aktivieren können.
Weitere Informationen zum Echtzeit-Ziel finden Sie stattdessen auf [dieser Dokumentationsseite](magnite-streaming.md) .

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Magnite]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen kontaktieren Sie diese bitte direkt unter `adobe-tech@magnite.com`.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Magnite: Batch-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1 {#use-case-1}

Sie haben eine Zielgruppe im Echtzeit-Ziel Magnite aktiviert.

Alle Zielgruppen, die über das Echtzeit-Ziel von Magnite aktiviert werden, müssen auch das Ziel Magnite: Batch verwenden, da die Daten des Batch-Versands dazu bestimmt sind, die Daten des Echtzeit-Versands innerhalb der Magnite-Streaming-Plattform zu ersetzen/beizubehalten.

### Anwendungsfall 2 {#use-case-2}

Sie möchten eine Zielgruppe nur in einem Batch-/täglichen Cadence für die Magnite-Streaming-Plattform aktivieren.

Über das Magnite: Batch-Ziel aktivierte Audiences werden in Batch-/Tageskadenz bereitgestellt und stehen dann für das Targeting in der Magnite-Streaming-Plattform zur Verfügung.

## Voraussetzungen {#prerequisites}

Um die [!DNL Magnite] -Ziele in Adobe Experience Platform zu verwenden, müssen Sie zunächst über ein Magnite-Streaming-Konto verfügen. Wenn Sie über ein [!DNL Magnite Streaming] -Konto verfügen, wenden Sie sich an Ihren [!DNL Magnite] -Kundenbetreuer, um Anmeldeinformationen für den Zugriff auf [!DNL Magnite's] -Ziele zu erhalten. Wenn Sie kein [!DNL Magnite Streaming] -Konto haben, wenden Sie sich an adobe-tech@magnite.com

## Unterstützte Identitäten {#supported-identities}

Das Magnite: Batch-Ziel kann *beliebige* Identitätsquellen aus der Adobe-CDP empfangen. Derzeit verfügt dieses Ziel über drei Target-Identitätsfelder, denen Sie zuordnen können.

>[!NOTE]
>
>*Alle* Identitätsquellen können jeder der `magnite_deviceId` Zielidentitäten zugeordnet werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|:--------------------------- |:------------------------------------------------------------------------------------------------ |:------------------------------------------------------------------------------------- |
| Magma_deviceId_GAID | GOOGLE ADVERTISING ID | Wählen Sie diese Target-Identität aus, wenn Ihre Quellidentität eine GAID ist. |
| size_deviceId_IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität IDFA ist. |
| size_deviceId_CUSTOM | Benutzerdefinierte/benutzerdefinierte ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität keine GAID oder IDFA ist oder wenn es sich um eine benutzerdefinierte oder benutzerdefinierte ID handelt. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

| Audience Origin | Unterstützt | Beschreibung |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

| Element | Typ | Anmerkungen |
|-----------------------------|----------|----------|
| Exporttyp | Zielgruppenexport | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im Ziel Magnite: Batch verwendet werden. |
| Exporthäufigkeit | Batch | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Erfahren Sie mehr über Batch [dateibasierte Ziele](/help/destinations/destination-types.md). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

Nachdem Sie Ihre Zielnutzung genehmigt und Ihre Anmeldeinformationen für Magnite Streaming freigegeben haben, führen Sie die folgenden Schritte aus, um Daten zu authentifizieren, zuzuordnen und freizugeben.

### Beim Ziel authentifizieren {#authenticate}

Suchen Sie das Ziel Magnite: Batch im Adobe-Erlebniskatalog. Klicken Sie auf die Schaltfläche für zusätzliche Optionen (\...) und konfigurieren Sie dann die Zielverbindung/Instanz.

Wenn Sie bereits über ein bestehendes Konto verfügen, können Sie es finden, indem Sie die Option Kontotyp in &quot;Vorhandenes Konto&quot;ändern. Andernfalls erstellen Sie unten ein Konto:

Um ein neues Konto zu erstellen und es zum ersten Mal am Ziel zu authentifizieren, füllen Sie die erforderlichen Felder &quot;S3-Zugriffsschlüssel&quot;und &quot;S3-geheimer Schlüssel&quot;aus (die Ihnen über Ihren Kundenbetreuer zur Verfügung gestellt werden) und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Nicht ausgefüllte Zielkonfigurationsauth-Felder](../../assets/catalog/advertising/magnite/destination-batch-config-auth-unfilled.png)

>[!NOTE]
>
>Die Sicherheitsrichtlinie von Magnite Streaming erfordert eine regelmäßige Rotation der S3-Schlüssel. Sie sollten in Zukunft Ihr Konto mit neuen S3-Zugangsschlüsseln und S3-geheimen Schlüsseln aktualisieren. Sie müssen nur das Konto selbst aktualisieren. Ziele, die dieses Konto verwenden, verwenden automatisch die aktualisierten Schlüssel. Wenn die neuen Schlüssel nicht hochgeladen werden, können die Daten nicht an dieses Ziel gesendet werden.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, mit dem Sie diese Zielverbindung/Instanz im
Zukunft.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses
Zielverbindung/-instanz in der Zukunft.
* **[!UICONTROL Ihr Firmenname]**: Ihr Name für den Kunden/das Unternehmen. Es stehen nur unterstützte [!DNL Magnite Streaming] -Clients zur Auswahl zur Verfügung.

>[!NOTE]
>
>Der Unternehmensname muss eine Zeichenfolge sein, die mit dem Namen des Amazon S3-Bereitstellungsbuckets übereinstimmt, den Sie mit Magnite konfiguriert und im Schritt [Für Ziel authentifizieren](#authenticate) eingerichtet haben. Zu den unterstützten Zeichen gehören &quot;a-z&quot;, &quot;A-Z&quot;, &quot;0-9&quot;, &quot;-&quot;(Bindestrich) oder &quot;_&quot;(Unterstrich).

![ Felder für die Zielkonfigurationsauth ](../../assets/catalog/advertising/magnite/destination-batch-config-auth-filled.png)

>[!NOTE]
>
>Wenn Sie planen, mehrere ID-Typen (GAID, IDFA usw.) mit dem Batch-Ziel zu senden, ist jeweils eine neue Ziel-Verbindung/-Instanz erforderlich. Weitere Informationen erhalten Sie von Ihrem Magnite-Kundenbetreuer.

Sie können dann fortfahren, indem Sie **[!UICONTROL Weiter]** auswählen

Im nächsten Bildschirm mit dem Titel &quot;Governance-Richtlinien und Durchsetzungsaktionen (optional)&quot;können Sie optional relevante Data Governance-Richtlinien auswählen. &quot;Datenexport&quot;ist im Allgemeinen für das Magnite: Batch-Ziel ausgewählt.

![Optionale Governance-Richtlinie und Durchsetzungsaktionen](../../assets/catalog/advertising/magnite/destination-batch-config-grouping-policy.png)

Wählen Sie nach der Auswahl oder wenn Sie diesen optionalen Bildschirm überspringen möchten, **[!UICONTROL Erstellen]**

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

### Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Im Feld **[!UICONTROL Source]** können Sie ein beliebiges Attribut oder eine beliebige Identität für Ihre Geräte auswählen. In diesem Beispiel haben wir eine benutzerdefinierte IdentityMap namens &quot;DeviceId&quot;ausgewählt
![Ordnen Sie die gewünschten Datenfelder dem Feld device_id zu](../../assets/catalog/advertising/magnite/destination-batch-active-audience-field-mapping.png)

Im Feld **[!UICONTROL Ziel]**:
![Wählen Sie den entsprechenden Gerätetyp als Zielidentität aus.](../../assets/catalog/advertising/magnite/destination-batch-active-audience-select-device-type.png) Weitere Informationen finden Sie unter [Unterstützte Identitäten](#supported-identities) .
In diesem Beispiel haben wir das **[!UICONTROL Zielfeld]**: Magma_deviceId_CUSTOM ausgewählt, da unser **[!UICONTROL Source-Feld]** als benutzerdefinierte IdentityMap: DeviceID definiert wurde.

>[!NOTE]
>
>Wenn Sie planen, mithilfe des Batch-Ziels mehrere ID-Typen (GAID, IDFA usw.) zu senden/zuzuordnen, ist jeweils eine neue Zielverbindung/Instanz erforderlich. Weitere Informationen erhalten Sie von Ihrem Magnite-Kundenbetreuer.


Im Bildschirm &quot;Konfigurieren eines Dateinamens und eines Exportzeitplans für jede Zielgruppe&quot;müssen Sie jetzt für jede Zielgruppe ein Startdatum (obligatorisch), ein Enddatum (optional) und eine Zuordnungs-ID (obligatorisch) konfigurieren.

>[!IMPORTANT]
>
> Für dieses Ziel ist eine Zuordnungs-ID oder &quot;KEINE&quot;erforderlich.
>
> Eine Zuordnungs-ID sollte bereitgestellt werden, wenn eine Zielgruppe über eine bereits vorhandene Segment-ID verfügt, die zuvor für Magnite Streaming bekannt war. Andernfalls sollte &quot;KEINE&quot;als Zuordnungs-ID verwendet werden.
>
> Fügen Sie bei der Konfiguration des Dateinamens für jede Zielgruppe die Zuordnungs-ID über das Feld &quot;Benutzerdefinierter Text&quot; hinzu, das hinzugefügt werden soll. Die Zuordnungs-ID wird wie folgt angehängt: `{previous_filename}\_\[MAPPING_ID\].` Wenn diese Zielgruppe neu im Magnite-Streaming ist und Sie keine Zuordnungs-ID angeben, sollte &quot;KEINE&quot;in das Feld &quot;Benutzerdefinierter Text&quot;eingegeben werden. Der neue Dateiname sollte in diesem Fall: `{previous_filename}\_\[NONE\]` lauten.

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach dem Hochladen Ihrer Zielgruppen können Sie überprüfen, ob Ihre Zielgruppen korrekt erstellt und hochgeladen wurden.

* Das Magnite: Batch-Ziel liefert S3-Dateien täglich an Magnite Streaming. Nach dem Versand und der Erfassung werden Zielgruppen/Segmente voraussichtlich im Magnite-Streaming angezeigt und können auf einen Deal angewendet werden. Sie können dies bestätigen, indem Sie die Segment-ID oder den Segmentnamen nachschlagen, die bzw. der während der Aktivierungsschritte in der Adobe Experience Platform freigegeben wurde.

>[!NOTE]
>
>Zielgruppen, die für Magnite aktiviert/bereitgestellt werden: Das Batch-Ziel ersetzt *1} die gleichen Zielgruppen, die über das Echtzeit-Ziel Magnite aktiviert/bereitgestellt wurden.* Wenn Sie ein Segment mithilfe des Segmentnamens nachschlagen, finden Sie das Segment möglicherweise erst in Echtzeit, nachdem der Batch von der Magnite-Streaming-Plattform erfasst und verarbeitet wurde.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Hilfedokumentation finden Sie im [Magnite Help Center](https://help.magnite.com/help).
