# WORKSHOP-Node-RED
Learn the basics of Node-RED!
In this workshop, you will learn how to install and use Node-RED.

## Pre-requisites

If you want to use Docker, simply execute the following command to pull and run a Node-RED container:
`docker run -p 1880:1880 nodered/node-red`

Otherwise:

Install Node.js
`sudo apt install npm`

Install Node-RED
`sudo npm install -g node-red`

Start Node-RED
`node-red`

Once started, you can access the Node-RED interface with your browser at http://localhost:1880.

## Let's get started!

### First things first

Node-RED is a visual developing tool based on node.js.
It is mostly used for small projects, often falling in the IoT domain.

In this workshop, we will learn how to make a basic server with it.



First, you can see a grid, which is called "Flow", this is where we will place our "Nodes" and link them to execute our program.

![](https://cdn.discordapp.com/attachments/517409912129716224/717510220867305492/unknown.png)
On the left side, you can see a list of nodes, sorted in categories. We'll start with the first available node, "Inject". Simply drag it from the left panel and drop it in the flow.
Now drag and drop a "Debug" node in the flow, and link the nodes together by dragging the output from "Inject" to the input of "Debug".
You can now deploy your flow with the "Deploy" button, open the console tab, and trigger your Inject node to see what happens.
If everything went right, triggering your Inject node outputs a timestamp in your console. Great!
![](https://cdn.discordapp.com/attachments/517409912129716224/717510997669183618/unknown.png)

Now let's head to the HTTP section to make our server.

Grab a `http in` node to configure our first route.
Double click on the node to open its settings. In here you can set the HTTP method you wish to receive (we'll use GET for this example), as well as the URL to your route (we'll use "/test" for this example).
![](https://cdn.discordapp.com/attachments/517409912129716224/719529756001042432/unknown.png)
Link your "http in" node to a debug node and deploy.
Now you can try to access your new route with your browser (http://localhost:1880/test if you followed the example).
You won't receive any response because we haven't set one yet, but in your Node-RED console you should be able to see a new output, generated by your request.

Now let's see how to send a response to a request:
Grab a `http response` node, drop it in your flow and link it to the previous "http in" node.
Again, by double-clicking it you can access its settings. Here you can set the status code you wish to respond with, as well as some HTTP headers. For this example, we'll simply send a *200* status code (OK).
![](https://cdn.discordapp.com/attachments/517409912129716224/719531322816725022/unknown.png)

You can now deploy your flow, and try to access http://localhost:1880/test again.
While the response is still empty, at least it was completed.

We'll now grab a `http request` to fill up our response.
This node is a bit more complex, so let's break it down:
![](https://cdn.discordapp.com/attachments/517409912129716224/719532071579680798/unknown.png)
First you can see this node has both an *input* and an *output*, which means we can use it to make a request whenever it receives one from the "http in" node, and output the response into the "http response" node.
In the settings you can set the HTTP method to use (we'll use GET for this example), as well as the URL to the ressource we want, a few HTTP settings that we're going to ignore for now, and a return type (we'll set it to "a parsed JSON object" for this example).

As for the URL, in this example we'll use https://api.jokes.one/jod, a simple joke API that delivers jokes.

Now you can save your node settings, make sure it is linked to both HTTP nodes, and deploy. Now if you try to access http://localhost:1880/test, you should receive a JSON object containing a joke.

Finally, another node worth mentioning is the `function` node. It is a highly flexible node that executes any javascript code you put in it. It has many uses and can be set to have as many inputs/outputs to satisfy all your needs.

If you're feeling adventurous, you can try to output only the text part of the joke to make it user-friendly!
