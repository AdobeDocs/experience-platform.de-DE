---
title: Vorlage für Dokumentations-Self-Service // Ersetzen durch den Namen Ihres Ziels
description: Verwenden Sie diese Vorlage, um eine öffentliche Dokumentation für Ihr Ziel im Adobe Experience Platform-Katalog zu erstellen. // Ersetzen Sie durch den Absatz im Abschnitt "Übersicht".
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 48efe49a51c2917cd4bda9b6d8aaed72d8f0f90b
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 35%

---

# YourDestination connection {#your-destination}

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle kursiv gedruckten Absätze (beginnend mit dieser).*

*Aktualisieren Sie zunächst die Metadaten (Titel und Beschreibung) oben auf der Seite. Bitte ignorieren Sie alle UICONTROL Instanzen auf dieser Seite. Dies ist ein Tag, das unseren maschinellen Übersetzungsprozessen hilft, die Seite korrekt in die verschiedenen Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation Tags hinzu, nachdem Sie sie gesendet haben.*

>[!IMPORTANT]
>
>* Füllen Sie alle Abschnitte in dieser Vorlage in der Reihenfolge aus, in der sie in der Vorlage beschrieben sind.
>* Diese Vorlage wird aufgrund des Partner-Feedbacks gelegentlich aktualisiert. Bevor Sie mit der Erstellung der Dokumentation für Ihr Ziel beginnen, stellen Sie sicher, dass Sie die [aktuelle Version der Vorlage](../assets/docs-framework/yourdestination-template.zip) heruntergeladen haben.

## Übersicht {#overview}

