---
title: AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresseneinstellung für Streaming-Aufnahme-API
description: Erfahren Sie, wie Sie den Zugriff auf die Streaming-Aufnahme-API sichern, indem Sie durch Zulassungsauflistung nur bestimmte IP-Adressen zulassen. In diesem Handbuch wird beschrieben, wie Sie IP-Adressbasierte Einschränkungen für die API-Sicherheit einrichten, aktivieren und verwalten.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 3%

---

# AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresseneinstellung für Streaming-Aufnahme-API

>[!AVAILABILITY]
>
>Auf die Zulassungsliste setzen Die Unterstützung für die IP-Adressverwaltung für die Streaming-Aufnahme-API befindet sich in der Beta-Phase und Ihre Organisation hat möglicherweise noch keinen Zugriff darauf. Die Funktionalität und Dokumentation können sich ändern.

Auf die Zulassungsliste setzen Sie können jetzt IP-Adressen für die Streaming-Aufnahme-API ändern. Verwenden Sie diese Funktion, um Ihre Aufnahme-Endpunkte zu schützen, indem Sie den Zugriff nur auf die von Ihnen angegebenen IP-Adressen beschränken.

## Auf die Zulassungsliste setzen Funktionsweise der IP-Adressverwaltung

Die IP-Zulassungsauflistung funktioniert wie folgt:

1. **Übermittlungs-IP-Adressen** Sie geben eine Liste vertrauenswürdiger IP-Adressen an, die Ihren Sandboxes zugeordnet sind.
2. **Konfiguration:** Adobe auf die Zulassungsliste setzen konfiguriert die auf Organisations- und Sandbox-Ebene für Ihr Unternehmen.
3. **Durchsetzung:** eingehenden Anfragen werden anhand Ihrer angegebenen Zulassungsliste ausgewertet:
   * Wenn die IP-Adresse mit Ihrer -Zulassungsliste übereinstimmt, wird die Anfrage normal verarbeitet.
   * Wenn sich die IP-Adresse nicht auf der -Zulassungsliste befindet, wird die Anfrage blockiert und ein HTTP 403-Fehler wird ohne Antworttext empfangen.

## Wichtige Aspekte

* Die Funktion zur Zulassungsauflistung von IP-Adressen gilt nur für die [Streaming-Aufnahme](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)-API (`dcs.adobedc.net`) und **nicht** für `server.adobedc.net` oder `edge.adobedc.net`.
* Neue Sandboxes sind standardmäßig geöffnet, bis die Zulassungsauflistung aktiviert ist.
* Wenn Sie eine Sandbox aus der Zulassungsliste entfernen, wird sie erneut im Internet geöffnet.
* Auf die Zulassungsliste setzen Sie müssen die vollständige Liste der Zuordnungen von Sandboxes zu IP-Adressen auf Ihrer Seite beibehalten und immer die vollständige Liste im Formular zur IP-Adressenzuordnung senden. Inkrementelle Aktualisierungen werden nicht unterstützt.

## Auf die Zulassungsliste setzen IP-Adresseneinstellung aktivieren

Auf die Zulassungsliste setzen Gehen Sie wie folgt vor, um die IP-Adressverwaltung für Ihr Unternehmen zu aktivieren:

1. Auf die Zulassungsliste setzen Laden Sie das [IP-Adressformular](../images/assets/ip_allowlisting_aep.xlsx.zip) herunter und füllen Sie es aus.
2. Öffnen Sie ein Support-Ticket und melden Sie den Betreff als **AEP Auf die Zulassungsliste setzen DCS- und Streaming-Aufnahme - IP-Anfrage** an. Fügen Sie diesem Ticket das ausgefüllte Formular hinzu.
3. Nachdem Sie Ihr Ticket gesendet haben, leitet die Adobe-Kundenunterstützung Ihre Anfrage an das Engineering weiter.
4. Techniker aktivieren die Zulassungsauflistung und bestätigen die Einrichtung.
5. Anschließend validieren Sie den Zugriff und bestätigen ihn mithilfe des Support-Tickets.

| Organisation | Sandbox-Name | Zulässige IP-Adressen |
| --- | --- | --- |
| KUPPEL | prod | 203.0.113.42, 198.51.100.25, 192.0.2.10 |
| KUPPEL | Entw. | 203.0.113.43, 198.51.100.26, 192.0.2.11 |
| LUMA | prod | 203.0.113.46, 198.51.100.29, 192.0.2.14 |

## Häufig gestellte Fragen

Im Folgenden finden Sie Antworten auf häufig gestellte Fragen zur Zulassungsauflistung von IP-Adressen für die Streaming-Aufnahme-API.

### Welche APIs werden behandelt?

Nur die `dcs.adobedc.net` Streaming-Aufnahme-API-Endpunkte.

## Was passiert, wenn meine Anfrage von einer nicht aufgelisteten IP-Adresse stammt?

Sie ist mit einem HTTP 403-Fehler blockiert.

### Sind neue Sandboxes automatisch geschützt?

Nein. Sie sind geöffnet, bis Sie über das Formular zur Zulassungsauflistung IP-Adresszuordnungen angeben.

### Kann ich nur aktualisierte IP-Adressen senden, wenn sich meine Zulassungsliste ändert?

Nein. Sie müssen immer die vollständige Liste der Sandbox- und IP-Adresszuordnungen senden. Teilweise (inkrementelle) Aktualisierungen werden nicht akzeptiert.