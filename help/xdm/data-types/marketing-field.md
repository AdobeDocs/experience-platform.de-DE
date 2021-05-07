---
solution: Experience Platform
title: Allgemeiner Datentyp für Marketing-Voreinstellungen
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp des Generischen Marketingvorgabefelds.
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 2%

---

# [!UICONTROL Generischer ] Felddatentyp für Marketing-Voreinstellungen

[!UICONTROL Generische Marketing-Voreinstellungsfelder ] sind ein standardmäßiger XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Marketingvorgabe beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll dazu verwendet werden, die Struktur der Schema für die Zustimmung Ihres Unternehmens mithilfe der Feldgruppe [[!UICONTROL Datenschutz/Personalisierung/Marketing-Voreinstellungen (Zusätze)] als Grundlage anzupassen.](../field-groups/profile/consents.md)
>
>Wenn Sie eine `subscriptions`-Zuordnung für ein bestimmtes Marketing-Voreinstellungsfeld benötigen, müssen Sie stattdessen das Marketingfeld [mit dem Abonnement-Datentyp](./marketing-field-subscriptions.md) verwenden.

![](../images/data-types/marketing-field.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `reason` | Zeichenfolge | Wenn ein Kunde sich aus einer Marketing-Verwendungsszenario ausschließt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |
| `time` | DateTime | Ein Zeitstempel nach ISO 8601, der angibt, wann sich die Marketing-Voreinstellung geändert hat (falls zutreffend). |
| `val` | Zeichenfolge | Die vom Kunden angebotene Voreinstellungsoption für diesen Marketing-Verwendungsfall. Die unten stehende Tabelle enthält akzeptierte Werte und Definitionen. |

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

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