*Geben Sie einen kurzen Überblick über Ihr Unternehmen, einschließlich des Nutzens, den es für Kunden bietet. Fügen Sie einen Link zu Ihrer Homepage für die Produktdokumentation hinzu, um ihn weiter zu lesen.*

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite wird von der *YourDestination* Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *Fügen Sie einen Link oder eine E-Mail-Adresse ein, an die Sie zur Aktualisierung gelangen können, beispielsweise `support@YourDestination.com`.*

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die *YourDestination* Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1 {#use-case-1}

*Für mobile Messaging-Plattformen:*

*Eine Heimmiet- und Verkaufsplattform möchte Mobile-Benachrichtigungen an die Android- und iOS-Geräte von Kunden senden, um ihnen mitzuteilen, dass es 100 aktualisierte Listen in dem Bereich gibt, in dem sie zuvor nach einer Vermietung gesucht haben.*

### Anwendungsfall 2 {#use-case-2}

*Für soziale Netzwerkplattformen:*

*Eine Marke für Sportbekleidung möchte bestehende Kunden über ihre Social-Media-Konten erreichen. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in Adobe Experience Platform erfassen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an YourDestination senden, um Anzeigen in den Social-Media-Feeds ihrer Kunden anzuzeigen.*

## Voraussetzungen {#prerequisites}

*Fügen Sie in diesem Abschnitt Informationen zu allen Elementen hinzu, die Kunden kennen müssen, bevor sie mit der Einrichtung des Ziels in der Adobe Experience Platform-Benutzeroberfläche beginnen. Dabei kann es sich um Folgendes handeln:*

* *einer Zulassungsliste hinzugefügt werden müssen*
* *Anforderungen für das E-Mail-Hashing*
* *alle Kontospezifikationen auf Ihrer Seite*
* *Abrufen eines API-Schlüssels für die Verbindung mit Ihrer Plattform*

*Wenn dies für Kunden von Nutzen wäre, können Sie einen Link zu Ihrer relevanten Dokumentation erstellen.*

## Unterstützte Identitäten {#supported-identities}

*Fügen Sie in diesem Abschnitt Informationen zu den Identitäten hinzu, die von Ihrem Ziel unterstützt werden. Wir haben die Tabelle mit einigen Standardwerten vorausgefüllt. Löschen Sie die Werte, die nicht auf Ihr Ziel zutreffen, und/oder fügen Sie Werte hinzu, die nicht vorausgefüllt sind.*

*YourDestination* unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Lesen Sie das folgende Dokument unter [ECID](/help/identity-service/ecid.md) für weitere Informationen. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

*Fügen Sie in diesem Abschnitt Informationen zu den von Ihrem Ziel unterstützten Zielgruppen hinzu. Wir haben die Tabelle mit einigen Standardwerten vorausgefüllt. Verwenden Sie die `✓` und `X` Zeichen, um zu kennzeichnen, ob Ihr Zielgruppentyp von diesem Ziel unterstützt wird.*

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

*Behalten Sie in der Tabelle nur die Zeilen bei, die Ihrem Ziel entsprechen. Sie sollten eine Zeile für den Exporttyp und eine Zeile für die Exporthäufigkeit haben. Löschen Sie die Werte, die nicht auf Ihr Ziel zutreffen.*

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im *YourDestination* Ziel. |
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute auswählen der [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporttyp | **[!UICONTROL Datensatzexport]** | Sie exportieren Rohdatensätze, die nicht nach Zielgruppeninteressen oder Qualifikationen gruppiert oder strukturiert sind. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

*Fügen Sie die Felder hinzu, die Kunden bei der Authentifizierung für Ihr Ziel ausfüllen müssen. Diese Felder sind zielspezifisch und hängen von Ihrer Konfiguration in Destination SDK ab. Die Felder Ihres Ziels entsprechen möglicherweise nicht den unten aufgeführten. Bitte fügen Sie auch einen Screenshot hinzu, der dem unten gezeigten Beispiel-Screenshot ähnelt.*

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**.

![Beispiel-Screenshot mit der Authentifizierung für das Ziel](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

*Fügen Sie die Felder hinzu, die Kunden beim Konfigurieren eines neuen Ziels ausfüllen müssen. Diese Felder sind zielspezifisch und hängen von Ihrer Konfiguration in Destination SDK ab. Die Felder Ihres Ziels entsprechen möglicherweise nicht den unten aufgeführten. Bitte fügen Sie auch einen Screenshot hinzu, der dem unten gezeigten Beispiel-Screenshot ähnelt.*

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Beispiel-Screenshot, der zeigt, wie Details für Ihr Ziel ausgefüllt werden](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihr *YourDestination* Konto-ID.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

*Entf, falls zutreffend - Wenn Sie ein neues Streaming-Ziel dokumentieren, behalten Sie den ersten Absatz unten bei. Wenn Sie ein neues dateibasiertes Ziel dokumentieren, behalten Sie den zweiten Absatz bei. Wenn Sie ein Ziel dokumentieren, das Datensätze exportiert, behalten Sie den dritten Absatz bei.*

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

Lesen [(Beta) Datensätze exportieren](/help/destinations/ui/export-datasets.md) für ausführliche Anweisungen zum Exportieren von Datensätzen an dieses Ziel.

### Zuordnen von Attributen und Identitäten {#map}

*Fügen Sie im Schritt Zuordnung des Aktivierungs-Workflows Informationen zu unterstützten Zuordnungen zwischen Quell- und Zielfeldern hinzu. Ihr Ziel unterstützt möglicherweise das Exportieren von Profilattributen, Identitäts-Namespaces oder beidem. Einige Felder sind möglicherweise Pflichtfelder. Zielattribute können vordefiniert oder benutzerdefiniert sein. Machen Sie sich mit den wichtigen Einschränkungen vertraut und verwenden Sie Beispiele, vorzugsweise mit Screenshots. Zwei Beispiele für Zielseiten, die Sie als Referenz verwenden können:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Exportierte Daten/Datenexport validieren {#exported-data}

*Fügen Sie einen Absatz hinzu, in dem beschrieben wird, wie Daten an Ihr Ziel exportiert werden. Dadurch kann der Kunde sicherstellen, dass er korrekt in Ihr Ziel integriert ist. Sie können beispielsweise eine JSON-Beispieldatei wie die unten stehende bereitstellen. Alternativ können Sie Screenshots und Informationen aus der Benutzeroberfläche Ihres Ziels bereitstellen, die zeigen, wie Kunden erwarten sollten, dass Zielgruppen in die Zielplattform gelangen.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

*Sie können weitere Links zu Ihrer Produktdokumentation oder anderen Ressourcen bereitstellen, die Sie für den Erfolg des Kunden als wichtig erachten.*