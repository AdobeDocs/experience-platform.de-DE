---
solution: Experience Platform
title: Datentyp des allgemeinen Personalization-Präferenzfelds
description: Erfahren Sie mehr über den XDM-Datentyp Generisches Personalization-Präferenzfeld .
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# [!UICONTROL Generisches Personalization-Präferenzfeld] Datentyp

[!UICONTROL Generisches Personalization-Präferenzfeld] ist ein standardmäßiger XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Personalisierungsvoreinstellung beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll verwendet werden, um die Struktur der Einverständnisschemata Ihres Unternehmens mithilfe der Feldergruppe [[!UICONTROL Einverständnisse und Voreinstellungen] als ](../field-groups/profile/consents.md) anzupassen.

![](../images/data-types/personalization-field.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `val` | Zeichenfolge | Die vom Kunden bereitgestellte Präferenzauswahl für diesen Personalisierungs-Anwendungsfall. Siehe die nachstehende Tabelle für die akzeptierten Werte und Definitionen. |

{style="table-layout:auto"}

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

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
