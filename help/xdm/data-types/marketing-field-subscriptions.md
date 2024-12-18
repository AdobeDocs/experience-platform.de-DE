---
solution: Experience Platform
title: Feld für allgemeine Marketing-Voreinstellungen mit Abonnementdatentyp
description: Erfahren Sie mehr über das Feld "Allgemeine Marketing-Voreinstellung"mit dem XDM-Datentyp Abonnements.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# [!UICONTROL Generisches Marketing-Präferenzfeld mit Abonnements]-Datentyp

[!UICONTROL Generisches Feld für Marketing-Voreinstellungen mit Abonnements] ist ein standardmäßiger XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Marketing-Voreinstellung beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll verwendet werden, um die Struktur der Einwilligungsschemas Ihres Unternehmens mithilfe der Feldergruppe [[!UICONTROL Einverständnisse und Voreinstellungen]](../field-groups/profile/consents.md) als Grundlage anzupassen.
>
>Wenn Sie keine `subscriptions` -Zuordnung für ein bestimmtes Marketing-Voreinstellungsfeld benötigen, können Sie stattdessen den [grundlegenden Marketing-Felddatentyp](./marketing-field.md) verwenden.

![](../images/data-types/marketing-field-subscriptions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `reason` | Zeichenfolge | Wenn ein Kunde einen Marketing-Anwendungsfall ablehnt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |
| `subscriptions` | Zuordnung | Eine Karte der Marketing-Voreinstellungen von Kunden für bestimmte Abonnements. Weitere Informationen finden Sie im Abschnitt zu [Abonnements](#subscriptions) . |
| `time` | DateTime | Ein ISO 8601-Zeitstempel, mit dem die Marketing-Voreinstellung geändert wurde (falls zutreffend). |
| `val` | Zeichenfolge | Die vom Kunden bereitgestellte Voreinstellungsoption für diesen Marketing-Anwendungsfall. Akzeptierte Werte und Definitionen finden Sie im Abschnitt [nächster Abschnitt](#val) . |

{style="table-layout:auto"}

## `val` {#val}

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja (Opt-in) | Der Kunde hat sich für die Präferenz entschieden. Mit anderen Worten, sie stimmen **do** der Verwendung ihrer Daten zu, wie durch die betreffende Voreinstellung angegeben. |
| `n` | Nein (Opt-out) | Der Kunde hat sich von der Präferenz abgemeldet. Mit anderen Worten, sie stimmen **nicht** der Verwendung ihrer Daten zu, wie durch die betreffende Voreinstellung angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Präferenzwert erhalten. Dies wird meist im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird diese Zustimmung auf &quot;`p`&quot;gesetzt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf &quot;`y`&quot;aktualisiert.<br><br>Wenn diese Voreinstellung keinen zweistufigen Überprüfungsprozess verwendet, kann stattdessen die Option `p` verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einverständnisaufforderung reagiert hat. Sie können beispielsweise den Wert auf der ersten Seite einer Website automatisch auf &quot;`p`&quot;setzen, bevor der Kunde auf die Einwilligungsaufforderung reagiert hat. In Rechtsordnungen, die keine ausdrückliche Zustimmung erfordern, können Sie damit auch angeben, dass der Kunde sich nicht ausdrücklich abgemeldet hat (d. h., die Zustimmung wird angenommen). |
| `u` | Unbekannt | Die Präferenzinformationen des Kunden sind unbekannt. |
| `dy` | Standardwert Ja (Opt-in) | Der Kunde hat selbst keinen Zustimmungswert angegeben und wird standardmäßig als Opt-in (&quot;Ja&quot;) behandelt. Mit anderen Worten, die Zustimmung wird angenommen, bis der Kunde etwas Anderes angibt.<br><br>Beachten Sie, dass Sie alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen, wenn die Datenschutzrichtlinien Ihres Unternehmens Änderungen an den Standardeinstellungen einiger oder aller Benutzer zur Folge haben. |
| `dn` | Standardwert Nein (Opt-out) | Der Kunde hat selbst keinen Zustimmungswert angegeben und wird standardmäßig als Opt-out (&quot;Nein&quot;) behandelt. Mit anderen Worten, es wird angenommen, dass der Kunde die Zustimmung verweigert hat, bis er etwas Anderes angibt.<br><br>Beachten Sie, dass Sie alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen, wenn die Datenschutzrichtlinien Ihres Unternehmens Änderungen an den Standardeinstellungen einiger oder aller Benutzer zur Folge haben. |
| `LI` | Rechtliches Interesse | Das berechtigte geschäftliche Interesse, diese Daten für den angegebenen Zweck zu sammeln und zu verarbeiten, überwiegt den potenziellen Schaden, den sie für die Person darstellt. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wichtiges Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten für den festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

Einige Unternehmen ermöglichen es Kunden, sich für verschiedene Abonnements zu entscheiden, die mit einem bestimmten Marketing-Kanal verknüpft sind. Ein Bankunternehmen kann beispielsweise Kunden gestatten, Telefonwarnungen für überzogene Konten zu abonnieren oder Verkaufsanrufe für Treueprogramm-Angebote zu erhalten.

Die folgende JSON-Datei stellt ein Beispiel-Marketing-Feld für einen Marketing-Kanal für Telefonanrufe dar, der eine `subscriptions` -Zuordnung enthält. Jeder Schlüssel im `subscriptions` -Objekt stellt ein individuelles Abonnement für den Marketing-Kanal dar. Jedes Abonnement enthält wiederum einen Opt-in-Wert (`val`).

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
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
| `val` | Der [Zustimmungswert](#val) für das Abonnement. |
| `type` | Der Abonnementtyp. Dabei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, sofern diese 15 Zeichen oder weniger umfasst. |
| `topics` | Ein Array von Zeichenfolgen, die die Interessensgebiete darstellen, die ein Kunde abonniert hat und die zum Senden relevanter Inhalte verwendet werden können. |
| `subscribers` | Ein optionales Feld vom Typ Zuordnung , das eine Reihe von Kennungen (wie E-Mail-Adressen oder Telefonnummern) darstellt, die ein bestimmtes Abonnement abonniert haben. Jeder Schlüssel in diesem Objekt stellt die betreffende Kennung dar und enthält zwei Untereigenschaften: <ul><li>`time`: Ein ISO 8601-Zeitstempel, der angibt, wann die Identität abonniert hat (falls zutreffend).</li><li>`source`: Die Quelle, von der der Abonnent stammt. Dabei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, sofern diese 15 Zeichen oder weniger umfasst.</li></ul> |

{style="table-layout:auto"}

## Zusätzliche Ressourcen

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
