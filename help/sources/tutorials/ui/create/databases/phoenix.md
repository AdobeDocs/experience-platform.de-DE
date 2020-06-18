---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Phoenix-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Erstellen eines Phoenix-Quellconnectors in der Benutzeroberfläche

> [!NOTE]
> Der Phoenix-Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden die Schritte zum Erstellen eines Phoenix-Quell-Connectors mithilfe der Benutzeroberfläche &quot;Platform&quot;beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige Phoenix-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses fortfahren](../../dataflow/databases.md)

### Erforderliche Berechtigungen erfassen

Um auf Ihr Phoenix-Konto bei Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des Phoenix-Servers. |
| `port` | Der TCP-Anschluss, den der Phoenix-Server verwendet, um auf Clientverbindungen zu warten. Wenn Sie eine Verbindung zu einem Azurblauen HDInsights herstellen, geben Sie den Anschluss als 443 an. |
| `httpPath` | Die Teil-URL, die dem Phoenix-Server entspricht. Geben Sie /hbasephoenix0 an, wenn Sie den Azurblaus HDInsights-Cluster verwenden. |
| `username` | Der Benutzername, mit dem Sie auf den Phoenix-Server zugreifen. |
| `password` | Das dem Benutzer zugeordnete Kennwort. |
| `enableSsl` | Ein Umschalter, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |

Weitere Informationen zum Einstieg finden Sie in [diesem Phoenix-Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Verbinden Sie Ihr Phoenix-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Phoenix-Konto zu erstellen, um eine Verbindung zur Platform herzustellen.

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste **Quellen** , um auf den *Quellarbeitsbereich* zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden eine Reihe von Quellen angezeigt, für die Sie ein Inbound-Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *Datenbanken* &quot;die Option &quot; **Phoenix** &quot;aus, um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Verbindung zu erstellen, wählen Sie Quelle **verbinden**.

![Katalog](../../../../images/tutorials/create/phoenix/catalog.png)

Die Seite *Verbindung zu Phoenix* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **Neues Konto**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre Phoenix-Anmeldedaten für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **Verbinden** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das Phoenix-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **Weiter** , um fortzufahren.

![existing](../../../../images/tutorials/create/phoenix/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem Phoenix-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in die Platform](../../dataflow/databases.md)zu bringen.