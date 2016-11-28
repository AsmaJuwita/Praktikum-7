# Praktikum-7
include
include
include
define PORT 2000
WiFiClient client; 
WiFiServer server(PORT); 
char c;
String message;
const char *ssid = "xxx";
const char *password = "xxxxx"; 
void setup() 
{
pinMode(LED_BUILTIN, OUTPUT);
digitalWrite(LED_BUILTIN, HIGH); 
Serial.begin(115200); 
Serial.println("Wemos TCP Server"); 
Serial.print("Listening Port : "); 
Serial.println(PORT); delay(100);
// Koneksi ke akses point WiFi.begin(ssid, password);
Serial.println("Connecting to Access Point ..."); // Tunggu sampai terkoneksi while(WiFi.status() != WL_CONNECTED) 
{
delay(500);
}
Serial.print("."); // Tampilkan IP Address Wemos 
Serial.println(""); 
Serial.print("Connected to "); 
Serial.println(ssid); 
Serial.print("IP address: "); 
Serial.println(WiFi.localIP()); // Start TCP Server } server.begin();
void loop() 
{
if (!client.connected()) 
{
// Tunngu koneksi dari client } client = server.available(); // Client terkoneksi while (client.connected()) {
// Tampilkan data dari client ke serial port if (client.available()) 
{
while (client.available() > 0) { c = (char)client.read(); //Serial.print(c); message += c;
if (message.equals("on")) 
{ 
digitalWrite(LED_BUILTIN, LOW);
}//Serial.println("LED ON");
else if (message.equals("off")) 
{ 
digitalWrite(LED_BUILTIN, HIGH);
}}}//Serial.println("LED OFF");
}}message = "";
Program c# using System;
using System.Collections.Generic; using System.ComponentModel; using System.Data; using System.Drawing; using System.Linq; using System.Text; using System.Windows.Forms; using System.Net.Sockets; using System.Net; using System.IO;
namespace TCP_Client
{ 
public partial class Form1 : Form { TcpClient tcpclient;
public Form1()
{ 
InitializeComponent(); 
}
private void Form1_Load(object sender, EventArgs e) {} tcpclient = new TcpClient();
private void buttonConnect_Click(object sender, EventArgs e) { bool err = false; try {
} 
tcpclient.Connect(textBoxIP.Text, Int32.Parse(textBoxPort.Text)); catch (Exception ex) { MessageBox.Show(ex.ToString()); } err = true; if (!err)
{} buttonConnect.Enabled = false;
}
private void buttonLedOn_Click(object sender, EventArgs e)
{ 
try
{ 
Stream tcpData = tcpclient.GetStream(); ASCIIEncoding asen = new ASCIIEncoding(); String data = "on";
byte[] ba = asen.GetBytes(data); 
tcpData.Write(ba, 0, ba.Length); 
} 
catch (Exception err)
{ 
MessageBox.Show(err.ToString());
} }
private void buttonLedOff_Click(object sender, EventArgs e)
{ 
try
{ 
Stream tcpData = tcpclient.GetStream(); 
ASCIIEncoding asen = new ASCIIEncoding(); 
String data = "off"; 
byte[] ba = asen.GetBytes(data); 
tcpData.Write(ba, 0, ba.Length); 
} 
catch (Exception err) 
{ 
MessageBox.Show(err.ToString()); 
} } } }
