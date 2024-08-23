# nfc_capsense_wakeup
MCU-wakeup from SLEEP using ST25R3911(B) CapSense-wakeup functionality.

After wakeup, code scans for NFC-tag(s) then - if relevant - reads NDEF-info from NFC type A/B/F/V tags.

Using PlatformIO/Arduino w. ESP32-S3 Mini-M1 kit and "ST25R3911B-DISCO" kit.

NOTE: configured to read NFC-A/B/F/V tags (ISO14443(A) etc.).



# Setup

"config.h" contains the GPIO definitions for the SPI.
Set to work w. ESP32-S3 Mini-M1 kit connected to SPI-header on ST25R3911B-DISCO kit.
Can also work with the X-NUCLEO-NFC05A1 add-on kit.

The RFAL-lib (from STmicro) can be configured in the "src/rfal_platform/rfal_platform.h" file, 
for specific NFC functionality.

# ST RFAL implementation

- src/rfal_core
- src/rfal_core/st25r3911
- src/rfal_platform

# ST NDEF implementation

- src/ndef
- src/ndef/polling
- src/ndef/message

# Debug Output:

Shows sleep entered, then wakeup from CapSense-event.

Each step in NFC-handling returns the ST25 NFC-lib error code.
The UID represent the unique ID of the NFC device.
NDEF type and content is printed on console.

```text

ALIVE ...


ALIVE ...

NFCA Passive ISO-DEP device found. UID: 02A30000E35B79
READ/WRITE NDEF detected.
 * URI record: 
st.com/st25
Operation completed
Tag can be removed from the field

ALIVE ...


ALIVE ...

ISO15693/NFC-V card found. UID: E002230057156112
NDEF NOT DETECTED (ndefPollerNdefDetect returns 5)
Operation completed
Tag can be removed from the field

ALIVE ...


```

