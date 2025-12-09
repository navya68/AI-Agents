API kay is the API of our own AI that we are going to use

1. OpenAI() is a class

It is like a blueprint that knows how to talk to OpenAI servers.

2. client is an object created from that class

- This object knows how to perform actions like:

- generate text

- analyze images

- get embeddings

3. You give API key TO THAT OBJECT
Why?
Because this object needs identity to communicate with the server

🔹 OpenAI is a special class

Not a normal one like:

```sh
class Car:
```

Instead, this class has code inside that knows how to:

make internet requests

talk to OpenAI server

send API calls

format responses

validate authentication
