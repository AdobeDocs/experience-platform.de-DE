---
title: Nachschlagen von Edge-Profilattributen in Echtzeit
description: Erfahren Sie, wie Sie Edge-Profilattribute mithilfe des benutzerdefinierten Personalization-Ziels und der Edge Network-API in Echtzeit suchen
type: Tutorial
exl-id: e185d741-af30-4706-bc8f-d880204d9ec7
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 3%

---

# Profilattribute am Edge in Echtzeit nachschlagen

Adobe Experience Platform verwendet das [Echtzeit-Kundenprofil](../../profile/home.md) als zentrale Datenquelle für alle Profildaten. Für den schnellen Datenabruf in Echtzeit werden [Edge-Profile](../../profile/edge-profiles.md) verwendet, bei denen es sich um einfache Profile handelt, die über die gesamte [Edge Network verteilt &#x200B;](../../collection/home.md#edge). Dies ermöglicht Anwendungsfälle für die schnelle Personalisierung in Echtzeit.

## Anwendungsfälle {#use-cases}

Im Folgenden finden Sie zwei Anwendungsfälle, in denen die Suche nach Edge-Profilen hilfreich sein kann.

* **Echtzeit-Personalization**: Schnelles Abrufen von Profilinformationen aus dem Edge-Profil, um das Erlebnis eines Benutzers auf Ihrer Website zu personalisieren.
* **Support**: Profilinformationen in Echtzeit abrufen, wenn ein Kunde einen Support-Center-Agenten anruft.

Auf dieser Seite werden die Schritte beschrieben, die Sie befolgen müssen, um Edge-Profildaten in Echtzeit nachzuschlagen, Personalisierungserlebnisse bereitzustellen oder über nachgelagerte Anwendungen Entscheidungsregeln zu informieren.

## Terminologie und Voraussetzungen {#prerequisites}

Beim Konfigurieren des auf dieser Seite beschriebenen Anwendungsfalls verwenden Sie die folgenden Experience Platform-Komponenten:

* [Datenströme](../../datastreams/overview.md): Ein Datenstrom empfängt eingehende Ereignisdaten von Web SDK und antwortet mit Edge-Profildaten.
* [Zusammenführungsrichtlinien](../../segmentation/ui/segment-builder.md#merge-policies): Sie erstellen eine [!UICONTROL Active-On-Edge] Zusammenführungsrichtlinie, um sicherzustellen, dass die Edge-Profile die richtigen Profildaten verwenden.
* [Benutzerdefinierte Personalization-Verbindung](../catalog/personalization/custom-personalization.md): Sie konfigurieren eine neue benutzerdefinierte Personalisierungsverbindung, die die Profilattribute an die Edge Network sendet.
* [Edge Network-](https://developer.adobe.com/data-collection-apis/docs/): Sie verwenden die Edge Network-API [interaktive Datenerfassung](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/), um Profilattribute schnell aus den Edge-Profilen abzurufen.

## Performance-Garantien {#guardrails}

Anwendungsfälle für die Profilsuche in Edge unterliegen den spezifischen Leistungsschutzmechanismen, die in der folgenden Tabelle beschrieben werden. Weitere Informationen zu den Edge Network-API-Leitplanken finden Sie auf der Dokumentationsseite [Leitplanken](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/).

| Edge Network-Service | Edge-Segmentierung | Anfragen pro Sekunde |
|---------|----------|---------|
| [Benutzerdefiniertes Personalisierungsziel](../catalog/personalization/custom-personalization.md) über die [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/api/) | Ja | 1.500 |
| [Benutzerdefiniertes Personalisierungsziel](../catalog/personalization/custom-personalization.md) über die [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/api/) | Nein | 1.500 |

## Schritt 1: Erstellen und Konfigurieren eines Datenstroms {#create-datastream}

Führen Sie die Schritte in der Dokumentation [Datenstromkonfiguration](../../datastreams/configure.md#create-a-datastream) aus, um einen neuen Datenstrom mit den folgenden **[!UICONTROL Service]**-Einstellungen zu erstellen:

* **[!UICONTROL Service]**: [!UICONTROL Adobe Experience Platform]
* **[!UICONTROL Personalization Destinations]**: aktiviert
* **[!UICONTROL Edge Segmentation]**: Wenn Sie die Edge-Segmentierung benötigen, aktivieren Sie diese Option. Wenn Sie nur an der Suche nach Profilattributen am Edge interessiert sind, aber keine Segmentierung basierend auf den Edge-Profilen durchführen möchten, lassen Sie diese Option deaktiviert.


<!-- >[!IMPORTANT]
>
>Enabling edge segmentation limits the maximum number of lookup requests to 1500 request per second. If you need a higher request throughput, disable edge segmentation for your datastream. See the [guardrails documentation](../guardrails.md#edge-destinations-activation) for detailed information. -->

![Bild der Experience Platform-Benutzeroberfläche mit dem Bildschirm für die Datenstromkonfiguration.](../assets/ui/activate-edge-profile-lookup/datastream-config.png)


## Schritt 2: Konfigurieren Sie Ihre Zielgruppen für die Edge-Evaluierung. {#audience-edge-evaluation}

Für das Nachschlagen von Profilattributen am Edge müssen Ihre Zielgruppen für die Edge-Evaluierung konfiguriert werden.

Stellen Sie sicher, dass für die Zielgruppen, die Sie aktivieren möchten, die [Zusammenführungsrichtlinie „Active-On-Edge](../../segmentation/ui/segment-builder.md#merge-policies) als Standard festgelegt ist. Die [!DNL Active-On-Edge] Zusammenführungsrichtlinie stellt sicher, dass Zielgruppen ständig [on the Edge) ausgewertet &#x200B;](../../segmentation/methods/edge-segmentation.md) für Anwendungsfälle der Echtzeit-Personalisierung verfügbar sind.

Befolgen Sie die Anweisungen unter [Erstellen einer Zusammenführungsrichtlinie](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) und stellen Sie sicher, dass Sie den Umschalter **[!UICONTROL Active-On-Edge Merge Policy]** aktivieren.

>[!IMPORTANT]
>
>Wenn Ihre Zielgruppen eine andere Zusammenführungsrichtlinie verwenden, können Sie keine Profilattribute vom Edge abrufen und keine Edge-Profilsuche durchführen.

## Schritt 3: Senden von Profilattributdaten an Edge Network{#configure-custom-personalization-connection}

Um Edge-Profile, einschließlich Attributen und Daten zur Zielgruppenzugehörigkeit, in Echtzeit zu suchen, müssen die Daten auf der Edge Network verfügbar gemacht werden. Dazu müssen Sie eine Verbindung zu einem **[!UICONTROL Custom Personalization With Attributes]** Ziel erstellen und die Zielgruppen aktivieren, einschließlich der Attribute, die Sie in den Edge-Profilen nachschlagen möchten.

+++ Konfigurieren einer benutzerdefinierten Personalization mit Verbindungsattributen

Im [Tutorial zur Erstellung von Zielverbindungen](../ui/connect-destination.md) finden Sie detaillierte Anweisungen zum Erstellen einer neuen Zielverbindung.

Wählen Sie beim Konfigurieren des neuen Ziels den Datenstrom aus, den Sie in [Schritt 1](#create-datastream) im Feld **[!UICONTROL Datastream ID]** erstellt haben. **[!UICONTROL Integration alias]** können Sie jeden Wert verwenden, der Ihnen bei der zukünftigen Identifizierung dieser Zielverbindung hilft, z. B. den Zielnamen.

![Bild der Experience Platform-Benutzeroberfläche mit dem Konfigurationsbildschirm für benutzerdefinierte Personalization mit Attributen.](../assets/ui/activate-edge-profile-lookup/destination-config.png)

+++

+++Aktivieren Sie Ihre Zielgruppen für die Verbindung Benutzerdefinierte Personalization mit Attributen .

Nachdem Sie eine **[!UICONTROL Custom Personalization With Attributes]** erstellt haben, können Sie jetzt Profildaten an Edge Network senden.

>[!IMPORTANT]
> 
> * Um Daten zu aktivieren und den [Zuordnungsschritt](#mapping) des Workflows zu aktivieren, benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
> 
> Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

1. Wechseln Sie zu **[!UICONTROL Connections > Destinations]** und wählen Sie die Registerkarte **[!UICONTROL Catalog]** aus.

   ![Registerkarte „Zielkatalog“ in der Experience Platform-Benutzeroberfläche hervorgehoben.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Suchen Sie die **[!UICONTROL Custom Personalization With Attributes]** Zielkarte und wählen Sie dann **[!UICONTROL Activate audiences]** aus, wie in der Abbildung unten dargestellt.

   ![Zielgruppen-Steuerelement aktivieren, das auf einer Zielkarte im Katalog hervorgehoben ist.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Wählen Sie die zuvor konfigurierte Zielverbindung aus und klicken Sie dann auf **[!UICONTROL Next]**.

   ![Zielschritt im Aktivierungs-Workflow auswählen.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Auswählen Ihrer Zielgruppen. Aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen, um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, und klicken Sie dann auf **[!UICONTROL Next]**.

   Je nach Herkunft können Sie aus verschiedenen Arten von Zielgruppen auswählen:

   * **[!UICONTROL Segmentation Service]**: Zielgruppen, die in Experience Platform vom Segmentierungs-Service generiert werden. Weitere Informationen finden Sie [Segmentierungsdokumentation](../../segmentation/ui/overview.md) .
   * **[!UICONTROL Custom upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Experience Platform hochgeladen wurden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation unter [Importieren einer Zielgruppe](../../segmentation/ui/overview.md#import-audience).
   * Andere Arten von Zielgruppen, die aus anderen Adobe-Lösungen wie [!DNL Audience Manager] stammen.

     ![Schritt „Zielgruppen auswählen“ des Aktivierungs-Workflows mit mehreren hervorgehobenen Zielgruppen.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

1. Wählen Sie die Profilattribute aus, die Sie für die Edge-Profile verfügbar machen möchten.

   * **Quellattribute auswählen**. Um Quellattribute hinzuzufügen, wählen Sie die **[!UICONTROL Add new field]** in der Spalte **[!UICONTROL Source field]** aus und suchen oder navigieren Sie zum gewünschten XDM-Attributfeld, wie unten dargestellt.

     ![Bildschirmaufzeichnung, die zeigt, wie ein Zielattribut im Zuordnungsschritt ausgewählt wird.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

   * **Auswählen der Zielattribute**. Um Zielattribute hinzuzufügen, wählen Sie das **[!UICONTROL Add new field]** in der Spalte **[!UICONTROL Target field]** aus und geben Sie den benutzerdefinierten Attributnamen ein, dem Sie das Quellattribut zuordnen möchten.

     ![Bildschirmaufzeichnung, die zeigt, wie ein XDM-Attribut im Zuordnungsschritt ausgewählt wird](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

Wenn Sie mit der Zuordnung von Profilattributen fertig sind, wählen Sie **[!UICONTROL Next]** aus.

Auf der Seite **[!UICONTROL Review]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Cancel]** aus, um den Fluss zu unterbrechen, **[!UICONTROL Back]**, Ihre Einstellungen zu ändern, oder **[!UICONTROL Finish]** , um Ihre Auswahl zu bestätigen und mit dem Senden von Profildaten an die Edge Network zu beginnen.

![Zusammenfassung der Auswahl im Überprüfungsschritt.](../assets/ui/activate-edge-personalization-destinations/review.png)

+++

+++Auswertung der Einverständnisrichtlinie

Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL View applicable consent policies]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Weitere Informationen finden [&#x200B; unter &#x200B;](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) der Einverständnisrichtlinie .

**Prüfungen der Datennutzungsrichtlinien**

Im **[!UICONTROL Review]** Schritt prüft Experience Platform auch, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Zielgruppenaktivierungs-Workflow erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Dokumentationsabschnitt zur Data Governance.

![Beispiel für eine Datenrichtlinienverletzung.](../assets/common/data-policy-violation.png)

+++

+++Audiences filtern

Im **[!UICONTROL Review]** Schritt können Sie die auf der Seite verfügbaren Filter verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde. Sie können auch umschalten, welche Tabellenspalten angezeigt werden sollen.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)


Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Finish]** aus, um Ihre Auswahl zu bestätigen.

+++

## Schritt 4: Profilattribute am Edge nachschlagen {#configure-edge-profile-lookup}

Mittlerweile sollten Sie mit der [Konfiguration Ihres Datenstroms](#create-datastream) fertig sein. Sie haben [eine neue Zielverbindung für benutzerdefinierte Personalization mit Attributen erstellt](#configure-destination) und Sie haben diese Verbindung verwendet, um [die Profilattribute zu senden](#activate-audiences), die Sie dann in der Edge Network nachschlagen können.

Der nächste Schritt besteht darin, Ihre Personalisierungslösung so zu konfigurieren, dass Profilattribute aus den Edge-Profilen abgerufen werden.

>[!IMPORTANT]
>
>Profilattribute können vertrauliche Daten enthalten. Zum Schutz dieser Daten müssen Sie die Profilattribute über die [Edge Network-API abrufen](https://developer.adobe.com/data-collection-apis/docs/getting-started/). Darüber hinaus müssen Sie die Profilattribute über die Edge Network-API [Endpunkt für die interaktive Datenerfassung](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) abrufen, damit die API-Aufrufe authentifiziert werden.
>
>Wenn Sie die oben genannten Anforderungen nicht erfüllen, basiert die Personalisierung nur auf der Zielgruppenzugehörigkeit, und Ihnen stehen keine Profilattribute zur Verfügung.

Der in [Schritt 1) konfigurierte Datenstrom &#x200B;](#create-datastream) jetzt eingehende Ereignisdaten akzeptieren und mit Edge-Profilinformationen antworten.

Konfigurieren Sie Ihre Integration, um Edge-Profilinformationen abzurufen, wie in den Beispielen unten gezeigt.

### Anfrage {#request}

Um Edge-Profildaten abzurufen, senden Sie einen leeren `POST`-Aufruf an den `/interact`-Endpunkt, wobei die primäre Identität, für die Sie Profilattribute nachschlagen, im Ereignis enthalten ist, wie unten dargestellt.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
    "event":
    {
        "xdm": {
            "identityMap": {
                "Email": [
                    {  
                        "id":"test123@adobetest.com",
                        "primary":true
                    }
                ]
            }
        }
    }
    
}'
```

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | Die Datenstrom-ID des Datenstroms, den Sie in ([&#x200B; 1) erstellt &#x200B;](#create-datastream). |

### Antwort {#response}

Bei einer erfolgreichen Antwort wird der HTTP-Status `200 OK` mit einem `Handle`-Objekt zurückgegeben, das Informationen ähnlich den Beispielen in den unten stehenden Registerkarten enthält, je nachdem, ob das Profil am Edge gefunden wird oder nicht.

>[!NOTE]
>
>Die API-Antworten sind modular und das `handle` kann mehrere `payload` Objekte verschiedener Typen enthalten. Die Informationen zur Suche nach Edge-Profilen sind unter dem `payload` mit `"type": "activation:pull"` gruppiert.

>[!BEGINTABS]

>[!TAB Profil ist am Edge vorhanden]

Wenn das Profil am Edge vorhanden ist, können Sie je nach den Profilattributen und den für den Edge aktivierten Zielgruppen eine -Antwort mit Attributen und Zielgruppenzugehörigkeiten ähnlich der folgenden erwarten.

```json
{
  "requestId": "3c600138-d785-42ca-a025-bb725f4b5da9",
  "handle": [
    {
      "payload": [
        {
          "type": "profileLookup",
          "destinationId": "9218b727-ec59-4a46-b8b9-05503f138c5d",
          "alias": "rk-demo-custom-personalization-XXXX",
          "attributes": {
            "zip": {
              "value": "19000"
            },
            "firstName": {
              "value": "Test"
            },
            "lastName": {
              "value": "User123"
            },
            "gender": {
              "value": "male"
            },
            "city": {
              "value": "Philadelphia"
            },
            "state": {
              "value": "PA"
            },
            "email": {
              "value": "test123@adobetest.com"
            }
          },
          "segments": [
            {
              "id": "85018bd8-7ad1-4e17-ae30-8389c04bd3c0",
              "namespace": "ups"
            },
            {
              "id": "d09a8159-8b30-4178-b2f2-7a8c5e3168d9",
              "namespace": "ups"
            }
          ]
        }
      ],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

Das `handle`-Objekt stellt die in der folgenden Tabelle beschriebenen Informationen bereit.

| Parameter | Beschreibung |
|---------|----------|
| `payload` | Das `payload`, das die Edge-Lookup-Informationen enthält. Die Antwort kann mehrere zusätzliche `payload`-Objekte enthalten, die nicht mit der Edge-Suche zusammenhängen. |
| `type` | Payloads werden in der Antwort nach ihrem Typ gruppiert. Der Payload-Typ für die Edge-Profilsuche ist immer auf `profileLookup` festgelegt. |
| `destinationId` | Die ID der **[!UICONTROL Custom Personalization]** Verbindungsinstanz, die Sie in ([&#x200B; 3) erstellt &#x200B;](#configure-custom-personalization-connection). |
| `alias` | Der Alias der Zielverbindung, der von den Benutzenden beim Erstellen der Zielverbindung [Benutzerdefinierte Personalization](../catalog/personalization/custom-personalization.md) konfiguriert wird. |
| `attributes` | Dieses Array enthält die Edge-Profilattribute der Zielgruppen, die Sie in ([&#x200B; 3) aktiviert &#x200B;](#configure-custom-personalization-connection). |
| `segments` | Dieses Array enthält die Zielgruppen, die Sie in ([&#x200B; 3) aktiviert &#x200B;](#configure-custom-personalization-connection). |
| `type` | `handle` Objekte werden nach Typ gruppiert. Bei Anwendungsfällen für die Kantenprofilsuche wird der Typ des `handle` immer `activation:pull`. |
| `eventIndex` | Die Edge Network empfängt Ereignisse vom Client in Form von Arrays. Die Reihenfolge der Ereignisse im Array wird während ihrer Verarbeitung beibehalten und von diesem Index übernommen. Die Ereignisindizierung beginnt mit `0`. |

>[!TAB Profil ist am Edge nicht vorhanden]

Wenn das Profil nicht am Edge vorhanden ist, können Sie eine ähnliche Antwort wie die folgende erwarten.

```json
{
  "requestId": "531b541a-4541-419e-ac99-fd7e452f0c0f",
  "handle": [
    {
      "payload": [],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

Das `handle`-Objekt stellt die in der folgenden Tabelle beschriebenen Informationen bereit.

| Parameter | Beschreibung |
|---------|----------|
| `payload` | Wenn das Profil nicht auf der Kante vorhanden ist, ist das `payload` leer. |
| `type` | `payload` Objekte werden nach Typ gruppiert. Bei Anwendungsfällen für die Kantenprofilsuche wird der Typ des `payload` immer `activation:pull`. |
| `eventIndex` | Die Edge Network empfängt Ereignisse vom Client in Form von Arrays. Die Reihenfolge der Ereignisse im Array wird während ihrer Verarbeitung beibehalten und von diesem Index übernommen. Die Ereignisindizierung beginnt mit `0`. |

>[!ENDTABS]

>[!SUCCESS]
>
>Wenn Sie die Integration richtig konfiguriert haben, haben Sie jetzt Zugriff auf die Edge-Profildaten und Sie können die Attribute und die Zielgruppenzugehörigkeit Ihrer Edge-Profile verwenden, um die Echtzeit-Personalisierung in Ihrer nachgelagerten Personalisierungs-Engine Trigger.

## Zusammenfassung {#conclusion}

Wenn Sie die oben genannten Schritte ausführen, können Sie Edge-Profilattribute effizient in Echtzeit nachschlagen und so personalisierte Erlebnisse und fundierte Entscheidungen durch nachgelagerte Anwendungen ermöglichen.
