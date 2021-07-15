---
solution: Experience Platform
title: Generischer Datentyp für Einverständnisfelder
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Generisches Einverständnisfeld".
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 3%

---

# [!UICONTROL Generischer ] Einverständnisfeldatentyp

[!UICONTROL Generisches Einverständnisfeld ] ist ein standardmäßiger XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Zustimmungsvoreinstellung beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll verwendet werden, um die Struktur der Einwilligungsschemas Ihres Unternehmens mithilfe der Feldergruppe [[!UICONTROL Einverständnisse und Voreinstellungen]](../field-groups/profile/consents.md) als Grundlinie anzupassen.

![](../images/data-types/consent-field.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `val` | Zeichenfolge | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Die nachstehende Tabelle enthält akzeptierte Werte und Definitionen. |

{style=&quot;table-layout:auto&quot;}

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja | Der Kunde hat sich für die Zustimmung entschieden. Mit anderen Worten, sie stimmen **do** der Verwendung ihrer Daten zu, wie durch die betreffende Einwilligung angegeben. |
| `n` | Nein | Der Kunde hat sich von der Zustimmung abgemeldet. Mit anderen Worten, sie **stimmen nicht** der Verwendung ihrer Daten zu, wie durch die betreffende Einwilligung angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen Wert für die endgültige Zustimmung erhalten. Dies wird meist im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird diese Zustimmung auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf `y` aktualisiert.<br><br>Wenn diese Einwilligung keinen zweistufigen Überprüfungsprozess verwendet, kann die  `p` Auswahl stattdessen verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einwilligungsaufforderung reagiert hat. Sie können beispielsweise den Wert auf `p` automatisch auf der ersten Seite einer Website festlegen, bevor der Kunde auf die Einverständnisaufforderung reagiert hat. In Rechtsordnungen, die keine ausdrückliche Zustimmung erfordern, können Sie damit auch angeben, dass der Kunde sich nicht ausdrücklich abgemeldet hat (d. h., die Zustimmung wird angenommen). |
| `u` | „Unbekannt“ | Die Einwilligungsinformationen des Kunden sind unbekannt. |
| `LI` | Rechtliches Interesse | Das berechtigte geschäftliche Interesse, diese Daten für den angegebenen Zweck zu sammeln und zu verarbeiten, überwiegt den potenziellen Schaden, den sie für die Person darstellt. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wichtiges Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten für den festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)
