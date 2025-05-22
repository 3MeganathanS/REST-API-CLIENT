# REST-API-CLIENT

*COMPANY*: CODTECH IT SOLUTIONS

*NAME*: MEGANATHAN S

*INTERN ID*: CT12DN552

*DOMAIN*: JAVA PROGRAMMING

*DURATION*: 12 WEEKS

*MENTOR*: NEELA SANTOSH

### Description of Task 2

Task 2 required the design and implementation of a Java-based *REST API Client* that:

1. Consumes a *public geocoding API* to translate city names into geographic coordinates (latitude & longitude).
2. Uses those coordinates to fetch *current weather data* (temperature, humidity, wind speed, timestamp) from a public weather API.
3. Presents the combined data in a clear, structured console output.

This two-stage approach showcases chaining of HTTP requests, robust JSON parsing, and a user‐friendly, loop-driven command-line interface.

## 2. Development Environment & Tools

* **Editor / IDE**: IntelliJ IDEA – chosen for its powerful code navigation, integrated build tools (Maven/Gradle), and seamless debugger interface.
* **Build & Dependency Management**: Maven (pom.xml) to pull in the `org.json.simple` library.
* **HTTP Client**: Java’s built-in `HttpURLConnection` for lightweight, no-external-dependency request handling.
* **JSON Parsing**: `org.json.simple` (JSONParser, JSONObject, JSONArray) for straightforward object mapping.
* **Utilities**:

  * `Scanner` for interactive user input.
  * `StringBuilder` for efficient response accumulation.
* **Runtime & Compiler**: Java SE 17 (OpenJDK)
* **Operating System**: Windows 11 / Ubuntu 22.04 (cross-platform testing)
* **Version Control**: Git + GitHub – repository initialized at project root; all source files, a `README.md` with setup steps, and the generated JAR in a `dist/` folder.

---

## 3. Functional Description

1. **Interactive Prompt Loop**

   * On launch, the program prints a separator line and prompts:

     ```
     Enter City (Say No to Quit):
     ```
   * Accepts multi-word city names (spaces replaced by `+` for URL safety).
   * Continues until user inputs “No” (case-insensitive).

2. **Geocoding API Call**

   * URL template:

     ```
     https://geocoding-api.open-meteo.com/v1/search?name=<city>&count=1&language=en&format=json
     ```
   * Parses the JSON response’s `results` array, extracts the first object’s `latitude` and `longitude`.
   * Handles cases where `results` is empty by notifying the user “City not found,” then loops back.

3. **Weather Forecast API Call**

   * URL template:

     ```
     https://api.open-meteo.com/v1/forecast?latitude=<lat>&longitude=<lon>&current=temperature_2m,relative_humidity_2m,wind_speed_10m
     ```
   * Parses the JSON object’s `current` section for:

     * `time` (ISO 8601 timestamp)
     * `temperature_2m` (°C)
     * `relative_humidity_2m` (%)
     * `wind_speed_10m` (m/s)
   * Prints each field with clear labels.

4. **Error Handling & Validation**

   * Checks HTTP response codes; non-200 codes print “Error: Could not connect to API (code).”
   * Wraps network and parsing calls in `try–catch` to prevent crashes on malformed JSON or I/O failures.

---

## 4. Real-World Applications

* **Command-Line Dashboards**
  Integrate live weather data into terminal‐based dashboards for system administrators or remote servers.
* **Microservices & Automation**
  Acts as a lightweight client in a larger microservice architecture, fetching weather data on schedule and pushing it to databases or message queues.
* **IoT & Edge Devices**
  Runs on embedded Linux boards (e.g., Raspberry Pi) to adjust environmental controls based on real-time conditions.
* **Educational Tools**
  Serves as a teaching example for HTTP networking, API integration, and JSON parsing in university or bootcamp settings.

---

## 5. Challenges & Resolutions

1. **Chaining API Calls**

   * **Issue**: Handling a missing geocoding result led to null pointers.
   * **Solution**: Added explicit checks on the `results` array length before casting.

2. **JSON Type Casting**

   * **Issue**: JSON numbers sometimes parse as `Long` vs. `Double`.
   * **Solution**: Used conditional casting (e.g., `instanceof`) and explicit conversions to uniform types.

3. **User-Input Robustness**

   * **Issue**: Empty strings and unexpected keywords caused the loop to misbehave.
   * **Solution**: Trimmed input, validated against a regex for “^\[A-Za-z ]+\$” before proceeding.

4. **Network Reliability**

   * **Issue**: Temporary connectivity failures triggered uncaught IOExceptions.
   * **Solution**: Wrapped connection logic in a retry loop with exponential back-off (up to three attempts).

---

## 6. Key Learning Outcomes

* **Mastered `HttpURLConnection`** for GET requests, headers, and response code handling.
* **Gained fluency with `org.json.simple`** for parsing nested objects and arrays.
* **Adopted best practices** in modular code design: clear separation (`getLocationData()`, `displayWeatherData()`, `fetchApiResponse()`, `readApiResponse()`).
* **Enhanced debugging skills**: step-through in IntelliJ, breakpoints in catch blocks, and inspection of parsed JSON.
* **Strengthened version control habits**: meaningful commit messages, branch for feature work, pull-request review simulation.

---

## Output
![Image](https://github.com/user-attachments/assets/9bc00632-5fc3-49f9-8186-25b22b792afe)
