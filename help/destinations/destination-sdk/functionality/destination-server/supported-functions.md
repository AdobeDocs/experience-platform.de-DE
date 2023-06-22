---
description: Das Destination SDK von Experience Platform verwendet Pebble-Vorlagen, mit denen Sie die aus Experience Platform exportierten Daten in das für Ihr Ziel erforderliche Format umwandeln können.
title: Unterstützte Umwandlungsfunktionen in Destination SDK
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: ht
source-wordcount: '579'
ht-degree: 100%

---


# Unterstützte Umwandlungsfunktionen in Destination SDK

Das Destination SDK von Experience Platform verwendet [[!DNL Pebble] -Vorlagen](https://pebbletemplates.io/), womit Sie die aus Experience Platform exportierten Daten in das für Ihr Ziel erforderliche Format umwandeln können.

Die [!DNL Pebble] -Implementierung in Experience Platform hat einige Änderungen gegenüber der nativen Version, die von [!DNL Pebble] bereitgestellt wird. Zusätzlich zu den vordefinierten Funktionen von [!DNL Pebble] hat Adobe einige zusätzliche Funktionen erstellt, die Sie mit Destination SDK verwenden können.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Verwendungsbereiche {#where-to-use}

Verwenden Sie die unten aufgeführten unterstützten Funktionen auf dieser Seite, wenn Sie für die Daten, die aus Experience Platform an Ihr Ziel exportiert wurden, [eine Nachrichtenumwandlungsvorlage erstellen ](../../testing-api/streaming-destinations/create-template.md).

Die Nachrichtenumwandlungsvorlage wird in der [Ziel-Server-Konfiguration](templating-specs.md) für Streaming-Ziele verwendet.

## Voraussetzungen {#prerequisites}

Um die Konzepte und Funktionen auf dieser Referenzseite zu verstehen, lesen Sie zunächst das Dokument zum [Nachrichtenformat](message-format.md). Sie müssen die [Profilstruktur](message-format.md#profile-structure) in Experience Platform verstehen, bevor Sie [!DNL Pebble]-Vorlagen zur Transformation der exportierten Daten verwenden können.

Bevor Sie zu den unten dokumentierten Funktionen übergehen, sehen Sie sich die Beispielvorlagen im Abschnitt [Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten](message-format.md#using-templating) an. Die Beispiele dort beginnen sehr einfach und werden immer komplexer.

## Unterstützte [!DNL Pebble]-Funktionen {#supported-functions}

Aus dem [!DNL Pebble]-Tags-Abschnitt unterstützt Destination SDK nur:

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Die Verwendung von `for` unterscheidet sich bei der Iteration durch *Array*- oder *Zuordnungs*-Elemente in einer Vorlage. Wenn Sie durch ein Array navigieren, können Sie das Element direkt abrufen. Wenn Sie durch eine Zuordnung (Map) navigieren, erhalten Sie jeden Map-Eintrag, der über ein Schlüssel-Wert-Paar verfügt.
>
> * Betrachten Sie zum Beispiel für ein Array-Element die Identitäten in einem [identityMap](message-format.md#identities)-Namespace, in dem Sie durch Elemente wie `identityMap.gaid`, `identityMap.email` oder Ähnliches iterieren können.
> * Nehmen Sie als Beispiel für ein Zuordnungselement [segmentMembership](message-format.md#segment-membership).

Aus dem Abschnitt der [!DNL Pebble]-Filter unterstützt Destination SDK alle Funktionen. Ein Beispiel weiter unten zeigt, wie die Funktion `date` in Destination SDK verwendet werden kann.

Aus dem [!DNL Pebble]-Funktionsabschnitt unterstützt Adobe *nicht* die Funktion [ range](https://pebbletemplates.io/wiki/function/range/).

## Beispiel für die Verwendung der Funktion `date` {#date-function}

Um zu veranschaulichen, wie die [!DNL Pebble]-Funktionen in Destination SDK verwendet werden, sehen Sie unten, wie die Datumsfunktion ([Link in der Pebble-Dokumentation](https://pebbletemplates.io/wiki/filter/date/)) verwendet wird, um das Format eines Zeitstempels zu transformieren.

### Anwendungsfall

Sie möchten den `lastQualificationTime` Zeitstempel vom Standard-[ISO 8601](https://de.wikipedia.org/wiki/ISO_8601)-Wert, den Experience Platform exportiert, in einen anderen von Ihrem Ziel bevorzugten Wert ändern.

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

## Von Adobe hinzugefügte Funktionen {#functions-added-by-adobe}

Zusätzlich zu den vordefinierten Funktionen von [!DNL Pebble] sehen Sie unten die zusätzlichen Funktionen, die von Adobe erstellt wurden und die Sie für Ihre Datenexporte verwenden können.

### Funktionen `addedSegments` und `removedSegments` {#addedsegments-removedsegments-functions}

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

Sie wissen jetzt, welche [!DNL Pebble] -Funktionen in Destination SDK unterstützt werden und wie Sie sie verwenden können, um das Format der exportierten Daten an Ihre Anforderungen anzupassen. Als Nächstes sollten Sie die folgenden Seiten lesen:

* [Erstellen und Testen einer Nachrichtenumwandlungsvorlage](../../testing-api/streaming-destinations/create-template.md)
* [API-Vorgänge für Rendervorlagen](../../testing-api/streaming-destinations/render-template-api.md)
