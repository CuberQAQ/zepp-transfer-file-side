# transfer-file-side

Polyfill of transferFile API for ZeppOS 1.0/2.0/2.1 app-side

Corrently not support "progress" event or cancel sending task.

Some api were not tested. I don't know whether it could work correctly.

**This repo is for app-side，not ZeppOS device**. see [CuberQAQ/zepp-transfer-file: Polyfill of @zos/ble/transfer-file API for ZeppOS 2.0/2.1 device.](https://github.com/CuberQAQ/zepp-transfer-file) for ZeppOS device polyfill.

This project includes @cuberqaq/fs-side module. It uses settings storage api to storage data, not a true file system, so don't save many big files. You should also access the files by @cuberqaq/fs-side module. see [CuberQAQ/zepp-fs-side: Simple Lib for ZeppOS 1.0/2.0/2.1 app-side to build a vitual file system.](https://github.com/CuberQAQ/zepp-fs-side#readme)

## 1. Install

Use Command `npm i @cuberqaq/transfer-file-side --save` to install transfer-file-side in your ZeppOS Miniapp project.

## 2. Import & Use

In your app-side JavaScript source file, use this to import transfer-file-side:

```js
import { transferFile } from "@cuberqaq/transfer-file-side";
```

Then you can use the methods in the same way you do with official transfer-file app-side API. Document see [Zepp OS Developers Documentation](https://docs.zepp.com/docs/reference/side-service-api/transfer-file/)

## 3. Example:

```js
import { transferFile } from "@cuberqaq/transfer-file-side";

const outbox = tranfserFile.getOutBox()

AppSideService({
  onInit() {
    const fileObject = outbox.enqueueFile('data://download/1.png', {type: "image", name: "fdsa"})

    file.on('change', (event) => {
        if (event.data.readyState === 'transferred') {
          console.log('transfered file success')
        } else (event.data.readyState === 'error') {
          console.log('error')
        }
    })
  }
})
```

By the way, it seems that the transfering speed could only reach 8kb/s :\)
