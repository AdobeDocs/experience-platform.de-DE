---
keywords: Experience Platform;Home;beliebte Themen;DSGVO;dsgvo;ccpa:CCPA;PDPA;PDPA;PDPA_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Übersicht über Privacy Service
description: Erfahren Sie, wie Privacy Service die automatische Einhaltung gesetzlicher Datenschutzbestimmungen bei Experience Cloud-Datenvorgängen erleichtern kann.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 61a5b4fd7af68e7379b456ddd37218d183e76256
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 43%

---

# Übersicht über Privacy Service

Um ein besseres Kundenerlebnis zu bieten, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu überschauen und respektieren. Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen.

Adobe Experience Platform Privacy Service wurde als Reaktion auf eine grundlegende Änderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Der Hauptzweck von Privacy Service ist die Automatisierung der Einhaltung von Datenschutzbestimmungen, die bei Verstößen zu erheblichen Geldbußen und Störungen des Datenbetriebs für Ihr Unternehmen führen können.

Privacy Service bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung von Kundendatenanfragen unterstützen. Sie können Privacy Service verwenden, um Anfragen zum Zugriff auf und Löschen von personenbezogenen oder vertraulichen Kundendaten aus Adobe Experience Cloud-Programmen zu stellen, was die automatische Einhaltung gesetzlicher und unternehmensinterner Datenschutzbestimmungen erleichtert.

>[!IMPORTANT]
>
>Privacy Service ist nur für Anfragen der betroffenen Person und für Verbraucherrechtsanfragen vorgesehen. Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig. Adobe ist gesetzlich verpflichtet, diese rechtzeitig zu erfüllen. Daher sind Lasttests auf Privacy Service nicht zulässig, da es sich um eine reine Produktionsumgebung handelt und ein unnötiger Rückstand gültiger Datenschutzanfragen erzeugt wird.
>
>Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern. Für Benutzende, bei denen ein Missbrauch des Systems festgestellt wurde, wird der Zugriff auf den Dienst deaktiviert. Anschließend wird mit ihnen ein Meeting abgehalten, bei dem ihr Handeln und die akzeptable Verwendung von Privacy Service erörtert wird.

## Erste Schritte mit Privacy Service {#getting-started}

Um Privacy Service optimal zu nutzen, müssen einige wichtige Entscheidungen getroffen werden, und zwar in Bezug auf die Datenschutzanforderungen Ihres Unternehmens, die Art der Identitätsdaten, die Sie von Ihren Kunden erfassen, und die beste Möglichkeit, Ihr CRM-System mit dem Service zu verbinden.

Diese Entscheidungen lassen sich anhand der folgenden Fragen zusammenfassen:

