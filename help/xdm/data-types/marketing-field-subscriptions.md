---
solution: Experience Platform
title: Allgemeines Feld für Marketingpräferenzen mit Abonnement-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über das Feld "Allgemeine Marketingvorgabe"mit dem XDM-Datentyp von Abonnements.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# [!UICONTROL Allgemeines Feld für Marketingpräferenzen mit ] Abonnementdatentyp

[!UICONTROL Generisches Feld für Marketingpräferenzen mit ] Abonnement ist ein Standard-XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Marketingvorgabe beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll dazu verwendet werden, die Struktur der Schema für die Zustimmung Ihres Unternehmens mithilfe der Feldgruppe [[!UICONTROL Datenschutz/Personalisierung/Marketing-Voreinstellungen (Zusätze)] als Grundlage anzupassen.](../field-groups/profile/consents.md)
>
>Wenn Sie keine `subscriptions`-Zuordnung für ein bestimmtes Feld mit Marketingpräferenzen benötigen, können Sie stattdessen den Datentyp [des grundlegenden Marketingfelds](./marketing-field.md) verwenden.

![](../images/data-types/marketing-field-subscriptions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `reason` | Zeichenfolge | Wenn ein Kunde sich aus einer Marketing-Verwendungsszenario ausschließt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |
| `subscriptions` | Zuordnung | Eine Übersicht der Kundenmarketing-Voreinstellungen für bestimmte Abonnement. Weitere Informationen finden Sie im Abschnitt [Abonnement](#subscriptions). |
| `time` | DateTime | Ein Zeitstempel nach ISO 8601, der angibt, wann sich die Marketing-Voreinstellung geändert hat (falls zutreffend). |
| `val` | Zeichenfolge | Die vom Kunden angebotene Voreinstellungsoption für diesen Marketing-Verwendungsfall. Akzeptierte Werte und Definitionen finden Sie im Abschnitt [Nächster Abschnitt](#val). |

## `val` {#val}

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja | Der Kunde hat sich für die Präferenz entschieden. Mit anderen Worten, sie stimmen der Verwendung ihrer Daten gemäß der jeweiligen Präferenz zu.**** |
| `n` | Nein | Der Kunde hat sich gegen die Präferenz entschieden. Mit anderen Worten, sie **stimmen der Verwendung ihrer Daten nicht** zu, wie in der betreffenden Präferenz angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Präferenzwert erhalten. Dies wird meistens im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Empfang von E-Mails entscheidet, wird diese Zustimmung auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um sicherzustellen, dass er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf `y` aktualisiert.<br><br>Verwendet diese Voreinstellung keinen zweistufigen Überprüfungsprozess, kann stattdessen die  `p` Auswahl verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Aufforderung zur Einwilligung reagiert hat. Beispielsweise können Sie den Wert auf der ersten Seite einer Website automatisch auf `p` einstellen, bevor der Kunde auf die Aufforderung zur Einwilligung reagiert hat. In Gerichtsbarkeiten, die keine ausdrückliche Zustimmung erfordern, können Sie diese auch verwenden, um anzugeben, dass der Kunde sich nicht explizit abgemeldet hat (d. h. die Zustimmung wird angenommen). |
| `u` | „Unbekannt“ | Die Angaben zum Kundenwunsch sind unbekannt. |
| `LI` | Rechtliches Interesse | Das legitime Geschäftsinteresse, diese Daten für den angegebenen Zweck zu erheben und zu verarbeiten, überwiegt den potenziellen Schaden, den sie dem Einzelnen verursachen. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertraglichen Verpflichtungen mit der Einzelperson nachzukommen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wesentliches Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist zum Schutz der vitalen Interessen des Einzelnen erforderlich. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten zu dem festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt durchzuführen. |

## `subscriptions` {#subscriptions}

Einige Unternehmen ermöglichen es Kunden, für verschiedene Abonnement zu Opt-in, die mit einem bestimmten Marketing-Kanal verbunden sind. Eine Bankverbindung könnte es Kunden beispielsweise ermöglichen, Telefonwarnungen für überzogene Programme zu abonnieren oder Verkaufsanrufe für treue Firma-Angebote zu empfangen.

Die folgende JSON-Datei stellt ein Beispielmarketingfeld für einen Telefonanruf-Marketing-Kanal dar, der eine `subscriptions`-Zuordnung enthält. Jeder Schlüssel im `subscriptions`-Objekt stellt ein einzelnes Abonnement für den Marketing-Kanal dar. Jedes Abonnement enthält wiederum einen Abmeldewert (`val`).

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Der Abonnement-Typ. Hierbei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, vorausgesetzt, diese darf nicht länger als 15 Zeichen sein. |
| `subscribers` | Ein optionales Kartenfeld, das einen Satz von Bezeichnern (wie E-Mail-Adressen oder Telefonnummern) darstellt, die ein bestimmtes Abonnement abonniert haben. Jeder Schlüssel in diesem Objekt stellt den betreffenden Bezeichner dar und enthält zwei Untereigenschaften: <ul><li>`time`: Ein ISO 8601-Zeitstempel zum Zeitpunkt des Abonnements der Identität, falls zutreffend.</li><li>`source`: Die Quelle, von der der Abonnent stammt. Hierbei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, vorausgesetzt, diese darf nicht länger als 15 Zeichen sein.</li></ul> |

## Zusätzliche Ressourcen

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
