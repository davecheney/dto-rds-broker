## Cloud Foundry RDS Service Broker

[![wercker status](https://app.wercker.com/status/9fd96a3ace53c3936c0111d34a1d889c/m "wercker status")](https://app.wercker.com/project/bykey/9fd96a3ace53c3936c0111d34a1d889c)

Cloud Foundry Service Broker to manage RDS instances and a shared RDS Database.

### Setup
There are important environment variables that should be overriden inside the `manifest.yml` file

> Note: All environment variables prefixed with `DB_` refer to attributes for the database the broker itself will use for internal uses.

1. `DB_URL`: The hostname / IP address of the database.
1. `DB_PORT`: The port number to access the database.
1. `DB_NAME`: The database name.
1. `DB_USER`: Username to access the database.
1. `DB_PASS`: Password to access the database.
1. `DB_TYPE`: The type of database. Currently supported types: `postgres` and `sqlite3`.
1. `DB_SSLMODE`: The type of SSL Mode to use when connecting to the database. Supported modes: `disabled`, `require` and `verify-ca`.
1. `AWS_ACCESS_KEY_ID`: The id credential with access to make requests to the Amazon RDS .
1. `AWS_SECRET_ACCESS_KEY`: The secret key (treat like a password) credential to access Amazon RDS.
1. `INSTANCE_TAGS`: Tags for the RDS instances.
1. `AWS_SEC_GROUP`: The security group for the RDS instances (`sg-xxxx`).
1. `AWS_DB_SUBNET_GROUP`: The name of DB subnet group for the RDS instances.

> Note the AWS Environment Variables should be generated by following the instructions [here](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/AWSCredentials.html)

> Make sure the account has write access to RDS and EC2 (particularly for VPC and Subnet).

> Example of permissions that suffice: `AmazonRDSFullAccess` and `AmazonEC2FullAccess`

### How to deploy it

1. `cf push`
1. `cf create-service-broker SERVICE-NAME USER PASS https://BROKER-URL`
1. `cf enable-service-access rds`


### How to use it

To use the service you need to create a service instance and bind it:

1. `cf create-service rds shared-psql MYDB`
1. `cf bind-service APP MYDB`

When you do that you will have all the credentials in the 
`VCAP_SERVICES` environment variable with the JSON key `rds`.

Also, you will have a `DATABASE_URL` environment variable that will
be the connection string to the DB.

### Public domain

This project is in the worldwide [public domain](LICENSE.md). As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.
