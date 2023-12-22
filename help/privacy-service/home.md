---
keywords: Experience Platform;Home;beliebte Themen;DSGVO;dsgvo;ccpa:CCPA;PDPA;PDPA;PDPA_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Übersicht über Privacy Service
description: Erfahren Sie, wie Privacy Service die automatische Einhaltung gesetzlicher Datenschutzbestimmungen bei Ihren Experience Cloud-Datenvorgängen erleichtern kann.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 19b33ddf2fc3f8d889d370eedfc732ac54178dcd
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 46%

---

# Übersicht über Privacy Service

Um bessere Kundenerlebnisse zu bieten, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu überschauen und respektieren. Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen.

Adobe Experience Platform Privacy Service wurde als Reaktion auf eine grundlegende Änderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Privacy Service hat in erster Linie die Aufgabe, die Einhaltung von Datenschutzbestimmungen zu automatisieren, die bei Verstößen zu hohen Geldbußen führen und den Datenbetrieb für Ihr Unternehmen stören können.

Privacy Service bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie Kundendatenanfragen verwalten können. Mit Privacy Service können Sie Anfragen zum Zugriff auf und zur Löschung personenbezogener Kundendaten aus Adobe Experience Cloud-Anwendungen einreichen, um die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen zu erleichtern.

>[!IMPORTANT]
>
>Privacy Service ist nur für Anfragen der betroffenen Person und für Verbraucherrechtsanfragen vorgesehen. Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig. Adobe ist gesetzlich verpflichtet, diese rechtzeitig zu erfüllen. Daher sind Lasttests auf Privacy Service nicht zulässig, da es sich um eine reine Produktionsumgebung handelt und ein unnötiger Rückstand gültiger Datenschutzanfragen erzeugt wird.
>
>Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern. Für Benutzende, bei denen ein Missbrauch des Systems festgestellt wurde, wird der Zugriff auf den Dienst deaktiviert. Anschließend wird mit ihnen ein Meeting abgehalten, bei dem ihr Handeln und die akzeptable Verwendung von Privacy Service erörtert wird.

## Erste Schritte mit Privacy Service {#getting-started}

Um den Privacy Service optimal zu nutzen, müssen bezüglich der Datenschutzanforderungen Ihres Unternehmens, der Art der von Ihnen erfassten Identitätsdaten und der besten Möglichkeit, Ihr CRM-System mit dem Dienst zu verbinden, mehrere wichtige Entscheidungen getroffen werden.

Diese Entscheidungen lassen sich anhand der folgenden Fragen zusammenfassen:

