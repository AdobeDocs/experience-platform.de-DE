---
keywords: Experience Platform; Homepage; beliebte Themen[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: Erstellen einer PostgreSQL-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine PostgreSQL-Quellverbindung erstellen.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: eea815f72c1e807f4ad6ca6273ba18a9da09ac6e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 13%

---

# Erstellen Sie eine [!DNL PostgreSQL] Quellverbindung in der Benutzeroberfläche

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden Schritte zum Erstellen eines [!DNL PostgreSQL] Quell-Connector mit [!DNL Platform] -Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Der standardisierte Rahmen, durch den [!DNL Experience Platform] organisiert Kundenerlebnisdaten.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial zum Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL PostgreSQL] Verbindung nutzen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss konfigurieren](../../dataflow/databases.md).

### Erforderliche Anmeldedaten sammeln

Um auf Ihre [!DNL PostgreSQL] Konto auf [!DNL Platform]müssen Sie den folgenden Wert angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die mit Ihrer [!DNL PostgreSQL] -Konto. Die [!DNL PostgreSQL] Verbindungszeichenfolgenmuster ist: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Weiterführende Informationen zu den ersten Schritten finden Sie in diesem Abschnitt [[!DNL PostgreSQL] Dokument](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Aktivieren der SSL-Verschlüsselung für Ihre Verbindungszeichenfolge

Sie können die SSL-Verschlüsselung für Ihre [!DNL PostgreSQL] Verbindungszeichenfolge, indem Sie Ihre Verbindungszeichenfolge mit den folgenden Eigenschaften anhängen:

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `EncryptionMethod` | Ermöglicht die Aktivierung der SSL-Verschlüsselung in der [!DNL PostgreSQL] Daten. | <uL><li>`EncryptionMethod=0`(Deaktiviert)</li><li>`EncryptionMethod=1`(Aktiviert)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validiert das Zertifikat, das von Ihrer [!DNL PostgreSQL] Datenbank bei `EncryptionMethod` angewendet wird. | <uL><li>`ValidationServerCertificate=0`(Deaktiviert)</li><li>`ValidationServerCertificate=1`(Aktiviert)</li></ul> |

Im Folgenden finden Sie ein Beispiel für eine [!DNL PostgreSQL] Verbindungszeichenfolge an SSL-Verschlüsselung angehängt: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Verbinden Sie Ihre [!DNL PostgreSQL] account

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL PostgreSQL] Konto [!DNL Platform].

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die **[!UICONTROL Quellen]** Arbeitsbereich. Die **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **[!UICONTROL Datenbanken]** category, select **[!UICONTROL PostgreSQL DB]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Daten hinzufügen]** , um eine neue [!DNL PostgreSQL] Connector.

![](../../../../images/tutorials/create/postgresql/catalog.png)

Die **[!UICONTROL Verbinden mit[!DNL PostgreSQL]]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL PostgreSQL] Anmeldedaten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![](../../../../images/tutorials/create/postgresql/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie die [!DNL PostgreSQL] Konto, mit dem Sie eine Verbindung herstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![](../../../../images/tutorials/create/postgresql/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrer [!DNL PostgreSQL] -Konto. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md).
