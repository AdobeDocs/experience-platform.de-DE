---
title: Sandboxes-Tooling
description: Exportieren und importieren Sie nahtlos Sandbox-Konfigurationen zwischen Sandboxes.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 9%

---


# [!BADGE Beta] Sandbox-Tools

>[!IMPORTANT]
>
>Die **Sandbox-Tools** Die unten beschriebene Funktion steht nur zur Auswahl von Beta-Kunden zur Verfügung.

>[!NOTE]
>
>Sandbox-Tools sind eine grundlegende Funktion, die beide unterstützt [!DNL Real-Time Customer Data Platform] und [!DNL Journey Optimizer] zur Verbesserung der Effizienz und Konfigurationsgenauigkeit des Entwicklungszyklus.<br><br>Sie benötigen die folgenden beiden rollenbasierten Zugriffssteuerungsberechtigungen, um die Sandbox-Tool-Funktion verwenden zu können:<br>- `manage-sandbox` oder `view-sandbox`<br>- `manage-package`

Verbessern der Konfigurationsgenauigkeit über Sandboxes hinweg und nahtloser Export und Import von Sandbox-Konfigurationen zwischen Sandboxes mit der Sandbox-Tool-Funktion. Verwenden Sie Sandbox-Tools, um die Wertschöpfungszeit für den Implementierungsprozess zu reduzieren und erfolgreiche Konfigurationen über Sandboxes hinweg zu verschieben.

Sie können die Sandbox-Tool-Funktion verwenden, um verschiedene Objekte auszuwählen und sie in ein Paket zu exportieren. Ein Paket kann aus einem einzelnen Objekt, mehreren Objekten oder einer gesamten Sandbox bestehen. Alle Objekte, die in einem Paket enthalten sind, müssen aus derselben Sandbox stammen.

## Für Sandbox-Tools unterstützte Objekte {#supported-objects}

In der folgenden Tabelle sind Objekte aufgeführt, die derzeit für die Sandbox-Werkzeuge unterstützt werden:

| Plattform | Objekt |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | Journeys |
| Kundendatenplattform | Quellen |
| Kundendatenplattform | Segmente |
| Kundendatenplattform | Identitäten |
| Kundendatenplattform | Richtlinien |
| Kundendatenplattform | Schemata |
| Kundendatenplattform | Datensätze |

Die folgenden Objekte werden importiert, befinden sich jedoch im Status Entwurf oder deaktiviert :

| Funktion | Objekt | Status |
| --- | --- | --- |
| Importstatus | Datenfluss der Quelle | Entwurf |
| Importstatus | Journey | Entwurf |
| Unified Profile | Schema | Deaktiviert |
| Unified Profile | Datensatz | Deaktiviert |
| Richtlinien | Einverständnisrichtlinien | Deaktiviert |
| Richtlinien | Data Governance-Richtlinien | Deaktiviert |

Die im Folgenden aufgeführten Edge-Fälle sind nicht im Paket enthalten:

* Schemabeziehungen

## Objekte in ein Package exportieren {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="Speichern und Beenden eines Pakets"
>abstract="Um das Paket zu beenden und zu speichern, können Benutzende einfach die Option „Zurück“ verwenden."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Entfernen eines Objekts"
>abstract="Die Benutzerin bzw. der Benutzer muss die Zeile auswählen und dann die Löschoption (die bei Auswahl verfügbar gemacht wird) verwenden, um die entsprechende Zeile zu entfernen."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Ablaufeinstellungen des Pakets"
>abstract="Das Datum ist ab heute für 90 Tage festgelegt. Dieses Datum verändert sich, bis das Paket veröffentlicht wird. Wenn eine Benutzerin bzw. ein Benutzer das Paket morgen im Entwurfsstatus besucht, wird das Datum um +1 Tag verschoben (es sei denn, dies wird von der Benutzerin bzw. vom Benutzer festgelegt)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Paketstatus"
>abstract="Standardmäßig ist der Status auf „Entwurf“ gesetzt. Sobald das Paket veröffentlicht wurde, wird der Status in „veröffentlicht“ geändert. Nach der Veröffentlichung des Pakets können keine Änderungen vorgenommen werden."

>[!NOTE]
>
>Sie können ein Package nur importieren, wenn Sie Zugriff auf die Objekte haben.

In diesem Beispiel wird der Export eines Schemas und dessen Hinzufügen zu einem Package dokumentiert. Sie können denselben Prozess verwenden, um andere Objekte zu exportieren, z. B. Datensätze, Journey und viele andere.

