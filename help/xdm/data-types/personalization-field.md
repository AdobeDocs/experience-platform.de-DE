---
solution: Experience Platform
title: Datentyp "Generische Personalisierungseinstellung"
description: Erfahren Sie mehr über den XDM-Datentyp "Generisches Personalisierungsfeld".
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# [!UICONTROL Feld für allgemeine Personalisierungseinstellungen] Datentyp

[!UICONTROL Feld für allgemeine Personalisierungseinstellungen] ist ein standardmäßiger XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Personalisierungseinstellung beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll verwendet werden, um die Struktur der Einwilligungsschemas Ihres Unternehmens mithilfe der Variablen [[!UICONTROL Einverständnis und Voreinstellungen] Feldergruppe](../field-groups/profile/consents.md) als Grundlinie.

![](../images/data-types/personalization-field.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `val` | Zeichenfolge | Die vom Kunden angegebene Voreinstellungsoption für diesen Personalisierungsfall. Die nachstehende Tabelle enthält akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

In der folgenden Tabelle sind die für `val`:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja (Opt-in) | Der Kunde hat sich für die Präferenz entschieden. Mit anderen Worten, sie **do** Zustimmung zur Verwendung ihrer Daten, wie durch die betreffende Präferenz angegeben. |
| `n` | Nein (Opt-out) | Der Kunde hat sich von der Präferenz abgemeldet. Mit anderen Worten, sie **nicht** Zustimmung zur Verwendung ihrer Daten, wie durch die betreffende Präferenz angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Präferenzwert erhalten. Dies wird meist im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird diese Zustimmung auf `p` bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat; an diesem Punkt würde die Zustimmung auf `y`.<br><br>Wenn diese Voreinstellung keinen zweistufigen Überprüfungsprozess verwendet, wird die `p` choice kann stattdessen verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einverständnisaufforderung reagiert hat. Sie können beispielsweise den Wert automatisch auf `p` auf der ersten Seite einer Website, bevor der Kunde auf die Einwilligungsaufforderung reagiert hat. In Rechtsordnungen, die keine ausdrückliche Zustimmung erfordern, können Sie damit auch angeben, dass der Kunde sich nicht ausdrücklich abgemeldet hat (d. h., die Zustimmung wird angenommen). |
| `u` | Unbekannt | Die Präferenzinformationen des Kunden sind unbekannt. |
| `dy` | Standardwert Ja (Opt-in) | Der Kunde hat selbst keinen Zustimmungswert angegeben und wird standardmäßig als Opt-in (&quot;Ja&quot;) behandelt. Mit anderen Worten, die Zustimmung wird angenommen, bis der Kunde etwas Anderes angibt.<br><br>Beachten Sie, dass Sie alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen, wenn die Datenschutzrichtlinien Ihres Unternehmens Änderungen an den Standardeinstellungen einiger oder aller Benutzer zur Folge haben. |
| `dn` | Standardwert Nein (Opt-out) | Der Kunde hat selbst keinen Zustimmungswert angegeben und wird standardmäßig als Opt-out (&quot;Nein&quot;) behandelt. Mit anderen Worten, es wird angenommen, dass der Kunde die Zustimmung verweigert hat, bis er etwas Anderes angibt.<br><br>Beachten Sie, dass Sie alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen, wenn die Datenschutzrichtlinien Ihres Unternehmens Änderungen an den Standardeinstellungen einiger oder aller Benutzer zur Folge haben. |
| `LI` | Rechtliches Interesse | Das berechtigte geschäftliche Interesse, diese Daten für den angegebenen Zweck zu sammeln und zu verarbeiten, überwiegt den potenziellen Schaden, den sie für die Person darstellt. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wichtiges Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten für den festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
