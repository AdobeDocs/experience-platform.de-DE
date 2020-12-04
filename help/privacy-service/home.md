---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d2f1255be48c1df04757f7e071221e0552a0b921
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 3%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

Um eine bessere Kundenerfahrung zu erzielen, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu verstehen und zu respektieren. Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen.

Adobe Experience Platform [!DNL Privacy Service] wurde als Reaktion auf eine grundlegende Änderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Das zentrale Ziel von [!DNL Privacy Service] ist es, die Einhaltung der Datenschutzbestimmungen zu automatisieren, die bei Verstößen zu hohen Geldbußen und zu Störungen des Datenbetriebs für Ihr Unternehmen führen können.

[!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung von Kundendatenanforderungen unterstützen. With [!DNL Privacy Service], you can submit requests to access and delete personal customer data from Adobe Experience Cloud applications, facilitating automated compliance with legal and organizational privacy regulations.

## Getting started with [!DNL Privacy Service] {#getting-started}

Um diese Vorteile nutzen zu können, müssen [!DNL Privacy Service]einige wichtige Entscheidungen in Bezug auf die Datenschutzanforderungen Ihres Unternehmens, die Art der Identitätsdaten, die Sie von Ihren Kunden erfassen, und die beste Möglichkeit getroffen werden, Ihr CRM-System mit dem Service zu verbinden.

Diese Entscheidungen lassen sich wie folgt zusammenfassen:

1. **Welche Informationen erfassen Sie von meinen Kunden?**
   * Um die Daten optimal zu nutzen, [!DNL Privacy Service]müssen Sie genau wissen, welche Arten von Daten Sie von Ihren Kunden erfassen und welche davon den Datenschutzbestimmungen unterliegen. Weitere Informationen finden Sie im Abschnitt zur [Festlegung der Datenschutzanforderungen](#requirements) .
1. **Habe ich meine Daten richtig gekennzeichnet?**
   * Die Daten müssen ordnungsgemäß beschriftet werden, damit der Dienst feststellen kann, welche Felder während der Datenschutzaufträge aufgerufen oder gelöscht werden sollen. Weitere Informationen finden Sie im Abschnitt zu [Kennzeichnungsdaten](#label) .
1. **Weiß ich, an welche IDs ich senden soll [!DNL Privacy Service]?**
   * Beim Senden von Datenschutzanfragen müssen individuelle Kunden-IDs für bestimmte Adoben angegeben werden. Weitere Informationen finden Sie in den Abschnitten zur [Bereitstellung von Identitätsdaten](#identity) und [zur Anforderung](#requests) des Datenschutzes.
1. **Wie verfolge ich meine Datenschutzaufträge?**
   * Nachdem Sie Datenschutzanforderungen gestellt haben, stehen Ihnen verschiedene Optionen zur Verfolgung ihres Status und ihrer Ergebnisse zur Verfügung. Weitere Informationen finden Sie im Abschnitt zur [Überwachung von Datenschutzaufträgen](#monitor) .

Die folgenden Abschnitte enthalten allgemeine Anleitungen zu diesen wichtigen erforderlichen Schritten sowie Links zu weiteren [!DNL Privacy Service] Dokumentationen.

### Bestimmen Sie die Datenschutzanforderungen Ihres Unternehmens. {#requirements}

Abhängig von der Art Ihres Unternehmens und den Gerichtsbarkeiten, unter denen Ihr Unternehmen tätig ist, unterliegen Ihre Datenoperationen möglicherweise den gesetzlichen Datenschutzbestimmungen. Diese Bestimmungen geben Ihren Kunden oft das Recht, den Zugriff auf die von ihnen gesammelten Daten anzufordern und die Löschung dieser gespeicherten Daten zu beantragen. Diese Kundenanfragen nach ihren persönlichen Daten werden in der Dokumentation als &quot;Datenschutzanfragen&quot;bezeichnet.

Einzelheiten zu den verschiedenen gesetzlichen Datenschutzbestimmungen, die Anfragen [!DNL Privacy Service] verwalten, einschließlich Schlüsselbegriffen und Antworten auf häufig gestellte Fragen, finden Sie in der Dokumentation [zu den](./regulations/overview.md)Datenschutzbestimmungen.

Wenn Ihre Datenvorgänge unter eine der unterstützten Richtlinien fallen, lesen Sie die Dokumentation für wichtige Informationen, wie die spezifischen Datenschutzrechte, die Sie Ihren Kunden gewähren, und Compliance-Fenster, um Datenschutzanforderungen zu erfüllen. Diese Informationen sollten bei der Entscheidung, wie Sie in Ihr CRM-System integrieren und wie Kunden mit Ihrer Website interagieren sollten, um Datenschutzanforderungen zu stellen, berücksichtigt werden. [!DNL Privacy Service]

Zusätzlich zu den gesetzlichen Bestimmungen sollten bei diesen Entscheidungen auch alle für Ihr Unternehmen geltenden Organisations- oder Branchenstandards berücksichtigt werden.

### Label data for privacy requests {#label}

Abhängig von den [!DNL Experience Cloud] Anwendungen, die Sie verwenden, müssen Sie die spezifischen Datenfelder beschriften, auf die bei Datenschutzanforderungen zugegriffen oder gelöscht werden soll. Das Verfahren zur Kennzeichnung von Daten ist je nach Anwendung unterschiedlich. Informationen zum Beschreiben von Daten für jede unterstützte Adobe finden Sie im Dokument zu [Experience Cloud-Anwendungen](./experience-cloud-apps.md).

### Bestimmen Sie die Identitätsdaten, an die gesendet werden soll. [!DNL Privacy Service] {#identity}

Damit eine Datenschutzanforderung eines Kunden verarbeitet [!DNL Privacy Service] werden kann, muss in der Anforderung selbst mindestens ein eindeutiger Identitätswert für diesen Kunden angegeben werden. Ein eindeutiger Identitätswert ist jede Information, die zur Identifizierung einer Person und ihrer in Ihren [!DNL Experience Cloud] Datenspeichern gespeicherten personenbezogenen Daten verwendet werden kann. [!DNL Privacy Service] verwendet diese Identitätsinformationen, um die personenbezogenen Daten des Kunden entsprechend der Art der Anforderung zu finden und zu verarbeiten (Zugriff, Löschen oder Ausschluss).

Je nach den [!DNL Experience Cloud] Anwendungen, die Ihr CRM-System nutzt, variieren die Art und Anzahl der Identitätswerte, die Sie für jeden Kunden angeben müssen. Einige Anwendungen verwenden ihre eigenen internen Kunden-ID-Werte (z. B. Adobe Target IDs), während andere auf globalen IDs aus Adobe [!DNL Experience Cloud Identity Service] (ECID) basieren, die die Aktivität von Kunden in allen [!DNL Experience Cloud] Anwendungen verfolgen. Darüber hinaus können allgemeine persönliche Informationen wie eine E-Mail-Adresse oder Telefonnummer auch als gültige Identitätsdaten dienen.

Das Dokument zu [Identitätsdaten für Datenschutzanfragen](./identity-data.md) enthält detailliertere Informationen zu den Arten von Identitätsinformationen, die für [!DNL Privacy Service]die Verwendung zugelassen werden. Das Dokument bietet außerdem Anleitungen dazu, wie Adoben genutzt werden können, um die entsprechenden Identitätsinformationen von Ihren Kunden bei der Interaktion mit Ihrer Website effektiv abzurufen und diese Daten an [!DNL Privacy Service] API-Anforderungen zu senden.

### Beginn, die Datenschutzanforderungen stellen {#requests}

Sobald Sie die Datenschutzbedürfnisse Ihres Unternehmens ermittelt und die Identitätswerte festgelegt haben, an die Sie [!DNL Privacy Service]den Beginn senden können, können Sie Datenschutzanforderungen stellen. [!DNL Privacy Service] ermöglicht Ihnen, Datenschutzanforderungen entweder über die API oder die Benutzeroberfläche zu senden.

>[!IMPORTANT]
>
>Die folgenden Abschnitte enthalten Links zur Dokumentation, in der beschrieben wird, wie allgemeine Datenschutzanforderungen in der API oder Benutzeroberfläche ausgeführt werden. Je nach verwendeter [!DNL Experience Cloud] Anwendung können sich die Felder, die Sie in der Anforderungsnutzlast senden müssen, jedoch von den Beispielen in diesen Handbüchern unterscheiden.
>
>Wenn Sie die API- oder UI-Anleitungen befolgen, lesen Sie bitte das Dokument zu [Privacy Service- und Experience Cloud-Anwendungen](./experience-cloud-apps.md) , um weitere Informationen zum Formatieren von Datenschutzanforderungen für Ihre jeweilige(n) [!DNL Experience Cloud] Anwendung(en) zu erhalten.
>
>Beachten Sie außerdem, dass Datenschutzanforderungen asynchron in allen Experience Cloud-Anwendungen verarbeitet werden. Sobald eine Anforderung beim Privacy Service eingegangen ist, kann die Bearbeitung der Anfrage innerhalb von Minuten und Wochen erfolgen. Der Zeitraum, der zum Abschließen der einzelnen Anforderungen benötigt wird, hängt von der Anwendung ab, mit der Sie arbeiten, und von der Menge der zu verarbeitenden Daten.

#### Verwenden der API

Das [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) bietet mehrere Endpunkte zum Erstellen und Verwalten von Datenschutzaufträgen mithilfe von RESTful-API-Aufrufen, mit denen Sie die Einhaltung der Datenschutzvorschriften für Ihre [!DNL Experience Cloud] Anwendungen programmatisch angehen können. Ausführliche Anweisungen zur Verwendung der API finden Sie im Entwicklerhandbuch für die [Privacy Service-API](api/getting-started.md).

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
| [!DNL Privacy Events] | [!DNL Privacy Events] adobe i/o-Ereignis, die an einen konfigurierten Webhaken gesendet werden, nutzen, um eine effiziente Auftragsautomatisierung zu ermöglichen. They reduce or eliminate the need to poll the [!DNL Privacy Service] API in order to check if a job is complete or if a certain milestone within a workflow has been reached. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Datenschutzrichtlinien-Ereignissen](./privacy-events.md) . |

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die wichtigsten Schritte [!DNL Privacy Service] und die Schritte, die erforderlich sind, um den Beginn mit den Dienstfunktionen zu ermöglichen. Weitere Informationen zu den verschiedenen Aspekten der Zusammenarbeit finden Sie in der Dokumentation, auf die Sie im gesamten Überblick Bezug nehmen [!DNL Privacy Service].
