# TD1: Installation of PostGIS and Creation of a Spatial Database

## Objective
This tutorial explains how to install PostgreSQL and PostGIS, and create a spatial database using pgAdmin 4.

---

## 1. Download and Install PostgreSQL
- Visit the [PostgreSQL download page](https://www.postgresql.org/download/) and download the latest version for your operating system (Linux, macOS, Windows, BSD, Solaris).
- Follow the installation guide for your operating system.
- During the installation process, set a password for the default `postgres` user. Make sure it is memorable, as it will be required to connect to the database.

---

## 2. Download and Install PostGIS
- During the PostgreSQL installation, check all components, including the **Stack Builder**.
- After the installation, the Stack Builder will launch automatically. Use it to download and install **PostGIS**, a spatial database extension.
- Follow these steps:
  1. Select the PostgreSQL version you just installed.
  2. Ensure you are connected to the internet.
  3. Select **PostGIS** as the application to download.
  4. Complete the installation process by specifying the installation directory and confirming when prompted.

---

## 3. Create a Database Using pgAdmin 4
1. Launch **pgAdmin 4**, a database management tool that comes with PostgreSQL.
2. Log in using the `postgres` password you set during installation.
3. Expand the **Servers** section, right-click on **PostgreSQL**, and select `Create > Database`.
4. Enter a name for your database (e.g., `spatial-db-1`) and click **Save**.

---

## 4. Add the PostGIS Extension
1. Navigate to your newly created database under **Databases**.
2. Right-click on the database and select **Query Tool**.
3. Run the following SQL command:
   ```sql
   CREATE EXTENSION postgis;

