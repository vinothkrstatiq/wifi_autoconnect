Reconnect to Wi-Fi Network After Lost Connection
To reconnect to Wi-Fi after a connection is lost, you can use WiFi.reconnect() to try to reconnect to the previously connected access point:

WiFi.reconnect()
Or, you can call WiFi.disconnect() followed by WiFi.begin(ssid,password).

WiFi.disconnect();
WiFi.begin(ssid, password);
Alternatively, you can also try to restart the ESP32 with ESP.restart() when the connection is lost.

You can add something like the snippet below to the loop() that checks once in a while if the board is connected and tries to reconnect if it has lost connection.

unsigned long currentMillis = millis();
// if WiFi is down, try reconnecting
if ((WiFi.status() != WL_CONNECTED) && (currentMillis - previousMillis >=interval)) {
  Serial.print(millis());
  Serial.println("Reconnecting to WiFi...");
  WiFi.disconnect();
  WiFi.reconnect();
  previousMillis = currentMillis;
}
Don’t forget to declare the previousMillis and interval variables. The interval corresponds to the period of time between each check in milliseconds (for example 30 seconds):

unsigned long previousMillis = 0;
unsigned long interval = 30000;
