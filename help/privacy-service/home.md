---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 5%

---


# Übersicht über Adobe Experience Platform Privacy Service

Um eine bessere Kundenerfahrung zu erzielen, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu verstehen und zu respektieren. Die neuen gesetzlichen und organisatorischen Vorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten auf Anfrage aus Ihren Datenspeichern zuzugreifen oder sie zu löschen.

Adobe Experience Platform Privacy Service wurde als Reaktion auf eine grundlegende Veränderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Der Hauptzweck von Privacy Service ist die Automatisierung der Einhaltung von Datenschutzbestimmungen, die bei Verstößen zu hohen Geldbußen führen und den Datenbetrieb für Ihr Unternehmen stören können.

Privacy Service bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung von Kundendatenanforderungen unterstützen. Mit Privacy Service können Sie Anfragen zum Zugriff auf und Löschen von Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, um die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen zu erleichtern.

## Erste Schritte mit Privacy Service {#getting-started}

Um Privacy Service nutzen zu können, müssen einige wichtige Entscheidungen in Bezug auf die Datenschutzanforderungen Ihres Unternehmens, die Art der von Ihren Kunden erfassten Identitätsdaten und die beste Möglichkeit getroffen werden, Ihr CRM-System mit dem Dienst zu verbinden.

Diese Entscheidungen lassen sich wie folgt zusammenfassen:

