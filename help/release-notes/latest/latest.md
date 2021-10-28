---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 45c4486dc9860da13daa6984b23ef80038ea2f8d
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 39%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 27. Oktober 2021**

## Aktualisierungen der Experience Platform

Aktualisierungen der Experience Platform.

### [Benutzeroberfläche] {#ui}

Die Benutzeroberfläche wurde mit den folgenden Änderungen aktualisiert:

| Funktion | Beschreibung |
| --- | --- |
| Dunkles Thema | Verwenden Sie den Dark-Design-Schalter, um in der Platform-Oberfläche zwischen hellen und dunklen Themen umzuschalten. Der Schalter befindet sich im Benutzerprofil unter Benutzername und E-Mail. |
| Navigation links umschalten | Verwenden Sie den verbesserten Navigations-Umschalter oben in der App-Kopfzeile, um das Menü mit den Funktionen Ihrer Experience Platform ein- oder auszublenden. Das System speichert Ihre letzte Auswahl und zeigt nur die Funktionen an, auf die Sie Zugriff haben. |
| Sichtbarkeit des Zugriffs | In der linken Navigationsleiste werden nur die Funktionen angezeigt, auf die Sie zugreifen können. In früheren Versionen von Adobe Experience Platform waren nicht verfügbare Elemente sichtbar, selbst wenn Sie nicht darauf zugreifen konnten. |

Siehe [Handbuch zur Platform-Benutzeroberfläche](../../landing/ui-guide.md) , um mehr zu erfahren.

## Aktualisierungen vorhandener Funktionen

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Quellen](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| `contains_key`-Funktion | Die `contains_key` -Funktion eingeführt wurde, mit der Sie überprüfen können, ob das Objekt in der Quelle vorhanden ist. Diese Funktion ersetzt die `is_set` -Funktion, die jetzt nicht mehr unterstützt wird. |
| Fehlermeldungen | Von der `/mappingSets/preview` -Endpunkt in der Data Prep-API ist nun mit den Fehlermeldungen konsistent, die während der Laufzeit generiert werden. |

Siehe [[!DNL Data Prep] Übersicht](../../data-prep/home.md) , um mehr über diesen Dienst zu erfahren.

### Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Amazon S3]-Quellverbesserungen | Sie können jetzt die `s3SessionToken` Parameter zum Verbinden Ihrer [!DNL Amazon S3] -Konto für Platform mit temporären Sicherheitsberechtigungen erstellen. Mit diesem Token können Sie kurzfristigen, temporären Zugriff auf Ihre [!DNL Amazon S3] Ressourcen für Benutzer in nicht vertrauenswürdigen Umgebungen. Siehe [[!DNL Amazon S3] Dokumentation](../../sources/connectors/cloud-storage/s3.md#prerequisites) für weitere Informationen. |
| [!DNL Generic REST API] (Betaversion) | Sie können jetzt eine [!DNL Generic REST API] Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) oder [Benutzeroberfläche](../../sources/tutorials/ui/create/protocols/generic-rest.md) , um Daten von einer generischen REST-Anwendung an Platform zu übertragen. Weitere Informationen finden Sie in der [[!DNL Generic REST API] Übersicht über](../../sources/connectors/protocols/generic-rest.md). |
| [!DNL Zoho CRM] (Betaversion) | Sie können jetzt eine [!DNL Zoho CRM] Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) oder [Benutzeroberfläche](../../sources/tutorials/ui/create/crm/zoho.md) Daten von [!DNL Zoho CRM] -Konto auf Platform. Weitere Informationen finden Sie in der [[!DNL Zoho CRM] Übersicht über](../../sources/connectors/crm/zoho.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