1. **Welche Informationen erfasse ich von meinen Kunden?**
   * Um Privacy Service optimal nutzen zu können, müssen Sie über ein detailliertes Verständnis der Datentypen verfügen, die Sie von Ihren Kunden erfassen, und wissen, welche davon den Datenschutzbestimmungen unterliegen. Weitere Informationen finden Sie im Abschnitt [Festlegen von Datenschutzanforderungen](#requirements).
1. **Habe ich meine Daten richtig gekennzeichnet?**
   * Daten müssen für den Service ordnungsgemäß gekennzeichnet sein, um zu bestimmen, auf welche Felder während Datenschutzaufträgen zugegriffen werden soll oder welche gelöscht werden sollen. Weitere Informationen finden Sie im Abschnitt [Kennzeichnen von ](#label)&quot;.
1. **Weiß ich, welche IDs ich an den Privacy Service senden soll?**
   * Beim Senden von Datenschutzanfragen müssen für bestimmte Adobe-Programme jeweils individuelle Kunden-IDs angegeben werden. Weitere Informationen finden Sie in den Abschnitten [Bereitstellen von Identitätsdaten](#identity) und [Erstellen von Datenschutzanfragen](#requests).
1. **Wie verfolge ich meine Datenschutzaufträge?**
   * Nachdem Sie Datenschutzanfragen gestellt haben, stehen Ihnen verschiedene Optionen zur Verfolgung ihrer Status und Ergebnisse zur Verfügung. Weitere Informationen finden Sie im Abschnitt [Überwachen von Datenschutzaufträgen](#monitor).

Die folgenden Abschnitte enthalten allgemeine Anleitungen zu diesen wichtigen Schritten sowie Links zu weiteren Privacy Service-Dokumentationen mit weiteren Details.

### Bestimmen der Datenschutzanforderungen Ihres Unternehmens {#requirements}

Abhängig von der Art Ihres Unternehmens und den Gerichtsbarkeiten, unter denen es tätig ist, unterliegen Ihre Datenoperationen möglicherweise den gesetzlichen Datenschutzbestimmungen. Diese Bestimmungen geben Ihren Kunden oft das Recht, den Zugriff auf die von Ihnen gesammelten Daten anzufordern und die Löschung dieser gespeicherten Daten zu beantragen. Diese Kundenanfragen nach ihren persönlichen Daten werden in der Dokumentation als „Datenschutzanfragen“ bezeichnet.

Einzelheiten zu den verschiedenen gesetzlichen Datenschutzbestimmungen, die von Privacy Service für Anfragen verwendet werden, einschließlich Schlüsselbegriffe und Antworten auf häufig gestellte Fragen, finden Sie in der [Dokumentation zu Datenschutzbestimmungen](./regulations/overview.md).

Wenn Ihre Datenvorgänge unter eine der unterstützten Richtlinien fallen, lesen Sie die Dokumentation, um wichtige Informationen zu erhalten, etwa zu den spezifischen Datenschutzrechten, die Sie Ihren Kunden gewähren, und zu den korrekten Zeitfenstern für die Beantwortung von Datenschutzanfragen. Diese Informationen sollten bei der Entscheidung berücksichtigt werden, wie Privacy Service in Ihr CRM-System integriert werden soll und wie Kunden mit Ihrer Website interagieren sollten, um Datenschutzanfragen zu stellen.

Zusätzlich zu den gesetzlichen Bestimmungen sollten bei diesen Entscheidungen auch alle für Ihr Unternehmen geltenden Organisations- oder Branchenstandards berücksichtigt werden.

### Kennzeichnen von Daten für Datenschutzanfragen {#label}

Je nach den von Ihnen verwendeten [!DNL Experience Cloud]-Programmen müssen Sie die spezifischen Datenfelder kennzeichnen, auf die bei Datenschutzanfragen zugegriffen werden soll bzw. die gelöscht werden sollen. Das Verfahren zur Kennzeichnung von Daten ist je nach Anwendung unterschiedlich. Informationen zum Kennzeichnen von Daten für jedes unterstützte Adobe-Programm finden Sie im Dokument zu [Experience Cloud-Programmen](./experience-cloud-apps.md).

### Bestimmen Sie die Arten von Identitätsdaten, die an den Privacy Service gesendet werden sollen {#identity}

Damit Privacy Service eine Datenschutzanfrage eines Kunden verarbeiten kann, muss in der Anfrage selbst mindestens ein eindeutiger Identitätswert für diesen Kunden angegeben werden. Ein eindeutiger Identitätswert ist jede Information, die zur Identifizierung einer einzelnen Person und ihrer gespeicherten persönlichen Daten in Ihren [!DNL Experience Cloud]-Datenspeichern verwendet werden kann. Der Privacy Service verwendet diese Identitätsinformationen, um die personenbezogenen Daten des Kunden entsprechend der Art der Anfrage zu finden und zu verarbeiten (Zugriff, Löschen oder Opt-out).

Je nach den [!DNL Experience Cloud] Anwendungen, die Ihr CRM-System verwendet, variieren der Typ und die Anzahl der Identitätswerte, die Sie für jeden Kunden angeben müssen. Einige Programme verwenden ihre eigenen internen Werte für Kunden-IDs (z. B. Adobe Target-IDs), während andere auf globalen IDs von Adobe [!DNL Experience Cloud Identity Service] (ECID) basieren, die die Kundenaktivität in allen [!DNL Experience Cloud]-Programmen verfolgen. Darüber hinaus können auch allgemeine persönliche Informationen wie eine E-Mail-Adresse oder Telefonnummer als gültige Identitätsdaten dienen.

Lesen Sie das Dokument unter [Identitätsdaten für Datenschutzanfragen](./identity-data.md) für detailliertere Informationen zu den Arten von Identitätsinformationen, die für den Privacy Service akzeptiert werden. Das Dokument bietet außerdem Anleitungen dazu, wie Adobe-Technologien angewendet werden können, um die entsprechenden Identitätsinformationen von Ihren Kunden bei der Interaktion mit Ihrer Website effektiv abzurufen und diese Daten in API-Anfragen an den Privacy Service zu senden.

### Beginnen mit dem Stellen von Datenschutzanfragen {#requests}

Sobald Sie die Datenschutzanfragen für Ihr Unternehmen festgelegt und entschieden haben, welche Identitätswerte an den Privacy Service gesendet werden sollen, können Sie beginnen, Datenschutzanfragen zu stellen. Verwenden Sie den -Privacy Service, um Datenschutzanfragen entweder über die API oder die Benutzeroberfläche zu senden.

#### Zugriff auf Details der Anfragedatei {#access-requests}

Als Antwort auf eine erfolgreiche Zugriffsanfrage gibt es eine **Download-URL** die mehrere Dateien enthält. Für jede Adobe-Anwendung, für die Daten angefordert wurden, wird eine Datei bereitgestellt. Beachten Sie, dass das Dateiformat für jede Anwendung je nach Datenstruktur der Anwendung unterschiedlich sein kann.

#### Löschanfragen - Keine Download-URL {#delete-requests}

In **Antwort für eine** Löschanfrage **gibt es keine Download-URL** da keine Kundendaten abgerufen werden.

>[!IMPORTANT]
>
>Die folgenden Abschnitte enthalten Links zur Dokumentation, in der beschrieben wird, wie allgemeine Datenschutzanfragen in der API oder Benutzeroberfläche ausgeführt werden. Je nach den von Ihnen verwendeten [!DNL Experience Cloud]-Programmen können sich jedoch die Felder, die Sie in der Anfrage-Payload senden müssen, von den Beispielen in diesen Anleitungen unterscheiden.
>
>Beim Folgen der API- oder UI-Anleitungen lesen Sie das Dokument zu [Privacy Service- und Experience Cloud-Anwendungen](./experience-cloud-apps.md) um weitere Informationen zum Formatieren von Datenschutzanfragen für Ihre speziellen [!DNL Experience Cloud]-Anwendungen zu erhalten.
>
>Beachten Sie außerdem, dass Datenschutzanfragen asynchron über alle Experience Cloud-Programme hinweg verarbeitet werden. Wenn eine Anfrage bei Privacy Service eingegangen ist, kann die Bearbeitung der Anfrage innerhalb von Minuten erfolgen oder aber Wochen dauern. Der Zeitraum, der zum Abschließen der einzelnen Anfragen benötigt wird, hängt von dem Programm ab, mit dem Sie arbeiten, sowie von der Menge der zu verarbeitenden Daten.

#### Verwenden der API {#api}

Um die Einhaltung der Datenschutzregeln für Ihre [!DNL Experience Cloud]-Programme programmgesteuert anzugehen, können Sie RESTful-API-Aufrufe an [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/)-Endpunkte verwenden, um Datenschutzaufträge zu erstellen und zu verwalten. Ausführliche Anweisungen zur Verwendung der API finden Sie im [API-Handbuch für Privacy Service](api/overview.md).

#### Verwenden der Benutzeroberfläche {#ui}

>[!NOTE]
>
>Die Privacy Service-Benutzeroberfläche unterstützt derzeit nur Zugriffs- und Löschanfragen. Alle Anfragen zum Ausstieg müssen über die API erfolgen.

Sie können Datenschutzaufträge über eine grafische Oberfläche mit der Privacy Service-Benutzeroberfläche erstellen und überwachen. Die Benutzeroberfläche enthält ein **[!UICONTROL Statusbericht]**-Widget, das den Status aller aktiven Anfragen visuell darstellt. Sie können Anfragen mit dem integrierten **[!UICONTROL Request Builder“]** Hochladen von JSON-Dateien erstellen. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md).

### Überwachen von Datenschutzaufträgen {#monitor}

Sobald Sie Datenschutzaufträge abgeschlossen haben, stehen Ihnen verschiedene Optionen zur Überwachung ihrer Status und Ergebnisse zur Verfügung:

| Überwachungsmethode | Beschreibung |
| --- | --- |
| Privacy Service-Benutzeroberfläche | Sie können eine visuelle Darstellung des Status aller aktiven Anfragen mit dem Überwachungs-Dashboard der Privacy Service-Benutzeroberfläche anzeigen. Weiterführende Informationen finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md). |
| Privacy Service-API | Sie können den Status von Datenschutzaufträgen programmgesteuert überwachen, indem Sie die von der Privacy Service-API bereitgestellten Lookup-Endpunkte verwenden. Ausführliche Anweisungen zur Verwendung der API finden Sie im [Privacy Service-Entwicklerhandbuch](./api/overview.md). |
| [!DNL Privacy Events] | [!DNL Privacy Events] verwenden Adobe I/O-Ereignisse, die an einen konfigurierten Webhook gesendet werden, um eine effiziente Auftragsautomatisierung zu ermöglichen. Sie verringern oder eliminieren die Notwendigkeit, die Privacy Service-API abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen oder eine bestimmte Etappe in einem Workflow erreicht wurde. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Privacy Events](./privacy-events.md). |

#### Antworten für nicht vorhandene Benutzer {#non-existing-users}

Wenn Sie eine Zugriffs- oder Löschanfrage senden, gibt die Antwort bei erfolgreichem Aufruf immer eine `success` zurück, auch wenn die Benutzerdaten nicht gefunden wurden. Das bedeutet, dass ein Zugriff oder eine Löschung auch dann erfolgreich abgeschlossen werden kann, wenn die Daten nicht vorhanden sind, ohne dass Daten abgerufen oder gelöscht werden.

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick über den Privacy Service und die wichtigsten Schritte, die erforderlich sind, um mit der Nutzung der Funktionen des Service zu beginnen. Weitere Informationen zu den verschiedenen Aspekten der Arbeit mit Privacy Service finden Sie in den Dokumentationen, auf die wir Sie im Laufe dieses Überblicks immer wieder verweisen.