### Objekt zu einem neuen Paket hinzufügen {#add-object-to-new-package}

Auswählen **[!UICONTROL Schemas]** aus der linken Navigation und wählen Sie dann die **[!UICONTROL Durchsuchen]** -Tab, in dem die verfügbaren Schemas aufgelistet werden. Wählen Sie als Nächstes die Auslassungszeichen (`...`) neben dem ausgewählten Schema und eine Dropdown-Liste zeigt Steuerelemente an. Auswählen **[!UICONTROL Zu Paket hinzufügen]** aus dem Dropdown-Menü aus.

![Liste der Schemata, die das Dropdown-Menü anzeigen, in dem die [!UICONTROL Zu Paket hinzufügen] Kontrolle.](../images/ui/sandbox-tooling/add-to-package.png)

Aus dem **[!UICONTROL Zu Paket hinzufügen]** wählen Sie das **[!UICONTROL Neues Paket erstellen]** -Option. Stellen Sie eine [!UICONTROL Name] für Ihr Paket und optional [!UICONTROL Beschreibung], wählen Sie **[!UICONTROL Hinzufügen]**.

![Die [!UICONTROL Zu Paket hinzufügen] Dialogfeld mit [!UICONTROL Neues Paket erstellen] ausgewählte und hervorgehobene Elemente [!UICONTROL Hinzufügen].](../images/ui/sandbox-tooling/create-new-package.png)

Sie kehren zum **[!UICONTROL Schemas]** Umgebung. Sie können dem von Ihnen erstellten Package jetzt zusätzliche Objekte hinzufügen, indem Sie die folgenden Schritte ausführen.

### Hinzufügen eines Objekts zu einem vorhandenen Paket und Veröffentlichen {#add-object-to-existing-package}

Um eine Liste der verfügbaren Schemata anzuzeigen, wählen Sie **[!UICONTROL Schemas]** aus der linken Navigation und wählen Sie dann die **[!UICONTROL Durchsuchen]** Registerkarte. Wählen Sie als Nächstes die Auslassungszeichen (`...`) neben dem ausgewählten Schema, um die Kontrolloptionen in einem Dropdown-Menü anzuzeigen. Auswählen **[!UICONTROL Zu Paket hinzufügen]** aus dem Dropdown-Menü aus.

![Liste der Schemata, die das Dropdown-Menü anzeigen, in dem die [!UICONTROL Zu Paket hinzufügen] Kontrolle.](../images/ui/sandbox-tooling/add-to-package.png)

Die **[!UICONTROL Zu Paket hinzufügen]** angezeigt. Wählen Sie die **[!UICONTROL Vorhandenes Paket]** und wählen Sie anschließend die **[!UICONTROL Paketname]** und wählen Sie das gewünschte Paket aus. Wählen Sie abschließend **[!UICONTROL Hinzufügen]** um Ihre Auswahl zu bestätigen.

