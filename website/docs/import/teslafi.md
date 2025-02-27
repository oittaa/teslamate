---
title: Import from TeslaFi (BETA)
sidebar_label: TeslaFi
---

## Requirements

- **CREATE A [BACKUP](../maintenance/backup_restore.md) OF YOUR DATA‼️**

- If you have been using TeslaMate since before the 1.16 release, the [docker-compose.yml](../installation/docker) needs to be updated. Add the following volume mapping to the `teslamate` service:

  ```yml {4-5}
  services:
    teslamate:
      # ...
      volumes:
        - ./import:/opt/app/import
  ```

- Export your TeslaFi data (for one car) as CSV by month: `Settings -> Account -> Download TeslaFi Data`.

## Instructions

1. Copy the exported CSV files into a **directory named `import`** next to the _docker-compose.yml_:

   ```console
   .
   ├── docker-compose.yml
   └── import
       ├── TeslaFi82019.csv
       ├── TeslaFi92019.csv
       ├── TeslaFi102019.csv
       ├── TeslaFi112019.csv
       └── TeslaFi122019.csv
   ```

   :::tip
   The path of the import directory can be customized with the **IMPORT_DIR** [environment variable](../configuration/environment_variables).
   :::

2. **Restart** the teslamate service and open the TeslaMate admin interface. Now the import form should be displayed instead of the vehicle summary.
3. Since the raw data is in the local timezone (assigned by the home address in the TeslaFi settings page) you need to **select your local timezone**. Then start the import.
4. On low-end hardware like the Raspberry Pi, importing a large data set spanning several years will take a couple of hours. After the import is complete, remove or **empty the `import` directory** and **restart** the `teslamate` service.

:::note
If there is an overlap between the already existing TeslaMate and TeslaFi data, only the data prior to the first TeslaMate data will be imported.
:::

:::note
Since the exported CSV files do not contain addresses, they are added automatically during and after the import. So please note that not all addresses are visible immediately after the import/restarting. Depending on the amount of data imported, it may take a while before they appear. The same applies to elevation data.
:::
