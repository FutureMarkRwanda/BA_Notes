# Console Access

Routers and switches, unlike computers, don’t have monitors or built-in user interfaces. To configure them initially, especially before enabling remote management (SSH or Telnet), administrators use the **console port**, also known as the **management port**.

## Summary

This topic covers:

* The purpose and use of the console port.
* Required cables and adapters for console connection.
* How to access router or switch CLI using a console connection on both Windows and Linux.
* Common tools and methods used for console access.

---

## What is Console Access?

Every Cisco router or switch includes a **console port**, located on the device's rear. It is used to directly connect a computer to the router/switch for **initial configuration**, especially when no network-based access (like SSH or Telnet) is yet available.

Since these devices have no screens or keyboards, console access provides the only way to interact with the **CLI (Command Line Interface)** in the early stages of setup.

Once the device is configured and connected to a network, remote access methods like **SSH** or **Telnet** can be used instead.

---

## Console Cables and Adapters

To connect a PC to the console port, special cables are needed:

* **Rollover Cable**: A flat cable that connects the **serial (COM) port** on a computer to the **RJ45 console port** on the router/switch.

  * One end is typically a **DB9 serial connector** (for PCs).
  * The other end is an **RJ45 connector** (for network devices).

  ![Rollover Cable and Adapter](https://user-images.githubusercontent.com/console-ports-db9-rj45.jpg)

* **USB-to-Serial Adapter**: Since modern laptops no longer include serial ports, a **USB-to-Serial (RS232) adapter** is used.

  * This adapter connects a USB port on the laptop to the DB9 connector of the rollover cable.

  ![USB to Serial Adapter](https://user-images.githubusercontent.com/usb-serial-converter.jpg)

---

## Accessing the CLI on Windows

To configure the router/switch from a **Windows PC**, you can use **PuTTY**, a free terminal emulator.

### Steps:

1. **Connect the cable**: Plug the rollover cable between the device’s console port and your PC (using a USB adapter if needed).
2. **Check COM Port**:

   * Open **Device Manager** from the Start menu.
   * Look under “Ports (COM & LPT)” to identify the COM port assigned (e.g., COM4).
   * Alternatively, open **Command Prompt** and type:

     ```
     mode
     ```

     This lists available COM ports.
3. **Open PuTTY**:

   * Set the **Connection Type** to “Serial”.
   * Enter the COM port (e.g., COM4) in the “Serial line” field.
   * Click “Open” to start the session.

Once connected, the router’s CLI will appear, ready for configuration.

---

## Accessing the CLI on Linux

Linux systems offer multiple tools to access routers via the console without needing PuTTY.

### Method 1: Using `screen`

1. Install the screen utility:

   ```
   sudo apt install screen -y
   ```
2. Start the session:

   ```
   sudo screen /dev/ttyUSB0
   ```

   Replace `/dev/ttyUSB0` with your actual device if different.

### Method 2: Using `minicom`

1. Install minicom:

   ```
   sudo apt install minicom
   ```
2. Identify the port:

   ```
   dmesg | grep tty
   ```
3. Set up minicom:

   ```
   sudo minicom -s
   ```

   * Disable **Hardware Flow Control** (press "F", set to "No").
   * Save the setup as default ("Save setup as dfl").
4. Start minicom:

   ```
   sudo minicom
   ```

   If you get a lock error:

   ```
   sudo killall -9 minicom
   sudo minicom
   ```

### Optional: Using PuTTY on Linux

If you still prefer PuTTY:

```
sudo apt install putty
```

Then run:

```
putty
```

Choose **Serial**, and enter the correct `/dev/ttyUSB0` port.

---

## Final Notes

* **Console access is essential for initial setup or recovery** when remote access is unavailable.
* Always verify the **correct COM or USB port** and ensure drivers for USB-to-Serial adapters are installed.
* Tools like **PuTTY**, **screen**, and **minicom** provide flexible options for CLI access depending on your operating system.
* Once remote access (SSH/Telnet) is configured, console access becomes a backup or emergency option.

