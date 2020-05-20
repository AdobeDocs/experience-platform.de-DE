---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Unterstützte Beschriftungen für die Datenverwendung
topic: labels
translation-type: tm+mt
source-git-commit: 5aa0325a051d9e6e6dd65234db27ab251cfb2d9e
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 2%

---


# Unterstützte Beschriftungen für die Datenverwendung

Die Adobe Experience Platform umfasst eine Infrastruktur für die Datenverwaltung mit der Datenausnutzung-Kennzeichnung und -Durchsetzung (DULE).  Mit den Funktionen DULE können Datenverwendungsbeschriftungen auf Datensätze und Felder angewendet werden, um Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien zu kategorisieren.

In der folgenden Liste werden alle Datenverwendungsbeschriftungen beschrieben, die derzeit von Experience Platform unterstützt werden.

Weitere Informationen zu Datenverwaltung und DUL finden Sie in der Übersicht über die [Datenverwaltung](../home.md).

## Vertragsbezeichnungen

Die &quot;C&quot;-Beschriftungen des Vertrags werden zur Kategorisierung von Daten verwendet, die vertragliche Verpflichtungen haben oder mit den Datenschutzrichtlinien Ihres Unternehmens in Zusammenhang stehen.

| Beschriftung | Definition |
|---|---|
| **C1** | Daten können nur in aggregierter Form aus Adobe Experience Cloud exportiert werden, ohne dass dabei einzelne IDs oder Geräte-IDs einbezogen werden. [Weitere Infos...](#c1) |
| **C2** | Daten können nicht in einen Drittanbieter exportiert werden. [Weitere Infos...](#c2) |
| **C3** | Daten können nicht mit direkt identifizierbaren Informationen kombiniert oder anderweitig verwendet werden. [Weitere Infos...](#c3) |
| **C4** | Daten können nicht für das Targeting von Anzeigen oder Inhalten verwendet werden, weder auf der Site noch auf der Site. [Weitere Infos...](#c4) |
| **C5** | Daten können nicht für interessensbasiertes, Site-übergreifendes Targeting von Inhalten oder Anzeigen verwendet werden. [Weitere Infos...](#c5) |
| **C6** | Daten können nicht für das Targeting von Onsite-Anzeigen verwendet werden. [Weitere Infos...](#c6) |
| **C7** | Daten können nicht für das Targeting von Inhalten auf der Site verwendet werden. [Weitere Infos...](#c7) |
| **C8** | Daten können nicht zur Messung der Websites oder Apps Ihres Unternehmens verwendet werden. [Weitere Infos...](#c8) |
| **C9** | Daten können nicht in Data Science Workflows verwendet werden. [Weitere Infos...](#c9) |

## Identitätsbezeichnungen

Identitäts-&quot;I&quot;-Beschriftungen werden zur Kategorisierung von Daten verwendet, die eine bestimmte Person identifizieren oder kontaktieren können.

| Beschriftung | Definition |
|---|---|
| **I1** | Direkt identifizierbare Daten, mit denen eine bestimmte Person anstatt eines Geräts identifiziert oder kontaktiert werden kann. |
| **I2** | Indirekte identifizierbare Daten, die in Verbindung mit anderen Daten zur Identifizierung oder zum Kontakt mit einer bestimmten Person verwendet werden können. |

## Sensible Beschriftungen

Sensible &quot;S&quot;-Beschriftungen werden verwendet, um Daten zu kategorisieren, die Sie und Ihr Unternehmen als vertraulich betrachten.

Eine Art von Daten, die Sie als sensibel betrachten, kann verschiedene Arten geografischer Daten sein; Diese Kategorie ist jedoch nicht auf geografische Daten beschränkt.

| Beschriftung | Definition |
|---|---|
| **S1** | Daten zur Angabe von Breiten- und Längengrad, die zur Bestimmung der genauen Position eines Geräts verwendet werden können. |
| **S2** | Daten, die zur Bestimmung eines allgemein definierten Geofence-Bereichs verwendet werden können. |


## Weitere Informationen

Im folgenden Abschnitt finden Sie detaillierte Informationen zur Implementierung spezifischer Etiketten.

### C1 {#c1}

Einige Daten können nur in aggregierter Form aus Adobe Experience Cloud exportiert werden, ohne dass dabei einzelne IDs oder Geräte-IDs einbezogen werden. Zum Beispiel Daten, die aus sozialen Netzwerken stammen.

### C2 {#c2}

Einige Datenanbieter haben in ihren Verträgen Bedingungen, die den Export von Daten, von denen sie ursprünglich erfasst wurden, verbieten. So wird beispielsweise die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, oft eingeschränkt. Das C2-Etikett ist restriktiver als [C1](#c1), was nur Aggregation und anonyme Daten erfordert.

### C3 {#c3}

Einige Datenanbieter haben Vertragsbedingungen, die die Kombination oder Verwendung dieser Daten mit direkt identifizierbaren Informationen verbieten. Verträge über Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten bezogen werden, enthalten beispielsweise oft spezifische vertragliche Verbote für die Verwendung solcher Daten mit direkt identifizierbaren Daten.

### C4 {#c4}

C4 ist die restriktivste Bezeichnung - sie umfasst die Etiketten [C5](#c5), [C6](#c6)und [C7](#c7).

### C5 {#c5}

Interessensbasiertes Targeting oder Personalisierung tritt auf, wenn die folgenden drei Bedingungen erfüllt sind: Die vor Ort erfassten Daten werden (1) verwendet, um Rückschlüsse auf die Interessen der Benutzer zu ziehen, (2) in einem anderen Kontext verwendet, z. B. auf einer anderen Site oder App (außerhalb der Site) UND (3) wird verwendet, um festzulegen, welche Inhalte oder Anzeigen auf der Grundlage dieser Schlussfolgerungen bereitgestellt werden.

Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als Site-übergreifende Daten bezeichnet. Verschiedene Sites stellen unterschiedliche Kontexte dar, sodass die Verwendung von Site-übergreifenden Daten in jedem Kontext anders ist als das Original. Site-übergreifende Daten werden in der Regel gesammelt und verarbeitet, um Rückschlüsse auf die Interessen der Benutzer zu ziehen. Die Verwendung von Site-übergreifenden Daten zum Targeting von Anzeigen oder Inhalten gilt daher in der Regel als interessenbasiertes Targeting, unabhängig davon, ob die Anzeige oder der Inhalt auf der Site oder außerhalb der Site erscheint. Wenn z. B. Onsite-Daten in Kombination mit Offsite-Daten verwendet wurden, um auszuwählen, welche Anzeige einem Benutzer auf der eigenen Website eines Unternehmens angezeigt werden soll, würde diese Verwendung als interessensbasiertes Targeting gelten. Ein weiteres Beispiel: Das erneute Targeting von Anzeigen auf Benutzer außerhalb der Site würde wahrscheinlich auch als interessensbasiertes Targeting gelten.

Die Verwendung von Offsite-Daten allein für das Targeting würde wahrscheinlich auch als zinsbasiertes Targeting gelten, da Offsite-Daten in der Regel gesammelt und verarbeitet werden, um Rückschlüsse auf die Interessen der Benutzer zu ziehen.

Beim Targeting von Inhalten oder Anzeigen, die ausschließlich Onsite-Daten verwenden, wird das Targeting jedoch in der Regel nicht als interessensbasiertes Targeting eingestuft. Das On-Site-Targeting, das ansonsten nicht als zinsbasiertes Targeting gilt, wird als zwei unterschiedliche Bezeichnungen behandelt. Das Label C6 befasst sich insbesondere mit dem Onsite-Targeting und dem Berichte von Anzeigen und bezieht sich insbesondere auf die Auswahl von Anzeigen, Versand und Berichte, und das Label C7 bezieht sich auf die Inhaltsauswahl, den Versand und den Berichte auf der Site (Targeting von Inhalten auf der Site).

Letztendlich liegt die Interpretation der Beschriftung und die Art und Weise, wie die Nutzung der Daten mit dieser Beschriftung erzwungen wird, bei Ihnen. Nachstehend sind die IAB- und DAA-Rahmenwerke als Referenz aufgeführt:

IAB: Personalisierung. Die Erfassung und Verarbeitung von Informationen über Ihre Nutzung dieses Dienstes zur späteren Personalisierung von Werbung und/oder Inhalten für Sie in anderen Kontexten, z. B. auf anderen Websites oder Apps, im Laufe der Zeit. Normalerweise wird der Inhalt der Site oder App verwendet, um Rückschlüsse auf Ihre Interessen zu ziehen, die die zukünftige Auswahl von Werbung und/oder Inhalten beeinflussen.

DAA: Online-verhaltensbasierte Werbung. Erfassen von Daten über das Verhalten von Webansichten auf einem bestimmten Computer oder Gerät im Zeitverlauf und über Websites, die keine Tochterunternehmen sind, zum Zweck der Verwendung solcher Daten zur Vorhersage von Benutzervorlieben oder -interessen, um auf der Grundlage von Voreinstellungen oder Interessen, die aus solchen Webansichtsverhalten abgeleitet werden, Werbung für diesen Computer oder dieses Gerät zu liefern.

### C6 {#c6}

Anzeigen sind Nachrichten oder Benachrichtigungen, einschließlich Text und Bilder, die auf einer Website oder App erscheinen und in erster Linie dazu dienen, den Verkauf von Waren oder Dienstleistungen zu fördern. Es liegt an Ihnen, den Zweck solcher Nachrichten oder Benachrichtigungen zu bestimmen. Anzeigen sind getrennt von Inhalten auf der Site, die unter das Etikett [C7](#c7)fallen. Daten mit einem C6-Etikett können nicht für das Targeting von Anzeigen auf der Site verwendet werden, einschließlich der Auswahl und des Versands von Anzeigen auf den Websites oder Apps Ihres Unternehmens oder zur Messung des Versands und der Effektivität solcher Anzeigen. Dazu gehören die Verwendung von zuvor erfassten Onsite-Daten über die Interessen der Benutzer bei der Auswahl von Anzeigen, Prozessdaten darüber, wann und wo Werbung angezeigt wurde und ob die Benutzer Aktionen im Zusammenhang mit der Werbung ergriffen haben, z. B. das Klicken auf eine Anzeige oder einen Kauf. In der Regel würden die auf den Aktivitäten der Benutzer vor Ort beruhenden Präferenzen und die Verwendung dieser Präferenzen beim Targeting von Anzeigen vor Ort nicht als interessenbasiertes Targeting (auch Personalisierung genannt) gelten, da nicht alle drei erforderlichen Voraussetzungen für ein interessenbasiertes Targeting erfüllt würden. _[Diese Anforderungen finden Sie auf dem Etikett C5.](#c5)_

Letztendlich liegt die Interpretation der Beschriftung und die Art und Weise, wie die Nutzung der Daten mit dieser Beschriftung erzwungen wird, bei Ihnen. Nachstehend sind die IAB- und DAA-Rahmenwerke als Referenz aufgeführt:

IAB: 3. Anzeigenauswahl, Versand, Berichte: Die Erfassung von Informationen und die Kombination mit zuvor gesammelten Informationen, um Anzeigen für Sie auszuwählen und zu liefern und den Versand und die Effektivität solcher Anzeigen zu messen. Dazu gehören die Verwendung von zuvor erfassten Informationen zu Ihren Interessen zur Auswahl von Anzeigen, die Verarbeitung von Daten darüber, welche Anzeigen angezeigt wurden, wie oft sie angezeigt wurden, wann und wo sie angezeigt wurden und ob Sie irgendwelche Aktionen im Zusammenhang mit der Werbung unternommen haben, z. B. das Klicken auf eine Anzeige oder den Einkauf. Dies umfasst nicht Personalisierung, d. h. die Erfassung und Verarbeitung von Informationen über Ihre Nutzung dieses Dienstes, um später Werbung und/oder Inhalte für Sie in anderen Kontexten, wie Websites oder Apps, personalisieren zu können.

DAA: Die Online-verhaltensbasierte Werbung umfasst nicht die Aktivitäten von Erstanbietern, Anzeigen-Versand oder Anzeigen-Berichte oder kontextbezogene Werbung (d. h. Werbung, die auf dem Inhalt der besuchten Webseite, dem aktuellen Besuch eines Abfrage auf einer Webseite oder einer Suchseite basiert).

### C7 {#c7}

Inhalt auf der Site ist Text und Bilder, die zur Information, Ausbildung oder Unterhaltung konzipiert sind und nicht zur Förderung des Verkaufs von Waren oder Dienstleistungen erstellt wurden. Es liegt an Ihnen, den Zweck des Inhalts zu bestimmen, einschließlich der Frage, ob der Inhalt als native Werbung gelten würde. Das C7-Etikett ist nicht für Onsite-Anzeigen vorgesehen, die unter das Etikett [C6](#c6)fallen. Daten mit einer C7-Bezeichnung können nicht für das Targeting von Inhalten auf der Site verwendet werden, einschließlich der Auswahl und des Versands von Inhalten auf den Websites oder Apps Ihres Unternehmens oder zur Messung des Versands und der Effektivität solcher Inhalte. Dazu gehören zuvor erfasste Informationen über die Interessen der Benutzer an ausgewählten Inhalten, die Verarbeitung von Daten darüber, welche Inhalte angezeigt wurden, wie oft und wie lange sie angezeigt wurden, wann und wo sie angezeigt wurden und ob die Verwendungszwecke Aktionen im Zusammenhang mit dem Inhalt, z. B. das Klicken auf den Inhalt, durchgeführt haben. In der Regel würden die auf den Aktivitäten der Benutzer vor Ort beruhenden Präferenzen und die Verwendung dieser Präferenzen beim Targeting von Inhalten vor Ort nicht als interessenbasiertes Targeting (auch Personalisierung genannt) gelten, da nicht alle drei erforderlichen Voraussetzungen für ein interessenbasiertes Targeting erfüllt würden. _[Diese Anforderungen finden Sie auf dem Etikett C5.](#c5)_

Letztendlich liegt die Interpretation der Beschriftung und die Art und Weise, wie die Nutzung der Daten mit dieser Beschriftung erzwungen wird, bei Ihnen. Nachstehend sind die IAB- und DAA-Rahmenwerke als Referenz aufgeführt:

IAB: 4. Inhaltsauswahl, Versand, Berichte: Die Erfassung von Informationen und die Kombination mit zuvor erfassten Informationen, um Inhalte für Sie auszuwählen und bereitzustellen und den Versand und die Effektivität solcher Inhalte zu messen. Dazu gehören die Verwendung von zuvor erfassten Informationen zu Ihren Interessen zur Auswahl von Inhalten, die Verarbeitung von Daten darüber, welche Inhalte angezeigt wurden, wie oft und wie lange sie angezeigt wurden, wann und wo sie angezeigt wurden und ob Sie im Zusammenhang mit dem Inhalt irgendwelche Aktionen durchgeführt haben, z. B. das Klicken auf Inhalte. Dies umfasst nicht Personalisierung, d. h. die Erfassung und Verarbeitung von Informationen über Ihre Nutzung dieses Dienstes, um Inhalte und/oder Werbung für Sie in anderen Kontexten, wie Websites oder Apps, im Laufe der Zeit zu personalisieren.

DAA: Die Online-verhaltensbasierte Werbung umfasst nicht die Aktivitäten von Erstanbietern, Anzeigen-Versand oder Anzeigen-Berichte oder kontextbezogene Werbung (d. h. Werbung, die auf dem Inhalt der Webseite basiert, die gerade besucht wird, dem aktuellen Besuch eines Abfrage auf einer Webseite oder einer Suchseite).

### C8 {#c8}

Daten können nicht verwendet werden, um die Nutzung der Sites oder Apps Ihres Unternehmens durch Benutzer zu messen, zu verstehen und Berichte darüber zu erstellen. Dies umfasst nicht das interessensbasierte Targeting (Cross-Site-Targeting), d. h. die Sammlung von Informationen über Ihre Nutzung dieses Dienstes, um Inhalte und/oder Werbung später für Sie in anderen Kontexten, z. B. auf anderen Diensten wie Websites oder Apps, im Laufe der Zeit zu personalisieren.

### C9 {#c9}

Einige Verträge beinhalten explizite Verbote der Datenverwendung für die Datenwissenschaft. Manchmal werden diese Begriffe in Begriffen ausgedrückt, die die Verwendung von Daten für künstliche Intelligenz (AI), maschinelles Lernen (ML) oder Modellierung verbieten.