![[!UICONTROL Zu Paket hinzufügen] angezeigt, um ein ausgewähltes Paket aus der Dropdown-Liste anzuzeigen.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Die Liste der dem Paket hinzugefügten Objekte wird aufgelistet. Um das Paket zu veröffentlichen und es für den Import in Sandboxes verfügbar zu machen, wählen Sie **[!UICONTROL Veröffentlichen]**.

![Eine Liste der Objekte im Paket, die die [!UICONTROL Veröffentlichen] -Option.](../images/ui/sandbox-tooling/publish-package.png)

Auswählen **[!UICONTROL Veröffentlichen]** zur Bestätigung der Veröffentlichung des Pakets.

![Veröffentlichen Sie das Bestätigungsdialogfeld für das Paket, indem Sie die [!UICONTROL Veröffentlichen] -Option.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Nach der Veröffentlichung kann der Inhalt des Pakets nicht mehr geändert werden. Um Kompatibilitätsprobleme zu vermeiden, stellen Sie sicher, dass alle erforderlichen Assets ausgewählt wurden. Wenn Änderungen vorgenommen werden müssen, müssen Sie ein neues Paket erstellen.

Sie kehren zum **[!UICONTROL Pakete]** im [!UICONTROL Sandboxes] Umgebung, in der das neue veröffentlichte Paket angezeigt wird.

![Liste der Sandbox-Pakete, die das neue veröffentlichte Paket hervorheben.](../images/ui/sandbox-tooling/published-packages.png)

## Importieren eines Pakets in eine Ziel-Sandbox {#import-package-to-target-sandbox}

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zu den Sandboxes . **[!UICONTROL Durchsuchen]** und wählen Sie das Pluszeichen (+) neben dem Sandbox-Namen aus.

![Die Sandboxes **[!UICONTROL Durchsuchen]** -Tab, der die Auswahl des Importpakets markiert.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Wählen Sie im Dropdown-Menü die **[!UICONTROL Paketname]** Sie möchten in die Ziel-Sandbox importieren. Hinzufügen eines optionalen **[!UICONTROL Auftragsname]**, der für die künftige Überwachung verwendet wird, wählen Sie **[!UICONTROL Nächste]**.

![Auf der Seite mit den Importdetails wird die [!UICONTROL Paketname] Dropdown-Auswahl](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

Die [!UICONTROL Paketobjekt und Abhängigkeiten] -Seite enthält eine Liste aller in diesem Paket enthaltenen Assets. Das System erkennt automatisch abhängige Objekte, die für den erfolgreichen Import ausgewählter übergeordneter Objekte erforderlich sind.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] zeigt eine Liste der im Paket enthaltenen Assets an.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>Abhängige Objekte können in der Ziel-Sandbox durch vorhandene ersetzt werden, sodass Sie vorhandene Objekte wiederverwenden können, anstatt eine neue Version zu erstellen. Wenn Sie beispielsweise ein Paket mit Schemas importieren, können Sie vorhandene benutzerdefinierte Feldergruppen und Identitäts-Namespaces in der Ziel-Sandbox wiederverwenden. Alternativ können Sie beim Importieren eines Pakets mit Journey bestehende Segmente in der Ziel-Sandbox wiederverwenden.

Um ein vorhandenes Objekt zu verwenden, wählen Sie das Stiftsymbol neben dem abhängigen Objekt aus. Die Optionen zum Erstellen neuer oder Verwenden vorhandener Elemente werden angezeigt. Auswählen **[!UICONTROL Vorhandene verwenden]**.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] Seite mit abhängigen Objektoptionen [!UICONTROL Neu erstellen] und [!UICONTROL Vorhandene verwenden].](../images/ui/sandbox-tooling/use-existing-object.png)

Die **[!UICONTROL Feldergruppe]** zeigt eine Liste von Feldergruppen an, die für das Objekt verfügbar sind. Wählen Sie die erforderlichen Feldergruppen aus und klicken Sie auf **[!UICONTROL Speichern]**.

![Eine Liste der Felder, die im [!UICONTROL Feldergruppe] Dialog, das die [!UICONTROL Speichern] auswählen. ](../images/ui/sandbox-tooling/field-group-list.png)

Sie kehren zum [!UICONTROL Paketobjekt und Abhängigkeiten] Seite. Wählen Sie von hier aus **[!UICONTROL Beenden]** , um den Package-Import abzuschließen.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] Seite zeigt eine Liste der im Paket enthaltenen Assets, die hervorgehoben werden [!UICONTROL Beenden].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportieren und Importieren einer gesamten Sandbox

### Gesamte Sandbox exportieren {#export-entire-sandbox}

