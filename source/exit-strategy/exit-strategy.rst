Exit strategy
=============

There are two primary ways of systematically exporting the data from OS2iot:

1. Using the REST API

    a. Ideal if you want to import/change it into something else, and OS2iot is still running.

2. Exporting the database

    a. If OS2iot is no longer running, the postgres database will contain all the data from the system.

Export using the REST API
-------------------------

The REST API documentation is available at https://your-backend-hostname.tld/api/v1/docs/#/

After using the login endpoint to get a JWT, use it for the calls.

It is recommended that you use a user with Global Admin privileges to export data.

Depending on the goal of the exit, you want to use different data, but in general the following order to export data is recommended:

1. Organization

2. Applications

3. Device Model

4. IoTDevices

5. Datatargets

6. Payload decoder

7. IoT-Device, PayloadDecoder and DataTarget Connection

Optionally you can export the internal users and their access groups:

1. User

2. Permission

If you want to export Sigfox data too then:

1. Sigfox Group

2. Sigfox Device Type

3. Sigfox Contract

If you want to export LoRaWAN (Chirpstack) data then:

1. Gateway

2. Service Profile

3. Device Profile

Export using the database
-------------------------

A full database dump of the PostgreSQL database will backup most of the data. 
Sigfox data is stored in their backend; LoRaWAN gateways, service-profiles, and device-profiles are stored in Chirpstacks PostgreSQL database.

It is recommended to use :code:`pg_dump` to dump the database: https://www.postgresql.org/docs/current/backup-dump.html 

I.e. :code:`pg_dump -d os2iot -U os2iot -W -h localhost -p 5433 > backup.sql` will perform the export on the docker-compose setup described in the `Installation Guide <installation-guide/installation-guide.html>`_.
