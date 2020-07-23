# Lab 2 - Lets get RESTful :dancer: 

In this lab you are going to create a web app with some routes. To do this you will use the `net/http` library. You will then extend this to output a random joke by calling an open API without the need for authentication. The API in this lab is a random dad joke API but feel free to explore and chose another if you'd like, the principals are the same!

### Step 1

We will start by creating a route handler. Below your `main()` function in `main.go`, add the following snippet of code.

```golang
func home(w http.ResponseWriter, r *http.Request) {
	// Assign the 'msg' variable with a string value
	msg := "Hello, welcome to your app. Use the following suffix's on the URL to show the different results.\n1)'/scrape' to show results of web scraping.\n2)'/crawl' to show results of a web crawler"

	// Logs a message to the terminal using the 3rd party import logrus
	logr.Info("Received request for the home page")

	// Write the response to the byte array - Sprintf formats and returns a string without printing it anywhere
	w.Write([]byte(fmt.Sprintf(msg)))
}
```

> **Note**: You will also need to add the following import to your code (this makes the terminal logs look pretty). To do this, your imports should look like:

```golang
import (
    "fmt"
    "net/http"
    "io/ioutil"

    // You can prefix imports to make it easier to reference them in your code, like this one
    logr "github.com/sirupsen/logrus"
)
```

### Step 2

Now you have got a route handler, you need to create the web server to invoke it. To do this, use the code snippet below and insert it into your `main()` function. You will be using the standard `net/http` library and this demonstrates just how easy it is to spin one up in Golang!

```golang
// Create the first route handler listening on '/'
http.HandleFunc("/", home)
logr.Info("Starting up on 8080")

// Start the sever
http.ListenAndServe(":8080", nil)
```

### Step 3

Head back to your terminal window and run your code using the command `go run cmd/main.go`. This will start up a server on port :8080.

> **Note**: You may be prompted by your system to allow a network connection (you need to allow this otherwise the application may not run corretly)

Open up a browser and type `localhost:8080` into the top URL bar, and you should see the output from the `home()` function on your screen.

The server is up and running but this is very basic. Use `control+c` in your terminal to terminate the server connection.

Now the server is ready, lets deploy this app and use the power of the cloud to build and process our requests. 

Continue to [Lab 3](./lab-3.md) to see how this is done.
