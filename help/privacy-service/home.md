---
keywords: Experience Platform;Home;beliebte Themen;GDPR;gdpr;ccpa:CCPA;PDPA;PDPA;PDPA_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Übersicht über Privacy Service
topic-legacy: overview
description: Mit Privacy Service können Sie die automatische Einhaltung gesetzlicher Datenschutzbestimmungen in Ihren Experience Cloud-Datenoperationen erleichtern.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 3%

---

# [!DNL Privacy Service]Übersicht

Um eine bessere Kundenerfahrung zu erzielen, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu verstehen und zu respektieren. Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen.

Adobe Experience Platform [!DNL Privacy Service] wurde als Reaktion auf eine grundlegende Änderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Der zentrale Zweck von [!DNL Privacy Service] ist die Automatisierung der Einhaltung von Datenschutzbestimmungen, die bei Verstößen zu erheblichen Geldbußen und Störungen des Datenbetriebs für Ihr Unternehmen führen können.

[!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung von Kundendatenanforderungen unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugriff und Löschen von persönlichen Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

## Erste Schritte mit [!DNL Privacy Service] {#getting-started}

Um [!DNL Privacy Service] nutzen zu können, müssen einige wichtige Entscheidungen in Bezug auf die Datenschutzanforderungen Ihres Unternehmens, die Art der Identitätsdaten, die Sie von Ihren Kunden erfassen, und die beste Möglichkeit getroffen werden, Ihr CRM-System mit dem Dienst zu verbinden.

Diese Entscheidungen lassen sich wie folgt zusammenfassen:

1. **Welche Informationen erfassen Sie von meinen Kunden?**
   * Um [!DNL Privacy Service] optimal nutzen zu können, müssen Sie über ein detailliertes Verständnis der Arten von Daten verfügen, die Sie von Ihren Kunden erfassen und welche davon den Datenschutzbestimmungen unterliegen. Weitere Informationen finden Sie im Abschnitt [Festlegen von Datenschutzanforderungen](#requirements).
1. **Habe ich meine Daten richtig gekennzeichnet?**
   * Die Daten müssen ordnungsgemäß beschriftet werden, damit der Dienst feststellen kann, welche Felder während der Datenschutzaufträge aufgerufen oder gelöscht werden sollen. Weitere Informationen finden Sie im Abschnitt [Kennzeichnungsdaten](#label).
1. **Weiß ich, an welche IDs ich senden soll  [!DNL Privacy Service]?**
   * Beim Senden von Datenschutzanfragen müssen individuelle Kunden-IDs für bestimmte Adoben angegeben werden. Weitere Informationen finden Sie in den Abschnitten [Identitätsdaten bereitstellen](#identity) und [Erstellen von Datenschutzanforderungen](#requests).
1. **Wie verfolge ich meine Datenschutzaufträge?**
   * Nachdem Sie Datenschutzanforderungen gestellt haben, stehen Ihnen verschiedene Optionen zur Verfolgung ihres Status und ihrer Ergebnisse zur Verfügung. Weitere Informationen finden Sie im Abschnitt [Überwachungs-Datenschutzaufträge](#monitor).

Die folgenden Abschnitte enthalten allgemeine Anleitungen zu diesen wichtigen Schritten, sowie Links zu weiteren [!DNL Privacy Service] Dokumentationen für weitere Details.

### Bestimmen Sie die Datenschutzanforderungen Ihres Unternehmens {#requirements}

Abhängig von der Art Ihres Unternehmens und den Gerichtsbarkeiten, unter denen Ihr Unternehmen tätig ist, unterliegen Ihre Datenoperationen möglicherweise den gesetzlichen Datenschutzbestimmungen. Diese Bestimmungen geben Ihren Kunden oft das Recht, den Zugriff auf die von ihnen gesammelten Daten anzufordern und die Löschung dieser gespeicherten Daten zu beantragen. Diese Kundenanfragen nach ihren persönlichen Daten werden in der Dokumentation als &quot;Datenschutzanfragen&quot;bezeichnet.

Einzelheiten zu den verschiedenen gesetzlichen Datenschutzbestimmungen, die von [!DNL Privacy Service] für Anfragen verwendet werden, einschließlich Schlüsselbegriffe und Antworten auf häufig gestellte Fragen, finden Sie in der [Dokumentation zu Datenschutzbestimmungen](./regulations/overview.md).

Wenn Ihre Datenvorgänge unter eine der unterstützten Richtlinien fallen, lesen Sie die Dokumentation für wichtige Informationen, wie die spezifischen Datenschutzrechte, die Sie Ihren Kunden gewähren, und Compliance-Fenster, um Datenschutzanforderungen zu erfüllen. Diese Informationen sollten bei der Entscheidung, wie [!DNL Privacy Service] in Ihr CRM-System integriert werden soll und wie Kunden mit Ihrer Website interagieren sollten, um Datenschutzanforderungen zu stellen, berücksichtigt werden.

Zusätzlich zu den gesetzlichen Bestimmungen sollten bei diesen Entscheidungen auch alle für Ihr Unternehmen geltenden Organisations- oder Branchenstandards berücksichtigt werden.

### Kennzeichnungsdaten für Datenschutzanforderungen {#label}

Abhängig von den von Ihnen verwendeten Anwendungen [!DNL Experience Cloud] müssen Sie die spezifischen Datenfelder beschriften, auf die bei Datenschutzanforderungen zugegriffen oder gelöscht werden soll. Das Verfahren zur Kennzeichnung von Daten ist je nach Anwendung unterschiedlich. Informationen zum Beschreiben von Daten für jede unterstützte Adobe finden Sie im Dokument zu [Experience Cloud-Anwendungen](./experience-cloud-apps.md).

### Bestimmen Sie die Arten von Identitätsdaten, die an [!DNL Privacy Service] {#identity} gesendet werden sollen.

Damit [!DNL Privacy Service] eine Datenschutzanforderung eines Kunden verarbeitet, muss in der Anforderung selbst mindestens ein eindeutiger Identitätswert für diesen Kunden angegeben werden. Ein eindeutiger Identitätswert ist jede Information, die zur Identifizierung einer einzelnen Person und ihrer gespeicherten persönlichen Daten in Ihren [!DNL Experience Cloud]-Datenspeichern verwendet werden kann. [!DNL Privacy Service] verwendet diese Identitätsinformationen, um die personenbezogenen Daten des Kunden entsprechend der Art der Anforderung zu finden und zu verarbeiten (Zugriff, Löschen oder Ausschluss).

Je nach den [!DNL Experience Cloud]-Anwendungen, die Ihr CRM-System verwendet, variieren der Typ und die Anzahl der Identitätswerte, die Sie für jeden Kunden angeben müssen. Einige Anwendungen verwenden ihre eigenen internen Kunden-ID-Werte (z. B. Adobe Target-IDs), während andere auf globalen IDs der Adobe [!DNL Experience Cloud Identity Service] (ECID) basieren, die die Aktivität von Kunden in allen [!DNL Experience Cloud]-Anwendungen verfolgen. Darüber hinaus können allgemeine persönliche Informationen wie eine E-Mail-Adresse oder Telefonnummer auch als gültige Identitätsdaten dienen.

Das Dokument zu [Identitätsdaten für Datenschutzanforderungen](./identity-data.md) enthält detailliertere Informationen zu den Identitätsinformationen, die für [!DNL Privacy Service] akzeptiert werden. Das Dokument bietet außerdem Anleitungen dazu, wie Adoben genutzt werden können, um die entsprechenden Identitätsinformationen von Ihren Kunden bei der Interaktion mit Ihrer Website effektiv abzurufen und diese Daten in API-Anforderungen an [!DNL Privacy Service] zu senden.

### Beginn, der Datenschutzanforderungen {#requests} stellt

Sobald Sie die Datenschutzanforderungen für Ihr Unternehmen festgelegt und entschieden haben, welche Identitätswerte an [!DNL Privacy Service] gesendet werden sollen, können Sie Beginn Datenschutzanforderungen stellen. [!DNL Privacy Service] ermöglicht Ihnen, Datenschutzanforderungen entweder über die API oder die Benutzeroberfläche zu senden.

>[!IMPORTANT]
>
>Die folgenden Abschnitte enthalten Links zur Dokumentation, in der beschrieben wird, wie allgemeine Datenschutzanforderungen in der API oder Benutzeroberfläche ausgeführt werden. Je nach den von Ihnen verwendeten [!DNL Experience Cloud]-Anwendungen können sich die Felder, die Sie in der Anforderungsnutzlast senden müssen, jedoch von den Beispielen in diesen Handbüchern unterscheiden.
>
>Wenn Sie die API- oder UI-Anleitungen befolgen, lesen Sie bitte das Dokument [Privacy Service- und Experience Cloud-Anwendungen](./experience-cloud-apps.md), um weitere Informationen zum Formatieren von Datenschutzanforderungen für Ihre bestimmte [!DNL Experience Cloud]-Anwendung(en) zu erhalten.
>
>Beachten Sie außerdem, dass Datenschutzanforderungen asynchron in allen Experience Cloud-Anwendungen verarbeitet werden. Sobald eine Anforderung beim Privacy Service eingegangen ist, kann die Bearbeitung der Anfrage innerhalb von Minuten und Wochen erfolgen. Der Zeitraum, der zum Abschließen der einzelnen Anforderungen benötigt wird, hängt von der Anwendung ab, mit der Sie arbeiten, und von der Menge der zu verarbeitenden Daten.

#### Verwenden der API

Die [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) stellt mehrere Endpunkte zum Erstellen und Verwalten von Datenschutzaufträgen mit RESTful-API-Aufrufen bereit, mit denen Sie die Einhaltung der Datenschutzregeln für Ihre [!DNL Experience Cloud]-Anwendungen programmgesteuert angehen können. Ausführliche Anweisungen zur Verwendung der API finden Sie im [API-Entwicklerhandbuch für Privacy Service](api/getting-started.md).

#### Verwenden der UI

>[!NOTE]
>
>Die Benutzeroberfläche [!DNL Privacy Service] unterstützt derzeit nur Zugriff- und Löschanforderungen. Alle Abmeldeanfragen müssen stattdessen über die API erfolgen.

Die [!DNL Privacy Service]-Benutzeroberfläche ermöglicht es Ihnen, Datenschutzaufträge mithilfe einer grafischen Oberfläche zu erstellen und zu überwachen. Die Benutzeroberfläche enthält ein Widget **[!UICONTROL Statusbericht]**, das den Status aller aktiven Anforderungen visuell darstellt und Ihnen das Erstellen neuer Anforderungen mithilfe des integrierten **[!UICONTROL Anforderungs-Builders]** oder durch Hochladen von JSON-Dateien ermöglicht. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md).

### Überwachen von Datenschutzaufträgen {#monitor}

Sobald Sie Datenschutzaufträge abgeschlossen haben, stehen Ihnen verschiedene Optionen zur Überwachung ihres Status und ihrer Ergebnisse zur Verfügung:

| Überwachungsmethode | Beschreibung |
| --- | --- |
| [!DNL Privacy Service] Benutzeroberfläche | Die [!DNL Privacy Service]-Benutzeroberfläche bietet ein Dashboard zur Überwachung, mit dem Sie eine visuelle Darstellung des Status aller aktiven Anforderungen Ansicht haben. Weitere Informationen finden Sie im Benutzerhandbuch [Privacy Service](ui/overview.md). |
| [!DNL Privacy Service] API | Sie können den Status von Datenschutzaufträgen programmgesteuert überwachen, indem Sie die von der API [!DNL Privacy Service] bereitgestellten Lookup-Endpunkte verwenden. Ausführliche Anweisungen zur Verwendung der API finden Sie im [Privacy Service-Entwicklerhandbuch](./api/getting-started.md). |
| [!DNL Privacy Events] | [!DNL Privacy Events] nutzen Sie Adobe I/O-Ereignis, die an einen konfigurierten WebHook gesendet werden, um eine effiziente Auftragsautomatisierung zu ermöglichen. Sie verringern oder beseitigen die Notwendigkeit, die [!DNL Privacy Service]-API abzufragen, um zu prüfen, ob ein Auftrag abgeschlossen ist oder ein bestimmter Meilenstein in einem Workflow erreicht wurde. Weitere Informationen finden Sie im Tutorial [zum Abonnieren von Privacy Ereignisses](./privacy-events.md). |

## Nächste Schritte

Dieses Dokument bietet einen Überblick über [!DNL Privacy Service] und die wichtigsten Schritte, die erforderlich sind, um Beginn mit den Dienstfunktionen zu ermöglichen. Weitere Informationen zu den verschiedenen Aspekten der Arbeit mit [!DNL Privacy Service] finden Sie in der Dokumentation, auf die Sie im gesamten Überblick verweisen.
