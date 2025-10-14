---
solution: Experience Platform
title: Generisches Feld für Marketing-Voreinstellungen mit Datentyp Abonnements
description: Erfahren Sie mehr über das Feld „Allgemeine Marketing-Voreinstellungen“ mit dem Datentyp XDM-Abonnements .
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# [!UICONTROL &#x200B; Datentyp „Generisches Feld für Marketing-Voreinstellungen &#x200B;] Abonnements“

[!UICONTROL Generisches Feld für Marketing-Voreinstellungen mit Abonnements] ist ein standardmäßiger XDM-Datentyp, der die Auswahl einer Kundin oder eines Kunden für eine bestimmte Marketing-Voreinstellung beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll verwendet werden, um die Struktur der Einverständnisschemata Ihres Unternehmens mithilfe der Feldergruppe [[!UICONTROL Einverständnisse und Voreinstellungen] als &#x200B;](../field-groups/profile/consents.md) anzupassen.
>
>Wenn Sie für ein bestimmtes Marketing-Präferenzfeld keine `subscriptions` benötigen, können Sie stattdessen den Datentyp [Einfaches Marketing-Feld](./marketing-field.md) verwenden.

![](../images/data-types/marketing-field-subscriptions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `reason` | Zeichenfolge | Wenn ein Kunde sich von einem Marketing-Anwendungsfall abmeldet, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |
| `subscriptions` | Zuordnung | Eine Karte der Marketing-Voreinstellungen von Kunden für bestimmte Abonnements. Weitere Informationen finden Sie im Abschnitt [Abonnements](#subscriptions) . |
| `time` | DateTime | Ein ISO 8601-Zeitstempel, der angibt, wann sich die Marketing-Voreinstellung geändert hat, falls zutreffend. |
| `val` | String | Die vom Kunden bereitgestellte Präferenzauswahl für diesen Marketing-Anwendungsfall. Siehe [nächster Abschnitt](#val) für gültige Werte und Definitionen. |

{style="table-layout:auto"}

## `val` {#val}

In der folgenden Tabelle sind die akzeptierten Werte für `val` aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja (Opt-in) | Der Kunde hat sich für die Voreinstellung entschieden. Mit anderen Worten, sie **nicht** der Verwendung ihrer Daten, wie in der betreffenden Präferenz angegeben. |
| `n` | Nein (Opt-out) | Der Kunde hat die Voreinstellung abgelehnt. Mit anderen Worten, sie **(nicht** der Verwendung ihrer Daten, wie in der betreffenden Präferenz angegeben. |
| `p` | Überprüfung ausstehend | Das System hat noch keinen endgültigen Präferenzwert erhalten. Dies wird am häufigsten im Rahmen einer Einwilligung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird dieses Einverständnis auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Ab diesem Zeitpunkt wird das Einverständnis auf `y` aktualisiert.<br><br>Wenn diese Voreinstellung keinen zweistufigen Verifizierungsprozess verwendet, kann stattdessen die `p` verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einverständnisaufforderung reagiert hat. Beispielsweise können Sie den Wert auf der ersten Seite einer Website automatisch auf `p` setzen, bevor der Kunde auf die Einverständnisaufforderung reagiert hat. In Rechtssystemen, die keine ausdrückliche Zustimmung erfordern, können Sie diese auch verwenden, um anzugeben, dass der Kunde nicht explizit widersprochen hat (mit anderen Worten, eine Zustimmung wird vorausgesetzt). |
| `u` | Unbekannt | Die Präferenzinformationen des Kunden sind unbekannt. |
| `dy` | Standard von „Ja“ (Opt-in) | Der Kunde hat selbst keinen Einverständniswert angegeben und wird standardmäßig als Opt-in („Ja„) behandelt. Mit anderen Worten wird die Einwilligung so lange vorausgesetzt, bis der Kunde etwas Anderes angibt.<br><br>Beachten Sie, dass Sie, wenn Gesetze oder Änderungen an den Datenschutzrichtlinien Ihres Unternehmens zu Änderungen an den Standardwerten einiger oder aller Benutzer führen, alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen. |
| `dn` | Standard von „Nein“ (Opt-out) | Der Kunde hat selbst keinen Einverständniswert angegeben und wird standardmäßig als Opt-out („Nein„) behandelt. Mit anderen Worten wird davon ausgegangen, dass der Kunde seine Zustimmung verweigert hat, bis er etwas Anderes angibt.<br><br>Beachten Sie, dass Sie, wenn Gesetze oder Änderungen an den Datenschutzrichtlinien Ihres Unternehmens zu Änderungen an den Standardwerten einiger oder aller Benutzer führen, alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen. |
| `LI` | berechtigtes Interesse | Das berechtigte geschäftliche Interesse an der Erhebung und Verarbeitung dieser Daten für den angegebenen Zweck überwiegt den potenziellen Schaden, den sie für den Einzelnen darstellen. |
| `CT` | Vertrag | Die Erhebung von Daten für den genannten Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Lebensnotwendiges Interesse des Einzelnen | Die Erhebung von Daten für den genannten Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | öffentliches Interesse | Die Erhebung von Daten für den genannten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

Einige Unternehmen ermöglichen es Kunden, sich für verschiedene Abonnements zu registrieren, die mit einem bestimmten Marketing-Kanal verbunden sind. Beispielsweise kann eine Bankgesellschaft ihren Kunden erlauben, telefonische Benachrichtigungen für überzogene Konten zu abonnieren oder Verkaufsanrufe für Treueprogramm-Angebote zu erhalten.

Die folgende JSON-Datei enthält ein Beispiel für ein Marketing-Feld für einen Telefonanruf-Marketing-Kanal mit einer `subscriptions`. Jeder Schlüssel im `subscriptions`-Objekt stellt ein individuelles Abonnement für den Marketing-Kanal dar. Jedes Abonnement enthält einen Opt-in-Wert (`val`).

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
| `val` | Der [Einverständniswert](#val) für das Abonnement. |
| `type` | Der Abonnementtyp. Dabei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, sofern sie maximal 15 Zeichen umfasst. |
| `topics` | Ein Array von Zeichenfolgen, die die Interessenbereiche darstellen, die eine Kundin oder ein Kunde abonniert hat und die zum Senden relevanter Inhalte verwendet werden können. |
| `subscribers` | Ein optionales Feld vom Typ Zuordnung , das für einen Satz von Kennungen (z. B. E-Mail-Adressen oder Telefonnummern) steht, die sich für ein bestimmtes Abonnement angemeldet haben. Jeder Schlüssel in diesem Objekt stellt die betreffende Kennung dar und enthält zwei Untereigenschaften: <ul><li>`time`: Ein ISO 8601-Zeitstempel, der angibt, wann sich die Identität angemeldet hat, falls zutreffend.</li><li>`source`: Die Quelle, aus der der Abonnent stammt. Dabei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, sofern sie maximal 15 Zeichen umfasst.</li></ul> |

{style="table-layout:auto"}

## Zusätzliche Ressourcen

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
