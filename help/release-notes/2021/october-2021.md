---
title: Adobe Experience Platform – Versionshinweise, Oktober 2021
description: Versionshinweise von Oktober 2021 für Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 100%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 27. Oktober 2021**

## Aktualisierungen in Experience Platform

Aktualisierungen in Experience Platform

### Benutzeroberfläche {#ui}

An der Benutzeroberfläche wurden folgende Änderungen vorgenommen:

| Funktion | Beschreibung |
| --- | --- |
| Dunkles Design | Verwenden Sie den Umschalter für dunkles Design, um in der Platform-Oberfläche zwischen hellem und dunklem Design zu wechseln. Der Umschalter befindet sich im Benutzerprofil unter Benutzername und E-Mail. |
| Ein- und Ausblenden der linken Navigationsleiste | Verwenden Sie den verbesserten Umschalter für die Navigation oben in der Kopfzeile des Programms, um das Menü mit den Funktionen von Experience Platform ein- oder auszublenden. Das System speichert Ihre letzte Auswahl und zeigt nur die Funktionen an, auf die Sie Zugriff haben. |
| Sichtbarkeit des Zugriffs | In der linken Navigationsleiste werden nur die Funktionen angezeigt, auf die Sie zugreifen können. In früheren Versionen von Adobe Experience Platform waren nicht verfügbare Elemente sichtbar, selbst wenn Sie nicht darauf zugreifen konnten. |

Weitere Informationen erhalten Sie im [Handbuch zur Platform-Benutzeroberfläche](../../landing/ui-guide.md).

## Aktualisierungen vorhandener Funktionen

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Quellen](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| `contains_key`-Funktion | Es wurde die Funktion `contains_key` eingeführt, mit der Sie überprüfen können, ob das Objekt in der Quelle vorhanden ist. Diese Funktion ersetzt die Funktion `is_set`, die jetzt nicht mehr unterstützt wird. |
| Fehlermeldungen | Vom Endpunkt `/mappingSets/preview` in der Data Prep-API zurückgegebene Fehlermeldungen stimmen nun mit den Fehlermeldungen überein, die während der Laufzeit generiert werden. |

Weitere Informationen über diesen Service finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

### Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der [!DNL Amazon S3]-Quelle | Sie können jetzt den Parameter `s3SessionToken` verwenden, um Ihr [!DNL Amazon S3]-Konto mithilfe temporärer Sicherheitsberechtigungen mit Platform zu verknüpfen. Mit diesem Token können Sie Benutzern in nicht vertrauenswürdigen Umgebungen einen kurzfristigen, temporären Zugriff auf Ihre [!DNL Amazon S3]-Ressourcen bereitstellen. Weitere Informationen finden Sie in der [[!DNL Amazon S3] Dokumentation](../../sources/connectors/cloud-storage/s3.md#prerequisites). |
| [!DNL Generic REST API] (Betaversion) | Sie können jetzt eine [!DNL Generic REST API]-Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) erstellen, um Daten von einer generischen REST-Anwendung an Platform zu übertragen. Weitere Informationen finden Sie in der [[!DNL Generic REST API] Übersicht](../../sources/connectors/protocols/generic-rest.md). |
| [!DNL Zoho CRM] (Betaversion) | Sie können jetzt eine [!DNL Zoho CRM]-Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) oder der [Benutzeroberfläche](../../sources/tutorials/ui/create/crm/zoho.md) erstellen, um Daten von Ihrem [!DNL Zoho CRM]-Konto in Platform zu übertragen. Weitere Informationen finden Sie in der [[!DNL Zoho CRM] Übersicht über](../../sources/connectors/crm/zoho.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
