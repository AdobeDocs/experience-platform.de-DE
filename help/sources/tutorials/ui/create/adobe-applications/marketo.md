---
title: Erstellen einer Marketo Engage-Quellverbindung und eines Datenflusses in der Benutzeroberfläche
description: In diesem Tutorial erfahren Sie, wie Sie in der Benutzeroberfläche eine Marketo Engage-Quellverbindung und einen Datenfluss erstellen, um B2B-Daten in Adobe Experience Platform zu importieren.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 46%

---

# Erstellen Sie eine [!DNL Marketo Engage] Quellverbindung und Datenfluss in der Benutzeroberfläche

>[!IMPORTANT]
>
>Vor der Erstellung [!DNL Marketo Engage] Quellverbindung und einen Datenfluss müssen Sie zunächst sicherstellen, dass Sie [Ihrer Adobe-Organisations-ID zugeordnet](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) in [!DNL Marketo]. Außerdem müssen Sie sicherstellen, dass Sie [automatisch Ihre [!DNL Marketo] B2B-Namespaces und -Schemata](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) vor der Erstellung einer Quellverbindung und eines Datenflusses.

In diesem Tutorial erfahren Sie, wie Sie einen [!DNL Marketo Engage]-Quell-Connector (im Folgenden als „[!DNL Marketo]“ abgekürzt) in der Benutzeroberfläche erstellen, um B2B-Daten in Adobe Experience Platform einzubringen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [B2B-Namespaces und Dienstprogramm zur automatischen Schemaerstellung](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Mithilfe der B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung können Sie [!DNL Postman] , um automatisch Werte für Ihre B2B-Namespaces und -Schemas zu generieren. Sie müssen zuerst Ihre B2B-Namespaces und -Schemas abschließen, bevor Sie eine [!DNL Marketo] Quellverbindung und Datenfluss.
* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Experience-Datenmodell (XDM)](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../../../../../xdm/ui/resources/schemas.md): Erfahren Sie, wie Sie in der Benutzeroberfläche Schemata erstellen und bearbeiten.
* [Identitäts-Namespaces](../../../../../identity-service/features/namespaces.md): Identitäts-Namespaces sind eine Komponente von [!DNL Identity Service], die als Indikatoren für den Kontext dienen, auf den sich eine Identität bezieht. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre [!DNL Marketo] -Konto auf Experience Platform angegeben haben, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---- | ---- |
| `munchkinId` | Die Munchkin-ID ist die eindeutige Kennung für eine bestimmte [!DNL Marketo]-Instanz. |
| `clientId` | Die eindeutige Client-ID Ihrer [!DNL Marketo]-Instanz. |
| `clientSecret` | Das eindeutige Client-Geheimnis Ihrer [!DNL Marketo]-Instanz. |

