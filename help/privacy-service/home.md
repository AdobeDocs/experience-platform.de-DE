---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 5%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

Um eine bessere Kundenerfahrung zu erzielen, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu verstehen und zu respektieren. Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen.

Die Adobe Experience Platform [!DNL Privacy Service] wurde als Reaktion auf eine grundlegende Veränderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Das zentrale Ziel von [!DNL Privacy Service] ist es, die Einhaltung der Datenschutzbestimmungen zu automatisieren, die bei Verstößen zu hohen Geldbußen und zu Störungen des Datenbetriebs für Ihr Unternehmen führen können.

[!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung von Kundendatenanforderungen unterstützen. With [!DNL Privacy Service], you can submit requests to access and delete personal customer data from Adobe Experience Cloud applications, facilitating automated compliance with legal and organizational privacy regulations.

## Getting started with [!DNL Privacy Service] {#getting-started}

Um diese Vorteile nutzen zu können, müssen [!DNL Privacy Service]einige wichtige Entscheidungen in Bezug auf die Datenschutzanforderungen Ihres Unternehmens, die Art der Identitätsdaten, die Sie von Ihren Kunden erfassen, und die beste Möglichkeit getroffen werden, Ihr CRM-System mit dem Service zu verbinden.

Diese Entscheidungen lassen sich wie folgt zusammenfassen:

1. **Welche Informationen erfassen Sie von meinen Kunden?**
   * Um die Daten optimal zu nutzen, [!DNL Privacy Service]müssen Sie genau wissen, welche Arten von Daten Sie von Ihren Kunden erfassen und welche davon den Datenschutzbestimmungen unterliegen. Weitere Informationen finden Sie im Abschnitt zur [Festlegung der Datenschutzanforderungen](#requirements) .
1. **Habe ich meine Daten richtig gekennzeichnet?**
   * Die Daten müssen ordnungsgemäß beschriftet werden, damit der Dienst feststellen kann, welche Felder während der Datenschutzaufträge aufgerufen oder gelöscht werden sollen. Weitere Informationen finden Sie im Abschnitt zu [Kennzeichnungsdaten](#label) .
1. **Weiß ich, an welche IDs ich senden soll[!DNL Privacy Service]?**
   * Beim Senden von Datenschutzanfragen müssen individuelle Kunden-IDs für bestimmte Adobe-Anwendungen angegeben werden. Weitere Informationen finden Sie in den Abschnitten zur [Bereitstellung von Identitätsdaten](#identity) und [zur Anforderung](#requests) des Datenschutzes.
1. **Wie verfolge ich meine Datenschutzaufträge?**
   * Nachdem Sie Datenschutzanforderungen gestellt haben, stehen Ihnen verschiedene Optionen zur Verfolgung ihres Status und ihrer Ergebnisse zur Verfügung. Weitere Informationen finden Sie im Abschnitt zur [Überwachung von Datenschutzaufträgen](#monitor) .

Die folgenden Abschnitte enthalten allgemeine Anleitungen zu diesen wichtigen erforderlichen Schritten sowie Links zu weiteren [!DNL Privacy Service] Dokumentationen.

### Bestimmen Sie die Datenschutzanforderungen Ihres Unternehmens. {#requirements}

Abhängig von der Art Ihres Unternehmens und den Gerichtsbarkeiten, unter denen Ihr Unternehmen tätig ist, unterliegen Ihre Datenoperationen möglicherweise den gesetzlichen Datenschutzbestimmungen. Diese Bestimmungen geben Ihren Kunden oft das Recht, den Zugriff auf die von ihnen gesammelten Daten anzufordern und die Löschung dieser gespeicherten Daten zu beantragen. Diese Kundenanfragen nach ihren persönlichen Daten werden in der Dokumentation als &quot;Datenschutzanfragen&quot;bezeichnet.

In der folgenden Tabelle sind die gesetzlichen Datenschutzbestimmungen für Anfragen [!DNL Privacy Service] aufgeführt, einschließlich Links zur Dokumentation für weitere Informationen:

| Verordnung | Beschreibung |
| --- | --- |
| CCPA (Kalifornien) | The [!DNL California Consumer Privacy Act] (CCPA) enhances privacy rights and consumer protection for residents of California, United States. Das CCPA bietet kalifornischen Einwohnern neue Datenschutzrechte, darunter das Recht auf Zugang zu ihren personenbezogenen Daten und deren Löschung, um zu erfahren, ob ihre personenbezogenen Daten verkauft oder offen gelegt werden (und an wen), sowie das Recht, ihre Daten an Dritte zu Opt-out.<br/><br/>Links zur weiteren Dokumentation: <ul><li>[Rechtlicher Überblick](https://oag.ca.gov/privacy/ccpa)</li><li>[Häufig gestellte Fragen zu CCPA](ccpa/faq.md)</li></ul> |
| GDPR (Europäische Vereinigung) | The [!DNL General Data Protection Regulation] (GDPR) introduced several new data privacy rights for members of the European Union, including the **Right to Access** and the **Right to be Forgotten**. Dies bedeutet, dass jeder EU-Bürger, dessen personenbezogene Daten von Ihrem Unternehmen erfasst wurden, jederzeit den Zugriff auf oder die Löschung seiner Daten beantragen kann. <br/><br/>Links zur weiteren Dokumentation: <ul><li>[Rechtlicher Überblick](https://gdpr-info.eu/)</li><li>[Häufig gestellte Fragen zur DSGVO](gdpr/faq.md)</li><li>[DSGVO-Terminologie](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thailand) | Das Gesetz über den Schutz personenbezogener Daten in Thailand (PDPA) wurde eingeführt, um die thailändischen Dateneigner vor der illegalen Erhebung, Verwendung oder Weitergabe ihrer personenbezogenen Daten zu schützen. Auf der Grundlage des GDPR der Europäischen Vereinigung gewährt die Verordnung den thailändischen Bürgern das Recht, Zugang zu ihren gespeicherten personenbezogenen Daten oder deren Löschung zu beantragen.<br/><br/>Links zur weiteren Dokumentation: <ul><li>[Rechtlicher Überblick](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[PDPA_THA FAQ](pdpa-tha/faq.md)</li><li>[PDPA_THA-Terminologie](pdpa-tha/terminology.md)</li></ul> |

Wenn Ihre Datenvorgänge unter eine der oben genannten Verordnungen fallen, lesen Sie in der Dokumentation wichtige Informationen wie die spezifischen Datenschutzrechte, die Sie Ihren Kunden gewähren, und Compliance-Fenster, um Datenschutzanforderungen zu erfüllen. Diese Informationen sollten bei der Entscheidung, wie Sie in Ihr CRM-System integrieren und wie Kunden mit Ihrer Website interagieren sollten, um Datenschutzanforderungen zu stellen, berücksichtigt werden. [!DNL Privacy Service]

Zusätzlich zu den gesetzlichen Bestimmungen sollten bei diesen Entscheidungen auch alle für Ihr Unternehmen geltenden Organisations- oder Branchenstandards berücksichtigt werden.

### Label data for privacy requests {#label}

Abhängig von den [!DNL Experience Cloud] Anwendungen, die Sie verwenden, müssen Sie die spezifischen Datenfelder beschriften, auf die bei Datenschutzanforderungen zugegriffen oder gelöscht werden soll. Das Verfahren zur Kennzeichnung von Daten ist je nach Anwendung unterschiedlich. Informationen zum Beschreiben von Daten für jede unterstützte Adobe-Anwendung finden Sie im Dokument zu [Experience Cloud-Anwendungen](./experience-cloud-apps.md).

### Bestimmen Sie die Identitätsdaten, an die gesendet werden soll. [!DNL Privacy Service] {#identity}

Damit eine Datenschutzanforderung eines Kunden verarbeitet [!DNL Privacy Service] werden kann, muss in der Anforderung selbst mindestens ein eindeutiger Identitätswert für diesen Kunden angegeben werden. Ein eindeutiger Identitätswert ist jede Information, die zur Identifizierung einer Person und ihrer in Ihren [!DNL Experience Cloud] Datenspeichern gespeicherten personenbezogenen Daten verwendet werden kann. [!DNL Privacy Service] verwendet diese Identitätsinformationen, um die personenbezogenen Daten des Kunden entsprechend der Art der Anforderung zu finden und zu verarbeiten (Zugriff, Löschen oder Ausschluss).

Je nach den [!DNL Experience Cloud] Anwendungen, die Ihr CRM-System nutzt, variieren die Art und Anzahl der Identitätswerte, die Sie für jeden Kunden angeben müssen. Einige Anwendungen verwenden ihre eigenen internen Kunden-ID-Werte (z. B. Adobe Target-IDs), während andere auf globalen IDs von Adobe [!DNL Experience Cloud Identity Service] (ECID) basieren, die die Aktivität von Kunden in allen [!DNL Experience Cloud] Anwendungen verfolgen. Darüber hinaus können allgemeine persönliche Informationen wie eine E-Mail-Adresse oder Telefonnummer auch als gültige Identitätsdaten dienen.

Das Dokument zu [Identitätsdaten für Datenschutzanfragen](./identity-data.md) enthält detailliertere Informationen zu den Arten von Identitätsinformationen, die für [!DNL Privacy Service]die Verwendung zugelassen werden. Das Dokument bietet außerdem Anleitungen dazu, wie Adobe-Technologien genutzt werden können, um bei der Interaktion mit Ihrer Website die entsprechenden Identitätsinformationen von Ihren Kunden abzurufen und diese Daten an [!DNL Privacy Service] API-Anforderungen zu senden.

### Beginn, die Datenschutzanforderungen stellen {#requests}

Sobald Sie die Datenschutzbedürfnisse Ihres Unternehmens ermittelt und die Identitätswerte festgelegt haben, an die Sie [!DNL Privacy Service]den Beginn senden können, können Sie Datenschutzanforderungen stellen. [!DNL Privacy Service] ermöglicht Ihnen, Datenschutzanforderungen entweder über die API oder die Benutzeroberfläche zu senden.

>[!IMPORTANT]
>
>Die folgenden Abschnitte enthalten Links zur Dokumentation, in der beschrieben wird, wie allgemeine Datenschutzanforderungen in der API oder Benutzeroberfläche ausgeführt werden. Je nach verwendeter [!DNL Experience Cloud] Anwendung können sich die Felder, die Sie in der Anforderungsnutzlast senden müssen, jedoch von den Beispielen in diesen Handbüchern unterscheiden.
>
>Wenn Sie die API- oder UI-Anleitungen befolgen, lesen Sie bitte das Dokument zu [Privacy Service- und Experience Cloud-Anwendungen](./experience-cloud-apps.md) , um weitere Informationen zum Formatieren von Datenschutzanforderungen für Ihre jeweilige(n) [!DNL Experience Cloud] Anwendung(en) zu erhalten.

#### Verwenden der API

Die [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) bietet mehrere Endpunkte zum Erstellen und Verwalten von Datenschutzaufträgen mithilfe von RESTful-API-Aufrufen, mit denen Sie die Einhaltung der Datenschutzbestimmungen für Ihre [!DNL Experience Cloud] Anwendungen programmatisch angehen können. Ausführliche Anweisungen zur Verwendung der API finden Sie im Entwicklerhandbuch für die [Privacy Service-API](api/getting-started.md).

#### Verwenden der UI

>[!NOTE]
>
>Die [!DNL Privacy Service] Benutzeroberfläche unterstützt derzeit nur Zugriffs- und Löschanforderungen. Alle Abmeldeanfragen müssen stattdessen über die API erfolgen.

Die [!DNL Privacy Service] Benutzeroberfläche ermöglicht Ihnen, Datenschutzaufträge mithilfe einer grafischen Oberfläche zu erstellen und zu überwachen. Die Benutzeroberfläche enthält ein **[!UICONTROL Statusbericht]** -Widget, das den Status aller aktiven Anforderungen visuell darstellt und Ihnen das Erstellen neuer Anforderungen mithilfe des integrierten **[!UICONTROL Anforderungs-Builders]** oder durch Hochladen von JSON-Dateien ermöglicht. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md).

### Überwachen von Datenschutzaufträgen {#monitor}

Sobald Sie Datenschutzaufträge abgeschlossen haben, stehen Ihnen verschiedene Optionen zur Überwachung ihres Status und ihrer Ergebnisse zur Verfügung:

| Überwachungsmethode | Beschreibung |
| --- | --- |
| [!DNL Privacy Service] Benutzeroberfläche | Die [!DNL Privacy Service] Benutzeroberfläche bietet ein Dashboard zur Überwachung, mit dem Sie eine visuelle Darstellung des Status aller aktiven Anforderungen Ansicht haben. See the [Privacy Service user guide](ui/overview.md) for more information. |
| [!DNL Privacy Service] API | Sie können den Status von Datenschutzaufträgen programmgesteuert überwachen, indem Sie die von der [!DNL Privacy Service] API bereitgestellten Lookup-Endpunkte verwenden. Ausführliche Anweisungen zur Verwendung der API finden Sie im [Privacy Service Developer Guide](./api/getting-started.md) . |
| [!DNL Privacy Events] | [!DNL Privacy Events] nutzen Sie Adobe-I/O-Ereignis, die an einen konfigurierten Web-Haken gesendet werden, um eine effiziente Auftragsabwicklungsautomatisierung zu ermöglichen. They reduce or eliminate the need to poll the [!DNL Privacy Service] API in order to check if a job is complete or if a certain milestone within a workflow has been reached. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Datenschutzrichtlinien-Ereignissen](./privacy-events.md) . |

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die wichtigsten Schritte [!DNL Privacy Service] und die Schritte, die erforderlich sind, um den Beginn mit den Dienstfunktionen zu ermöglichen. Weitere Informationen zu den verschiedenen Aspekten der Zusammenarbeit finden Sie in der Dokumentation, auf die Sie im gesamten Überblick Bezug nehmen [!DNL Privacy Service].
