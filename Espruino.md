### Stuff to digg to be able to customize an Espruino build for our particular board :p
- https://github.com/espruino/Espruino/blob/master/boards/STM32F4DISCOVERY.py
- Build Process: https://github.com/espruino/Espruino/blob/master/README_BuildProcess.md
- Building Espruino: https://github.com/espruino/Espruino/blob/master/README_Building.md#for-stm32-boards-incl-espruino-board
- Libs: https://github.com/espruino/Espruino/blob/master/libs/README.md
- Extending Espruino: http://www.espruino.com/Extending+Espruino+1

### from https://github.com/espruino/Espruino/blob/master/src/jswrap_espruino.c: 
```javascript
// ----------------------------------------- USB Specific Stuff

#ifdef USE_USB_HID
#include "usbd_cdc_hid.h"

/*JSON{
  "type" : "staticmethod",
  "ifdef" : "USE_USB_HID",
  "class" : "E",
  "name" : "setUSBHID",
  "generate" : "jswrap_espruino_setUSBHID",
  "params" : [
    ["opts","JsVar","An object containing at least reportDescriptor, an array representing the report descriptor. Pass undefined to disable HID."]
  ]
}
USB HID will only take effect next time you unplug and re-plug your Espruino. If you're
disconnecting it from power you'll have to make sure you have `save()`d after calling
this function.
 */
void jswrap_espruino_setUSBHID(JsVar *arr) {
  if (jsvIsUndefined(arr)) {
    // Disable HID
    jsvObjectRemoveChild(execInfo.hiddenRoot, JS_USB_HID_VAR_NAME);
    return;
  }
  if (!jsvIsObject(arr)) {
    jsExceptionHere(JSET_TYPEERROR, "Expecting Object, got %t", arr);
    return;
  }

  JsVar *report = jsvObjectGetChild(arr, "reportDescriptor", 0);
  if (!(jsvIsArray(report) || jsvIsArrayBuffer(report) || jsvIsString(report))) {
    jsExceptionHere(JSET_TYPEERROR, "Object.reportDescriptor should be an Array or String, got %t", arr);
    jsvUnLock(report);
    return;
  }
  JsVar *s = jswrap_espruino_toString(report);
  jsvUnLock(report);
  // Enable HID
  jsvObjectSetChildAndUnLock(execInfo.hiddenRoot, JS_USB_HID_VAR_NAME, s);
}

/*JSON{
  "type" : "staticmethod",
  "ifdef" : "USE_USB_HID",
  "class" : "E",
  "name" : "sendUSBHID",
  "generate" : "jswrap_espruino_sendUSBHID",
  "params" : [
    ["data","JsVar","An array of bytes to send as a USB HID packet"]
  ],
  "return" : ["bool","1 on success, 0 on failure"]
}
 */
bool jswrap_espruino_sendUSBHID(JsVar *arr) {
  unsigned char data[HID_DATA_IN_PACKET_SIZE];
  unsigned int l = jsvIterateCallbackToBytes(arr, data, HID_DATA_IN_PACKET_SIZE);
  if (l>HID_DATA_IN_PACKET_SIZE) return 0;

  return USBD_HID_SendReport(data, l) == USBD_OK;
}

#endif
```
