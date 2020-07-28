---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Schema und Datensatz für Einzelhandelsumsätze erstellen
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 64%

---


# Schema und Datensatz für Einzelhandelsumsätze erstellen

This tutorial provides you with the prerequisites and assets required for all other [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutorials. Upon completion, the Retail Sales schema and datasets will be available for you and members of your IMS Organization on [!DNL Experience Platform].

## Erste Schritte

Bevor Sie mit diesem Tutorial beginnen, müssen Sie folgende Voraussetzungen erfüllen:
- Access to [!DNL Adobe Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.
- Authorization to make [!DNL Experience Platform] API calls. Führen Sie die Anleitung zum [Authentifizieren und Aufrufen von Adobe Experience Platform-APIs](../../tutorials/authentication.md) aus, um die folgenden Werte abzurufen, damit die Anleitung erfolgreich abgeschlossen werden kann:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Client-Geheimnis: `{CLIENT_SECRET}`
   - Client-Zertifikat: `{PRIVATE_KEY}`
- Beispieldaten und Quelldateien für das [Rezept „Einzelhandelsumsätze“](../pre-built-recipes/retail-sales.md). Download the assets required for this and other [!DNL Data Science Workspace] tutorials from the [Adobe public Git repository](https://github.com/adobe/experience-platform-dsw-reference/).
- [ >= 2.7](https://www.python.org/downloads/)[!DNL Python] und die folgenden Python-Pakete:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Ein grundlegendes Verständnis der folgenden in dieser Anleitung verwendeten Konzepte:
   - [!DNL Experience Data Model (XDM)](../../xdm/home.md)
   - [Grundlagen der Schemakomposition](../../xdm/schema/field-dictionary.md)

## Schema und Datensatz für Einzelhandelsumsätze erstellen

Das Schema und die Datensätze für Einzelhandelsumsätze werden mithilfe des bereitgestellten Bootstrap-Skripts automatisch erstellt. Führen Sie folgende Schritte in der richtigen Reihenfolge aus:

### Dateien konfigurieren

1. Inside the [!DNL Experience Platform] tutorial resource package, navigate into the directory `bootstrap`, and open `config.yaml` using an appropriate text editor.
2. Geben Sie unter dem Abschnitt `Enterprise` die folgenden Werte ein:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Bearbeiten Sie die Werte, die Sie im Abschnitt `Platform` finden, wie im folgenden Beispiel:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: Der Basispfad für API-Aufrufe. Ändern Sie diesen Wert nicht.
   - `ims_token`: Ihr `{ACCESS_TOKEN}` gehört hier hin.
   - `ingest_data`: Setzen Sie für diese Anleitung den Wert auf `"True"`, um die Schemas und Datensätze für Einzelhandelsumsätze zu erstellen. Beim Wert `"False"` werden nur die Schemas erstellt.
   - `build_recipe_artifacts`: Setzen Sie für diese Anleitung den Wert auf `"False"`, um zu verhindern, dass das Skript ein Rezeptartefakt generiert.
   - `kernel_type`: Der Ausführungstyp des Rezeptartefakts. Lassen Sie diesen Wert unverändert bei `Python`, wenn `build_recipe_artifacts` auf `"False"` gesetzt ist; geben Sie andernfalls den entspechenden Ausführungstyp an.

4. Geben Sie unter dem Abschnitt `Titles` die folgenden Informationen für die Beispieldaten der Einzelhandelsumsätze ein; speichern und schließen Sie die Datei, nachdem Sie die Änderungen vorgenommen haben. Beispiel:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Bootstrap-Skript ausführen

1. Open your terminal application and navigate to the [!DNL Experience Platform] tutorial resource directory.
2. Set the `bootstrap` directory as the current working path and run the `bootstrap.py` [!DNL Python] script by entering the following command:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE] Das Skript kann mehrere Minuten in Anspruch nehmen.

## Nächste Schritte

Upon successful completion of the bootstrap script, the Retail Sales input and output schemas and datasets can be viewed on [!DNL Experience Platform]. Weiterführende Informationen finden Sie in der Anleitung zum [Anzeigen einer Vorschau von Schemadaten](./preview-schema-data.md).

You have also successfully ingested Retail Sales sample data into [!DNL Experience Platform] using the provided bootstrap script.

So arbeiten Sie weiter mit den aufgenommenen Daten:
- [Daten mit Jupyter-Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter Notebooks in Data Science Workspace, um auf Ihre Daten zuzugreifen, sie zu untersuchen, zu visualisieren und zu verstehen.
- [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md)
   - Follow this tutorial to learn how to bring your own Model into [!DNL Data Science Workspace] by packaging source files in an importable Recipe file.