Um eine gesamte Sandbox zu exportieren, navigieren Sie zum [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** Registerkarte und wählen Sie **[!UICONTROL Package erstellen]**.

![Die [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** Tabulatorhervorhebung [!UICONTROL Package erstellen].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Auswählen **[!UICONTROL Gesamte Sandbox]** für den Pakettyp im [!UICONTROL Package erstellen] angezeigt. Stellen Sie eine [!UICONTROL Paketname] und wählen Sie die **[!UICONTROL Sandbox]** aus dem Dropdown-Menü aus. Wählen Sie abschließend **[!UICONTROL Erstellen]** um Ihre Einträge zu bestätigen.

![Die [!UICONTROL Package erstellen] Dialogfeld mit ausgefüllten Feldern und Markierung [!UICONTROL Erstellen].](../images/ui/sandbox-tooling/create-package-dialog.png)

Das Paket wurde erfolgreich erstellt, wählen Sie **[!UICONTROL Veröffentlichen]** um das Paket zu veröffentlichen.

![Liste der Sandbox-Pakete, die das neue veröffentlichte Paket hervorheben.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Sie kehren zum **[!UICONTROL Pakete]** im [!UICONTROL Sandboxes] Umgebung, in der das neue veröffentlichte Paket angezeigt wird.

### Importieren des gesamten Sandbox-Pakets {#import-entire-sandbox-package}

Um das Paket in eine Ziel-Sandbox zu importieren, navigieren Sie zum [!UICONTROL Sandboxes] **[!UICONTROL Durchsuchen]** und wählen Sie das Pluszeichen (+) neben dem Sandbox-Namen aus.

![Die Sandboxes **[!UICONTROL Durchsuchen]** -Tab, der die Auswahl des Importpakets markiert.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Wählen Sie über das Dropdown-Menü die vollständige Sandbox mithilfe der **[!UICONTROL Paketname]** Dropdown. Hinzufügen eines optionalen **[!UICONTROL Auftragsname]**, der für die künftige Überwachung verwendet wird, wählen Sie **[!UICONTROL Nächste]**.

![Auf der Seite mit den Importdetails wird die [!UICONTROL Paketname] Dropdown-Auswahl](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Beim Import einer gesamten Sandbox werden alle Objekte aus dem Package als neu erstellt. Die Objekte werden nicht im [!UICONTROL Paketobjekt und Abhängigkeiten] Seite, da es mehrere sein kann. Es wird eine Inline-Meldung angezeigt, die Hinweise zu nicht unterstützten Objekttypen enthält.

Sie werden zum [!UICONTROL Paketobjekt und Abhängigkeiten] -Seite, auf der Sie die Anzahl der Objekte und Abhängigkeiten sehen können, die importiert und ausgeschlossen werden. Wählen Sie von hier aus **[!UICONTROL Import]** , um den Package-Import abzuschließen.

![Die [!UICONTROL Paketobjekt und Abhängigkeiten] Seite zeigt die Inline-Meldung der nicht unterstützten Objekttypen an, Hervorhebung [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

## Importvorgänge überwachen und Importobjektdetails anzeigen

Um die importierten Objekte und die importierten Details anzuzeigen, navigieren Sie zum [!UICONTROL Sandboxes] **[!UICONTROL Importe]** und wählen Sie das Paket aus der Liste aus. Alternativ können Sie die Suchleiste verwenden, um nach dem Paket zu suchen.

![Die Sandboxes [!UICONTROL Importe] markiert die Auswahl des Importpakets.](../images/ui/sandbox-tooling/imports-tab.png)

### Importierte Objekte anzeigen {#view-imported-objects}

Im **[!UICONTROL Importe]** im [!UICONTROL Sandboxes] Umgebung auswählen **[!UICONTROL Importierte Objekte anzeigen]** im rechten Detailbereich.

Auswählen **[!UICONTROL Importierte Objekte anzeigen]** aus dem rechten Detailbereich auf der **[!UICONTROL Importe]** im [!UICONTROL Sandboxes] Umgebung.

![Die Sandboxes [!UICONTROL Importe] hervorgehobene Registerkarte [!UICONTROL Importierte Objekte anzeigen] Auswahl im rechten Bereich.](../images/ui/sandbox-tooling/view-imported-objects.png)

Mithilfe der Pfeile können Sie Objekte erweitern, um die vollständige Liste der in das Package importierten Felder anzuzeigen.

![Die Sandboxes [!UICONTROL Importierte Objekte] zeigt eine Liste der in das Package importierten Objekte an.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### Importdetails anzeigen {#view-import-details}

Auswählen **[!UICONTROL Importdetails anzeigen]** im rechten Detailbereich im **[!UICONTROL Importe]** in der Sandbox-Umgebung.

![Die Sandboxes [!UICONTROL Importe] hervorgehobene Registerkarte [!UICONTROL Importdetails anzeigen] Auswahl im rechten Bereich.](../images/ui/sandbox-tooling/view-import-details.png)

Die **[!UICONTROL Importdetails]** zeigt eine detaillierte Aufschlüsselung der Importe.

![Die [!UICONTROL Importdetails] -Dialogfeld mit einer detaillierten Aufschlüsselung der Importe.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>Nach Abschluss eines Imports erhalten Sie Benachrichtigungen in der Platform-Benutzeroberfläche. Sie können auf diese Benachrichtigungen über das Warnungssymbol zugreifen. Sie können von hier aus zur Fehlerbehebung navigieren, wenn ein Auftrag nicht erfolgreich war.

## Nächste Schritte

In diesem Dokument erfahren Sie, wie Sie die Sandbox-Tool-Funktion in der Experience Platform-Benutzeroberfläche verwenden. Informationen zu Sandboxes finden Sie unter [Sandbox-Benutzerhandbuch](../ui/user-guide.md).

Anweisungen zum Ausführen verschiedener Vorgänge mit der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md). Eine allgemeine Übersicht über Sandboxes im Experience Platform finden Sie im Abschnitt [Übersichtsdokumentation](../home.md).