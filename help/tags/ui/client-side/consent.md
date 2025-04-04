---
title: Bereitstellung von JavaScript-Tags zur Verwaltung des Einverständnisses von Kunden
description: Erfahren Sie, wie Sie die Opt-in- und Opt-out-Signale von Kunden für verschiedene Adobe-Lösungen in Adobe Experience Platform verwalten.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 94%

---

# Bereitstellung von JavaScript-Tags zur Verwaltung des Einverständnisses von Kunden

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Rechtliche Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) erfordern, dass Unternehmen in der Lage sind, die Einwilligung ihrer Benutzer zu verwalten. Adobe-Kunden können von Besuchern verlangen, dass sie sich anmelden, bevor Adobe-Lösungen für den jeweiligen Besucher ausgeführt werden können. Besucher sollten die Möglichkeit erhalten, ihre Opt-in- und Opt-out-Status selbst zu verwalten.

Adobe Experience Cloud-Kunden benötigen eine Vielzahl von Implementierungen dieser Anforderungen. Manche verwenden externe Einwilligungsmanager, andere bauen eigene auf.

Entwickler von Adobe Experience Platform-Erweiterungen verwenden Erweiterungen und den Regel-Builder, um Opt-In- und Opt-Out-Lösungen zu definieren.

In diesem Dokument erfahren Sie, wie Sie verhindern können, dass Adobe-Tags ausgelöst werden, bevor die Einwilligung erfolgt.

## Advertising Cloud

Adobe Experience Platform löst [!DNL Advertising Cloud] nicht automatisch aus. [!DNL Advertising Cloud] wird nur ausgelöst, wenn Sie dies in einer Regelaktion speziell festlegen. Bestimmen Sie mithilfe der Regelbedingungen, was wann ausgelöst werden soll. Wenn Sie beispielsweise Cookies zur Bestimmung des Anmeldestatus verwenden möchten, legen Sie ein Datenelement fest, das dieses Cookie ausliest, und verwenden Sie es in der Regel als Bedingung, um zu bestimmen, wann die erste „Konversionen verfolgen“-Aktion ausgelöst werden soll.

Integrationen mit Zustimmungsmanagern (wie OneTrust) können die Zustimmungscookies für Kunden festlegen und verfolgen. Diese können dann im Regel-Builder verwendet werden.

## Analytics

Vergewissern Sie sich im Abschnitt „Linktracking“ der Konfigurationseinstellungen der [!DNL Analytics]-Erweiterung, dass die folgenden Optionen *nicht* aktiviert sind:

* Downloadlinks verfolgen
* Ausgehende Links verfolgen

Wenn diese Einstellungen nicht aktiviert sind, löst Experience Platform [!DNL Adobe Analytics] nicht automatisch aus. [!DNL Analytics] wird nur dann ausgelöst, wenn Sie dies in einer Regelaktion speziell festlegen. Bestimmen Sie mithilfe der Regelbedingungen, was wann ausgelöst werden soll. Wenn Sie beispielsweise Cookies zur Bestimmung des Anmeldestatus verwenden möchten, legen Sie ein Datenelement fest, das dieses Cookie ausliest, und verwenden Sie es in der Regel als Bedingung, um zu bestimmen, wann die erste „Beacon senden“-Aktion ausgelöst werden soll.

Sie können auch erwägen, das [Adobe-Anmeldeobjekt](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de) zu verwenden, um die Auslösung dieses Tags in Abstimmung mit Ihrer Einwilligungsverwaltungs-Plattform zu steuern.

Integrationen mit Zustimmungsmanagern (wie OneTrust) können die Zustimmungscookies für Kunden festlegen und verfolgen. Diese können dann im Regel-Builder verwendet werden.

## Audience Manager

Die DIL wird derzeit automatisch ausgelöst, wenn sie auf einer Kundenseite platziert wird. Erwägen Sie, das Auslösen dieses Tags mithilfe des [Adobe-Anmeldeobjekts](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de) in Übereinstimmung mit Ihrer Einwilligungsverwaltungs-Plattform zu steuern.

[!DNL Adobe] empfiehlt, die Server-seitige Weiterleitung in [!DNL Analytics] zu verwenden.

## Experience Cloud ID

Die [!DNL Experience Cloud ID] wird derzeit automatisch ausgelöst, wenn sie auf einer Kundenseite platziert wird.

Erwägen Sie, das Auslösen dieses Tags mithilfe des [Adobe-Anmeldeobjekts](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de) in Übereinstimmung mit Ihrer Einwilligungsverwaltungs-Plattform zu steuern.

## Target

Adobe Experience Platform löst [!DNL Target] nicht automatisch aus. [!DNL Target] wird nur dann ausgelöst, wenn Sie dies in einer Regelaktion speziell festlegen. Bestimmen Sie mithilfe der Regelbedingungen, was wann ausgelöst werden soll. Wenn Sie beispielsweise Cookies zur Bestimmung des Anmeldestatus verwenden möchten, legen Sie ein Datenelement fest, das dieses Cookie ausliest, und verwenden Sie es in der Regel als Bedingung, um zu bestimmen, wann die erste „[!DNL Target] laden“-Aktion ausgelöst werden soll.

Sie können auch erwägen, das [Adobe-Anmeldeobjekt](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de) zu verwenden, um die Auslösung dieses Tags in Abstimmung mit Ihrer Einwilligungsverwaltungs-Plattform zu steuern.

Integrationen mit Zustimmungsmanagern (wie OneTrust) können die Zustimmungscookies für Kunden festlegen und verfolgen. Diese können dann im Regel-Builder verwendet werden.
