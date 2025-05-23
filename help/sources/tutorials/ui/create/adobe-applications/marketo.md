---
title: Erstellen einer Marketo Engage Source-Verbindung und eines Datenflusses in der Benutzeroberfläche
description: In diesem Tutorial werden Schritte zum Erstellen einer Marketo Engage-Quellverbindung und eines Datenflusses in der Benutzeroberfläche beschrieben, um B2B-Daten in Adobe Experience Platform zu importieren.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 43%

---

# Erstellen einer [!DNL Marketo Engage] Quellverbindung und eines Datenflusses in der Benutzeroberfläche

>[!IMPORTANT]
>
>Bevor Sie eine [!DNL Marketo Engage]-Quellverbindung und einen Datenfluss erstellen, müssen Sie zunächst sicherstellen, dass Sie [Ihre Adobe-Organisations-](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=de)) in [!DNL Marketo] zugeordnet haben. Darüber hinaus müssen Sie auch sicherstellen, dass Sie [automatische Ausfüllen Ihrer B2B [!DNL Marketo] Namespaces und -Schemata) ](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) haben, bevor Sie eine Quellverbindung und einen Datenfluss erstellen.

In diesem Tutorial erfahren Sie, wie Sie einen [!DNL Marketo Engage]-Quell-Connector (im Folgenden als „[!DNL Marketo]“ abgekürzt) in der Benutzeroberfläche erstellen, um B2B-Daten in Adobe Experience Platform einzubringen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [B2B-Namespaces und Dienstprogramm zur automatischen Schemaerstellung](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Mit dem B2B-Namespace- und dem Dienstprogramm zur automatischen Schemaerstellung können Sie [!DNL Postman] verwenden, um automatisch Werte für Ihre B2B-Namespaces und -Schemas zu generieren. Sie müssen zuerst Ihre B2B-Namespaces und -Schemata abschließen, bevor Sie eine [!DNL Marketo] Quellverbindung und einen Datenfluss erstellen.
* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Experience-Datenmodell (XDM)](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../../../../../xdm/ui/resources/schemas.md): Erfahren Sie, wie Sie in der Benutzeroberfläche Schemata erstellen und bearbeiten.
* [Identitäts-Namespaces](../../../../../identity-service/features/namespaces.md): Identitäts-Namespaces sind eine Komponente von [!DNL Identity Service], die als Indikatoren für den Kontext dienen, auf den sich eine Identität bezieht. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Marketo]-Konto in Experience Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---- | ---- |
| `munchkinId` | Die Munchkin-ID ist die eindeutige Kennung für eine bestimmte [!DNL Marketo]-Instanz. |
| `clientId` | Die eindeutige Client-ID Ihrer [!DNL Marketo]-Instanz. |
| `clientSecret` | Das eindeutige Client-Geheimnis Ihrer [!DNL Marketo]-Instanz. |

