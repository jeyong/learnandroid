# uart

## 순서
 * permission 추가
```xml
<uses-permission android:name="com.google.android.things.permission.USE_PERIPHERAL_IO" />
```
 * connection 관리
   * 특정 UART에 연결을 open하기 위해서 port 이름이 필요
   * PeripheralManager의 getUartDeviceList()로 목록 얻어와서 확인하기
```java
PeripheralManager manager = PeripheralManager.getInstance();
List<String> deviceList = manager.getUartDeviceList();
if (deviceList.isEmpty()) {
    Log.i(TAG, "No UART port available on this device.");
} else {
    Log.i(TAG, "List of available devices: " + deviceList);
}
```

 * 연결 close()
```java
@Override
    protected void onDestroy() {
        super.onDestroy();

        if (mDevice != null) {
            try {
                mDevice.close();
                mDevice = null;
            } catch (IOException e) {
                Log.w(TAG, "Unable to close UART device", e);
            }
        }
    }

```
 * 설정하기
```java
public void configureUartFrame(UartDevice uart) throws IOException {
    // Configure the UART port
    uart.setBaudrate(115200);
    uart.setDataSize(8);
    uart.setParity(UartDevice.PARITY_NONE);
    uart.setStopBits(1);
}
```
 * flow control
```java
public void setFlowControlEnabled(UartDevice uart, boolean enable) throws IOException {
    if (enable) {
        // Enable hardware flow control
        uart.setHardwareFlowControl(UartDevice.HW_FLOW_CONTROL_AUTO_RTSCTS);
    } else {
        // Disable flow control
        uart.setHardwareFlowControl(UartDevice.HW_FLOW_CONTROL_NONE);
    }
}

```
 * data 전송하기
```java
public void writeUartData(UartDevice uart) throws IOException {
    byte[] buffer = {...};
    int count = uart.write(buffer, buffer.length);
    Log.d(TAG, "Wrote " + count + " bytes to peripheral");
}

```
 * data 수신하기
```java
public void readUartBuffer(UartDevice uart) throws IOException {
    // Maximum amount of data to read at one time
    final int maxCount = ...;
    byte[] buffer = new byte[maxCount];

    int count;
    while ((count = uart.read(buffer, buffer.length)) > 0) {
        Log.d(TAG, "Read " + count + " bytes from peripheral");
    }
}

```
 * 불필요한 UART polling 막기
   *  onUartDeviceDataAvailable() callback의 리턴값
     * false : 자동으로 unregister
     * true : 계속해서 수신
```java
public class HomeActivity extends Activity {
    private UartDevice mDevice;
    ...

    @Override
    protected void onStart() {
        super.onStart();
        // Begin listening for interrupt events
        mDevice.registerUartDeviceCallback(uartCallback);
    }

    @Override
    protected void onStop() {
        super.onStop();
        // Interrupt events no longer necessary
        mDevice.unregisterUartDeviceCallback(uartCallback);
    }

    private UartDeviceCallback uartCallback = new UartDeviceCallback() {
        @Override
        public boolean onUartDeviceDataAvailable(UartDevice uart) {
            // Read available data from the UART device
            try {
                readUartBuffer(uart);
            } catch (IOException e) {
                Log.w(TAG, "Unable to access UART device", e);
            }

            // Continue listening for more interrupts
            return true;
        }

        @Override
        public void onUartDeviceError(UartDevice uart, int error) {
            Log.w(TAG, uart + ": Error event " + error);
        }
    };
}

```