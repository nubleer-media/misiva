Misiva
======

Misiva is an Elixir/OTP application that sends push notifications (using the Apple Push Notification Service) to iOS apps.

## How to use it
- Create a connection passing the Push notification Certificate path, the path to the Push notification key, and an atom to identify the environment (:development or :production):

```elixir
{:ok, apns} = Misiva.connect {:production, "/etc/certificates/cert.pem", "/etc/certificates/key.pem"}
```

- Using that connection, you can send notifications using the *send* method. You can send and alert, a sound and a badge number

```elixir
Misiva.send apns,
 "f6af6af6af6af6af6af6af6af6af6af6af6af6af6af6af6af6af6af6af6af6aa", %Misiva.ApnsMessage{alert: "Hi from Misiva"}
```

Finally, once you finish sending the messages, call the *close* method to close the connection to the Apple server:
```elixir
Misiva.close apns
```

## Certificate creation
The certificates should be in *PEM* format. You can extract them from a *.p12* certificate file:


```
openssl pkcs12 -clcerts -nokeys -out cert.pem -in cert.p12

openssl pkcs12 -nocerts -out key.pem -in key.p12
```

Remove password from pem file

```
openssl rsa -in key.pem -out key-noenc.pem
```

