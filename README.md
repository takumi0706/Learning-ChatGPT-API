# ChatGPT Travel Planner Assistant

This Java application uses the OpenAI ChatGPT API to generate travel plans based on user input. The program sends a prompt to the ChatGPT model and retrieves a response with travel recommendations.

## Features

- Connects to the OpenAI ChatGPT API
- Generates travel plans based on user prompts
- Extracts and displays relevant information from the API response

## Prerequisites

- Java Development Kit (JDK) installed
- OpenAI API key

## Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/takumi0706/LearningForMybatis.git
   cd LearningForMybatis
   ```

2. **Set up your OpenAI API key:**

   Open the `Main.java` file and replace `"YOUR_API_KEY"` with your actual OpenAI API key:

   ```java
   String apiKey = "YOUR_API_KEY";
   ```

## Usage

1. **Compile the Java program:**

   ```bash
   javac Main.java
   ```

2. **Run the program:**

   ```bash
   java Main
   ```

   By default, the program sends a prompt about travel planning for Hawaii. You can modify the prompt in the `main` method as needed:

   ```java
   String temp_prompt = """
   You are a travel planner assistant. Please respond to the user's question in the following format:

   - Destination:
   - Recommended Activities:
   - Best Time to Visit:
   - Important Notes:
   """;
   System.out.println(chatGPT(temp_prompt + "Hawaii"));
   ```

## Code Explanation

### Main.java

- **chatGPT(String prompt):** This method sends a POST request to the OpenAI API with the specified prompt and retrieves the response.

- **extractMessageFromJSONResponse(String response):** This method extracts the relevant message from the JSON response returned by the API.

- **main(String[] args):** The entry point of the program. It sets up the prompt and calls the `chatGPT` method to get the travel plan.

### Example Code

```java
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {

    public static String chatGPT(String prompt) {
        String url = "https://api.openai.com/v1/chat/completions";
        String apiKey = "YOUR_API_KEY";
        String model = "gpt-3.5-turbo";

        try {
            URL obj = new URL(url);
            HttpURLConnection connection = (HttpURLConnection) obj.openConnection();
            connection.setRequestMethod("POST");
            connection.setRequestProperty("Authorization", "Bearer " + apiKey);
            connection.setRequestProperty("Content-Type", "application/json");

            // The request body
            String body = String.format("{\"model\": \"%s\", \"messages\": [{\"role\": \"user\", \"content\": \"%s\"}]}", model, prompt.replace("\n", "\\n"));
            connection.setDoOutput(true);
            OutputStreamWriter writer = new OutputStreamWriter(connection.getOutputStream());
            writer.write(body);
            writer.flush();
            writer.close();

            // Response from ChatGPT
            BufferedReader br = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String line;
            StringBuffer response = new StringBuffer();

            while ((line = br.readLine()) != null) {
                response.append(line);
            }
            br.close();

            // calls the method to extract the message.
            return extractMessageFromJSONResponse(response.toString());

        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }

    public static String extractMessageFromJSONResponse(String response) {
        int start = response.indexOf("content") + 11;
        int end = response.indexOf("\"", start);
        return response.substring(start, end);
    }

    public static void main(String[] args) {
        String temp_prompt = """
        You are a travel planner assistant. Please respond to the user's question in the following format:

        - Destination:
        - Recommended Activities:
        - Best Time to Visit:
        - Important Notes:
        """;
        System.out.println(chatGPT(temp_prompt + "Hawaii"));
    }
}
```

## Troubleshooting

- **API Authentication Error:** Ensure that your API key is correctly set in the `Main.java` file.
- **Connection Error:** Check your internet connection and ensure that the OpenAI API endpoint is accessible.
- **Response Parsing Error:** If the API response format changes, you may need to update the `extractMessageFromJSONResponse` method.

## Additional Resources

- [OpenAI API Documentation](https://platform.openai.com/docs/api-reference)
- [Java HTTPURLConnection Documentation](https://docs.oracle.com/javase/8/docs/api/java/net/HttpURLConnection.html)

This README provides a comprehensive guide to setting up and using the Java application to interact with the ChatGPT API for generating travel plans.

Citations:
[1] https://www.etsy.com/listing/1113912704/travel-planner-travel-journal-vacation?gpla=1
[2] https://www.amazon.com/Inspired-Travel-Journal-Women-Avocado/dp/B0CFLC9XKM?psc=1&smid=AV2KARB6UJKZT
[3] https://www.etsy.com/listing/1747264415/digital-travel-planner-organizer-trip?gpla=1
[4] https://www.etsy.com/listing/1703302338/travel-planner-for-google-sheets-trip?gpla=1
[5] https://www.amazon.com/Inspired-Ink-Travel-Journal-Women/dp/B0CQKHZLNQ?psc=1&smid=AV2KARB6UJKZT
[6] https://www.etsy.com/listing/1025787053/complete-travel-planner-sunday-start?gpla=1
[7] https://www.inspireuplift.com/Trip-Planner-Travel-Planner-Trip-Itinerary-Digital-Vacation-Planner-/iu/849003?variant=26285255
[8] https://www.sears.com/erin-condren-a5-spiral-bound-travel-journalvacation-planner/p-A117359703?sid=ISxMP3xSOxGGxDTxSURF
[9] https://www.zirtual.com/what-we-do/travel-planning/
[10] https://rollbar.com/blog/how-to-use-chatgpt-api-with-java/
[11] https://platform.openai.com/docs/api-reference
[12] https://www.travelive.com/careers/travel-planner-assistant
[13] https://gist.github.com/gantoin/190684c344bb70e5c5f9f2339c7be6ed
[14] https://platform.openai.com/docs/guides/chat
[15] https://copilot2trip.com
[16] https://zenn.dev/umi_mori/books/chatbot-chatgpt/viewer/openai_chatgpt_api_java
[17] https://platform.openai.com/docs/guides/text-generation/text-generation-models
[18] https://www.meetsam.io
[19] https://www.bmc.com/blogs/how-to-access-chatgpt-api-java/
[20] https://chatgpt.com/g/g-I1XNbsyDK-api-docs