1. **Welche Informationen erfassen Sie von meinen Kunden?**
   * Um den Privacy Service optimal zu nutzen, müssen Sie genau wissen, welche Daten Sie von Ihren Kunden erfassen und welche davon den Datenschutzbestimmungen unterliegen. Weitere Informationen finden Sie im Abschnitt zur [Festlegung der Datenschutzanforderungen](#requirements) .
1. **Habe ich meine Daten richtig gekennzeichnet?**
   * Die Daten müssen ordnungsgemäß beschriftet werden, damit der Dienst feststellen kann, welche Felder während der Datenschutzaufträge aufgerufen oder gelöscht werden sollen. Weitere Informationen finden Sie im Abschnitt zu [Kennzeichnungsdaten](#label) .
1. **Weiß ich, welche IDs an Privacy Service gesendet werden sollen?**
   * Beim Senden von Datenschutzanfragen müssen individuelle Kunden-IDs für bestimmte Adobe-Anwendungen angegeben werden. Weitere Informationen finden Sie in den Abschnitten zur [Bereitstellung von Identitätsdaten](#identity) und [zur Anforderung](#requests) des Datenschutzes.
1. **Wie verfolge ich meine Datenschutzaufträge?**
   * Nachdem Sie Datenschutzanforderungen gestellt haben, stehen Ihnen verschiedene Optionen zur Verfolgung ihres Status und ihrer Ergebnisse zur Verfügung. Weitere Informationen finden Sie im Abschnitt zur [Überwachung von Datenschutzaufträgen](#monitor) .

Die folgenden Abschnitte enthalten allgemeine Anleitungen zu diesen wichtigen erforderlichen Schritten sowie Links zu weiteren Privacy Services.

### Bestimmen Sie die Datenschutzanforderungen Ihres Unternehmens. {#requirements}

Abhängig von der Art Ihres Unternehmens und den Gerichtsbarkeiten, unter denen Ihr Unternehmen tätig ist, unterliegen Ihre Datenoperationen möglicherweise den gesetzlichen Datenschutzbestimmungen. Diese Bestimmungen geben Ihren Kunden oft das Recht, den Zugriff auf die von ihnen gesammelten Daten anzufordern und die Löschung dieser gespeicherten Daten zu beantragen. Diese Kundenanfragen nach ihren persönlichen Daten werden in der Dokumentation als &quot;Datenschutzanfragen&quot;bezeichnet.

In der folgenden Tabelle sind die rechtlichen Datenschutzvorschriften aufgeführt, die Privacy Service für Anfragen einhalten, einschließlich Links zur Dokumentation für weitere Informationen:

| Verordnung | Beschreibung |
| --- | --- |
| CCPA (Kalifornien) | Der California Consumer Privacy Act (CCPA) erweitert die Datenschutzrechte und den Verbraucherschutz für Einwohner von Kalifornien, USA. Das CCPA bietet kalifornischen Einwohnern neue Datenschutzrechte, darunter das Recht auf Zugang zu ihren personenbezogenen Daten und deren Löschung, um zu erfahren, ob ihre personenbezogenen Daten verkauft oder offen gelegt werden (und an wen), sowie das Recht, ihre Daten an Dritte zu Opt-out.<br/><br/>Links zur weiteren Dokumentation: <ul><li>[Rechtlicher Überblick](https://oag.ca.gov/privacy/ccpa)</li><li>[Häufig gestellte Fragen zum CCPA](ccpa/faq.md)</li></ul> |
| GDPR (Europäische Vereinigung) | Mit der Datenschutz-Grundverordnung (DSGVO) wurden mehrere neue Datenschutzrechte für Mitglieder der Europäischen Union eingeführt, darunter das **Recht auf Zugriff** und das **Recht auf Vergessenwerden**. Dies bedeutet, dass jeder EU-Bürger, dessen personenbezogene Daten von Ihrem Unternehmen erfasst wurden, jederzeit den Zugriff auf oder die Löschung seiner Daten beantragen kann. <br/><br/>Links zur weiteren Dokumentation: <ul><li>[Rechtlicher Überblick](https://gdpr-info.eu/)</li><li>[Häufig gestellte Fragen zur DSGVO](gdpr/faq.md)</li><li>[DSGVO-Terminologie](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thailand) | Das Gesetz über den Schutz personenbezogener Daten in Thailand (PDPA) wurde eingeführt, um die thailändischen Dateneigner vor der illegalen Erhebung, Verwendung oder Weitergabe ihrer personenbezogenen Daten zu schützen. Auf der Grundlage des GDPR der Europäischen Vereinigung gewährt die Verordnung den thailändischen Bürgern das Recht, Zugang zu ihren gespeicherten personenbezogenen Daten oder deren Löschung zu beantragen.<br/><br/>Links zur weiteren Dokumentation: <ul><li>[Rechtlicher Überblick](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[PDPA_THA FAQ](pdpa-tha/faq.md)</li><li>[PDPA_THA-Terminologie](pdpa-tha/terminology.md)</li></ul> |

Wenn Ihre Datenvorgänge unter eine der oben genannten Verordnungen fallen, lesen Sie in der Dokumentation wichtige Informationen wie die spezifischen Datenschutzrechte, die Sie Ihren Kunden gewähren, und Compliance-Fenster, um Datenschutzanforderungen zu erfüllen. Diese Informationen sollten bei der Entscheidung, wie Privacy Service in Ihr CRM-System integriert werden kann und wie Kunden mit Ihrer Website interagieren sollten, um Datenschutzanforderungen zu stellen, berücksichtigt werden.

Zusätzlich zu den gesetzlichen Bestimmungen sollten bei diesen Entscheidungen auch alle für Ihr Unternehmen geltenden Organisations- oder Branchenstandards berücksichtigt werden.

### Kennzeichnungsdaten für Datenschutzanforderungen {#label}

Abhängig von den verwendeten Experience Cloud-Anwendungen müssen Sie die spezifischen Datenfelder beschriften, auf die bei Datenschutzanforderungen zugegriffen oder gelöscht werden soll. Das Verfahren zur Kennzeichnung von Daten ist je nach Anwendung unterschiedlich. Informationen zum Beschreiben von Daten für jede unterstützte Adobe-Anwendung finden Sie im Dokument zu [Experience Cloud-Anwendungen](./experience-cloud-apps.md).

### Bestimmen der Identitätsdaten, die an Privacy Service gesendet werden sollen {#identity}

Damit der Privacy Service eine Datenschutzanforderung eines Kunden verarbeiten kann, muss in der Anforderung selbst mindestens ein eindeutiger Identitätswert für diesen Kunden angegeben werden. Ein eindeutiger Identitätswert ist jede Information, die zur Identifizierung einer Person und ihrer in Ihren Experience Cloud-Datenspeichern gespeicherten personenbezogenen Daten verwendet werden kann. Privacy Service verwendet diese Identitätsinformationen, um die personenbezogenen Daten des Kunden entsprechend der Art der Anforderung zu finden und zu verarbeiten (Zugriff, Löschen oder Ausschluss).

Je nachdem, welche Experience Cloud-Applikationen Ihr CRM-System verwendet, variieren die Art und Anzahl der Identitätswerte, die Sie für jeden Kunden angeben müssen. Einige Anwendungen verwenden ihre eigenen internen Kunden-ID-Werte (z. B. Adobe Target-IDs), während andere auf globalen IDs des Adobe Experience Cloud Identity Service (ECID) basieren, die die Aktivität von Kunden in allen Experience Cloud-Anwendungen verfolgen. Darüber hinaus können allgemeine persönliche Informationen wie eine E-Mail-Adresse oder Telefonnummer auch als gültige Identitätsdaten dienen.

Das Dokument zu [Identitätsdaten für Datenschutzanfragen](./identity-data.md) enthält detailliertere Informationen zu den Identitätsinformationen, die für den Privacy Service akzeptiert werden. Das Dokument bietet außerdem Anleitungen dazu, wie Adobe-Technologien genutzt werden können, um bei der Interaktion mit Ihrer Website die entsprechenden Identitätsinformationen effektiv abzurufen und diese Daten an den Privacy Service in API-Anforderungen zu senden.

### Beginn, die Datenschutzanforderungen stellen {#requests}

Sobald Sie die Datenschutzbedürfnisse Ihres Unternehmens ermittelt und die Identitätswerte festgelegt haben, die Sie an den Privacy Service senden möchten, können Sie Beginn Datenschutzanforderungen stellen. Mit Privacy Service können Sie Datenschutzanforderungen entweder über die API oder die Benutzeroberfläche senden.

>[!IMPORTANT]
>
>Die folgenden Abschnitte enthalten Links zur Dokumentation, in der beschrieben wird, wie allgemeine Datenschutzanforderungen in der API oder Benutzeroberfläche ausgeführt werden. Je nach den von Ihnen verwendeten Experience Cloud-Anwendungen können sich die Felder, die Sie in der Anforderungs-Nutzlast senden müssen, jedoch von den Beispielen in diesen Handbüchern unterscheiden.
>
>Wenn Sie die API- oder UI-Anleitungen befolgen, lesen Sie bitte das Dokument zu [Privacy Service- und Experience Cloud-Anwendungen](./experience-cloud-apps.md) , um weitere Informationen zur Formatierung von Datenschutzanforderungen für Ihre(n) Experience Cloud-Anwendung(en) zu erhalten.

#### Verwenden der API

Die [Privacy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) bietet mehrere Endpunkte zum Erstellen und Verwalten von Datenschutzaufträgen mithilfe von RESTful-API-Aufrufen, mit denen Sie die Einhaltung der Datenschutzvorschriften für Ihre Experience Cloud-Anwendungen programmatisch angehen können. Ausführliche Anweisungen zur Verwendung der API finden Sie im Entwicklerhandbuch für die [Privacy Service-API](api/getting-started.md).

#### Verwenden der Benutzeroberfläche

>[!NOTE]
>
>Die Benutzeroberfläche des Privacy Service unterstützt derzeit nur Zugriffs- und Löschanforderungen. Alle Abmeldeanfragen müssen stattdessen über die API erfolgen.

Die Benutzeroberfläche des Privacy Service ermöglicht Ihnen, Datenschutzaufträge über eine grafische Benutzeroberfläche zu erstellen und zu überwachen. Die Benutzeroberfläche enthält ein **Statusbericht** -Widget, das den Status aller aktiven Anforderungen visuell darstellt und Ihnen das Erstellen neuer Anforderungen mithilfe des integrierten **Anforderungs-Builders** oder durch Hochladen von JSON-Dateien ermöglicht. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md).

### Überwachen von Datenschutzaufträgen {#monitor}

Sobald Sie Datenschutzaufträge abgeschlossen haben, stehen Ihnen verschiedene Optionen zur Überwachung ihres Status und ihrer Ergebnisse zur Verfügung:

| Überwachungsmethode | Beschreibung |
| --- | --- |
| Benutzeroberfläche des Privacy Service | Die Benutzeroberfläche des Privacy Service bietet ein Dashboard zur Überwachung, mit dem Sie eine visuelle Darstellung des Status aller aktiven Anforderungen Ansichten vornehmen können. Weitere Informationen finden Sie im Benutzerhandbuch für [Privacy Service](ui/overview.md) . |
| Privacy Service-API | Sie können den Status von Datenschutzaufträgen programmgesteuert überwachen, indem Sie die von der Privacy Service-API bereitgestellten Lookup-Endpunkte verwenden. Ausführliche Anweisungen zur Verwendung der API finden Sie im [Privacy Service Developer Guide](./api/getting-started.md) . |
| Datenschutz-Ereignisse | Datenschutzrichtlinien-Ereignis nutzen Adobe-I/O-Ereignis, die an einen konfigurierten Webhaken gesendet werden, um eine effiziente Auftragsabwicklungsautomatisierung zu ermöglichen. Dadurch wird die Abfrage der Privacy Service-API reduziert oder vermieden, um zu überprüfen, ob ein Auftrag abgeschlossen ist oder ein bestimmter Meilenstein innerhalb eines Workflows erreicht wurde. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Datenschutzrichtlinien-Ereignissen](./privacy-events.md) . |

## Nächste Schritte

In diesem Dokument erhalten Sie einen Überblick über den Privacy Service und die wichtigsten Schritte, die erforderlich sind, um den Beginn mit den Dienstfunktionen zu ermöglichen. Detaillierte Informationen zu den verschiedenen Aspekten der Zusammenarbeit mit Privacy Service finden Sie in der Dokumentation, auf die Sie im gesamten Überblick zugreifen können.