1. **Welche Informationen erfasse ich von meinen Kunden?**
   * Um Privacy Service optimal zu nutzen, müssen Sie über ein detailliertes Verständnis der von Ihnen von Ihren Kunden erfassten Datentypen und der Art der Daten verfügen, die den Datenschutzbestimmungen unterliegen. Weitere Informationen finden Sie im Abschnitt [Festlegen von Datenschutzanforderungen](#requirements).
1. **Habe ich meine Daten richtig gekennzeichnet?**
   * Die Daten müssen für den Dienst ordnungsgemäß beschriftet sein, um zu bestimmen, welche Felder während Datenschutzaufträgen aufgerufen oder gelöscht werden sollen. Siehe Abschnitt zu [Kennzeichnungsdaten](#label) für weitere Informationen.
1. **Weiß ich, welche IDs an Privacy Service gesendet werden sollen?**
   * Beim Senden von Datenschutzanfragen müssen für bestimmte Adobe-Programme jeweils individuelle Kunden-IDs angegeben werden. Weitere Informationen finden Sie in den Abschnitten [Bereitstellen von Identitätsdaten](#identity) und [Erstellen von Datenschutzanfragen](#requests).
1. **Wie verfolge ich meine Datenschutzaufträge?**
   * Nachdem Sie Datenschutzanfragen gestellt haben, stehen Ihnen verschiedene Optionen zur Verfolgung ihrer Status und Ergebnisse zur Verfügung. Weitere Informationen finden Sie im Abschnitt [Überwachen von Datenschutzaufträgen](#monitor).

Die folgenden Abschnitte enthalten allgemeine Anleitungen zu diesen wichtigen erforderlichen Schritten sowie Links zur weiteren Privacy Service-Dokumentation, um weitere Informationen zu erhalten.

### Bestimmen der Datenschutzanforderungen Ihres Unternehmens {#requirements}

Abhängig von der Art Ihres Unternehmens und den Gerichtsbarkeiten, unter denen es tätig ist, unterliegen Ihre Datenoperationen möglicherweise den gesetzlichen Datenschutzbestimmungen. Diese Bestimmungen geben Ihren Kunden oft das Recht, den Zugriff auf die von Ihnen gesammelten Daten anzufordern und die Löschung dieser gespeicherten Daten zu beantragen. Diese Kundenanfragen nach ihren persönlichen Daten werden in der Dokumentation als „Datenschutzanfragen“ bezeichnet.

Einzelheiten zu den verschiedenen gesetzlichen Datenschutzbestimmungen, nach denen Privacy Service Anfragen verwaltet, einschließlich Schlüsselbegriffen und Antworten auf häufig gestellte Fragen, finden Sie im Abschnitt [Dokumentation zu Datenschutzbestimmungen](./regulations/overview.md).

Wenn Ihre Datenvorgänge unter eine der unterstützten Richtlinien fallen, lesen Sie die Dokumentation, um wichtige Informationen zu erhalten, etwa zu den spezifischen Datenschutzrechten, die Sie Ihren Kunden gewähren, und zu den korrekten Zeitfenstern für die Beantwortung von Datenschutzanfragen. Diese Informationen sollten bei der Entscheidung berücksichtigt werden, wie Privacy Service in Ihr CRM-System integriert werden kann und wie Kunden mit Ihrer Website interagieren sollten, um Datenschutzanfragen zu stellen.

Zusätzlich zu den gesetzlichen Bestimmungen sollten bei diesen Entscheidungen auch alle für Ihr Unternehmen geltenden Organisations- oder Branchenstandards berücksichtigt werden.

### Kennzeichnen von Daten für Datenschutzanfragen {#label}

Je nach den von Ihnen verwendeten [!DNL Experience Cloud]-Programmen müssen Sie die spezifischen Datenfelder kennzeichnen, auf die bei Datenschutzanfragen zugegriffen werden soll bzw. die gelöscht werden sollen. Der Prozess für die Kennzeichnung von Daten ist je nach Anwendung unterschiedlich. Informationen zum Kennzeichnen von Daten für jedes unterstützte Adobe-Programm finden Sie im Dokument zu [Experience Cloud-Programmen](./experience-cloud-apps.md).

### Bestimmen der Arten von Identitätsdaten, die an den Privacy Service gesendet werden {#identity}

Damit der Privacy Service eine Datenschutzanfrage eines Kunden verarbeiten kann, muss in der Anfrage selbst mindestens ein eindeutiger Identitätswert für diesen Kunden angegeben werden. Ein eindeutiger Identitätswert ist jede Information, die zur Identifizierung einer einzelnen Person und ihrer gespeicherten persönlichen Daten in Ihren [!DNL Experience Cloud]-Datenspeichern verwendet werden kann. Privacy Service verwendet diese Identitätsinformationen, um die personenbezogenen Daten des Kunden entsprechend der Art der Anforderung zu lokalisieren und zu verarbeiten (Zugriff, Löschen oder Opt-out).

Je nach [!DNL Experience Cloud] Anwendungen, die Ihr CRM-System verwendet, variieren der Typ und die Anzahl der Identitätswerte, die Sie für jeden Kunden angeben müssen. Einige Anwendungen verwenden ihre eigenen internen Kunden-ID-Werte (z. B. Adobe Target IDs), während andere Lösungen auf globale IDs von Adobe basieren [!DNL Experience Cloud Identity Service] (ECID), die die Kundenaktivität über alle [!DNL Experience Cloud] Anwendungen. Darüber hinaus können auch allgemeine persönliche Informationen wie eine E-Mail-Adresse oder Telefonnummer als gültige Identitätsdaten dienen.

Lesen Sie das Dokument unter [Identitätsdaten für Datenschutzanfragen](./identity-data.md) für detailliertere Informationen über die Arten von Identitätsinformationen, die für den Privacy Service akzeptiert werden. Das Dokument enthält außerdem Anleitungen zur Anwendung von Adobe-Technologien, um die entsprechenden Identitätsinformationen von Ihren Kunden bei der Interaktion mit Ihrer Website effektiv abzurufen und diese Daten in API-Anfragen an den Privacy Service zu senden.

### Beginnen mit dem Stellen von Datenschutzanfragen {#requests}

Sobald Sie die Datenschutzanforderungen Ihres Unternehmens ermittelt und entschieden haben, welche Identitätswerte an Privacy Service gesendet werden, können Sie mit Datenschutzanfragen beginnen. Verwenden Sie Privacy Service, um Datenschutzanfragen entweder über die API oder die Benutzeroberfläche zu senden.

>[!IMPORTANT]
>
>Die folgenden Abschnitte enthalten Links zur Dokumentation, in der beschrieben wird, wie allgemeine Datenschutzanfragen in der API oder Benutzeroberfläche ausgeführt werden. Je nach den von Ihnen verwendeten [!DNL Experience Cloud]-Programmen können sich jedoch die Felder, die Sie in der Anfrage-Payload senden müssen, von den Beispielen in diesen Anleitungen unterscheiden.
>
>Wenn Sie die API- oder Benutzeroberflächen-Handbücher befolgen, lesen Sie das Dokument unter [Privacy Service- und Experience Cloud-Anwendungen](./experience-cloud-apps.md) für weitere Dokumentationen zum Formatieren von Datenschutzanfragen für Ihr bestimmtes [!DNL Experience Cloud] Anwendungen.
>
>Beachten Sie außerdem, dass Datenschutzanfragen asynchron über alle Experience Cloud-Programme hinweg verarbeitet werden. Wenn eine Anfrage bei Privacy Service eingegangen ist, kann die Bearbeitung der Anfrage innerhalb von Minuten erfolgen oder aber Wochen dauern. Der Zeitraum, der zum Abschließen der einzelnen Anfragen benötigt wird, hängt von dem Programm ab, mit dem Sie arbeiten, sowie von der Menge der zu verarbeitenden Daten.

#### Verwenden der API {#api}

So wenden Sie sich programmatisch an die Einhaltung der Datenschutzbestimmungen für Ihre [!DNL Experience Cloud] -Anwendungen verwenden, können Sie RESTful-API-Aufrufe für [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) Endpunkte zum Erstellen und Verwalten von Datenschutzaufträgen. Ausführliche Anweisungen zur Verwendung der API finden Sie im [API-Handbuch für Privacy Service](api/overview.md).

#### Verwenden der Benutzeroberfläche {#ui}

>[!NOTE]
>
>Die Privacy Service-Benutzeroberfläche unterstützt derzeit nur Zugriffs- und Löschanfragen. Alle Anfragen zum Ausstieg müssen über die API erfolgen.

Sie können Datenschutzaufträge über eine grafische Benutzeroberfläche mit der Privacy Service-Benutzeroberfläche erstellen und überwachen. Die Benutzeroberfläche umfasst eine **[!UICONTROL Statusbericht]** Widget, das eine visuelle Darstellung des Status aller aktiven Anforderungen bereitstellt und mit der integrierten **[!UICONTROL Request Builder]** oder durch Hochladen von JSON-Dateien. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md).

### Überwachen von Datenschutzaufträgen {#monitor}

Sobald Sie Datenschutzaufträge abgeschlossen haben, stehen Ihnen verschiedene Optionen zur Überwachung ihrer Status und Ergebnisse zur Verfügung:

| Überwachungsmethode | Beschreibung |
| --- | --- |
| Privacy Service-Benutzeroberfläche | Mit dem Monitoring-Dashboard der Privacy Service-Benutzeroberfläche können Sie eine visuelle Darstellung des Status aller aktiven Anforderungen anzeigen. Weiterführende Informationen finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md). |
| Privacy Service-API | Sie können den Status von Datenschutzaufträgen programmgesteuert überwachen, indem Sie die von der Privacy Service-API bereitgestellten Lookup-Endpunkte verwenden. Ausführliche Anweisungen zur Verwendung der API finden Sie im [Privacy Service-Entwicklerhandbuch](./api/overview.md). |
| [!DNL Privacy Events] | [!DNL Privacy Events] Verwenden Sie Adobe I/O-Ereignisse, die an einen konfigurierten Webhook gesendet werden, um eine effiziente Automatisierung von Auftragsanfragen zu ermöglichen. Sie verringern oder eliminieren die Notwendigkeit, die Privacy Service-API abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen ist oder ob ein bestimmter Meilenstein innerhalb eines Workflows erreicht wurde. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Privacy Events](./privacy-events.md). |

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick über den Privacy Service und die wichtigsten Schritte, die zur Nutzung der Funktionen des Dienstes erforderlich sind. Detaillierte Informationen zu den verschiedenen Aspekten der Arbeit mit Privacy Service finden Sie in der Dokumentation, die im gesamten Überblick verknüpft ist.
