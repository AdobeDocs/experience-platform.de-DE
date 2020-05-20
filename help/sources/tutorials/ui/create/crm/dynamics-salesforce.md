---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Microsoft Dynamics- oder Salesforce-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Erstellen eines Microsoft Dynamics- oder Salesforce-Quellconnectors in der Benutzeroberfläche

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte CRM-Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines Microsoft Dynamics (nachfolgend &quot;Dynamics&quot;) oder Salesforce-Quellconnectors mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine Microsoft Dynamics- oder Salesforce-Basisverbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/crm.md)fortfahren.

### Erforderliche Berechtigungen erfassen

Um auf Ihr Dynamics-Konto auf der Plattform zugreifen zu können, müssen Sie einen **Dienst-URI**, einen **Benutzernamen** und ein **Kennwort** angeben.

Für den Zugriff auf Ihr Salesforce-Konto auf der Plattform müssen Sie eine **Umgebung-URL**, einen **Benutzernamen**, ein **Kennwort** und ein **Sicherheitstoken** angeben.

## Verbinden Sie Ihr Dynamics- oder Salesforce-Konto

Mit den Anmeldeinformationen Ihres CRM-Systems können Sie die unten stehenden Schritte ausführen, um eine neue eingehende Basisverbindung zu erstellen, um Ihr Dynamics- oder Salesforce-Konto mit Platform zu verknüpfen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Vielzahl von Quellen angezeigt, mit denen Sie eingehende Basisverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Basisverbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der *CRM* -Kategorie entweder **Microsoft Dynamics** oder **Salesforce** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zur Ansicht der Dokumentation oder zur Verbindung mit der Quelle. Um eine neue eingehende Basisverbindung zu erstellen, klicken Sie auf Quelle **verbinden**.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

Geben Sie im Eingabedatum die Basisverbindung mit einem Namen, einer optionalen Beschreibung und Ihren Dynamics- oder Salesforce-Anmeldeinformationen ein. Klicken Sie schließlich auf **Verbinden** und lassen Sie dann etwas Zeit, bis die neue Basisverbindung hergestellt ist.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

Sobald eine Basisverbindung mit Ihrem CRM-System hergestellt wurde, können Sie den nächsten Abschnitt fortsetzen und einen Datendurchlauf konfigurieren, um CRM-Daten in die Plattform zu bringen.

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Basisverbindung zu Ihrem Dynamics- oder Salesforce-Konto aufgebaut. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in Plattform](../../dataflow/crm.md)zu übertragen.