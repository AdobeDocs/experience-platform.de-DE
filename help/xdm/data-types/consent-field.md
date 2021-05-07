---
solution: Experience Platform
title: Allgemeiner Typ für übereinstimmende Felddaten
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp des generischen Kennwortfelds.
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# [!UICONTROL Allgemeiner Typ des ] Kennwortfelds

[!UICONTROL Generisches ] Feld für Zustimmung ein Standard-XDM-Datentyp, der die Auswahl eines Kunden für eine bestimmte Einstellung der Zustimmung beschreibt.

>[!NOTE]
>
>Dieser Datentyp soll dazu verwendet werden, die Struktur der Schema für die Zustimmung Ihres Unternehmens mithilfe der Feldgruppe [[!UICONTROL Datenschutz/Personalisierung/Marketing-Voreinstellungen (Zusätze)] als Grundlage anzupassen.](../field-groups/profile/consents.md)

![](../images/data-types/consent-field.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `val` | Zeichenfolge | Die vom Kunden angegebene Auswahl der Zustimmung für diesen Verwendungsfall. Die unten stehende Tabelle enthält akzeptierte Werte und Definitionen. |

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja | Der Kunde hat sich für die Zustimmung entschieden. Mit anderen Worten, sie stimmen der Verwendung ihrer Daten, wie in der betreffenden Einwilligung angegeben, zu.**** |
| `n` | Nein | Der Kunde hat sich von der Zustimmung ausgeschlossen. Mit anderen Worten, sie **stimmen der Verwendung ihrer Daten nicht** zu, wie in der betreffenden Einwilligung angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Zustimmungswert erhalten. Dies wird meistens im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Empfang von E-Mails entscheidet, wird diese Zustimmung auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um sicherzustellen, dass er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf `y` aktualisiert.<br><br>Verwendet diese Zustimmung keinen zweistufigen Überprüfungsprozess, kann die  `p` Auswahl stattdessen verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Aufforderung zur Einwilligung reagiert hat. Beispielsweise können Sie den Wert auf der ersten Seite einer Website automatisch auf `p` einstellen, bevor der Kunde auf die Aufforderung zur Einwilligung reagiert hat. In Gerichtsbarkeiten, die keine ausdrückliche Zustimmung erfordern, können Sie diese auch verwenden, um anzugeben, dass der Kunde sich nicht explizit abgemeldet hat (d. h. die Zustimmung wird angenommen). |
| `u` | „Unbekannt“ | Die Einwilligungsinformationen des Kunden sind unbekannt. |
| `LI` | Rechtliches Interesse | Das legitime Geschäftsinteresse, diese Daten für den angegebenen Zweck zu erheben und zu verarbeiten, überwiegt den potenziellen Schaden, den sie dem Einzelnen verursachen. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertraglichen Verpflichtungen mit der Einzelperson nachzukommen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wesentliches Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist zum Schutz der vitalen Interessen des Einzelnen erforderlich. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten zu dem festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt durchzuführen. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)
