---
title:  "Utility to debug Java http connection"
date:   2017-07-25 21:27:21 +0800
categories: java
---

If the certificate of the host is not valid (self signed) or didn't well configured in java keystore, then it will fail to connect.

```java

import java.io.InputStream;
import java.io.OutputStream;
import java.io.PrintStream;
import javax.net.ssl.SSLHandshakeException;
import javax.net.ssl.SSLSocket;
import javax.net.ssl.SSLSocketFactory;

public class SSLPoke
{
  public static void main(String[] paramArrayOfString)
  {
    if (paramArrayOfString.length != 2)
    {
      System.err.println("Utility to debug Java connections to SSL servers");
      System.err.println("Usage: ");
      System.err.println("  java " + SSLPoke.class.getName() + " <host> <port>");
      System.err.println("or for more debugging:");
      System.err.println("  java -Djavax.net.debug=ssl " + SSLPoke.class.getName() + " <host> <port>");
      System.err.println();
      System.err.println("Eg. to test the SSL certificate at https://localhost, use");
      System.err.println("  java " + SSLPoke.class.getName() + " localhost 443");
      System.exit(1);
    }
    try
    {
      SSLSocketFactory localSSLSocketFactory = (SSLSocketFactory)SSLSocketFactory.getDefault();
      SSLSocket localSSLSocket = (SSLSocket)localSSLSocketFactory.createSocket(paramArrayOfString[0], Integer.parseInt(paramArrayOfString[1]));

      InputStream localInputStream = localSSLSocket.getInputStream();
      OutputStream localOutputStream = localSSLSocket.getOutputStream();

      localOutputStream.write(1);
      while (localInputStream.available() > 0) {
        System.out.print(localInputStream.read());
      }
      System.out.println("Successfully connected");
      System.exit(0);
    }
    catch (SSLHandshakeException localSSLHandshakeException)
    {
      if (localSSLHandshakeException.getCause() != null) {
        localSSLHandshakeException.getCause().printStackTrace();
      } else {
        localSSLHandshakeException.printStackTrace();
      }
    }
    catch (Exception localException)
    {
      localException.printStackTrace();
    }
    System.exit(1);
  }
}

```

----------

***If can't connect to SSL server, please use [portecle](http://portecle.sourceforge.net/ "portecle") to import the host's certificate into java keystore and test again.***
