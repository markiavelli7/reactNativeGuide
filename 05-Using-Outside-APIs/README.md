## Using Outside APIs

We are going to use Axios to interact with exterior APIs. Axios gives us easy-to-use, sensible defaults.

## Setting up an API File for Reusability

**src/api/yelp.js**
```javascript
import axios from "axios";

export default axios.create({
  baseURL: "https://api.yelp.com/v3/businesses",
  headers: {
    Authorization:
      "Bearer oDwbxW3XCsj8viCgxxYGo0Qo20YPGBYv_o0i_bzD91ZIFIp19BIDx1kjieucM15VHXijgM39-JfuXl9jL_wtaHTlSxwBU3exhMY_UdfnYS4IIwDjCoMBZgA9v7nxXXYx"
  }
});
```

Adding this boilerplate will let us make requests without needing to use the full URL and adding the Authorization Bearer token on every single request.

**HomeScreen.js**
```javascript
import yelp from "../api/yelp";

function HomeScreen() {
  var [term, setTerm] = useState("");
  var [restaurants, setRestaurants] = useState([]);

  async function searchApi() {
    var apiResponse = await yelp.get("/search", {
      params: {
        limit: 50,
        term,
        location: "edmonton"
      }
    });
    setRestaurants(apiResponse.data.businesses);
  }

  ...
```

## Handling Errors

```javascript
function HomeScreen() {
  var [term, setTerm] = useState("");
  var [restaurants, setRestaurants] = useState([]);
  var [errorMessage, setErrorMessage] = useState("");

  async function searchApi() {
    try {
      var apiResponse = await yelp.get("/search", {
        params: {
          limit: 50,
          term,
          location: "edmonton"
        }
      });

      setRestaurants(apiResponse.data.businesses);
    } catch (err) {
      setErrorMessage("Something went wrong!");
    }
  }
```