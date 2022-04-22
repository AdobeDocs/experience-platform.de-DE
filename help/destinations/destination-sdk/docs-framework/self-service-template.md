---
title: Vorlage für Dokumentations-Self-Service // Ersetzen Sie durch den Namen Ihres Ziels.
description: Verwenden Sie diese Vorlage, um eine öffentliche Dokumentation für Ihr Ziel im Adobe Experience Platform-Katalog zu erstellen. // Ersetzen Sie durch den Absatz im Abschnitt "Übersicht".
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: f9938aca8a5c72a53a688152ac2ab0c0abe632ce
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 6%

---

# YourDestination connection {#your-destination}

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle kursiv gedruckten Absätze (beginnend mit dieser).*

*Aktualisieren Sie zunächst die Metadaten (Titel und Beschreibung) oben auf der Seite. Bitte ignorieren Sie alle UICONTROL Instanzen auf dieser Seite. Dies ist ein Tag, das unseren maschinellen Übersetzungsprozessen hilft, die Seite korrekt in die verschiedenen Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation Tags hinzu, nachdem Sie sie gesendet haben.*

>[!IMPORTANT]
>
>* Füllen Sie alle Abschnitte in dieser Vorlage in der Reihenfolge aus, in der sie in der Vorlage beschrieben sind.
>* Diese Vorlage wird aufgrund des Partner-Feedbacks gelegentlich aktualisiert. Bevor Sie mit der Erstellung der Dokumentation für Ihr Ziel beginnen, stellen Sie sicher, dass Sie die [aktuelle Version der Vorlage](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).


## Übersicht {#overview}

*Geben Sie einen kurzen Überblick über Ihr Unternehmen, einschließlich des Nutzens, den es für Kunden bietet. Fügen Sie einen Link zu Ihrer Homepage für die Produktdokumentation hinzu, um ihn weiter zu lesen.*

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde von der *YourDestination* Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *Fügen Sie einen Link oder eine E-Mail-Adresse ein, an die Sie zur Aktualisierung gelangen können, z. B. `support@YourDestination.com`.*

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die *YourDestination* Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1 {#use-case-1}

*Für mobile Messaging-Plattformen:*

*Eine Heimmiet- und Verkaufsplattform möchte Mobile-Benachrichtigungen an die Android- und iOS-Geräte von Kunden senden, um ihnen mitzuteilen, dass es 100 aktualisierte Listen in dem Bereich gibt, in dem sie zuvor nach einer Vermietung gesucht haben.*

### Anwendungsfall 2 {#use-case-2}

*Für soziale Netzwerkplattformen:*

*Eine Marke für Sportbekleidung möchte bestehende Kunden über ihre Social-Media-Konten erreichen. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in Adobe Experience Platform erfassen, Segmente aus ihren eigenen Offline-Daten erstellen und diese Segmente an YourDestination senden, um Anzeigen in den Social-Media-Feeds ihrer Kunden anzuzeigen.*

## Voraussetzungen {#prerequisites}

*Fügen Sie in diesem Abschnitt Informationen zu allen Elementen hinzu, die Kunden kennen müssen, bevor sie mit der Einrichtung des Ziels in der Adobe Experience Platform-Benutzeroberfläche beginnen. Dabei kann es sich um Folgendes handeln:*

* *einer Zulassungsliste hinzugefügt werden müssen*
* *Anforderungen für das E-Mail-Hashing*
* *alle Kontospezifikationen auf Ihrer Seite*
* *Abrufen eines API-Schlüssels für die Verbindung mit Ihrer Plattform*

*Wenn dies für Kunden von Nutzen wäre, können Sie einen Link zu Ihrer relevanten Dokumentation erstellen.*

## Unterstützte Identitäten {#supported-identities}

*Fügen Sie in diesem Abschnitt Informationen zu den Identitäten hinzu, die von Ihrem Ziel unterstützt werden. Wir haben die Tabelle mit einigen Standardwerten vorausgefüllt. Löschen Sie die Werte, die nicht auf Ihr Ziel zutreffen, sowie alle Werte, die nicht vorausgefüllt sind.*

*YourDestination* unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Alias referenziert werden: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Siehe folgendes Dokument unter [ECID](/help/identity-service/ecid.md) für weitere Informationen. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Sowohl einfache als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

*Behalten Sie in der Tabelle nur die Zeilen bei, die Ihrem Ziel entsprechen. Sie sollten eine Zeile für den Exporttyp und eine Zeile für die Exporthäufigkeit haben. Löschen Sie die Werte, die nicht auf Ihr Ziel zutreffen.*

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im *YourDestination* Ziel. |
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### An Ziel authentifizieren {#authenticate}

*Fügen Sie die Felder hinzu, die Kunden bei der Authentifizierung für Ihr Ziel ausfüllen müssen. Diese Felder sind zielspezifisch und hängen von Ihrer Konfiguration in Destination SDK ab. Die Felder Ihres Ziels entsprechen möglicherweise nicht den unten aufgeführten. Bitte fügen Sie auch einen Screenshot hinzu, der dem unten gezeigten Beispiel-Screenshot ähnelt.*

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

![Beispiel-Screenshot mit der Authentifizierung für das Ziel](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL Trägertoken]**: Füllen Sie das Trägertoken aus, um sich beim Ziel zu authentifizieren.

### Zieldetails ausfüllen {#destination-details}

*Fügen Sie die Felder hinzu, die Kunden beim Konfigurieren eines neuen Ziels ausfüllen müssen. Diese Felder sind zielspezifisch und hängen von Ihrer Konfiguration in Destination SDK ab. Die Felder Ihres Ziels entsprechen möglicherweise nicht den unten aufgeführten. Bitte fügen Sie auch einen Screenshot hinzu, der dem unten gezeigten Beispiel-Screenshot ähnelt.*

Füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Nächste]**.

![Beispiel-Screenshot, der zeigt, wie Details für Ihr Ziel ausgefüllt werden](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre *YourDestination* Konto-ID.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Export von Daten/Export validieren {#exported-data}

*Fügen Sie einen Absatz hinzu, in dem beschrieben wird, wie Daten an Ihr Ziel exportiert werden. Dadurch kann der Kunde sicherstellen, dass er korrekt in Ihr Ziel integriert ist. Sie können beispielsweise eine JSON-Beispieldatei wie die unten stehende bereitstellen. Sie können auch Screenshots und Informationen aus der Benutzeroberfläche Ihres Ziels bereitstellen, die zeigen, wie Kunden erwarten sollten, dass Segmente in die Zielplattform gefüllt werden.*

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
        "status": "existing"
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

## Weitere Ressourcen {#additional-resources}

*Sie können weitere Links zu Ihrer Produktdokumentation oder anderen Ressourcen bereitstellen, die Sie für den Erfolg des Kunden als wichtig erachten.*