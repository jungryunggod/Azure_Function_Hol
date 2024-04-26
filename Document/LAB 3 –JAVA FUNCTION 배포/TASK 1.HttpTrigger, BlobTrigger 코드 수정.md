# TASK 1.HttpTrigger, BlobTrigger 코드 수정

1.	[pom.xml](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Java/pom.xml)에 dependency를 추가합니다.
```xml
        <!-- 이미지 업로드 종속성 추가-->
        <dependency>
            <groupId>com.microsoft.azure.functions</groupId>
            <artifactId>azure-functions-java-library</artifactId>
            <version>3.1.0</version>
        </dependency>

        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-storage</artifactId>
            <version>8.6.5</version>
        </dependency>

        <!-- 썸네일 사용을 위한 의존성 추가 -->
        <dependency>
            <groupId>net.coobird</groupId>
            <artifactId>thumbnailator</artifactId>
            <version>0.4.8</version>
        </dependency>

        <!--BlobInputStream, BlobOutputStream 사용을 위한 의존성 추가-->
        <dependency>
            <groupId>com.azure</groupId>
            <artifactId>azure-storage-blob</artifactId>
            <version>12.25.3</version>
        </dependency>

        <!-- SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder". -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>2.13.5</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.13.5</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.dataformat</groupId>
            <artifactId>jackson-dataformat-xml</artifactId>
            <version>2.13.5</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.datatype</groupId>
            <artifactId>jackson-datatype-jsr310</artifactId>
            <version>2.13.5</version>
        </dependency>
```

2.	이미지 업로드시 파일정보를 알아내기 위해 기존에 추가했던 [BlobTriggerJava-OUTPUT.java](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Java/src/main/java/com/function/kms/BlobTriggerJava.java)파일의 코드를 수정합니다.
- Import 추가
```java
import java.io.IOException;
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import com.azure.storage.blob.*;
import com.microsoft.azure.functions.ExecutionContext;
import com.microsoft.azure.functions.annotation.FunctionName;
```

- BlobTrigger-OUTPUT 트리거 추가 
```java
    @FunctionName("BlobTriggerJava-OUTPUT")
    @StorageAccount("AzureWebJobsStorage")
    public void run(
        @BlobTrigger(name = "content", path = "output/{name}", dataType = "binary") byte[] content,
        @BindingName("name") String name,
        final ExecutionContext context
    ) {
        
        ByteArrayInputStream output = new ByteArrayInputStream(content);
        try {
            BufferedImage originalImage = ImageIO.read(output);
            int originalWidth = originalImage.getWidth();
            int originalHeight = originalImage.getHeight();
            
            if (name.startsWith("resizedImage")) {// 이미지 중복 체크
                context.getLogger().info("이미지가 output 컨테이너 Blob 저장소에 저장되었습니다. 파일명 :"+name); 
                context.getLogger().info("Image Size: " + originalWidth + "x" + originalHeight);
            } else {
                context.getLogger().info("Java Blob trigger function processed a blob. Name: " + name + "\n  Size: " + content.length + " Bytes");
            }
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
```


3.	이미지 리사이징을 위한 BlobTrigger-INPUT 코드(run2 메서드)를 추가합니다.
```java
    /* 저장대상 */
    private final String blobContainer = "output";
    
    @FunctionName("BlobTriggerJava-INOUT")
    @StorageAccount("AzureWebJobsStorage")
    public void run2(
        @BlobTrigger(name = "content", path = "input/{name}", dataType = "binary") byte[] content,
        @BindingName("name") String name,
        final ExecutionContext context
    ) {
        // Load image from input stream
        try {
            
            // 1. Load the input image
            ByteArrayInputStream input = new ByteArrayInputStream(content);
            BufferedImage originalImage = ImageIO.read(input);
            
            int 비율설정 = 2;

            // Get the dimensions of the original image
            int originalWidth = originalImage.getWidth();
            int originalHeight = originalImage.getHeight();
            int resizedWidth = originalImage.getWidth()/비율설정;
            int resizedHeight = originalImage.getHeight()/비율설정;
            
            // 2. Resize the image
            BufferedImage resizedImage = new BufferedImage(resizedWidth, resizedHeight, originalImage.getType());
            resizedImage.createGraphics().drawImage(originalImage, 0, 0, resizedWidth, resizedHeight, null);
            
            // 3. 처리된 이미지를 Blob 저장소에 업로드
            // 처리된 이미지를 ByteArrayOutputStream에 저장합니다.
            ByteArrayOutputStream output = new ByteArrayOutputStream();
            ImageIO.write(resizedImage, "png", output);
            
            // Azure Blob Storage 클라이언트 초기화
            // BlobServiceClient blobServiceClient = new BlobServiceClientBuilder().connectionString(storageConnectionString).buildClient();
            BlobServiceClient blobServiceClient = new BlobServiceClientBuilder().connectionString(System.getenv("AzureWebJobsStorage")).buildClient();
            BlobContainerClient containerClient = blobServiceClient.getBlobContainerClient(blobContainer);
            containerClient.getBlobClient("resizedImage_" + name).upload(new ByteArrayInputStream(output.toByteArray()), output.size());
            context.getLogger().info("이미지가 input 컨테이너 Blob 저장소에 저장되었습니다. 파일명 :"+name);
            context.getLogger().info("Original Image Size: " + originalWidth + "x" + originalHeight);
            context.getLogger().info("Resized Image Size: " + resizedWidth + "x" + resizedHeight);
            
        } catch (Exception e) {
            // TODO: handle exception
            context.getLogger().warning("Error processing image: " + e.getMessage());
            e.printStackTrace(); // 예외 스택 트레이스 출력
        }
    }
```