---
title: Connect with pgAdmin
---

import ConsoleLabel from "@site/src/components/ConsoleIcons";

Connect to an Aiven for AlloyDB Omni database using [pgAdmin](https://www.pgadmin.org/), which is a PostgreSQL® client useful for managing and querying databases.

## Prerequisites

- Aiven for AlloyDB Omni service running
- Values of your service's connection parameters identified in the Aiven Console >
  the service's <ConsoleLabel name="overview"/> page > **Connection information**

  - **Database name**
  - **Host**
  - **Port**
  - **User**
  - **Password**

- [pgAdmin installed on your computer](https://www.pgadmin.org/download/)

## Connect to a service

1. Open pgAdmin and click **Create new server**.
1. In the **General** tab, give the connection a name, for example `MyDatabase`.
1. In the **Connection** tab, set the connection parameters using the values available in
   the Aiven Console > the service's <ConsoleLabel name="overview"/> page >
   **Connection information**.

   - **Host name/address**
   - **Port**
   - **Maintenance database**
   - **Username**
   - **Password**

1. In the **SSL** tab, set **SSL mode** to `Require`.
1. Click **Save**.

:::tip
If you experience an SSL error while connecting, add the service CA certificate as the
**Root certificate**.

1. Download the CA certificate file to your computer.
1. In the pgAdmin connection settings > the **SSL** tab, select the downloaded CA
   certificate and save the settings.

:::

The connection to your Aiven for AlloyDB Omni service should now be opened, with the
pgAdmin **Dashboard** page showing activity metrics on your database.
