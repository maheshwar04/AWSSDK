
# AWS SDK for Java - Getting Started Guide

This guide will help you get started with the AWS SDK for Java, enabling you to integrate various AWS services into your Java applications.

## Prerequisites

Before you begin, ensure you have the following:

- Java Development Kit (JDK) 8 or later
- Maven or Gradle for managing project dependencies
- AWS account with valid access keys (Access Key ID and Secret Access Key)

## Setup Instructions

### 1. Create a New Maven Project

Start by creating a new Maven project, if you don't have one already. Then, add the AWS SDK dependency in your `pom.xml` file:

```xml
<dependencies>
    <dependency>
        <groupId>software.amazon.awssdk</groupId>
        <artifactId>sdk-core</artifactId>
        <version>2.17.x</version> <!-- Use the latest SDK version -->
    </dependency>
</dependencies>
```

### 2. Configure AWS Credentials

For AWS authentication, you can use one of the following methods:

- **Environment Variables**: Set `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
- **Shared Credentials File**: Store your credentials in `~/.aws/credentials` (Linux/macOS) or `C:\Users\<username>\.aws\credentials` (Windows).

Example of the credentials file:

```
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
```

### 3. Initialize AWS SDK Client

You can now create an AWS SDK client. Here's how to initialize an S3 client:

```java
import software.amazon.awssdk.auth.credentials.ProfileCredentialsProvider;
import software.amazon.awssdk.services.s3.S3Client;

public class AwsSdkExample {

    public static void main(String[] args) {
        // Create an S3 client
        S3Client s3Client = S3Client.builder()
                                    .credentialsProvider(ProfileCredentialsProvider.create())
                                    .build();

        // Test client initialization
        System.out.println("AWS SDK for Java initialized successfully!");
    }
}
```

### 4. Running Your Application

Once your project is set up, you can build and run the application using Maven:

```bash
mvn clean install
mvn exec:java
```

## Example: List S3 Buckets

Here's a simple Java example to list all S3 buckets in your AWS account:

```java
import software.amazon.awssdk.services.s3.S3Client;
import software.amazon.awssdk.services.s3.model.ListBucketsRequest;
import software.amazon.awssdk.services.s3.model.ListBucketsResponse;

public class ListS3Buckets {

    public static void main(String[] args) {
        // Create an S3 client
        S3Client s3Client = S3Client.create();

        // List buckets
        ListBucketsRequest listBucketsRequest = ListBucketsRequest.builder().build();
        ListBucketsResponse listBucketsResponse = s3Client.listBuckets(listBucketsRequest);

        // Output the bucket names
        listBucketsResponse.buckets().forEach(bucket -> System.out.println(bucket.name()));
    }
}
```

### 5. Additional Resources

For further details on using the AWS SDK for Java, refer to the following resources:

- [Official AWS SDK for Java Developer Guide](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/get-started.html)
- [AWS SDK for Java GitHub Repository](https://github.com/aws/aws-sdk-java)