Weitere Informationen darüber, wie Sie diese Werte erhalten, finden Sie im [[!DNL Marketo] Authentifizierungshandbuch](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die Schritte im nächsten Abschnitt ausführen.

## Verbinden Ihres [!DNL Marketo]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Adobe* Programme&rbrace; **[!UICONTROL Marketo Engage]** und dann **[!UICONTROL Daten hinzufügen]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit der ausgewählten Marketo Engage-Quelle.](../../../../images/tutorials/create/marketo/catalog.png)

Die Seite **[!UICONTROL Marketo Engage-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto verwenden oder auf ein vorhandenes Konto zugreifen.

>[!BEGINTABS]

>[!TAB Neues Konto erstellen]

Um ein neues Konto zu erstellen, wählen **[!UICONTROL Neues Konto]** und geben Sie einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle zum Authentifizieren eines neuen Marketo-Kontos.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Vorhandenes Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das Konto, das Sie verwenden möchten, aus dem vorhandenen Kontenkatalog aus.

Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die Benutzeroberfläche für vorhandene Konten, in der Sie ein vorhandenes Marketo-Konto auswählen können.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Auswählen eines Datensatzes

Nachdem Sie Ihr [!DNL Marketo]-Konto erstellt haben, können Sie im nächsten Schritt [!DNL Marketo]-Datensätze untersuchen.

Die linke Hälfte der Schnittstelle ist ein Verzeichnis-Browser, der die zehn [!DNL Marketo]-Datensätze anzeigt. Eine voll funktionsfähige [!DNL Marketo]-Quellverbindung erfordert das Aufnehmen der neun verschiedenen Datensätze. Wenn Sie außerdem die Funktion Account-Based Marketing (ABM) von [!DNL Marketo] verwenden, müssen Sie auch einen zehnten Datenfluss erstellen, um den Datensatz [!UICONTROL Benannte Konten] aufzunehmen.

>[!NOTE]
>
>Der Kürze halber wird im folgenden Tutorial [!UICONTROL Opportunities] als Beispiel verwendet, aber die unten beschriebenen Schritte gelten für jeden der zehn [!DNL Marketo]-Datensätze.

Wählen Sie den Datensatz aus, den Sie aufnehmen möchten. Dadurch wird die Benutzeroberfläche aktualisiert, damit eine Vorschau Ihres Datensatzes angezeigt wird. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Die Vorschau-Oberfläche](../../../../images/tutorials/create/marketo/preview.png)

## Datensatz- und Datenflussdetails angeben {#provide-dataset-and-dataflow-details}

Als Nächstes müssen Sie Informationen zu Ihrem Datensatz und Ihrem Datenfluss angeben.

### Datensatz-Details {#dataset-details}

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Daten, die erfolgreich in Experience Platform aufgenommen werden, werden im Data Lake als Datensätze gespeichert. In diesem Schritt können Sie einen neuen Datensatz erstellen oder einen vorhandenen Datensatz verwenden.

>[!BEGINTABS]

>[!TAB Verwenden eines neuen Datensatzes]

Um einen neuen Datensatz zu verwenden, wählen **[!UICONTROL Neuer Datensatz]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihren Datensatz an. Sie müssen auch ein Experience-Datenmodell-Schema (XDM) auswählen, dem Ihr Datensatz entspricht.

![Die neue Oberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Verwenden eines vorhandenen Datensatzes]

Wenn Sie bereits über einen vorhandenen Datensatz verfügen, wählen Sie **[!UICONTROL Vorhandener Datensatz]** und verwenden Sie dann die Option **[!UICONTROL Erweiterte Suche]**, um ein Fenster aller Datensätze in Ihrer Organisation anzuzeigen, einschließlich der entsprechenden Details, z. B. ob sie für die Aufnahme in das Echtzeit-Kundenprofil aktiviert sind oder nicht.

![Die vorhandene Oberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Datenflusskonfigurationen {#dataflow-configurations}

>[!IMPORTANT]
>
>Die [!DNL Marketo]-Quelle verwendet die Batch-Aufnahme, um alle historischen Datensätze aufzunehmen, und verwendet die Streaming-Aufnahme für Echtzeit-Aktualisierungen. Dadurch kann die Quelle beim Aufnehmen fehlerhafter Datensätze das Streaming fortsetzen. Aktivieren Sie den Umschalter **[!UICONTROL Teilweise Aufnahme]** und setzen Sie dann [!UICONTROL Fehler-Schwellenwert %] auf Maximum, um ein Fehlschlagen des Datenflusses zu verhindern.

Wenn Ihr Datensatz für das Echtzeit-Kundenprofil aktiviert ist, können Sie in diesem Schritt **[!UICONTROL Profildatensatz]** umschalten, um Ihre Daten für die Profilaufnahme zu aktivieren. Sie können diesen Schritt auch verwenden, um **[!UICONTROL Fehlerdiagnose]** und **[!UICONTROL Partielle Aufnahme]** zu aktivieren.

* **[!UICONTROL Fehlerdiagnose]**: Wählen Sie **[!UICONTROL Fehlerdiagnose]** aus, um die Quelle anzuweisen, Fehlerdiagnosen zu erstellen, auf die Sie später bei der Überwachung Ihrer Datensatzaktivität und des Datenflussstatus verweisen können.
* **[!UICONTROL Partielle Aufnahme]**: [Partielle Batch-Aufnahme](../../../../../ingestion/batch-ingestion/partial.md) ist die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten konfigurierbaren Schwellenwert aufzunehmen. Mit dieser Funktion können Sie alle Ihre korrekten Daten erfolgreich in Experience Platform aufnehmen, während alle Ihre falschen Daten separat mit Informationen darüber, warum sie ungültig sind, in Batches erfasst werden.

In diesem Schritt können Sie &quot;**[!UICONTROL -Datenfluss“ aktivieren]** um die Datenaufnahme zu begrenzen und zusätzliche Kosten zu vermeiden, die mit der Aufnahme aller historischen Daten, einschließlich Personenidentitäten, verbunden sind.

>[!BEGINSHADEBOX]

**Kurzanleitung zur Verwendung von Beispiel-Datenflüssen**

Beispieldatenfluss ist eine Konfiguration, die Sie für Ihren [!DNL Marketo] Datenfluss festlegen können, um Ihre Aufnahmegeschwindigkeit zu begrenzen und dann Experience Platform-Funktionen auszuprobieren, ohne große Datenmengen aufnehmen zu müssen.

* Aktivieren Sie den Beispieldatenfluss, um historische Daten zu beschränken, indem Sie bis zu 100.000 Datensätze (von der größten Datensatz-ID) oder die letzten 10 Tage der Aktivität während des Aufstockungsauftrags aufnehmen.
* Bei Verwendung der Beispiel-Datenflusskonfiguration für alle B2B-Entitäten müssen Sie berücksichtigen, dass möglicherweise einige verwandte Datensätze fehlen, da der gesamte Verlauf der Quelldaten nicht aufgenommen wird.

>[!ENDSHADEBOX]

![Der Abschnitt Datenflusskonfigurationen auf der Seite mit den Datenflussdetails.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Wenn Sie Daten aus dem Unternehmensdatensatz aufnehmen, können Sie außerdem „Nicht beanspruchte Konten ausschließen **[!UICONTROL aktivieren]** um nicht beanspruchte Konten von der Aufnahme auszuschließen.

Wenn Einzelpersonen ein Formular ausfüllen, erstellt [!DNL Marketo] einen Phantomkontodatensatz auf Grundlage des Firmennamens, der keine anderen Daten enthält. Bei neuen Datenflüssen ist der Umschalter zum Ausschließen nicht beanspruchter Konten standardmäßig aktiviert. Bei vorhandenen Datenflüssen können Sie die Funktion aktivieren oder deaktivieren, wobei Änderungen auf neu aufgenommene Daten und nicht auf vorhandene Daten angewendet werden.

![Ausschließen nicht beanspruchter Konten](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Zuordnen Ihrer [!DNL Marketo]-Datensatz-Quellfelder zu XDM-Zielfeldern

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Für jeden Datensatz des Typs [!DNL Marketo] gibt es eigene spezifische Zuordnungsregeln, die befolgt werden müssen. Weitere Informationen dazu, wie Sie [!DNL Marketo]-Datensätze XDM zuordnen, finden Sie nachstehend:

* [Aktivitäten](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programme](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Programmmitgliedschaften](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Firmen](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Statische Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Mitgliedschaften in statischen Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Benannte Konten](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Opportunities](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Rollen von Kontakten bei Opportunities](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personen](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

![Die Zuordnungsschnittstelle für Marketo-Daten.](../../../../images/tutorials/create/marketo/mapping.png)

Wenn Ihre Mapping-Sets fertig sind, klicken Sie auf **[!UICONTROL Weiter]** und warten Sie einige Augenblicke, während der neue Datenfluss hergestellt wird.

## Überprüfen des Datenflusses

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quellentität und die Anzahl der Spalten innerhalb dieser Quellentität an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, wählen Sie **[!UICONTROL Speichern und Aufnehmen]** und gewähren Sie etwas Zeit für die Herstellung des Datenflusses.

![Die Überprüfungsseite, auf der Sie Details Ihres Datenflusses vor der Aufnahme bestätigen können.](../../../../images/tutorials/create/marketo/review.png)

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss hergestellt worden ist, können Sie Daten, die dadurch aufgenommen werden, überwachen, um Informationen zu Aufnahmegeschwindigkeiten, Erfolg und Fehlern zu erhalten. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial zum [Überwachen von Datenflüssen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Löschen Ihrer Attribute

Benutzerdefinierte Attribute in Datensätzen können nicht rückwirkend ausgeblendet oder entfernt werden. Wenn Sie ein benutzerdefiniertes Attribut aus einem vorhandenen Datensatz ausblenden oder entfernen möchten, müssen Sie einen neuen Datensatz ohne dieses benutzerdefinierte Attribut sowie ein neues XDM-Schema erstellen und für den neuen Datensatz, den Sie erstellen, einen neuen Datenfluss konfigurieren. Außerdem müssen Sie den ursprünglichen Datenfluss deaktivieren oder löschen, der aus dem Datensatz mit dem benutzerdefinierten Attribut besteht, das Sie ausblenden oder entfernen möchten.

## Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich [!UICONTROL Datenflüsse] verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um B2B-Daten aus Ihrer [!DNL Marketo Engage] in Experience Platform aufzunehmen.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Richtlinien, die Sie bei der Verwendung der [!DNL Marketo] befolgen können.

### Fehlermeldungen in der Benutzeroberfläche {#error-messages}

Die folgenden Fehlermeldungen werden in der Benutzeroberfläche angezeigt, wenn Experience Platform Probleme mit Ihrem Setup erkennt:

#### [!DNL Munchkin ID] ist der entsprechenden Organisation nicht zugeordnet

Die Authentifizierung wird verweigert, wenn Ihr [!DNL Munchkin ID] nicht der von Ihnen verwendeten Experience Platform-Organisation zugeordnet ist. Konfigurieren Sie die Zuordnung zwischen Ihrer [!DNL Munchkin ID] und Ihrer Organisation mithilfe der [[!DNL Marketo] Benutzeroberfläche](https://app-sjint.marketo.com/#MM0A1).

![Eine Fehlermeldung, die anzeigt, dass die Marketo-Instanz nicht korrekt der Adobe-Organisation zugeordnet ist.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Primäre Identität fehlt

Ein Datenfluss kann nicht gespeichert und aufgenommen werden, wenn eine primäre Identität fehlt. Stellen Sie sicher[ dass in Ihrem XDM-Schema eine primäre Identität vorhanden ist](../../../../../xdm/tutorials/create-schema-ui.md) bevor Sie versuchen, einen Datenfluss zu konfigurieren.

![Eine Fehlermeldung, die anzeigt, dass die primäre Identität im XDM-Schema fehlt.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

