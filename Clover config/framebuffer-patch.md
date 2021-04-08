- AAPL,ig-platform-id table:

| CPU Generation |   iGPU   | iGPU + dGPU |                          SMBIOS                           |                             Note                             |
| :------------: | :------: | :---------: | :-------------------------------------------------------: | :----------------------------------------------------------: |
|    Haswell     | 0300220D |  04001204   |       - iMac14,4 (iGPU)<br>- iMac15,1 (iGPU + dGPU)       |                                                              |
|   Broadwell    | 07002216 |             |                     - iMac16,2 (iGPU)                     |                                                              |
|    Skylake     | 00001219 |  01001219   |                        - iMac17,1                         |     P530 users should have **device-id** = **1B190000**      |
|    Kabylake    | 00001259 |  03001259   |       - iMac18,1 (iGPU)<br>- iMac18,3 (iGPU + dGPU)       |                                                              |
|   Coffeelake   | 07009B3E |  0300913E   | - iMac19,1 (Mojave and newer)<br>- iMac18,3 (High Sierra) | If you got blackscreen with **07009B3E**, try **00009B3E** instead |
|   Cometlake    | 07009B3E |  0300C89B   |        - iMac20,1 (i3, i5, i7)<br>- iMac20,2 (i9)         | If you got blackscreen with **07009B3E**, try **00009B3E** instead. |

- Generic Patch:

  |           Key            | Type |  Value   |
  | :----------------------: | :--: | :------: |
  |   AAPL,ig-platform-id    | Data |  xxxxxx  |
  | framebuffer-patch-enable | Data | 01000000 |
  |  framebuffer-stolenmem   | Data | 00003001 |
  |        device-id         | Data |  zzzzzz  |

- Note:
  - Some iGPU you should add device-id to fake the id to get it works.
  - If your machine has iGPU only, and can't set/doesn't have framebuffer memory, you should add **framebuffer-patch-enable** and **framebuffer-stolenmem**.
  - In some motherboard, the share memory for iGPU displayed with different names:
    - Gigabyte: DVMT Pre-Allocated
    - Asus: DVMT Pre-Allocated
    - MSI: DVMT Pre-Allocated
    - Asrock: Share Memory
  - If your machine doesn't have iGPU, you can skip the framebuffer patch.
- Tip:
  - If your CPU is non-iGPU, means F series, and you have good AMD GPU like at least RX 580, you can use the following SMBIOS:
    - iMacPro1,1: For Skylake, Kabylake CPU.
    - MacPro7,1: For Coffeelake, Cometlake CPU (MacPro7,1 works well with AMD CPU).