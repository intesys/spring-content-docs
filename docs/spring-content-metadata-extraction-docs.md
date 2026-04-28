# Getting Started with Spring Content Metadata Extraction

## What you'll build

We'll build on the previous guide [Getting Started with Spring Content REST API](spring-content-rest-docs.md).

## What you'll need

- About 30 minutes

- A favorite text editor or IDE

- JDK 1.8 or later

- Maven 3.0+

## How to complete this guide

Before we begin let's set up our development environment:

- Download and unzip the source repository for this guide, or clone it
using Git: `git clone https://github.com/intesys/spring-content-gettingstarted.git`

- We are going to start where Getting Started with Spring Content REST API leaves off so
 `cd` into `spring-content-gettingstarted/spring-content-rest/complete`

When you’re finished, you can check your results against the code in
`spring-content-gettingstarted/spring-content-with-metadata-extraction/complete`.

## Update dependencies

Add the `it.intesys:spring-content-metadata-extraction-boot-starter` dependency.

`pom.xml`

```
{snippet: https://raw.githubusercontent.com/intesys/spring-content-gettingstarted/main/spring-content-with-metadata-extraction/complete/pom.xml 1-}
```

## Update FileContentStore

The Metadata Extraction module doesn't require any changes to your `ContentStore` interface. 
To be able to extract metadata from files, you need to import the MetadataExtractionService in your class:

```
@Service
public class MyServiceImpl implements MyService {

    private MetadataExtractionService metadataExtractionService;

    public MyServiceImpl(MetadataExtractionService metadataExtractionService) {
        this.metadataExtractionService = metadataExtractionService; (1)
    }

    public Map<String, Object> getFileMetadata(File file) {
        return metadataExtractionService.extractMetadata(file); (2)
    }
}
```

## Build an executable JAR

If you are using Maven, you can run the application using `mvn spring-boot:run`.
Or you can build the JAR file with `mvn clean package` and run the JAR
by typing:

`java -jar target/gettingstarted-spring-content-with-metadata-extraction-0.0.1.jar`

## Test Metadata Extraction

Create an entity from a real file:

`curl -X POST --form 'file=@Test.pdf' http://localhost:8080/files/from-real-file`

And you should see a response like this, with the metadata fields populated:

```
File successfully saved. Metadata: {fileName=Test.pdf, lastModifiedTime=2026-04-28T13:26:45.8672278Z, lastAccessTime=2026-04-28T13:26:45.8707391Z, size=39616, creationTime=2026-04-28T13:26:45.866221Z, fileExtension=pdf, mimeType=application/pdf}
```

## Summary

Congratulations!  You've just written a simple application that uses Spring Content and Spring Content Metadata Extraction to automatically extract metadata from your content.

This guide demonstrates the Spring Content Metadata Extraction Module. For more details see the Spring Content Metadata Extraction reference guide.
