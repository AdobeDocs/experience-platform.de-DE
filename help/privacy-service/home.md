---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---


# Übersicht über Adobe Experience Platform Privacy Service

Um eine bessere Kundenerfahrung zu erzielen, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu verstehen und zu respektieren. Die neuen gesetzlichen und organisatorischen Vorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten auf Anfrage aus Ihren Datenspeichern zuzugreifen oder sie zu löschen.

Adobe Experience Platform Privacy Service bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Datenanforderungen von Ihren Kunden unterstützen. Mit Privacy Service können Sie Anfragen zum Zugriff auf und Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

## Warum Privacy Service?

Privacy Service wurde als Reaktion auf eine grundlegende Veränderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Der Hauptzweck von Privacy Service ist die Automatisierung der Einhaltung von Datenschutzbestimmungen, die bei Verstößen zu hohen Geldbußen führen und den Datenbetrieb für Ihr Unternehmen stören können.

### Privacy Service und GDPR

Mit der [](https://eugdpr.org/)Datenschutz-Grundverordnung (DSGVO) wurden mehrere neue Datenschutzrechte für Mitglieder der Europäischen Union eingeführt, darunter das **Recht auf Zugriff** und das **Recht auf Vergessenwerden**. Dies bedeutet, dass jeder EU-Bürger, dessen personenbezogene Daten von Ihrem Unternehmen erfasst wurden, jederzeit den Zugriff auf oder die Löschung seiner Daten beantragen kann. Werden diese Anforderungen nicht innerhalb von 30 Tagen erfüllt, kann dies zu Geldstrafen in Höhe von mehreren Millionen Dollar für Ihr Unternehmen führen.

Privacy Service unterstützt den Zugriff und das Löschen von Anforderungen für GDPR und verfolgt diese unabhängig von Anforderungen gemäß der CCPA-Verordnung. Weitere Informationen finden Sie in den häufig gestellten Fragen [zum](gdpr/faq.md) GDPR und in den [terminologischen](gdpr/terminology.md) Dokumenten.

### Privacy Service und CPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. Das CCPA bietet kalifornischen Einwohnern neue Datenschutzrechte, darunter das Recht auf Zugang zu ihren personenbezogenen Daten und deren Löschung, um zu erfahren, ob ihre personenbezogenen Daten verkauft oder offen gelegt werden (und an wen), sowie das Recht, ihre Daten an Dritte zu Opt-out.

Privacy Service unterstützt den Zugriff und das Löschen von Anforderungen für die CCPA-Verordnung und verfolgt diese unabhängig von GDPR-Anforderungen. Privacy Service unterstützt auch das Senden von Ausschlussanfragen für Experience Cloud-Anwendungen, die diese unterstützen. Weitere Informationen finden Sie in den häufig gestellten Fragen zum [CCPA](ccpa/faq.md) .

## Verwendung von Privacy Service zur Verwaltung von Datenschutzanforderungen

Privacy Service bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die Anfragen Ihrer Kunden zum Zugriff/Löschen ihrer privaten Daten oder zum Ausschluss vom Verkauf verwalten können (auch als **Datenschutzaufträge** bezeichnet). Der Dienst bietet außerdem einen zentralen Audit- und Protokollierungsmechanismus, mit dem Sie den Status und die Ergebnisse von Datenschutzaufträgen, die Experience Cloud-Anwendungen betreffen, Ansicht haben können.

>[!NOTE]
>
>Ausschluss-Anfragen werden derzeit nur von der Privacy Service-API unterstützt.

### Verwenden der API

Mit der [Privacy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) können Sie Datenschutzaufträge mithilfe von RESTful-API-Aufrufen erstellen und verwalten. So können Sie die Einhaltung der Datenschutzvorschriften für Ihre Experience Cloud-Anwendungen programmatisch angehen. Ausführliche Anweisungen zur Verwendung der API finden Sie im Entwicklerhandbuch für die [Privacy Service-API](api/getting-started.md).

### Verwenden der Benutzeroberfläche

Die Benutzeroberfläche des Privacy Service ermöglicht Ihnen, Datenschutzaufträge über eine grafische Benutzeroberfläche zu erstellen und zu überwachen. Die Benutzeroberfläche enthält ein **Statusbericht** -Widget, das den Status aller aktiven Anforderungen visuell darstellt und Ihnen das Erstellen neuer Anforderungen mithilfe des integrierten **Anforderungs-Builders** oder durch Hochladen von JSON-Dateien ermöglicht. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/overview.md).