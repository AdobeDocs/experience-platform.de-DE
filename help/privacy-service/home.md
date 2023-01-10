---
keywords: Experience Platform;Home;beliebte Themen;DSGVO;dsgvo;ccpa:CCPA;PDPA;PDPA;PDPA_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Übersicht über Privacy Service
description: Mit Privacy Service können Sie die automatische Einhaltung gesetzlicher Datenschutzbestimmungen bei der Handhabung von Daten in Experience Cloud erleichtern.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 100%

---

# [!DNL Privacy Service] – Übersicht

Um eine bessere Kundenerfahrung zu bieten, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu überschauen und respektieren. Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen.

Adobe Experience Platform [!DNL Privacy Service] wurde als Reaktion auf eine grundlegende Änderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Der zentrale Zweck von [!DNL Privacy Service] ist die Automatisierung der Einhaltung von Datenschutzbestimmungen, die bei Verstößen zu erheblichen Geldbußen und Störungen des Datenbetriebs für Ihr Unternehmen führen können.

[!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung von Kundendatenanfragen unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugriff auf und Löschen von personenbezogenen oder vertraulichen Kundendaten aus Adobe Experience Cloud-Programmen stellen, was die automatische Einhaltung gesetzlicher und unternehmensinterner Datenschutzbestimmungen erleichtert.

## Erste Schritte mit [!DNL Privacy Service] {#getting-started}

Um [!DNL Privacy Service] nutzen zu können, müssen einige wichtige Entscheidungen getroffen werden, und zwar in Bezug auf die Datenschutzanforderungen Ihres Unternehmens, die Art der Identitätsdaten, die Sie von Ihren Kunden erfassen, und die beste Möglichkeit, Ihr CRM-System mit dem Service zu verbinden.

Diese Entscheidungen lassen sich anhand der folgenden Fragen zusammenfassen:

1. **Welche Informationen erfasse ich von meinen Kunden?**
   * Um [!DNL Privacy Service] optimal nutzen zu können, müssen Sie über ein detailliertes Verständnis der Datentypen verfügen, die Sie von Ihren Kunden erfassen, und wissen, welche davon den Datenschutzbestimmungen unterliegen. Weitere Informationen finden Sie im Abschnitt [Festlegen von Datenschutzanforderungen](#requirements).
1. **Habe ich meine Daten richtig gekennzeichnet?**
   * Die Daten müssen ordnungsgemäß gekennzeichnet werden, damit der Service feststellen kann, welche Felder während der Datenschutzaufträge aufgerufen oder gelöscht werden sollen. Weitere Informationen finden Sie im Abschnitt [Kennzeichnen von Daten](#label).
1. **Weiß ich, welche IDs ich an den [!DNL Privacy Service] senden soll?**
   * Beim Senden von Datenschutzanfragen müssen für bestimmte Adobe-Programme jeweils individuelle Kunden-IDs angegeben werden. Weitere Informationen finden Sie in den Abschnitten [Bereitstellen von Identitätsdaten](#identity) und [Erstellen von Datenschutzanfragen](#requests).
1. **Wie verfolge ich meine Datenschutzaufträge?**
   * Nachdem Sie Datenschutzanfragen gestellt haben, stehen Ihnen verschiedene Optionen zur Verfolgung ihrer Status und Ergebnisse zur Verfügung. Weitere Informationen finden Sie im Abschnitt [Überwachen von Datenschutzaufträgen](#monitor).

Die folgenden Abschnitte enthalten allgemeine Anleitungen zu diesen wichtigen Schritten sowie Links zu weiteren Dokumentationen zu [!DNL Privacy Service] mit weiteren Details.

### Bestimmen der Datenschutzanforderungen Ihres Unternehmens {#requirements}

Abhängig von der Art Ihres Unternehmens und den Gerichtsbarkeiten, unter denen es tätig ist, unterliegen Ihre Datenoperationen möglicherweise den gesetzlichen Datenschutzbestimmungen. Diese Bestimmungen geben Ihren Kunden oft das Recht, den Zugriff auf die von Ihnen gesammelten Daten anzufordern und die Löschung dieser gespeicherten Daten zu beantragen. Diese Kundenanfragen nach ihren persönlichen Daten werden in der Dokumentation als „Datenschutzanfragen“ bezeichnet.

Einzelheiten zu den verschiedenen gesetzlichen Datenschutzbestimmungen, die von [!DNL Privacy Service] für Anfragen verwendet werden, einschließlich Schlüsselbegriffe und Antworten auf häufig gestellte Fragen, finden Sie in der [Dokumentation zu Datenschutzbestimmungen](./regulations/overview.md).

Wenn Ihre Datenvorgänge unter eine der unterstützten Richtlinien fallen, lesen Sie die Dokumentation, um wichtige Informationen zu erhalten, etwa zu den spezifischen Datenschutzrechten, die Sie Ihren Kunden gewähren, und zu den korrekten Zeitfenstern für die Beantwortung von Datenschutzanfragen. Diese Informationen sollten bei der Entscheidung berücksichtigt werden, wie [!DNL Privacy Service] in Ihr CRM-System integriert werden soll und wie Kunden mit Ihrer Website interagieren sollten, um Datenschutzanfragen zu stellen.

Zusätzlich zu den gesetzlichen Bestimmungen sollten bei diesen Entscheidungen auch alle für Ihr Unternehmen geltenden Organisations- oder Branchenstandards berücksichtigt werden.

### Kennzeichnen von Daten für Datenschutzanfragen {#label}

Je nach den von Ihnen verwendeten [!DNL Experience Cloud]-Programmen müssen Sie die spezifischen Datenfelder kennzeichnen, auf die bei Datenschutzanfragen zugegriffen werden soll bzw. die gelöscht werden sollen. Das Verfahren zur Kennzeichnung von Daten ist je nach Programm unterschiedlich. Informationen zum Kennzeichnen von Daten für jedes unterstützte Adobe-Programm finden Sie im Dokument zu [Experience Cloud-Programmen](./experience-cloud-apps.md).

### Bestimmen Sie die Arten von Identitätsdaten, die an gesendet werden sollen [!DNL Privacy Service] {#identity}

Damit [!DNL Privacy Service] eine Datenschutzanfrage eines Kunden verarbeitet, muss in der Anfrage selbst mindestens ein eindeutiger Identitätswert für diesen Kunden angegeben werden. Ein eindeutiger Identitätswert ist jede Information, die zur Identifizierung einer einzelnen Person und ihrer gespeicherten persönlichen Daten in Ihren [!DNL Experience Cloud]-Datenspeichern verwendet werden kann. [!DNL Privacy Service] verwendet diese Identitätsinformationen, um die personenbezogenen Daten des Kunden entsprechend der Art der Anfrage zu finden und zu verarbeiten (Zugriff, Löschen oder Ausstieg).

Je nach den [!DNL Experience Cloud]-Programmen, die Ihr CRM-System verwendet, variieren der Typ und die Anzahl der Identitätswerte, die Sie für jeden Kunden angeben müssen. Einige Programme verwenden ihre eigenen internen Werte für Kunden-IDs (z. B. Adobe Target-IDs), während andere auf globalen IDs von Adobe [!DNL Experience Cloud Identity Service] (ECID) basieren, die die Aktivität von Kunden über alle [!DNL Experience Cloud]-Programme hinweg verfolgen. Darüber hinaus können auch allgemeine persönliche Informationen wie eine E-Mail-Adresse oder Telefonnummer als gültige Identitätsdaten dienen.

Das Dokument zu [Identitätsdaten für Datenschutzanfragen](./identity-data.md) enthält detailliertere Informationen zu den Arten von Identitätsinformationen, die für [!DNL Privacy Service] akzeptiert werden. Das Dokument bietet außerdem Anleitungen dazu, wie Adobe-Technologien genutzt werden können, um die entsprechenden Identitätsinformationen von Ihren Kunden bei der Interaktion mit Ihrer Website effektiv abzurufen und diese Daten in API-Anfragen an [!DNL Privacy Service] zu senden.

### Beginnen mit dem Stellen von Datenschutzanfragen {#requests}

Sobald Sie die Datenschutzanfragen für Ihr Unternehmen festgelegt und entschieden haben, welche Identitätswerte an den [!DNL Privacy Service] gesendet werden sollen, können Sie beginnen, Datenschutzanfragen zu stellen. [!DNL Privacy Service] ermöglicht Ihnen, Datenschutzanfragen entweder über die API oder über die Benutzeroberfläche zu senden.

>[!IMPORTANT]
>
>Die folgenden Abschnitte enthalten Links zur Dokumentation, in der beschrieben wird, wie allgemeine Datenschutzanfragen in der API oder Benutzeroberfläche ausgeführt werden. Je nach den von Ihnen verwendeten [!DNL Experience Cloud]-Programmen können sich jedoch die Felder, die Sie in der Anfrage-Payload senden müssen, von den Beispielen in diesen Anleitungen unterscheiden.
>
>Beim Folgen der API- oder UI-Anleitungen lesen Sie bitte das Dokument [Privacy Service- und Experience Cloud-Programme](./experience-cloud-apps.md), um weitere Informationen zum Formatieren von Datenschutzanfragen für Ihre speziellen [!DNL Experience Cloud]-Programme zu erhalten.
>
>Beachten Sie außerdem, dass Datenschutzanfragen asynchron über alle Experience Cloud-Programme hinweg verarbeitet werden. Wenn eine Anfrage bei Privacy Service eingegangen ist, kann die Bearbeitung der Anfrage innerhalb von Minuten erfolgen oder aber Wochen dauern. Der Zeitraum, der zum Abschließen der einzelnen Anfragen benötigt wird, hängt von dem Programm ab, mit dem Sie arbeiten, sowie von der Menge der zu verarbeitenden Daten.

#### Verwenden der API

Der [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) stellt mehrere Endpunkte zum Erstellen und Verwalten von Datenschutzaufträgen mit RESTful-API-Aufrufen bereit, mit denen Sie die Einhaltung der Datenschutzregeln für Ihre [!DNL Experience Cloud]-Programme programmgesteuert angehen können. Ausführliche Anweisungen zur Verwendung der API finden Sie im [API-Handbuch für Privacy Service](api/overview.md).

#### Verwenden der UI

>[!NOTE]
>
>Die Benutzeroberfläche von [!DNL Privacy Service] unterstützt derzeit nur Zugriffs- und Löschanforderungen. Alle Anfragen zum Ausstieg müssen über die API erfolgen.

Die [!DNL Privacy Service]-Benutzeroberfläche ermöglicht es Ihnen, Datenschutzaufträge mithilfe einer grafischen Oberfläche zu erstellen und zu überwachen. Die Benutzeroberfläche enthält ein Widget zum **[!UICONTROL Statusbericht]**, das den Status aller aktiven Anfragen visuell darstellt und Ihnen das Erstellen neuer Anfragen mithilfe des integrierten **[!UICONTROL Anfragen-Builders]** oder durch Hochladen von JSON-Dateien ermöglicht. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md).

### Überwachen von Datenschutzaufträgen {#monitor}

Sobald Sie Datenschutzaufträge abgeschlossen haben, stehen Ihnen verschiedene Optionen zur Überwachung ihrer Status und Ergebnisse zur Verfügung:

| Überwachungsmethode | Beschreibung |
| --- | --- |
| [!DNL Privacy Service] Benutzeroberfläche | Die Benutzeroberfläche von [!DNL Privacy Service] bietet ein Überwachungs-Dashboard, das Ihnen eine visuelle Darstellung des Status aller aktiven Anfragen zeigt. Weiterführende Informationen finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md). |
| [!DNL Privacy Service] API | Sie können den Status von Datenschutzaufträgen programmgesteuert überwachen, indem Sie die von der [!DNL Privacy Service]-API bereitgestellten Lookup-Endpunkte verwenden. Ausführliche Anweisungen zur Verwendung der API finden Sie im [Privacy Service-Entwicklerhandbuch](./api/overview.md). |
| [!DNL Privacy Events] | [!DNL Privacy Events] nutzt Adobe I/O Events, die an einen konfigurierten Webhook gesendet werden, um eine effiziente Auftragsautomatisierung zu ermöglichen. Sie verringern oder eliminieren die Notwendigkeit, die [!DNL Privacy Service]-API abzufragen, um zu prüfen, ob ein Auftrag abgeschlossen oder eine bestimmte Etappe in einem Workflow erreicht wurde. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Privacy Events](./privacy-events.md). |

## Nächste Schritte

Dieses Dokument bietet einen Überblick über den [!DNL Privacy Service] und die wichtigsten Schritte, die erforderlich sind, um mit der Nutzung der Funktionen des Service zu beginnen. Weitere Informationen zu den verschiedenen Aspekten der Arbeit mit [!DNL Privacy Service] finden Sie in den Dokumentationen, auf die wir Sie im Laufe dieses Überblicks immer wieder verweisen.