Weitere Informationen darüber, wie Sie diese Werte erhalten, finden Sie im [[!DNL Marketo] Authentifizierungshandbuch](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die Schritte im nächsten Abschnitt ausführen.

## Verbinden Ihres [!DNL Marketo]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *Adobe-Anwendungen* category, select **[!UICONTROL Marketo Engage]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Einrichten]** -Option, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto existiert, wird diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit der ausgewählten Marketo Engage-Quelle.](../../../../images/tutorials/create/marketo/catalog.png)

Die Seite **[!UICONTROL Marketo Engage-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto verwenden oder auf ein vorhandenes Konto zugreifen.

>[!BEGINTABS]

>[!TAB Neues Konto erstellen]

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle für die Authentifizierung eines neuen Marketo-Kontos.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Vorhandenes Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie dann das Konto aus, das Sie verwenden möchten, aus dem vorhandenen Kontokatalog.

Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die vorhandene Kontoschnittstelle, in der Sie ein vorhandenes Marketo-Konto auswählen können.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Auswählen eines Datensatzes

Nachdem Sie Ihr [!DNL Marketo]-Konto erstellt haben, können Sie im nächsten Schritt [!DNL Marketo]-Datensätze untersuchen.

Die linke Hälfte der Schnittstelle ist ein Verzeichnis-Browser, der die zehn [!DNL Marketo]-Datensätze anzeigt. Eine voll funktionsfähige [!DNL Marketo]-Quellverbindung erfordert das Aufnehmen der neun verschiedenen Datensätze. Wenn Sie außerdem die Funktion Account-Based Marketing (ABM) von [!DNL Marketo] verwenden, müssen Sie auch einen zehnten Datenfluss erstellen, um den Datensatz [!UICONTROL Benannte Konten] aufzunehmen.

>[!NOTE]
>
>Der Kürze halber wird im folgenden Tutorial [!UICONTROL Opportunities] als Beispiel verwendet, aber die unten beschriebenen Schritte gelten für jeden der zehn [!DNL Marketo]-Datensätze.

Wählen Sie den Datensatz aus, den Sie erfassen möchten. Dadurch wird die Benutzeroberfläche aktualisiert, um eine Vorschau Ihres Datensatzes anzuzeigen. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Vorschau-Benutzeroberfläche](../../../../images/tutorials/create/marketo/preview.png)

## Bereitstellen von Datensatz- und Datenflussdetails {#provide-dataset-and-dataflow-details}

Als Nächstes müssen Sie Informationen zu Ihrem Datensatz und Ihrem Datenfluss angeben.

### Datensatzdetails {#dataset-details}

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Daten, die erfolgreich in Experience Platform aufgenommen wurden, werden im Data Lake als Datensätze gespeichert. In diesem Schritt können Sie einen neuen Datensatz erstellen oder einen vorhandenen Datensatz verwenden.

>[!BEGINTABS]

>[!TAB Verwenden eines neuen Datensatzes]

Um einen neuen Datensatz zu verwenden, wählen Sie **[!UICONTROL Neuer Datensatz]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihren Datensatz an. Sie müssen auch ein Experience-Datenmodell (XDM)-Schema auswählen, dem Ihr Datensatz entspricht.

![Die neue Benutzeroberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Verwenden eines vorhandenen Datensatzes]

Wenn Sie bereits über einen vorhandenen Datensatz verfügen, wählen Sie **[!UICONTROL Vorhandener Datensatz]** und verwenden Sie dann **[!UICONTROL Erweiterte Suche]** -Option, um ein Fenster aller Datensätze in Ihrer Organisation anzuzeigen, einschließlich der entsprechenden Details, z. B. ob sie für die Erfassung in Echtzeit-Kundenprofil aktiviert sind oder nicht.

![Die vorhandene Oberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Datenflusskonfigurationen {#dataflow-configurations}

>[!IMPORTANT]
>
>Die [!DNL Marketo] -Quelle verwendet die Batch-Erfassung, um alle historischen Datensätze zu erfassen, und verwendet die Streaming-Erfassung für Echtzeit-Aktualisierungen. Dadurch kann die Quelle das Streaming fortsetzen, während fehlerhafte Datensätze erfasst werden. Aktivieren Sie den Umschalter **[!UICONTROL Teilweise Aufnahme]** und setzen Sie dann [!UICONTROL Fehler-Schwellenwert %] auf Maximum, um ein Fehlschlagen des Datenflusses zu verhindern.

Wenn Ihr Datensatz für das Echtzeit-Kundenprofil aktiviert ist, können Sie während dieses Schritts **[!UICONTROL Profildatensatz]** , um Ihre Daten für die Profilaufnahme zu aktivieren. Sie können diesen Schritt auch verwenden, um **[!UICONTROL Fehlerdiagnose]** und **[!UICONTROL Partielle Erfassung]**.

* **[!UICONTROL Fehlerdiagnose]**: Auswählen **[!UICONTROL Fehlerdiagnose]** , um die Quelle anzuweisen, eine Fehlerdiagnose zu erstellen, die Sie später bei der Überwachung Ihrer Datensatzaktivität und des Datenflussstatus referenzieren können.
* **[!UICONTROL Partielle Erfassung]**: [Partielle Batch-Erfassung](../../../../../ingestion/batch-ingestion/partial.md) ist die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten konfigurierbaren Schwellenwert zu erfassen. Mit dieser Funktion können Sie alle Ihre präzisen Daten erfolgreich in Experience Platform erfassen, während all Ihre falschen Daten separat mit Informationen darüber gestapelt werden, warum sie ungültig sind.

Während dieses Schritts können Sie **[!UICONTROL Beispiel-Datenfluss]** , um die Datenerfassung zu begrenzen und zusätzliche Kosten zu vermeiden, die durch die Erfassung aller historischen Daten, einschließlich Personen-Identitäten, entstehen.

>[!BEGINSHADEBOX]

**Kurzanleitung zur Verwendung des Beispiel-Datenflusses**

Beispiel-Datenfluss ist eine Konfiguration, die Sie für Ihre [!DNL Marketo] dataflow , um die Aufnahmerate zu begrenzen und dann Experience Platform-Funktionen auszuprobieren, ohne große Datenmengen aufnehmen zu müssen.

* Aktivieren Sie den Beispiel-Datenfluss, um historische Daten durch Aufnahme von bis zu 100.000 Datensätzen (aus der größten Datensatz-ID) oder bis zu den letzten 10 Tagen Aktivität während des Aufstockungsvorgangs zu begrenzen.
* Bei der Verwendung der Beispiel-Datenfluss-Konfiguration für alle B2B-Entitäten müssen Sie beachten, dass möglicherweise einige verwandte Datensätze fehlen, da der gesamte Verlauf der Quelldaten nicht erfasst wird.

>[!ENDSHADEBOX]

![Der Abschnitt &quot;Datenfluss-Konfigurationen&quot;der Datenflug-Detailseite.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Wenn Sie außerdem Daten aus dem Datensatz &quot;Unternehmen&quot;erfassen, können Sie **[!UICONTROL Nicht beanspruchte Konten ausschließen]** nicht beanspruchte Konten von der Erfassung auszuschließen.

Wenn Einzelpersonen ein Formular ausfüllen, [!DNL Marketo] erstellt einen Phantom-Kontodatensatz basierend auf dem Unternehmensnamen, der keine anderen Daten enthält. Bei neuen Datenflüssen ist die Umschaltung zum Ausschließen nicht beanspruchter Konten standardmäßig aktiviert. Für vorhandene Datenflüsse können Sie die Funktion aktivieren oder deaktivieren, wobei Änderungen auf neu aufgenommene Daten und nicht auf vorhandene Daten angewendet werden.

![Nicht beanspruchte Konten ausschließen](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

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

![Die Überprüfungsseite, auf der Sie Details Ihres Datenflusses vor der Erfassung bestätigen können.](../../../../images/tutorials/create/marketo/review.png)

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss hergestellt worden ist, können Sie Daten, die dadurch aufgenommen werden, überwachen, um Informationen zu Aufnahmegeschwindigkeiten, Erfolg und Fehlern zu erhalten. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial zum [Überwachen von Datenflüssen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Löschen Ihrer Attribute

Benutzerdefinierte Attribute in Datensätzen können nicht rückwirkend ausgeblendet oder entfernt werden. Wenn Sie ein benutzerdefiniertes Attribut aus einem vorhandenen Datensatz ausblenden oder entfernen möchten, müssen Sie einen neuen Datensatz ohne dieses benutzerdefinierte Attribut sowie ein neues XDM-Schema erstellen und für den neuen Datensatz, den Sie erstellen, einen neuen Datenfluss konfigurieren. Außerdem müssen Sie den ursprünglichen Datenfluss deaktivieren oder löschen, der aus dem Datensatz mit dem benutzerdefinierten Attribut besteht, das Sie ausblenden oder entfernen möchten.

## Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich [!UICONTROL Datenflüsse] verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um B2B-Daten aus Ihrer [!DNL Marketo Engage] -Quelle zu Experience Platform.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Richtlinien, die Sie bei der Verwendung von [!DNL Marketo] -Quelle.

### Fehlermeldungen in der Benutzeroberfläche {#error-messages}

Die folgenden Fehlermeldungen werden in der Benutzeroberfläche angezeigt, wenn Platform Probleme mit Ihrem Setup erkennt:

#### [!DNL Munchkin ID] ist nicht der entsprechenden Organisation zugeordnet

Die Authentifizierung wird verweigert, wenn Ihre [!DNL Munchkin ID] nicht der Platform-Organisation zugeordnet ist, die Sie verwenden. Konfigurieren Sie die Zuordnung zwischen [!DNL Munchkin ID] und Ihrer Organisation, die [[!DNL Marketo] Benutzeroberfläche](https://app-sjint.marketo.com/#MM0A1).

![Eine Fehlermeldung, die anzeigt, dass die Marketo-Instanz der Adobe-Organisation nicht korrekt zugeordnet ist.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Primäre Identität fehlt

Wenn eine primäre Identität fehlt, kann ein Datenfluss nicht gespeichert und erfasst werden. Stellen Sie sicher, dass [eine primäre Identität innerhalb Ihres XDM-Schemas vorhanden ist](../../../../../xdm/tutorials/create-schema-ui.md), bevor Sie versuchen, einen Datenfluss zu konfigurieren.

![Eine Fehlermeldung, die anzeigt, dass die primäre Identität im XDM-Schema fehlt.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

