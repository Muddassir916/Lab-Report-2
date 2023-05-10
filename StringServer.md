# **Greetings!**
## **Part 1**
Code for `StringServer`:
``` java
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;
    String msg = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Muddassir's number: %d", num);
        } else if (url.getPath().equals("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } else if (url.getPath().equals("/add-message") && url.getQuery().startsWith("s=")) {
            String query = url.getQuery()/*.split("&")[0] */.split("=")[1];
            msg += query + "\n";
            return msg;
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("count")) {
                    num += Integer.parseInt(parameters[1]);
                    return String.format("Number increased by %s! It's now %d", parameters[1], num);
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

Examples of `StringServer`:

![Image](ge.png)

In this screenshot, we added our first string 'Hello' by using `/add-message?s=Hello`. The method being called is `handleRequest`, which takes the url, looks at the end of it and if the path is equal to `/add-message?s=[ANYTHING]`, it adds it. The most relevant arguement is likely `/add-message?s=[ANYTHING]`, because typing it precisely like so is the only way for the server to update the string value. When we first run it, no values are changed, because it is the first string we added. 
`/add-message?s=
---

![Image](imge.png)

In this screenshot, we added our second string 'How are you' by using `/add-message?s=How are you`, which included it along with our pre-existing string 'Hello'. It uses the same method `handleRequest` in the class `Handler`, but it prints on the second line because of the `/n` in the code, where it moves it to a new line, and following the old added string. The most relevant arguement is also `/add-message?s=[ANYTHING]`, because it adds to the other string. The value, however, will be updated, so it does change the value when this is called a second time. 

## **Part 2**

This code displays a failure-inducing input for the buggy program
``` java
  @Test 
  public void testSumEvensLength4() {
    int[] input1 = { 12, 13, 7, 2};
    assertEquals(EvensExample.sumEvenIndices(input1), 19);
  }
```
The result of the code above (It fails): 

![Image](fail.png)
---
This code doesnt not display a failure-inducing input for the buggy program
``` java
  @Test
  public void testSumEvenLength6() {
    int[] input1 = { 12, 13, 7, 8, 5, 3};
    assertEquals(EvensExample.sumEvenIndices(input1), 24);
  }
```
The result of the code above (It passes): 

![Image](pass.png)


## **Part 3**
In the past two weeks, I did not know you are able to update the info of a webpage with methods inputted through the URL. I assumed to update the contents of a webpage, you would need to go to the specific code and input it there, but to be able to change the value from the site itself was pretty cool. Setting up a local host 4000 was also foreign to me, but I have heard it being mentioned, but now I understand how these localhosts work. I also didn't know browsers usually run on 80 or 443, so that was cool to know. 
