---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---
# Snippets

## Kontingente und Verarbeitungszeitpläne {#quotas}

Anfragen zum Löschen von Datensätzen unterliegen täglichen und monatlichen Obergrenzen für die Übermittlung von Identifikatoren, die durch die Lizenzberechtigung Ihres Unternehmens bestimmt werden. Diese Einschränkungen gelten sowohl für benutzeroberflächen- als auch für API-basierte Löschanfragen.

>[!NOTE]
>
>Sie können bis zu **1.000.000 Kennungen pro Tag**, jedoch nur, wenn Ihr restliches monatliches Kontingent dies zulässt. Wenn Ihre monatliche Obergrenze weniger als 1 Million beträgt, können Ihre täglichen Einreichungen diese Obergrenze nicht überschreiten.

### Berechtigung zur monatlichen Übermittlung nach Produkt {#quota-limits}

In der folgenden Tabelle sind die Beschränkungen für die Übermittlung von Kennungen nach Produkt und Berechtigungsebene aufgeführt. Für jedes Produkt ist die monatliche Obergrenze der niedrigere von zwei Werten: eine feste Kennungsobergrenze oder ein prozentualer Schwellenwert, der an Ihr lizenziertes Datenvolumen gebunden ist.

| Produkt | Beschreibung der Berechtigung | Monatliche Obergrenze (je nachdem, welcher Wert niedriger ist) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP oder Adobe Journey Optimizer | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 5 % der adressierbaren Zielgruppe |
| Real-Time CDP oder Adobe Journey Optimizer | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 10 % der adressierbaren Zielgruppe |
| Customer Journey Analytics | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 100 Kennungen pro Million CJA-Berechtigungszeilen |
| Customer Journey Analytics | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 200 Kennungen pro Million CJA-Berechtigungszeilen |

>[!NOTE]
>
> Die meisten Unternehmen verfügen über niedrigere monatliche Limits, die auf ihren tatsächlichen adressierbaren Zielgruppen- oder CJA-Zeilenberechtigungen basieren.

Die Kontingente werden am ersten Tag jedes Kalendermonats zurückgesetzt. Nicht verwendetes Kontingent wird **nicht** übertragen.

>[!NOTE]
>
>Kontingente basieren auf der lizenzierten monatlichen Berechtigung Ihres Unternehmens für **übermittelte Kennungen**. Diese werden von den Systemschutzmechanismen nicht durchgesetzt, können jedoch überwacht und überprüft werden.
>
>Löschen eines Datensatzes ist ein **freigegebener Dienst**. Die monatliche Obergrenze spiegelt die höchsten Berechtigungen für Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics und alle anwendbaren Shield-Add-ons wider.

### Zeitleisten für die Übermittlung von Identifikatoren {#sla-processing-timelines}

Nach der Übermittlung werden Anfragen zum Löschen von Datensätzen basierend auf Ihrer Berechtigungsstufe in die Warteschlange gestellt und verarbeitet.

| Produkt- und Berechtigungsbeschreibung | Warteschlangendauer | Maximale Verarbeitungszeit (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | Bis zu 15 Tage | 30 Tage |
| Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | In der Regel 24 Stunden | 15 Tage |

Wenn für Ihr Unternehmen höhere Limits erforderlich sind, wenden Sie sich zur Überprüfung der Berechtigungen an den Adobe-Support.
