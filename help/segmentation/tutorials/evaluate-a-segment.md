---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentbewertung;Segmentierungsdienst;Segmentierung;Segmentierung;Segmentierung;Segmentergebnisse auswerten;Segmentdaten auswerten und zugreifen;
solution: Experience Platform
title: Segmentergebnisse bewerten und aufrufen
topic-legacy: tutorial
type: Tutorial
description: In diesem Lernprogramm erfahren Sie, wie Sie mithilfe der Adobe Experience Platform Segmentierungsdienst-API Segmente auswerten und auf Segmentergebnisse zugreifen.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 15%

---

# Segmentergebnisse auswerten und darauf zugreifen

Dieses Dokument bietet eine Anleitung zum Evaluieren von Segmenten und zum Zugriff auf Segmentergebnisse mit dem [[!DNL Segmentation API]](../api/getting-started.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste, die beim Erstellen von Audiencen-Segmenten erforderlich sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

### Erforderliche Kopfzeilen

Für dieses Lernprogramm müssen Sie außerdem das [Authentifizierungstreffen](https://www.adobe.com/go/platform-api-authentication-en) abgeschlossen haben, um erfolgreich Aufrufe an [!DNL Platform]-APIs durchführen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Anforderungen an [!DNL Platform]-APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anforderungen ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Bewerten eines Segments

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten.

[Die geplante Auswertung](#scheduled-evaluation)  (auch als &quot;geplante Segmentierung&quot;bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während bei der  [On-Demand-](#on-demand-evaluation) Auswertung ein Segmentauftrag erstellt wird, um die Audience sofort zu erstellen. Die Schritte für die einzelnen Schritte sind nachfolgend beschrieben.

Wenn Sie das Tutorial [Segmentierung mit der Segmentierungs-API](./create-a-segment.md) noch nicht abgeschlossen haben oder eine Segmentdefinition mit [Segmentaufbau](../ui/overview.md) erstellt haben, führen Sie dies bitte aus, bevor Sie mit diesem Tutorial fortfahren.

## Geplante Evaluierung {#scheduled-evaluation}

Durch die geplante Auswertung kann Ihr IMS-Org einen wiederkehrenden Zeitplan erstellen, um Exportaufträge automatisch auszuführen.

>[!NOTE]
>
>Geplante Evaluierung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihr Unternehmen über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] in einer einzelnen Sandbox-Umgebung verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

Ausführlichere Informationen zur Verwendung dieses Endpunktes finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#create)

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

Ausführlichere Informationen zur Verwendung dieses Endpunktes finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-state)

### Zeitplanaktualisierung

Die Zeitplanung kann aktualisiert werden, indem eine PATCH an den `/config/schedules`-Endpunkt angefordert wird und die ID des Zeitplans in den Pfad aufgenommen wird.

Ausführlichere Informationen zur Verwendung dieses Endpunktes finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-schedule)

## On-Demand-Bewertung

Mit der On-Demand-Auswertung können Sie einen Segmentauftrag erstellen, um bei Bedarf ein Audiencen-Segment zu generieren. Im Gegensatz zur geplanten Auswertung erfolgt dies nur auf Anfrage und nicht wiederholt.

