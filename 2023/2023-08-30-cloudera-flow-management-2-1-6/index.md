# Cloudera Flow Management 2.1.6

Cloudera is proud to announce the release of Cloudera Flow Management 2.1.6 which brings the latest and greatest of Apache NiFi 1.23 to all our Cloudera customers with a large set of exclusive features.

This release is supported with Cloudera Data Platform Private Cloud Base CDP 7.1.7 (all service packs), CDP 7.1.8 and CDP 7.1.9 which adds support for Java 17.

Here is a non exhaustive list of all the things you want to know about this release!

## Components Documentation

Previously, access to NiFi’s components documentation was only available through the Apache NiFi website or within the NiFi UI in a running instance. However, with this release, Cloudera makes the documentation of all CFM components (including the Cloudera-exclusive components) available as part of Cloudera Flow Management documentation. It is important to note that Cloudera’s distributions of NiFi incorporate over 100 components that are not available in the convenience binary of Apache NiFi. To access this documentation, see the [Cloudera Apache NiFi Components Reference Guide](https://docs.cloudera.com/cfm/2.1.6/nifi-components/index.html).

## Cloudera-exclusive Flow Library

Cloudera introduces a new Registry Client implementation, designed to facilitate access to the exclusive Cloudera Flow Library. This library contains predefined flow configurations to expedite the development and deployment of use cases in NiFi. While the Flow Library will see ongoing enhancements, it already offers access to all ReadyFlows included in the Cloudera DataFlow for Public Cloud data service. For additional information and instructions on how to configure the registry client, see [Using Flow Library Registry Client](https://docs.cloudera.com/cfm/2.1.6/using-flow-library-registry-client/index.html).

## Per Process Group Logging

In the configuration of a Process Group, you can now define a custom log file as the target for all log messages generated by the components within that process group. This custom log file will inherit the same properties as those specified in logback.xml for the nifi-app.log file. Despite this customization, all logs will continue to be recorded in the nifi-app.log file, unaffected by the process group-specific configuration. This is extremely useful for our customers using NiFi in a multi-tenant way wishing to separate the logs for every deployed use case for example.

## Improved Cloudera Manager integration

Cloudera Flow Management comes with this option to deploy NiFi and all of its friends (Schema Registry, NiFi Registry, Zookeeper, Atlas, Ranger, Knox, etc) using Cloudera Manager. It facilitates the configuration management, the upgrades, the monitoring, the integration of all the components. NiFi’s integration with Cloudera Manager has been improved by introducing a set of new features:

- Automatic Heap Dump Capture: In the event of an Out Of Memory error, NiFi now automatically captures a heap dump to help with diagnostic.
- Schema Registry Integration: You can include the Schema Registry component as a dependency during NiFi installation. This will configuration for you a Cloudera Schema Registry controller service in NiFi to seamlessly connect with the Schema Registry instance of CDP.
- Thread Pool Adjustment: The default size of NiFi’s Thread Pool is automatically set in NiFi to follow the best practices related to the number of cores available on the NiFi host.
- Enhanced Health Checks: This release incorporates additional health checks related to NiFi’s memory utilization and configuration.

## New components added since CFM 2.1.5 SP1

A large number of components have been added in this release and we’re particularly excited to bring great new capabilities into NiFi.

### 19 New Processors

- ExtractRecordSchema — You can use this processor to define a Record Reader and have the schema of your data inferred and added as a FlowFile attribute. If schema inference is required, Cloudera recommends to use this processor over the unsupported and deprecated InferAvroSchema processor.
- GenerateRecord
- GetAwsPollyJobStatus, GetAwsTextractJobStatus, GetAwsTranscribeJobStatus, GetAwsTranslateJobStatus, StartAwsPollyJob, StartAwsTextractJob, StartAwsTranscribeJob, StartAwsTranslateJob
- GetAzureQueueStorage_v12, PutAzureQueueStorage_v12
- ListenNetFlow (Cloudera Exclusive) This processor supports receiving NetFlow Export Packets over UDP for the NetFlow versions 1, 5, and 9. See [this blog post](https://medium.com/cloudera-inc/collecting-netflow-records-with-cloudera-dataflow-f47d9f57c98) for more details.
- ModifyCompression
- PutIcebergCDC [Technical Preview] (Cloudera Exclusive) You can use this processor to apply CDC events into Iceberg formatted tables.
- QueryIoTDBRecord
- RemoveRecordField
- ValidateJson
- VerifyContentMAC

### 11 New Controller Services

- ADLSCredentialsControllerServiceLookup
- AmazonGlueSchemaRegistry
- AzureServiceBusJMSConnectionFactoryProvider (Cloudera Exclusive)
- AzureStorageCredentialsControllerServiceLookup_v12
- ClouderaSchemaRegistry (Cloudera Exclusive) — You can use this controller service as a replacement of the HortonworksSchemaRegistry controller service, as it has been deprecated and marked for removal in anticipation of NiFi 2.0 release in the Apache NiFi project.
- CMLLookupService [Technical Preview] (Cloudera Exclusive) — You can use this controller service in combination with the LookupRecord processor to enrich data by calling Cloudera Machine Learning API to do ML scoring on streams of data.
- EBCDICRecordReader [Technical Preview] (Cloudera Exclusive) — You can use this reader with Cobol copybook files to read Mainframe data with EBCDIC encoding and convert the data into another structured format such as JSON, Avro, and so on.
- ExcelReader
- PostgreSQLConnectionPool (Cloudera Exclusive)
- RedshiftConnectionPool (Cloudera Exclusive)
- StandardFileResourceService

### 1 New Parameter Provider

- CyberArkConjurParameterProvider (Cloudera Exclusive) You can use this parameter provider to source the values of your parameters from a CyberArk instance.

## Conclusion

This release brings the latest and greatest of NiFi with a large set of Cloudera exclusive features (Cloudera Flow Library, CDC for Iceberg, processing of Mainframe data, etc). We hope you’re as excited as we are! As always feel free to reach out or comment this post if you have questions!
