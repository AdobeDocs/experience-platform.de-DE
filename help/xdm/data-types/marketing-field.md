---
solution: Experience Platform
title: Datentyp für generische Marketing-Voreinstellungsfelder
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp des generischen Marketing-Voreinstellungsfelds.
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 3%

---

# [!UICONTROL Generischer Marketing-] Voreinstellungs-Felddatentyp

[!UICONTROL Generische Marketing-Voreinstellungsfelder ] sind ein standardmäßiger XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Marketing-Voreinstellung beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll verwendet werden, um die Struktur der Einwilligungsschemas Ihres Unternehmens mithilfe der Feldergruppe [[!UICONTROL Datenschutz/Personalisierung/Marketing-Voreinstellungen (Einverständnisse)]](../field-groups/profile/consents.md) als Grundlinie anzupassen.
>
>Wenn Sie eine `subscriptions`-Zuordnung für ein bestimmtes Marketing-Präferenzfeld benötigen, müssen Sie stattdessen das Marketing-Feld [mit dem Abonnementdatentyp](./marketing-field-subscriptions.md) verwenden.

![](../images/data-types/marketing-field.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `reason` | Zeichenfolge | Wenn ein Kunde einen Marketing-Anwendungsfall ablehnt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |
| `time` | DateTime | Ein ISO 8601-Zeitstempel, mit dem die Marketing-Voreinstellung geändert wurde (falls zutreffend). |
| `val` | Zeichenfolge | Die vom Kunden bereitgestellte bevorzugte Auswahl für diesen Marketing-Anwendungsfall. Die nachstehende Tabelle enthält akzeptierte Werte und Definitionen. |

{style=&quot;table-layout:auto&quot;}

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja | Der Kunde hat sich für die Präferenz entschieden. Mit anderen Worten, sie stimmen **do** der Verwendung ihrer Daten zu, wie durch die betreffende Voreinstellung angegeben. |
| `n` | Nein | Der Kunde hat sich gegen die Präferenz entschieden. Mit anderen Worten, sie **stimmen nicht** der Verwendung ihrer Daten zu, wie durch die betreffende Voreinstellung angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Präferenzwert erhalten. Dies wird meist im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird diese Zustimmung auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf `y` aktualisiert.<br><br>Wenn diese Voreinstellung keinen zweistufigen Überprüfungsprozess verwendet, kann die  `p` Auswahl stattdessen verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einwilligungsaufforderung reagiert hat. Sie können beispielsweise den Wert auf `p` automatisch auf der ersten Seite einer Website festlegen, bevor der Kunde auf die Einverständnisaufforderung reagiert hat. In Rechtsordnungen, die keine ausdrückliche Zustimmung erfordern, können Sie damit auch angeben, dass der Kunde sich nicht ausdrücklich abgemeldet hat (d. h., die Zustimmung wird angenommen). |
| `u` | „Unbekannt“ | Die Präferenzinformationen des Kunden sind unbekannt. |
| `LI` | Rechtliches Interesse | Das berechtigte geschäftliche Interesse, diese Daten für den angegebenen Zweck zu sammeln und zu verarbeiten, überwiegt den potenziellen Schaden, den sie für die Person darstellt. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wichtiges Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten für den festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