### Erstellen eines Segmentauftrags

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Zielgruppensegment erstellt wird. Es verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die steuern, wie [!DNL Real-time Customer Profile] überlappende Attribute über Ihre Profil-Fragmente hinweg zusammenführt. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe.

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST an den `/segment/jobs`-Endpunkt in der [!DNL Real-time Customer Profile]-API anfordern.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Endpunkt [Segmentaufträge](../api/segment-jobs.md#create)


### Status des Segmentauftrags suchen

Sie können das `id` für einen bestimmten Segmentauftrag verwenden, um eine Suchanfrage (GET) auszuführen, um den aktuellen Auftragsstatus Ansicht.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Endpunkt [Segmentaufträge](../api/segment-jobs.md#get)

## Segmentergebnisse interpretieren

Wenn Segmentaufträge erfolgreich ausgeführt werden, wird die Zuordnung `segmentMembership` für jedes Profil im Segment aktualisiert. `segmentMembership` speichert auch alle vorab ausgewerteten Audiencen, die in eingegliedert werden,  [!DNL Platform]sodass eine Integration mit anderen Lösungen wie  [!DNL Adobe Audience Manager].

Das folgende Beispiel zeigt, wie das `segmentMembership`-Attribut für jeden einzelnen Profil-Datensatz aussieht:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `lastQualificationTime` | Der Zeitstempel, zu dem die Zusicherung der Segmentmitgliedschaft erfolgte und das Profil das Segment ein- oder ausstieg. |
| `status` | Der Status der Segmentbeteiligung als Teil der aktuellen Anforderung. muss einem der folgenden bekannten Werte entsprechen: <ul><li>`existing`: Die Entität befindet sich weiterhin im Segment.</li><li>`realized`: Entität tritt in das Segment ein.</li><li>`exited`: Entität beendet das Segment.</li></ul> |

## Zugriff auf Segmentergebnisse

Auf die Ergebnisse eines Segmentauftrags kann auf zwei Arten zugegriffen werden: Sie können auf einzelne Profil zugreifen oder eine ganze Audience in einen Datensatz exportieren.

Die folgenden Abschnitte beschreiben diese Optionen detaillierter.

## Profil nachschlagen

Wenn Sie das spezifische Profil kennen, auf das Sie zugreifen möchten, können Sie dies mit der API [!DNL Real-time Customer Profile] tun. Die vollständigen Schritte zum Zugriff auf einzelne Profil finden Sie im Lehrgang [Echtzeit-Kundendaten über das Profil-API](../../profile/api/entities.md) aufrufen.

## Segment {#export} exportieren

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des `status`-Attributs lautet „SUCCEEDED“ (GELUNGEN)), können Sie Ihre Zielgruppe in einen Datensatz exportieren. In diesem Datensatz ist die Zielgruppe zugänglich und bearbeitbar.

Die folgenden Schritte sind erforderlich, um Ihre Audience zu exportieren:

- [Erstellen Sie einen Dataset](#create-a-target-dataset)  der Zielgruppe: Erstellen Sie den Datensatz, der Audiencen enthält.
- [Generieren von Profilen zur Audience im Datensatz](#generate-profiles-for-audience-members) : Füllen Sie den Datensatz mit XDM Individuelle Profil basierend auf den Ergebnissen eines Segmentauftrags.
- [Überwachung des Exportfortschritts](#monitor-export-progress)  - Überprüfen Sie den aktuellen Fortschritt des Exportprozesses.
- [Lesen Sie die Daten](#next-steps)  zur Audience - Rufen Sie die XDM-Profil für einzelne Mitglieder Ihrer Audience ab.

### Zielgruppen-Dataset erstellen

Beim Exportieren einer Audience muss zunächst ein Zielgruppe-Datensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert wird, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Musteranforderung). Um ein Segment zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigung-Schema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas, die dieselbe Klasse besitzen, Aggregat gibt, in diesem Fall die XDM-Klasse Individuelles Profil. Weitere Informationen zu Schemas der Vereinigung Ansicht finden Sie im Abschnitt [Kundenkonto in Echtzeit im Schema Registry Developer Guide](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** Die in diesem Lernprogramm beschriebenen Schritte beschreiben, wie ein Datensatz erstellt wird, der auf die  [!DNL XDM Individual Profile Union Schema] Verwendung der  [!DNL Catalog] API verweist.
- **Verwenden der Benutzeroberfläche:** Um mithilfe der  [!DNL Adobe Experience Platform] Benutzeroberfläche einen Datensatz zu erstellen, der auf das Schema &quot;Vereinigung&quot;verweist, führen Sie die Schritte im  [UI-](../ui/overview.md) Lernprogramm aus und kehren Sie dann zu diesem Lernprogramm zurück, um die Schritte zum  [Generieren von Profilen](#generate-xdm-profiles-for-audience-members) für die Audience fortzusetzen.

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen ID kennen, können Sie direkt mit dem Schritt für [Generieren von Profilen der Audience](#generate-xdm-profiles-for-audience-members) fortfahren.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Datensatz erstellt, der Konfigurationsparameter in der Nutzlast bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein beschreibender Name für den Datensatz. |
| `schemaRef.id` | Die ID der Vereinigung-Ansicht (Schema), der der Datensatz zugeordnet werden soll. |
| `fileDescription.persisted` | Ein boolescher Wert, der bei Festlegung auf `true` den Datenbestand in der Ansicht &quot;Vereinigung&quot;beibehalten kann. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die schreibgeschützte, systemgenerierte eindeutige ID des neu erstellten Datensatzes enthält. Für den erfolgreichen Export von Audiencen-Mitgliedern ist eine ordnungsgemäß konfigurierte Dataset-ID erforderlich.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generieren von Profilen für Audiencen-Mitglieder {#generate-profiles}

Nachdem Sie über einen Datensatz mit Vereinigung-Speicherung verfügen, können Sie einen Exportauftrag erstellen, um die Audiencen im Datensatz zu erhalten, indem Sie eine POST an den `/export/jobs`-Endpunkt in der [!DNL Real-time Customer Profile]-API anfordern und die Datensatzkennnummer und Segmentinformationen für die zu exportierenden Segmente angeben.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im Endpunktleitfaden [Exportaufträge](../api/export-jobs.md#create)

### Überwachung des Exportfortschritts

Bei der Verarbeitung eines Exportauftrags können Sie dessen Status überwachen, indem Sie eine GET an den Endpunkt `/export/jobs` und das `id` des Exportauftrags im Pfad anfordern. Der Exportauftrag ist abgeschlossen, sobald das Feld `status` den Wert &quot;SUCCEEDED&quot;zurückgibt.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im Endpunktleitfaden [Exportaufträge](../api/export-jobs.md#get)

## Nächste Schritte

Nach erfolgreichem Abschluss des Exports sind Ihre Daten im Ordner [!DNL Data Lake] in [!DNL Experience Platform] verfügbar. Verwenden Sie dann [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml), um mit dem mit dem Export verknüpften `batchId` auf die Daten zuzugreifen. Je nach Größe des Segments können die Daten in Blöcken vorliegen und der Stapel kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Verwenden der [!DNL Data Access]-API zum Zugriff auf und Herunterladen von Stapeldateien finden Sie im [Lernprogramm zum Datenzugriff](../../data-access/tutorials/dataset-data.md).

Sie können auch mit [!DNL Adobe Experience Platform Query Service] auf erfolgreich exportierte Segmentdaten zugreifen. Mithilfe der Benutzeroberfläche oder RESTful-API können Sie [!DNL Query Service] Abfragen für Daten innerhalb von [!DNL Data Lake] schreiben, überprüfen und ausführen.

Weitere Informationen zur Abfrage von Audiencen finden Sie in der Dokumentation zu [[!DNL Query Service]](../../query-service/home.md).
