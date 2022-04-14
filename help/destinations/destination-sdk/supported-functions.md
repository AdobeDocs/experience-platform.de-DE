---
description: Die Destination SDK der Experience Platform verwendet Blasen-Vorlagen, mit denen Sie die aus der Experience Platform exportierten Daten in das für Ihr Ziel erforderliche Format umwandeln können.
title: Unterstützte Umwandlungsfunktionen in Destination SDK
source-git-commit: 840404741da06ba1593b227c7d6ba459b5f43110
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 6%

---

# Unterstützte Umwandlungsfunktionen in Destination SDK

## Übersicht {#overview}

Verwendung von Experience Platform Destination SDK [[!DNL Pebble] templates](https://pebbletemplates.io/), sodass Sie die aus Experience Platform exportierten Daten in das für Ihr Ziel erforderliche Format umwandeln können.

Die Experience Platform [!DNL Pebble] Die Implementierung hat einige Änderungen gegenüber der nativen Version, die von [!DNL Pebble]. Zusätzlich zu den vordefinierten Funktionen von [!DNL Pebble], hat Adobe einige zusätzliche Funktionen erstellt, die Sie mit Destination SDK verwenden können.

## Verwendungsbereiche {#where-to-use}

Verwenden Sie die unten aufgeführten unterstützten Funktionen auf dieser Seite, wenn Sie [Erstellen einer Nachrichtenumwandlungsvorlage](./create-template.md) für die Daten, die aus der Experience Platform an Ihr Ziel exportiert wurden. Die Umwandlungsvorlage der Nachricht wird im [Zielserverkonfiguration](./server-and-template-configuration.md) für Streaming-Ziele.

## Voraussetzungen {#prerequisites}

Die Konzepte und Funktionen dieser Referenzseite werden im Abschnitt [Nachrichtenformat](/help/destinations/destination-sdk/message-format.md) Dokument zuerst. Sie müssen die [Profilstruktur](/help/destinations/destination-sdk/message-format.md#profile-structure) in der Experience Platform, bevor Sie [!DNL Pebble] Vorlagen, die umgewandelt und exportiert werden sollen.

Bevor Sie zu den unten dokumentierten Funktionen übergehen, lesen Sie die Beispielvorlagen im Abschnitt . [Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten](/help/destinations/destination-sdk/message-format.md#using-templating). Die Beispiele dort beginnen sehr einfach und erhöhen die Komplexität.

## Unterstützt [!DNL Pebble] Funktionen {#supported-functions}

Aus dem [!DNL Pebble] Tags-Abschnitt, Destination SDK unterstützt nur:
* [Filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [festgelegt](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Verwenden `for` unterscheidet sich bei der Iteration durch *array* oder *map* Elemente in einer Vorlage. Wenn Sie durch ein Array navigieren, können Sie das Element direkt abrufen. Wenn Sie durch eine Karte navigieren, erhalten Sie jeden Map-Eintrag, der über ein Schlüssel-Wert-Paar verfügt.
>
> * Betrachten Sie zum Beispiel die Identitäten in einem Array-Element [identityMap](./message-format.md#identities) Namespace, in dem Sie Elemente wie `identityMap.gaid`, `identityMap.email`oder Ähnliches.
> * Beispiel für ein Zuordnungselement: [segmentMembership](./message-format.md#segment-membership).


Aus dem [!DNL Pebble] Filterabschnitt, unterstützt Destination SDK alle Funktionen. Ein Beispiel weiter unten zeigt, wie die `date` -Funktion in Destination SDK verwendet werden.

Aus dem [!DNL Pebble] Funktionsabschnitt, die Adobe *not* unterstützen [Bereich](https://pebbletemplates.io/wiki/function/range/) -Funktion.

## Beispiel für die `date` -Funktion verwendet wird {#date-function}

So veranschaulichen Sie die [!DNL Pebble] -Funktionen in Destination SDK verwendet werden, sehen Sie unten, wie die Datumsfunktion ([Link in der Dokumentation zu Pebble](https://pebbletemplates.io/wiki/filter/date/)) wird verwendet, um das Format eines Zeitstempels zu transformieren.

### Anwendungsfall

Sie möchten die `lastQualificationTime` Zeitstempel vom Standard [ISO 8601](https://de.wikipedia.org/wiki/ISO_8601) -Wert, den die Experience Platform in einen anderen von Ihrem Ziel bevorzugten Wert exportiert.

### Beispiel

#### Eingabe

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Format

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Ausgabe

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Von der Adobe hinzugefügte Funktionen {#functions-added-by-adobe}

Zusätzlich zu den vordefinierten Funktionen von [!DNL Pebble], sehen Sie unten die zusätzlichen Funktionen, die von Adobe erstellt wurden und die Sie für Ihre Datenexporte verwenden können.

### `addedSegments` und `removedSegments` Funktionen {#addedsegments-removedsegments-functions}

#### Anwendungsfall

Diese Funktionen können verwendet werden, um eine Liste von Segmenten zu erhalten, die einem Profil hinzugefügt oder daraus entfernt wurden.

#### Beispiel

##### Eingabe

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Ausgabe

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## Nächste Schritte {#next-steps}

Sie wissen jetzt, [!DNL Pebble] -Funktionen werden in Destination SDK unterstützt und es wird beschrieben, wie Sie sie verwenden, um das Format der exportierten Daten an Ihre Anforderungen anzupassen. Als Nächstes sollten Sie die folgenden Seiten lesen:

* [Erstellen und Testen einer Nachrichten-Umwandlungsvorlage](/help/destinations/destination-sdk/create-template.md)
* [API-Vorgänge für Rendervorlagen](/help/destinations/destination-sdk/render-template-api.md)