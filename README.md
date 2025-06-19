
# Hoen Scanner Microservice (Skyscanner Task 1)

This is a Dropwizard-based Java microservice that serves hotel and rental car search results based on user input. It exposes a `/search` endpoint that accepts JSON-encoded POST requests and returns relevant listings.

---

## ✅ Project Setup

### 1. Requirements
- IntelliJ IDEA (recommended IDE)
- OpenJDK 19
- Maven

### 2. Getting Started
1. Clone the repository:
   ```bash
   git clone https://github.com/YOUR-USERNAME/hoen-scanner.git
   cd hoen-scanner
   ```

2. Open the project in IntelliJ IDEA.

3. Load Maven project when prompted.

4. Make sure JDK 19 is installed and selected in your project settings.

5. Run the application:
   - Click the green run arrow or use:
     ```bash
     mvn clean install
     java -jar target/hoen-scanner-1.0-SNAPSHOT.jar server config.yml
     ```

6. You should see `Welcome to Hoen Scanner!` in the logs.

---

## 🧩 Data Models

### `Search.java`
```java
import com.fasterxml.jackson.annotation.JsonProperty;

public class Search {
    @JsonProperty
    private String city;

    public Search() {}

    public String getCity() { return city; }
    public void setCity(String city) { this.city = city; }
}
```

### `SearchResult.java`
```java
import com.fasterxml.jackson.annotation.JsonProperty;

public class SearchResult {
    @JsonProperty private String city;
    @JsonProperty private String kind;
    @JsonProperty private String title;

    public SearchResult() {}

    public SearchResult(String city, String kind, String title) {
        this.city = city;
        this.kind = kind;
        this.title = title;
    }

    public String getCity() { return city; }
    public String getKind() { return kind; }
    public String getTitle() { return title; }
}
```

---

## ⚙️ Modify `HoenScannerApplication.java`
```java
@Override
public void run(HoenScannerConfiguration configuration, Environment environment) throws Exception {
    ObjectMapper mapper = new ObjectMapper();

    List<SearchResult> hotelResults = mapper.readValue(
        getClass().getResource("/hotels.json"),
        new TypeReference<List<SearchResult>>() {}
    );

    List<SearchResult> carResults = mapper.readValue(
        getClass().getResource("/rental_cars.json"),
        new TypeReference<List<SearchResult>>() {}
    );

    List<SearchResult> allResults = new ArrayList<>();
    allResults.addAll(hotelResults);
    allResults.addAll(carResults);

    environment.jersey().register(new SearchResource(allResults));
}
```

---

## 🌐 `SearchResource.java`
```java
import javax.ws.rs.*;
import javax.ws.rs.core.MediaType;
import java.util.List;
import java.util.stream.Collectors;

@Path("/search")
@Produces(MediaType.APPLICATION_JSON)
@Consumes(MediaType.APPLICATION_JSON)
public class SearchResource {
    private final List<SearchResult> searchResults;

    public SearchResource(List<SearchResult> searchResults) {
        this.searchResults = searchResults;
    }

    @POST
    public List<SearchResult> search(Search search) {
        return searchResults.stream()
                .filter(result -> result.getCity().equalsIgnoreCase(search.getCity()))
                .collect(Collectors.toList());
    }
}
```

---

## 🧪 Testing with Postman

1. Open [Postman](https://www.postman.com/)
2. Create a **POST** request to: `http://localhost:8080/search`
3. Go to **Body → raw → JSON** and paste:
```json
{
  "city": "petalborough"
}
```
4. Click **Send**
5. You should see the filtered results for that city.

Try also: `"city": "rustburg"` or `"city": "shaleport"`

---

## 🚀 Deploying to GitHub

```bash
git init
git add .
git commit -m "Initial commit: Hoen Scanner microservice with /search endpoint"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/hoen-scanner.git
git push -u origin main
```

Then submit this link as your final submission:
```
https://github.com/YOUR-USERNAME/hoen-scanner
```

---

## 📁 Provided Data Files
Place these in `src/main/resources/`:
- `hotels.json`
- `rental_cars.json`

---

## ✅ Task Complete!
If the microservice runs and returns results correctly via Postman, your task is complete.
