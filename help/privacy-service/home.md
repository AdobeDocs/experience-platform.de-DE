---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datenschutzdienst für Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Übersicht über den Adobe Experience Platform-Datenschutzdienst

Um eine bessere Kundenerfahrung zu erzielen, müssen Sie die personenbezogenen Daten Ihrer Kunden erfassen und speichern. Bei der Verwendung dieser Daten ist es wichtig, die Privatsphäre Ihrer Kunden zu verstehen und zu respektieren. Die neuen gesetzlichen und organisatorischen Vorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten auf Anfrage aus Ihren Datenspeichern zuzugreifen oder sie zu löschen.

Der Datenschutzdienst für Adobe Experience Platform stellt eine RESTful-API und eine Benutzeroberfläche bereit, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit dem Datenschutzdienst können Sie Anfragen zum Zugriff auf und Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

## Warum der Datenschutzdienst?

Der Datenschutzdienst wurde als Reaktion auf eine grundlegende Änderung der Art und Weise entwickelt, wie Unternehmen die personenbezogenen Daten ihrer Kunden verwalten müssen. Der Zweck des Datenschutzdienstes ist es, die Einhaltung der Datenschutzbestimmungen zu automatisieren, die bei Verstößen zu hohen Geldbußen und zu Störungen des Datenbetriebs für Ihr Unternehmen führen können.

### Datenschutzdienst und GDPR

Mit der [Allgemeinen Datenschutzverordnung](https://eugdpr.org/) (GDPR) wurden mehrere neue Datenschutzrechte für Mitglieder der Europäischen Vereinigung eingeführt, darunter das **Recht auf Zugang** und das **Recht auf Vergessenwerden**. Das bedeutet, dass jeder EU-Bürger, dessen personenbezogene Daten von Ihrem Unternehmen gesammelt wurden, jederzeit den Zugriff auf seine Daten oder deren Löschung beantragen kann. Werden diese Anforderungen nicht innerhalb von 30 Tagen erfüllt, kann dies zu Geldstrafen in Höhe von mehreren Millionen Dollar für Ihr Unternehmen führen.

Der Datenschutzdienst unterstützt den Zugriff und das Löschen von Anforderungen für GDPR und verfolgt diese unabhängig von Anforderungen gemäß der CCPA-Verordnung. Weitere Informationen finden Sie in den häufig gestellten Fragen [zum](gdpr/faq.md) GDPR und in den [terminologischen](gdpr/terminology.md) Dokumenten.

### Datenschutzdienst und CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. Das CCPA bietet kalifornischen Einwohnern neue Datenschutzrechte, darunter das Recht auf Zugang zu ihren personenbezogenen Daten und deren Löschung, um zu erfahren, ob ihre personenbezogenen Daten verkauft oder offen gelegt werden (und an wen), sowie das Recht, ihre Daten an Dritte zu Opt-out.

Der Datenschutzdienst unterstützt den Zugriff und das Löschen von Anforderungen für die CCPA-Verordnung und verfolgt diese unabhängig von GDPR-Anforderungen. Der Datenschutzdienst unterstützt auch das Senden von Abmeldeanfragen für Experience Cloud-Anwendungen, die diese unterstützen. Weitere Informationen finden Sie in den häufig gestellten Fragen zum [CCPA](ccpa/faq.md) .

## Verwendung des Datenschutzdienstes zur Verwaltung von Datenschutzanfragen

Der Datenschutzdienst bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die Anfragen Ihrer Kunden zum Zugriff/Löschen ihrer privaten Daten oder zum Ausschluss vom Verkauf verwalten können (auch als **Datenschutzaufträge** bezeichnet). Der Dienst bietet außerdem einen zentralen Prüfungs- und Protokollierungsmechanismus, mit dem Sie den Status und die Ergebnisse von Datenschutzaufträgen in Experience Cloud-Anwendungen Ansicht haben.

>[!NOTE] Ausschlussanfragen werden derzeit nur von der Datenschutzdienst-API unterstützt.

### Verwenden der API

Mit der [Datenschutzdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) können Sie Datenschutzaufträge mithilfe von RESTful-API-Aufrufen erstellen und verwalten, um die Einhaltung der Datenschutzvorschriften für Ihre Experience Cloud-Anwendungen programmatisch anzugehen. Ausführliche Anweisungen zur Verwendung der API finden Sie im Entwicklerhandbuch für die API des [Datenschutzdienstes](api/getting-started.md).

### Verwenden der Benutzeroberfläche

Die Benutzeroberfläche des Datenschutzdienstes ermöglicht Ihnen, Datenschutzaufträge mithilfe einer grafischen Oberfläche zu erstellen und zu überwachen. Die Benutzeroberfläche enthält ein **Statusbericht** -Widget, das den Status aller aktiven Anforderungen visuell darstellt und Ihnen das Erstellen neuer Anforderungen mithilfe des integrierten **Anforderungs-Builders** oder durch Hochladen von JSON-Dateien ermöglicht. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie im Benutzerhandbuch zum [Datenschutzdienst](ui/overview.md).