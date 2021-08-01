<p align="center">
  <img width="128" height="128" src="https://github.com/alphagruis/alphagruis-eth/blob/main/alphagruis-eth.svg">
  <img width="128" height="128" src="https://github.com/alphagruis/alphagruis-eth/blob/main/alphagruis-eth-logo.svg">
</p>

# :small_orange_diamond: alphagruis's Miner for Ethereum

**alphagruis**'s Miner for **Ethereum**, is a high performance and rock solid miner. This miner was designed and implemented in C++, OpenCL and CUDA **from scratch** by the **alphagruis** team, a small group of skilled developers, for a huge cryptocurrency mining farm. Now, **alphagruis** can finally publish its wonderful miner. Official binaries are currently only available for the **Windows** platform.

Try it, we are sure you will never want to go back.

## Table of Contents

* [Mining Backends](#mining-backends)
* [Mining Fee](#mining-fee)
* [Mining Transparency](#mining-transparency)
* [Install](#install)
* [Configuration](#configuration)
  * [`"fStratumAddressArray"`](#configuration-fstratumaddressarray)
  * [`"fMinerSettingsArray"`](#configuration-fminersettingsarray)
  * [`"fDevicePCIeTopology"`](#configuration-fdevicepcietopology)
  * [`"fDeviceOverclockSettings"`](#configuration-fdeviceoverclocksettings)
  * [`"fKernelSettings"`](#configuration-fkernelsettings)
* [Usage](#usage)
  * [System Requirements](#system-requirements)
  * [Virtual Memory Size](#virtual-memory-size)
* [License](#license)

## Mining Backends

- **OpenCL** for AMD GPUs.
- **CUDA** for NVIDIA GPUs.

*The miner is able to run on hardware with AMD GPUs and NVIDIA GPUs at the same time.*

## Mining Fee

**alphagruis**'s Miner for **Ethereum**, is not free. The mining fee time is 36 seconds every 60 minutes minus 36 seconds. In other words, the fee amounts to 1%. The miner unambiguously, display on the console when the mining fee is active.

## Mining Transparency

**alphagruis**'s Miner for **Ethereum** is completely transparent (the binary (executable machine code) is not packed). The hashrate reported by the miner is not inflated and will match, on average, to the effective hashrate calculated by the pool. Without any tricks. Everything the miner does is displayed on the console and written to the log file. Nothing is left out.

**alphagruis** encourages everyone to scan all files contained in this repository with their favorite antivirus.

## Install

Standalone executable for Windows is provided in the [Releases] section. Download the archive and unpack the content to a place accessible from command line.

## Configuration

To configure the miner, you can easily edit the default **alphagruis-eth.json** file in JSON format or, if you prefer, you can edit your own configuration file and specify its file path, as additional parameter, via the command line to run the executable. The choice to use a configuration file is essentially due to the number of customizable parameters, which are difficult to specify via the command line, without errors and without exceeding the same limits.

*All JSON field values can be filled with environment variables.*

ex. alphagruis.json file in JSON format to mine with the *ethermine* pool:

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional]
    "fLogFile": 1,

    // [optional]
    "fColors": 1,

    // [required]
    "fWorker": "alphagruis",

    // [required]
    "fStratumAddressArray":
    [
        //
        // [ETH] ethermine, nonSSL: 4444, SSL strict: 5555
        //

        {
            // [required]
            "fStratumMode": 0,

            // [required]
            "fWallet": "0x0000000000000000000000000000000000000000",

            // [optional]
            "fPassword": "",

            // [required]
            "fSocketAddressName": "eu1.ethermine.org",

            // [required]
            "fServerPort": 5555,

            // [optional]
            "fSSL": 2
        },

        {
            // [required]
            "fStratumMode": 0,

            // [required]
            "fWallet": "0x0000000000000000000000000000000000000000",

            // [optional]
            "fPassword": "",

            // [required]
            "fSocketAddressName": "us1.ethermine.org",

            // [required]
            "fServerPort": 5555,

            // [optional]
            "fSSL": 2
        },

        {
            // [required]
            "fStratumMode": 0,

            // [required]
            "fWallet": "0x0000000000000000000000000000000000000000",

            // [optional]
            "fPassword": "",

            // [required]
            "fSocketAddressName": "us2.ethermine.org",

            // [required]
            "fServerPort": 5555,

            // [optional]
            "fSSL": 2
        }
    ],

    // [required]
    "fMinerSettingsArray":
    [
        //
        // AMD
        //

        {
            // [required] OpenCL: 1
            "fPlatformType": 1,

            // [required] AMD: 1
            "fDeviceType": 1,

        /*
            // [optional]
            "fDevicePCIeTopology":
            {
                // [optional]
                "fDomain": 0,

                // [required]
                "fBus": 0,

                // [required]
                "fDevice": 0,

                // [required]
                "fFunction": 0
            },
        */

            // [optional]
            "fDeviceOverclockSettings":
            {
                // [optional] unit: percentage, expressed in RELATIVE value.
                "fPowerLimit": 0,

                // [optional] unit: celsius, expressed in ABSOLUTE value.
                "fTemperatureLimit": 70,

                // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
                "fClockGraphics": [1150, 850],

                // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
                "fClockMemory": [2050, 850],

                // [optional] unit: natural, AMD only.
                "fMemoryTimingLevel": 2,

                // [optional] unit: percentage, expressed in ABSOLUTE value.
                "fFanSpeed": 100
            },

            // [optional]
            "fKernelSettings":
            {
                // [optional] default: 2
                "fComputeDatasetChannels": 2,

                // [optional] default: 128
                "fComputeDatasetKernelLocalWorkSize": 128,

                // [optional] default: 262144
                "fComputeDatasetKernelGlobalWorkStep": 262144,

                // [optional] default: 2
                "fSearchChannels": 2,

                // [optional] default: 128
                "fEthashSearchKernelLocalWorkSize": 128,

                // [optional] default: 1048576
                "fEthashSearchKernelGlobalWorkSize": 1048576,

                // [optional] default: 8
                "fEthashThreadsPerHash": 8
            }
        },

        //
        // NVIDIA
        //

        {
            // [required] CUDA: 32
            "fPlatformType": 32,

            // [required] NVIDIA: 4
            "fDeviceType": 4,

        /*
            // [optional]
            "fDevicePCIeTopology":
            {
                // [optional]
                "fDomain": 0,

                // [required]
                "fBus": 0,

                // [required]
                "fDevice": 0,

                // [required]
                "fFunction": 0
            },
        */

            // [optional]
            "fDeviceOverclockSettings":
            {
                // [optional] unit: percentage, expressed in ABSOLUTE value.
                "fPowerLimit": 70,

                // [optional] unit: celsius, expressed in ABSOLUTE value.
                "fTemperatureLimit": 70,

                // [optional] unit: MHz, expressed in RELATIVE value.
                "fClockGraphics": 150,

                // [optional] unit: MHz, expressed in RELATIVE value.
                "fClockMemory": 500,

                // [optional] unit: percentage, expressed in ABSOLUTE value.
                "fFanSpeed": 100
            },

            // [optional]
            "fKernelSettings":
            {
                // [optional] default: 2
                "fComputeDatasetChannels": 2,

                // [optional] default: 128
                "fComputeDatasetKernelLocalWorkSize": 128,

                // [optional] default: 0, CUDA only.
                "fComputeDatasetKernelMinBlocksPerMultiprocessor": 0,

                // [optional] default: 262144
                "fComputeDatasetKernelGlobalWorkStep": 262144,

                // [optional] default: 2
                "fSearchChannels": 2,

                // [optional] default: 128
                "fEthashSearchKernelLocalWorkSize": 128,

                // [optional] default: 0, CUDA only.
                "fEthashSearchKernelMinBlocksPerMultiprocessor": 0,

                // [optional] default: 1048576
                "fEthashSearchKernelGlobalWorkSize": 1048576,

                // [optional] default: 4
                "fEthashThreadsPerHash": 4,

                // [optional] default: 0, CUDA only.
                "fMaximumAmountOfRegisters": 0
            }
        }
    ]
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fLogFile"`|Number|0 to disable logging to file.<br/>1 to enable logging to file.|1|
|`"fColors"`|Number|0 to disable color output on console.<br/>1 to enable color output on console.|1|
|`"fWorker"`|String|The name of your rig. It may only contain letters and numbers. Some pools also only allow up to a maximum of 8 characters.|"alphagruis"|
|`"fStratumAddressArray"`|Array|The array can contain one or more objects with the parameters necessary to connect to the pool. Objects should be specified in order of preemption, from highest to lowest. If connection to the pool is not possible, the miner tries to use the next object to connect to the pool. After 10 minutes, the miner attempts to reestablish the connection using the primary object. And so on.|See Configuration: [`"fStratumAddressArray"`](#configuration-fstratumaddressarray).|
|`"fMinerSettingsArray"`|Array|The array can contain one or more objects to select and configure an entire family of GPUs or a single GPU.|See Configuration: [`"fMinerSettingsArray"`](#configuration-fminersettingsarray).|

#### Configuration: "fStratumAddressArray"

`"fStratumAddressArray"` array, can contain one or more JSON objects as below:

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [required]
    "fStratumMode": 0,

    // [required]
    "fWallet": "0x0000000000000000000000000000000000000000",

    // [optional]
    "fPassword": "",

    // [required]
    "fSocketAddressName": "eu1.ethermine.org",

    // [required]
    "fServerPort": 5555,

    // [optional]
    "fSSL": 2
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fStratumMode"`|Number|The stratum mode supported by pool.<br/>0 to use the mining proxy protocol (the most widely supported by Ethereum and Ethereum Classic mining pools).<br/>1 to use the plain stratum protocol (the most widely supported by Ravencoin mining pools).<br/>2 to use the ethereum stratum protocol (NiceHash).|0|
|`"fWallet"`|String|The address of the wallet associated with the connection.|"0x0000000000000000000000000000000000000000"|
|`"fPassword"`|String|The password, only if required, to connect to the pool. Otherwise, leave it empty.|""|
|`"fSocketAddressName"`|String|The mining server address of the pool.|"eu1.ethermine.org"|
|`"fServerPort"`|Number|The mining server port of the pool.|5555|
|`"fSSL"`|Number|0 if `"fServerPort"` refers to an insecure connection (not recommended).<br/>1 if `"fServerPort"` refers to a secure connection (without Certificate Validation, to connect to the server which is using a self-signed certificate).<br/>2 if `"fServerPort"` refers to a secure connection (with Certificate Validation, to connect to the server which is using a CA-signed certificate).|2|

If possible, connect to your favorite mining pool using a secure connection (when available).

#### Configuration: "fMinerSettingsArray"

`"fMinerSettingsArray"` array, can contain one or more JSON objects as below:

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [required] OpenCL: 1
    "fPlatformType": 1,

    // [required] AMD: 1
    "fDeviceType": 1,

/*
    // [optional]
    "fDevicePCIeTopology":
    {
        // [optional]
        "fDomain": 0,

        // [required]
        "fBus": 0,

        // [required]
        "fDevice": 0,

        // [required]
        "fFunction": 0
    },
*/

    // [optional]
    "fDeviceOverclockSettings":
    {
        // [optional] unit: percentage, expressed in RELATIVE value.
        "fPowerLimit": 0,

        // [optional] unit: celsius, expressed in ABSOLUTE value.
        "fTemperatureLimit": 70,

        // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
        "fClockGraphics": [1150, 850],

        // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
        "fClockMemory": [2050, 850],

        // [optional] unit: natural, AMD only.
        "fMemoryTimingLevel": 2,

        // [optional] unit: percentage, expressed in ABSOLUTE value.
        "fFanSpeed": 100
    },

    // [optional]
    "fKernelSettings":
    {
        // [optional] default: 2
        "fComputeDatasetChannels": 2,

        // [optional] default: 128
        "fComputeDatasetKernelLocalWorkSize": 128,

        // [optional] default: 262144
        "fComputeDatasetKernelGlobalWorkStep": 262144,

        // [optional] default: 2
        "fSearchChannels": 2,

        // [optional] default: 128
        "fEthashSearchKernelLocalWorkSize": 128,

        // [optional] default: 1048576
        "fEthashSearchKernelGlobalWorkSize": 1048576,

        // [optional] default: 8
        "fEthashThreadsPerHash": 8
    }
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fPlatformType"`|Number|0 to disable this item.<br/>1 to enable and configure the OpenCL backend (likely when `"fDeviceType"` is equal to 1, namely AMD).<br/>32 to enable and configure the CUDA backend (likely when `"fDeviceType"` is equal to 4, namely NVIDIA).|1|
|`"fDeviceType"`|Number|1 to enable the platform `"fPlatformType"` to use AMD GPUs.<br/>4 to enable the platform `"fPlatformType"` to use NVIDIA GPUs.|1|
|`"fDevicePCIeTopology"`|Object|This object is optional and is used to configure one and only one GPU. This option is useful if your hardware is made up of different GPUs, each requiring an ad hoc customization.|See Configuration: [`"fDevicePCIeTopology"`](#configuration-fdevicepcietopology).|
|`"fDeviceOverclockSettings"`|Object|Overclock settings, to be applied to all GPUs identified with the combination `"fPlatformType"`, `"fDeviceType"` and optionally also with `"fDevicePCIeTopology"`.|See Configuration: [`"fDeviceOverclockSettings"`](#configuration-fdeviceoverclocksettings).|
|`"fKernelSettings"`|Object|Kernel settings, to be applied to all GPUs identified with the combination `"fPlatformType"`, `"fDeviceType"` and optionally also with `"fDevicePCIeTopology"`.|See Configuration: [`"fKernelSettings"`](#configuration-fkernelsettings).|

Simplifying:
- To use AMD GPUs, the `"fMinerSettingsArray"` array must contain an object with `"fPlatformType"` equal to 1 and `"fDeviceType"` equal to 1.
- To use NVIDIA GPUs, the `"fMinerSettingsArray"` array must contain an object with `"fPlatformType"` equal to 32 and `"fDeviceType"` equal to 4.
- To use AMD and NVIDIA together, the `"fMinerSettingsArray"` array must contain two objects, one for AMD and one for NVIDIA. 
- To configure *n* GPUs individually, add *n* objects to `"fMinerSettingsArray"` array, declaring the `"fDevicePCIeTopology"` object to uniquely specify a single GPU.

> If your hardware (single motherboard), for example, consists of 5 AMD Radeon RX 580, 1 AMD Radeon RX 6900 XT, 5 NVIDIA GTX 1070 and 1 NVIDIA RTX 3070, to configure the 4 types of GPU it will be necessary to add to `"fMinerSettingsArray"` array, 4 objects: 
>
> 1. an object to configure 5 AMD Radeon RX 580 (without `"fDevicePCIeTopology"` object).
> 2. an object to work with 1 AMD Radeon RX 6900 XT (with `"fDevicePCIeTopology"` object).
> 3. an object to configure 5 NVIDIA GTX 1070 (without `"fDevicePCIeTopology"` object).
> 4. an object to work with 1 NVIDIA RTX 3070 (with `"fDevicePCIeTopology"` object).

Easier done than said.

#### Configuration: "fDevicePCIeTopology"

This object can optionally be declared in the object added to `"fMinerSettingsArray"`, to uniquely specify a single GPU.

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional]
    "fDomain": 0,

    // [required]
    "fBus": 0,

    // [required]
    "fDevice": 0,

    // [required]
    "fFunction": 0
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fDomain"`|Number|PCI domain (always 0 on Windows).|0|
|`"fBus"`|Number|PCI bus number.|0|
|`"fDevice"`|Number|PCI device number.|0|
|`"fFunction"`|Number|PCI function number.|0|

*PCI Addressing.*

*Each PCI peripheral is identified by a **bus** number, a **device** number, and a **function** number. The PCI specification permits a single system to host up to 256 buses, but because 256 buses are not sufficient for many large systems, Linux now supports PCI domains. Each PCI **domain** can host up to 256 buses. Each bus hosts up to 32 devices, and each device can be a multifunction board (such as an audio device with an accompanying CD-ROM drive) with a maximum of eight functions.*

*On the Windows platform using the Task Manager application, you can easily see each GPU's PCIe values.*

#### Configuration: "fDeviceOverclockSettings"

This object can optionally be declared in the object added to `"fMinerSettingsArray"`, to handle overclocking.

![alt text](https://img.shields.io/badge/AMD_GPU_Overclock_Settings-red?color=ed1c24)

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional] unit: percentage, expressed in RELATIVE value.
    "fPowerLimit": 0,
    
    // [optional] unit: celsius, expressed in ABSOLUTE value.
    "fTemperatureLimit": 70,
    
    // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
    "fClockGraphics": [1150, 850],
    
    // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
    "fClockMemory": [2050, 850],
    
    // [optional] unit: natural, AMD only.
    "fMemoryTimingLevel": 2,
    
    // [optional] unit: percentage, expressed in ABSOLUTE value.
    "fFanSpeed": 100
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fPowerLimit"`|Number|unit: percentage, expressed in **RELATIVE** value.|0|
|`"fTemperatureLimit"`|Number|unit: celsius, expressed in **ABSOLUTE** value (this parameter is obsolete and recent AMD drivers, no longer seem to contemplate it).|70|
|`"fClockGraphics"`|Array or Number|unit: [MHz, mV] or MHz, expressed in **ABSOLUTE** value.|[1150, 850] or 1150|
|`"fClockMemory"`|Array or Number|unit: [MHz, mV] or MHz, expressed in **ABSOLUTE** value (latest AMD GPUs, do not include voltage control for the memory).|[2050, 850] or 2050|
|`"fMemoryTimingLevel"`|Number|unit: natural, AMD only.|2|
|`"fFanSpeed"`|Number|unit: percentage, expressed in **ABSOLUTE** value.|100|

**The miner overclock the AMD GPUs via AMD Display Library (ADL) SDK using AMD OverdriveN API (version 7) and AMD Overdrive 8 API (version 8). Overdrive versions earlier than version 7 are not supported.**

for more information:<br/>
https://gpuopen.com/adl/

*If you don't know the overclocking values, before launching the miner, temporarily comment out the whole object (multi-line comments start with `/*` and ends with `*/`). Launch the miner. While mining, use of AMD's Radeon WattMan utility to tune your GPU. Once you have determined a stable configuration, uncomment the the whole object and fill in the overclocking values with your optimal overclocking values. Restart the miner for the settings to take effect.*

*Overclocking is automatically applied to all GPUs by the miner, always and only at startup. Since WattMan tends to reset the values when switching to manual tuning mode, remember to switch to manual mode on the GPU you want to control, before starting the miner. If you don't want the miner to handle overclocking, just comment out the whole object.*

![alt text](https://img.shields.io/badge/NVIDIA_GPU_Overclock_Settings-green?color=76b900)

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional] unit: percentage, expressed in ABSOLUTE value.
    "fPowerLimit": 70,
    
    // [optional] unit: celsius, expressed in ABSOLUTE value.
    "fTemperatureLimit": 70,
    
    // [optional] unit: MHz, expressed in RELATIVE value.
    "fClockGraphics": 150,
    
    // [optional] unit: MHz, expressed in RELATIVE value.
    "fClockMemory": 450,
    
    // [optional] unit: percentage, expressed in ABSOLUTE value.
    "fFanSpeed": 100
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fPowerLimit"`|Number|unit: percentage, expressed in **ABSOLUTE** value.|70|
|`"fTemperatureLimit"`|Number|unit: celsius, expressed in **ABSOLUTE** value.|70|
|`"fClockGraphics"`|Number|unit: MHz, expressed in **RELATIVE** value.|150|
|`"fClockMemory"`|Number|unit: MHz, expressed in **RELATIVE** value.|450|
|`"fFanSpeed"`|Number|unit: percentage, expressed in **ABSOLUTE** value.|100|

**The miner overclok the NVIDIA GPUs via NVIDIA NVAPI and NVIDIA NVML API.**

for more information:<br/>
https://developer.nvidia.com/nvapi<br/>
https://docs.nvidia.com/deploy/nvml-api/index.html

*If you don't know the overclocking values, before starting the miner, play with the overclocking values of this object, incrementing them carefully and in small steps, starting from 0. Restart the miner for the settings to take effect.*

*Overclocking is automatically applied to all GPUs by the miner, always and only at startup. If you don't want the miner to handle overclocking, just comment out the whole object.*

#### Configuration: "fKernelSettings"

This object is optionally declared in the object added to `"fMinerSettingsArray"`, to set the optimal values to use for mining engines (kernels). The miner invokes two kernels: `ComputeDatasetKernel` kernel to compute the current epoch dataset (DAG), `EthashSearchKernel` kernel to compute the hashes. To improve the hashrate, focus on tweaking the parameters of this kernel.

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional] default: 2
    "fComputeDatasetChannels": 2,

    // [optional] default: 128
    "fComputeDatasetKernelLocalWorkSize": 128,

    // [optional] default: 0, CUDA only.
    "fComputeDatasetKernelMinBlocksPerMultiprocessor": 0,
  
    // [optional] default: 262144
    "fComputeDatasetKernelGlobalWorkStep": 262144,

    // [optional] default: 2
    "fSearchChannels": 2,

    // [optional] default: 128
    "fEthashSearchKernelLocalWorkSize": 128,

    // [optional] default: 0, CUDA only.
    "fEthashSearchKernelMinBlocksPerMultiprocessor": 0,

    // [optional] default: 1048576
    "fEthashSearchKernelGlobalWorkSize": 1048576,

    // [optional] default: 4
    "fEthashThreadsPerHash": 4,

    // [optional] default: 0, CUDA only.
    "fMaximumAmountOfRegisters": 0
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fComputeDatasetChannels"`|Number|Number of channels (command queues in OpenCL, streams in CUDA) to be used to compute the dataset (commonly also known as DAG, acronym for Directed Acyclic Graph).<br/><br/>Integer value, multiple of 1, between 1 and 8.|2|
|`"fComputeDatasetKernelLocalWorkSize"`|Number|The size of the work-group (OpenCL), the size of thread block (CUDA).<br/><br/>Integer value, multiple of 32, between 32 and 4096.|128|
|`"fComputeDatasetKernelMinBlocksPerMultiprocessor"`|Number|This value is optionally used as a parameter by the `__launch_bounds__()` qualifier in the definition of a `__global__` function, CUDA only.|0|
|`"fComputeDatasetKernelGlobalWorkStep"`|Number|Number of dataset items to compute with a kernel execution command, queued on a channel.<br/><br/>Integer value, multiple of 1024, between 1024 and (1024 * 1024).|262144|
|`"fSearchChannels"`|Number|Number of channels (command queues in OpenCL, streams in CUDA) to be used to compute hashes.<br/><br/>Integer value, multiple of 1, between 1 and 8.|2|
|`"fEthashSearchKernelLocalWorkSize"`|Number|The size of the work-group (OpenCL), the size of thread block (CUDA).<br/><br/>Integer value, multiple of 32, between 32 and 4096.<br/><br/>**:small_red_triangle: This parameter directly affects the hashrate. When setting up your GPU, always look for the best value between 64, 128, 192, 256.**|128|
|`"fEthashSearchKernelMinBlocksPerMultiprocessor"`|Number|This value is optionally used as a parameter by the `__launch_bounds__()` qualifier in the definition of a `__global__` function, CUDA only.|0|
|`"fEthashSearchKernelGlobalWorkSize"`|Number|Number of hashes to compute with a kernel execution command, queued on a channel.<br/><br/>Integer value, multiple of 1024, between 1024 and (1024 * 1024 * 1024).|1048576|
|`"fEthashThreadsPerHash"`|Number|Number of work-items (OpenCL), number of threads (CUDA) to compute a single hash in parallel.<br/><br/>Integer value: { 1, 2, 4, 8 }.<br/><br/>**:small_red_triangle: This parameter directly affects the hashrate. When setting up your GPU, always look for the best value between 4 and 8.**|4|
|`"fMaximumAmountOfRegisters"`|Number|Maximum number of registers that a thread may use, CUDA only.|0|

*Adjust the **global work size** parameters with caution, based on the capabilities of your GPU:*

- *the number of **work-groups** used to launch the kernel is equal to global work size divided by local work size. In other words, the kernel execution is invoked with `number of work-groups` * `work-items per work-group` **work-items** (OpenCL).*

- *the number of **thread blocks** used to launch the kernel is equal to global work size divided by local work size. In other words, the kernel execution is invoked with `number of thread blocks` * `threads per thread block` **threads** (CUDA).*

All kernel settings are automatically adjusted and validated by the miner if needed.

**OpenCL, attribute of the kernels**

The `ComputeDatasetKernel` kernel is compiled at runtime with the OpenCL backend of the driver, using the following attribute:

```OpenCL
#ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
#define _M_ComputeDatasetKernelLocalWorkSizeAttribute __attribute__ ((reqd_work_group_size (kComputeDatasetKernelLocalWorkSize, 1, 1)))
#endif
```

The `EthashSearchKernel` kernel is compiled at runtime with the OpenCL backend of the driver, using the following attribute:

```OpenCL
#ifndef _M_EthashSearchKernelLocalWorkSizeAttribute
#define _M_EthashSearchKernelLocalWorkSizeAttribute __attribute__ ((reqd_work_group_size (kEthashSearchKernelLocalWorkSize, 1, 1)))
#endif
```

> Basically, to maximize device utilization, you can choose to indirectly set the maximum number of registers per-kernel (using `"fEthashSearchKernelLocalWorkSize"`) adjusting kernel launch configuration.

for more information:<br/>
https://www.khronos.org/registry/OpenCL/sdk/2.2/docs/man/html/optionalAttributeQualifiers.html<br/>
https://www.khronos.org/registry/OpenCL/sdk/2.2/docs/man/html/clEnqueueNDRangeKernel.html

**CUDA, attribute of the kernels**

The `ComputeDatasetKernel` kernel is compiled at runtime with the CUDA backend of the driver, via NVIDIA NVRTC using the following attribute:

```CUDA
#if (qMaximumAmountOfRegisters > 0)
    #ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #define _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #endif
#elif (kComputeDatasetKernelMinBlocksPerMultiprocessor > 0)
    #ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #define _M_ComputeDatasetKernelLocalWorkSizeAttribute __launch_bounds__ (kComputeDatasetKernelLocalWorkSize, kComputeDatasetKernelMinBlocksPerMultiprocessor)
    #endif
#else
    #ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #define _M_ComputeDatasetKernelLocalWorkSizeAttribute __launch_bounds__ (kComputeDatasetKernelLocalWorkSize)
    #endif
#endif
```

The `EthashSearchKernel` kernel is compiled at runtime with the CUDA backend of the driver, via NVIDIA NVRTC using the following attribute:

```CUDA
#if (qMaximumAmountOfRegisters > 0)
    #ifndef _M_EthashSearchKernelLocalWorkSizeAttribute
    #define _M_EthashSearchKernelLocalWorkSizeAttribute
    #endif
#elif (kEthashSearchKernelMinBlocksPerMultiprocessor > 0)
    #ifndef _M_EthashSearchKernelLocalWorkSizeAttribute
    #define _M_EthashSearchKernelLocalWorkSizeAttribute __launch_bounds__ (kEthashSearchKernelLocalWorkSize, kEthashSearchKernelMinBlocksPerMultiprocessor)
    #endif
#else
    #ifndef _M_EthashSearchKernelLocalWorkSizeAttribute
    #define _M_EthashSearchKernelLocalWorkSizeAttribute __launch_bounds__ (kEthashSearchKernelLocalWorkSize)
    #endif
#endif
```

> Basically, to maximize device utilization, you can choose to set the maximum number of registers per-thread (using `"fMaximumAmountOfRegisters"`) or per-kernel (using `"fEthashSearchKernelLocalWorkSize"` and optionally `"fEthashSearchKernelMinBlocksPerMultiprocessor"`) adjusting kernel launch configuration.

for more information:<br/>
https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#execution-configuration-optimizations<br/>
https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#register-pressure

## Usage
  
The **alphagruis**'s Miner for **Ethereum** is a command line program. This means you launch it either from a Windows Command Prompt, or create shortcuts to predefined command lines using a Windows batch/cmd file. After setting up the configuration file, **alphagruis**'s Miner for **Ethereum** is ready to go. 

to launch the miner using the default **alphagruis-eth.json** file, type:

```batch
alphagruis-eth.exe
```

to launch the miner using your custom **alphagruis-eth-custom.json** file (can have any name you like), type:

```batch
alphagruis-eth.exe alphagruis-eth-custom.json
```

To ensure that the miner restarts automatically (in the unfortunate event of a crash), **alphagruis** recommends launch it via Windows batch/cmd file (see alphagruis-eth.cmd and variants, to connect to your favorite mining pool).

```batch
alphagruis-eth.cmd
```

:small_red_triangle: Press **ctrl+c** to exit gracefully.

*Note:*
- *To overclock AMD GPUs, AMD drivers do not require the executable to run as Administrator.*
- *To overclock NVIDIA GPUs, NVIDIA drivers **require** the executable to run as Administrator.*

#### System Requirements

|Components|Minimum Requirements|
|:--------:|--------------------|
|CPU|Multicore Intel processor (with 64-bit support) or AMD Athlon 64 processor.|
|OS|Windows 10 (64-bit).|
|RAM|8 GiB.|
|GPU|One or more discrete GPUs (AMD or NVIDIA) with **more** than 4 GiB of VRAM (must be above the DAG size). For development, we use hardware up to 12 GPUs each, however, for easy maintenance, we recommend not to exceed 8 GPUs per rig.|
|Storage|256 GiB SSD.|

#### Virtual Memory Size

The virtual memory size must be adjusted upwards according to the current DAG size and the number of discrete GPUs that are installed on your hardware. There is only one imperative rule to respect. The virtual memory size must be equal to or greater than `number of discrete GPUs` * `DAG size` + `size for OS`. For example, if the current DAG size is 4 GiB (4 * 1024 * 1024 * 1024 byte) and you have 7 GPUs, for each GPU you must allocate **at least** 4 GiB of virtual memory plus **at least** 8 GiB for OS: 7 * 4 GiB + 8 GIB = 36 GiB.

**alphagruis** recommends keeping the operating system and the GPU drivers updated to the latest version.

## License

**alphagruis**'s Miner for **Ethereum** is licensed under the terms of the [BSD 3-Clause License](https://github.com/alphagruis/alphagruis-eth/blob/main/LICENSE.txt). *alphagruis*, the *alphagruis logo* and the *alphagruis avatar picture* are trademarks of **alphagruis**. All other product names, trademarks or company names, not attributable to **alphagruis**, are used solely for identification and belong to their respective owners.

[Releases]: https://github.com/alphagruis/alphagruis-eth/releases

<details>
<summary>Sample log file (colorless, *.md file format does not support color).</summary>
<p>

```
Welcome to alphagruis's Miner for Ethereum, v1.0.2, build: 2021.07.29 19:56:43.000.

PCIe: 00000000:09:00.0, GPU.01: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:0a:00.0, GPU.02: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:04:00.0, GPU.03: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:0e:00.0, GPU.04: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:0d:00.0, GPU.05: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:02:00.0, GPU.06: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:0f:00.0, GPU.07: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:0c:00.0, GPU.08: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:06:00.0, GPU.09: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:01:00.0, GPU.10: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:03:00.0, GPU.11: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units
PCIe: 00000000:05:00.0, GPU.12: AMD Accelerated Parallel Processing, OpenCL 2.0 (3224.5), Radeon RX 580 Series, 8.00 GiB, 36 compute units

--- thread ID: 0xf5c, 2021.08.01 13:47:40.638, PCIe: 00000000:09:00.0, GPU.01 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:40.716, PCIe: 00000000:0a:00.0, GPU.02 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:40.795, PCIe: 00000000:04:00.0, GPU.03 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:40.859, PCIe: 00000000:0e:00.0, GPU.04 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:40.936, PCIe: 00000000:0d:00.0, GPU.05 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.014, PCIe: 00000000:02:00.0, GPU.06 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.092, PCIe: 00000000:0f:00.0, GPU.07 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.170, PCIe: 00000000:0c:00.0, GPU.08 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.248, PCIe: 00000000:06:00.0, GPU.09 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.326, PCIe: 00000000:01:00.0, GPU.10 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.405, PCIe: 00000000:03:00.0, GPU.11 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.482, PCIe: 00000000:05:00.0, GPU.12 fDeviceOverclockSettings:
fPowerLimit: min = -50%, max = +50%, default = +0%, set = +0%
fTemperatureLimit: min = 40°C, max = 90°C, default = 90°C, set = 90°C
fClockGraphics: min = [300 MHz, 750 mV], max = [2000 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [1150 MHz, 900 mV]
fClockMemory: min = [1700 MHz, 750 mV], max = [2300 MHz, 1200 mV], default = [300 MHz, 1200 mV], set = [2075 MHz, 900 mV]
fMemoryTimingLevel: min = 0, max = 2, default = 0, set = 2
fFanSpeed: min = 25%, max = 100%, default = 82%, set = 99%

--- thread ID: 0xf5c, 2021.08.01 13:47:41.495
connecting to eu1.ethermine.org:5555

--- thread ID: 0xf5c, 2021.08.01 13:47:41.601
connected to eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:00:00.116)

<<< thread ID: 0x2124, 2021.08.01 13:47:41.601, 0 ms
{"jsonrpc":"2.0","id":1,"method":"eth_submitLogin","params":["..."],"worker":"alphagruis"}

>>> thread ID: 0x1f38, 2021.08.01 13:47:41.616, 14 ms (14 ms)
{"id":1,"jsonrpc":"2.0","result":true}

<<< thread ID: 0x2610, 2021.08.01 13:47:41.616, 0 ms
{"jsonrpc":"2.0","id":14,"method":"eth_getWork","params":[]}

--- thread ID: 0x2170, 2021.08.01 13:47:41.616, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:00:00.131)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2985 rpm, 35°C], 0.000000 MH/s ( 4.33 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2651 rpm, 41°C], 0.000000 MH/s (18.89 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2726 rpm, 40°C], 0.000000 MH/s ( 4.33 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2696 rpm, 39°C], 0.000000 MH/s ( 4.33 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 3430 rpm, 41°C], 0.000000 MH/s ( 4.33 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 3314 rpm, 38°C], 0.000000 MH/s ( 5.57 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2607 rpm, 40°C], 0.000000 MH/s ( 5.99 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2745 rpm, 37°C], 0.000000 MH/s ( 6.01 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2708 rpm, 39°C], 0.000000 MH/s ( 4.33 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2735 rpm, 39°C], 0.000000 MH/s ( 5.99 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2692 rpm, 40°C], 0.000000 MH/s ( 5.57 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 0, S = 0, R = 0, I = 0], [00:00:01.052, 0 ms], [fan = 99%, 2736 rpm, 40°C], 0.000000 MH/s ( 5.99 W) = 0.000000 MH/s (75.67 W)

<<< thread ID: 0x2768, 2021.08.01 13:47:41.623, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000000000000","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0xedc, 2021.08.01 13:47:41.630, 13 ms
{"id":0,"jsonrpc":"2.0","result":["0x31d21c699d1bd47211e669c2a46fd8ed92bfe81f9467ed797bfd852e483457f5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570af"]}

--- thread ID: 0xedc, 2021.08.01 13:47:41.633
epoch = 431 (next epoch in 20561 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:47:41.637, 7 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0xedc, 2021.08.01 13:47:41.678
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute cache...

↓↓↓ thread ID: 0x25d8, 2021.08.01 13:47:41.859
PCIe: 00000000:0a:00.0, GPU.02: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x1970, 2021.08.01 13:47:42.195
PCIe: 00000000:09:00.0, GPU.01: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x2ec, 2021.08.01 13:47:42.503
PCIe: 00000000:04:00.0, GPU.03: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x2fc, 2021.08.01 13:47:42.814
PCIe: 00000000:0e:00.0, GPU.04: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x4e8, 2021.08.01 13:47:43.127
PCIe: 00000000:0d:00.0, GPU.05: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x10c4, 2021.08.01 13:47:43.455
PCIe: 00000000:02:00.0, GPU.06: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x1638, 2021.08.01 13:47:43.783
PCIe: 00000000:0f:00.0, GPU.07: mining is suspended, waiting for work.

↓↓↓ thread ID: 0xf4c, 2021.08.01 13:47:44.111
PCIe: 00000000:0c:00.0, GPU.08: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x2420, 2021.08.01 13:47:44.436
PCIe: 00000000:06:00.0, GPU.09: mining is suspended, waiting for work.

--- thread ID: 0xedc, 2021.08.01 13:47:44.674, 2995 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute cache: done.

↑↑↑ thread ID: 0x1638, 2021.08.01 13:47:44.674
PCIe: 00000000:0f:00.0, GPU.07: mining is resumed.

↑↑↑ thread ID: 0xf4c, 2021.08.01 13:47:44.674
PCIe: 00000000:0c:00.0, GPU.08: mining is resumed.

↑↑↑ thread ID: 0x2420, 2021.08.01 13:47:44.674
PCIe: 00000000:06:00.0, GPU.09: mining is resumed.

↑↑↑ thread ID: 0x10c4, 2021.08.01 13:47:44.674
PCIe: 00000000:02:00.0, GPU.06: mining is resumed.

↑↑↑ thread ID: 0x2fc, 2021.08.01 13:47:44.674
PCIe: 00000000:0e:00.0, GPU.04: mining is resumed.

↑↑↑ thread ID: 0x2ec, 2021.08.01 13:47:44.674
PCIe: 00000000:04:00.0, GPU.03: mining is resumed.

↑↑↑ thread ID: 0x4e8, 2021.08.01 13:47:44.674
PCIe: 00000000:0d:00.0, GPU.05: mining is resumed.

↑↑↑ thread ID: 0x1970, 2021.08.01 13:47:44.674
PCIe: 00000000:09:00.0, GPU.01: mining is resumed.

↑↑↑ thread ID: 0x25d8, 2021.08.01 13:47:44.674
PCIe: 00000000:0a:00.0, GPU.02: mining is resumed.

--- thread ID: 0x2fc, 2021.08.01 13:47:45.129
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0e:00.0, GPU.04 dataset...

--- thread ID: 0x23a0, 2021.08.01 13:47:45.719
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:01:00.0, GPU.10 dataset...

--- thread ID: 0x18c8, 2021.08.01 13:47:46.329
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:03:00.0, GPU.11 dataset...

--- thread ID: 0x5e8, 2021.08.01 13:47:46.744
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:05:00.0, GPU.12 dataset...

--- thread ID: 0x10c4, 2021.08.01 13:47:47.150
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:02:00.0, GPU.06 dataset...

>>> thread ID: 0x2628, 2021.08.01 13:47:47.343, 5705 ms
{"id":0,"jsonrpc":"2.0","result":["0x5989422a3647b106ac866564ae7279232a09ad920715faa2d0744f1bfb8bcd44","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570af"]}

--- thread ID: 0x2628, 2021.08.01 13:47:47.343
epoch = 431 (next epoch in 20561 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x4e8, 2021.08.01 13:47:47.562
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0d:00.0, GPU.05 dataset...

--- thread ID: 0x2ec, 2021.08.01 13:47:47.977
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:04:00.0, GPU.03 dataset...

--- thread ID: 0xf4c, 2021.08.01 13:47:48.388
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0c:00.0, GPU.08 dataset...

--- thread ID: 0x1970, 2021.08.01 13:47:48.805
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:09:00.0, GPU.01 dataset...

--- thread ID: 0x2420, 2021.08.01 13:47:49.219
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:06:00.0, GPU.09 dataset...

--- thread ID: 0x25d8, 2021.08.01 13:47:49.648
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0a:00.0, GPU.02 dataset...

--- thread ID: 0x1638, 2021.08.01 13:47:50.087
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0f:00.0, GPU.07 dataset...

>>> thread ID: 0x1df0, 2021.08.01 13:47:53.459, 6116 ms
{"id":0,"jsonrpc":"2.0","result":["0x60f3056ca5f98891c9da3670538857aad6eec8c8cfb4c087bd8eb4fb89c2d0e2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570af"]}

--- thread ID: 0x1df0, 2021.08.01 13:47:53.459
epoch = 431 (next epoch in 20561 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2fc, 2021.08.01 13:47:54.930, 9800 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0e:00.0, GPU.04 dataset: done.

--- thread ID: 0x23a0, 2021.08.01 13:47:54.997, 9278 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:01:00.0, GPU.10 dataset: done.

--- thread ID: 0x18c8, 2021.08.01 13:47:55.275, 8946 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:03:00.0, GPU.11 dataset: done.

--- thread ID: 0x5e8, 2021.08.01 13:47:55.689, 8944 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:05:00.0, GPU.12 dataset: done.

--- thread ID: 0x10c4, 2021.08.01 13:47:56.093, 8943 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:02:00.0, GPU.06 dataset: done.

--- thread ID: 0x4e8, 2021.08.01 13:47:56.522, 8960 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0d:00.0, GPU.05 dataset: done.

--- thread ID: 0x2170, 2021.08.01 13:47:56.634, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:00:15.149)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070,  2 ms], [fan = 99%, 2928 rpm, 42°C],  0.000000 MH/s ( 72.74 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 21 ms], [fan = 99%, 2624 rpm, 46°C],  0.000000 MH/s ( 71.93 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 44 ms], [fan = 99%, 2670 rpm, 47°C],  0.000000 MH/s ( 71.93 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 17 ms], [fan = 99%, 2647 rpm, 48°C], 27.684853 MH/s ( 98.97 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 29 ms], [fan = 99%, 3346 rpm, 48°C],  0.000000 MH/s ( 86.10 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 25 ms], [fan = 99%, 3281 rpm, 46°C],  0.000000 MH/s (100.66 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070,  4 ms], [fan = 99%, 2561 rpm, 47°C],  0.000000 MH/s ( 74.32 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 53 ms], [fan = 99%, 2696 rpm, 44°C],  0.000000 MH/s ( 74.78 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 33 ms], [fan = 99%, 2655 rpm, 46°C],  0.000000 MH/s ( 73.77 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 25 ms], [fan = 99%, 2678 rpm, 46°C], 27.728859 MH/s (100.25 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 47 ms], [fan = 99%, 2603 rpm, 49°C], 27.919513 MH/s (101.21 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 0, S = 0, R = 0, I = 0], [00:00:16.070, 60 ms], [fan = 99%, 2700 rpm, 50°C],  0.000000 MH/s (101.04 W) = 83.333225 MH/s (1027.71 W)

<<< thread ID: 0x18b4, 2021.08.01 13:47:56.638, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000004f79069","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:47:56.654, 3194 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2ec, 2021.08.01 13:47:56.924, 8946 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:04:00.0, GPU.03 dataset: done.

--- thread ID: 0xf4c, 2021.08.01 13:47:57.344, 8956 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0c:00.0, GPU.08 dataset: done.

--- thread ID: 0x1970, 2021.08.01 13:47:57.763, 8958 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:09:00.0, GPU.01 dataset: done.

--- thread ID: 0x2420, 2021.08.01 13:47:58.162, 8943 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:06:00.0, GPU.09 dataset: done.

--- thread ID: 0x25d8, 2021.08.01 13:47:58.604, 8955 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0a:00.0, GPU.02 dataset: done.

--- thread ID: 0x1638, 2021.08.01 13:47:59.048, 8960 ms
epoch = 431, cache size = 73268672 (69.87 MiB), dataset size = 4689231488 (4.37 GiB), compute PCIe: 00000000:0f:00.0, GPU.07 dataset: done.

>>> thread ID: 0x24b4, 2021.08.01 13:48:01.380, 4725 ms
{"id":0,"jsonrpc":"2.0","result":["0x636c6080f620a325f75812918c089d1cf82d1ddfd893429c769f54961b5040d1","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570af"]}

--- thread ID: 0x24b4, 2021.08.01 13:48:01.380
epoch = 431 (next epoch in 20561 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:48:08.103, 6722 ms
{"id":0,"jsonrpc":"2.0","result":["0xddbee687ba27a97c8eb73e5b1633ca006481808b9e16ea88e6d4cb8e8466b478","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b0"]}

--- thread ID: 0x2610, 2021.08.01 13:48:08.103
epoch = 431 (next epoch in 20560 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:48:08.298, 195 ms
{"id":0,"jsonrpc":"2.0","result":["0x2ce6243c3f22856f60977fd033f7699cd58ed2b2fc1b7ef541fc3a1f659bb786","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b0"]}

--- thread ID: 0x2768, 2021.08.01 13:48:08.298
epoch = 431 (next epoch in 20560 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:48:10.291, 1993 ms
{"id":0,"jsonrpc":"2.0","result":["0x3aacfdb4ebabfa4e42b60ba8d88085cad0e82118268afd425948200cae48c32c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b0"]}

--- thread ID: 0x2648, 2021.08.01 13:48:10.291
epoch = 431 (next epoch in 20560 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:48:11.649, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:00:30.165)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 30 ms], [fan = 99%, 2952 rpm, 47°C], 28.670644 MH/s ( 98.20 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085,  5 ms], [fan = 99%, 2617 rpm, 50°C], 28.709794 MH/s ( 97.73 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 49 ms], [fan = 99%, 2678 rpm, 51°C], 28.621216 MH/s ( 98.23 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 63 ms], [fan = 99%, 2671 rpm, 51°C], 28.883931 MH/s (100.24 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 22 ms], [fan = 99%, 3350 rpm, 52°C], 28.653170 MH/s ( 96.96 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 56 ms], [fan = 99%, 3283 rpm, 49°C], 29.159493 MH/s ( 99.81 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 11 ms], [fan = 99%, 2557 rpm, 52°C], 29.030994 MH/s (100.55 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085,  6 ms], [fan = 99%, 2680 rpm, 48°C], 28.712588 MH/s (100.84 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 45 ms], [fan = 99%, 2655 rpm, 50°C], 28.822010 MH/s (101.12 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 48 ms], [fan = 99%, 2662 rpm, 48°C], 28.728235 MH/s (100.69 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 31 ms], [fan = 99%, 2638 rpm, 52°C], 28.697878 MH/s (100.59 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 0, S = 0, R = 0, I = 0], [00:00:31.085, 35 ms], [fan = 99%, 2717 rpm, 53°C], 28.650859 MH/s (101.07 W) = 345.340812 MH/s (1196.04 W)

<<< thread ID: 0xedc, 2021.08.01 13:48:11.654, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014957b8c","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2628, 2021.08.01 13:48:11.668, 1376 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2fc, 2021.08.01 13:48:13.527, PCIe: 00000000:0e:00.0, GPU.04 share found (search channel 0).
 nonce: 0x13d0a81dee7fd197
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000e99f3508f9550762e03bdcd560574f315458dac1b8901f3e776e5c28
   mix: 0xee6834f71212e547e54a91b270755c4ae6a36d5615cf3e24423e791ef57f6999

<<< thread ID: 0x1df0, 2021.08.01 13:48:13.527, 0 ms
{"jsonrpc":"2.0","id":1001,"method":"eth_submitWork","params":["0x13d0a81dee7fd197","0x3aacfdb4ebabfa4e42b60ba8d88085cad0e82118268afd425948200cae48c32c","0xee6834f71212e547e54a91b270755c4ae6a36d5615cf3e24423e791ef57f6999"],"worker":"alphagruis"}

--- thread ID: 0x18b4, 2021.08.01 13:48:13.542, PCIe: 00000000:0e:00.0, GPU.04 share accepted.

>>> thread ID: 0x18b4, 2021.08.01 13:48:13.542, 1874 ms (15 ms)
{"id":1001,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2630, 2021.08.01 13:48:17.267, 3725 ms
{"id":0,"jsonrpc":"2.0","result":["0xd327179e7a993fc73a368d3fda050e834156a648a063c32c57ef1294d764beb1","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b1"]}

--- thread ID: 0x2630, 2021.08.01 13:48:17.267
epoch = 431 (next epoch in 20559 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:48:17.647, 379 ms
{"id":0,"jsonrpc":"2.0","result":["0x0f84f24bfae613d255f80631b96502bf7b6d13d109c24b17c5098231ebb31f63","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b1"]}

--- thread ID: 0x24b4, 2021.08.01 13:48:17.647
epoch = 431 (next epoch in 20559 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:48:21.358, 3711 ms
{"id":0,"jsonrpc":"2.0","result":["0xf989708918ec37b803a8955f7ee6af6f1a477a29e80263d0e4f085c9f0955192","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b1"]}

--- thread ID: 0x2610, 2021.08.01 13:48:21.358
epoch = 431 (next epoch in 20559 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:48:21.454, 96 ms
{"id":0,"jsonrpc":"2.0","result":["0xb381bf71a3bd0d1ae06714ff65c3cb0778279351d93925a5e43c73a5fc1fb820","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b1"]}

--- thread ID: 0x2768, 2021.08.01 13:48:21.454
epoch = 431 (next epoch in 20559 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:48:23.581, 2126 ms
{"id":0,"jsonrpc":"2.0","result":["0x8b39eaecedb6beecd179cb43df9ffdf03086a157eeea664cadbcf44ffaad1391","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b1"]}

--- thread ID: 0x2648, 2021.08.01 13:48:23.581
epoch = 431 (next epoch in 20559 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:48:24.583, 1002 ms
{"id":0,"jsonrpc":"2.0","result":["0x0c16fc1678c02bc1432bdf6d2eaf05c6bc8da3a8994b87bafac32c00ad3801be","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b2"]}

--- thread ID: 0xedc, 2021.08.01 13:48:24.583
epoch = 431 (next epoch in 20558 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:48:24.722, 139 ms
{"id":0,"jsonrpc":"2.0","result":["0x1f75cf5fba928f68f1e594b6650587b23522131b2da2c378ba9420d5fa532818","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b1"]}

--- thread ID: 0x2628, 2021.08.01 13:48:24.722
epoch = 431 (next epoch in 20559 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:48:24.861, 138 ms
{"id":0,"jsonrpc":"2.0","result":["0xb8d04bde717ef6659b5a7ffa86bd19566489958811c8fc1376f5bed72ba0c625","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b2"]}

--- thread ID: 0x1df0, 2021.08.01 13:48:24.861
epoch = 431 (next epoch in 20558 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2fc, 2021.08.01 13:48:26.480, PCIe: 00000000:0e:00.0, GPU.04 share found (search channel 1).
 nonce: 0x13d0a81ef9b60553
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000ec74de78ac288f6f4c576d880bb9d0dd002ff833f0fd93c2610e3695
   mix: 0x3acadfa9082b6b37b5b6ce547b6071a5e3eb39d11023d83b4c50b671707ee54d

<<< thread ID: 0x18b4, 2021.08.01 13:48:26.480, 0 ms
{"jsonrpc":"2.0","id":1002,"method":"eth_submitWork","params":["0x13d0a81ef9b60553","0xb8d04bde717ef6659b5a7ffa86bd19566489958811c8fc1376f5bed72ba0c625","0x3acadfa9082b6b37b5b6ce547b6071a5e3eb39d11023d83b4c50b671707ee54d"],"worker":"alphagruis"}

--- thread ID: 0x2630, 2021.08.01 13:48:26.497, PCIe: 00000000:0e:00.0, GPU.04 share accepted.

>>> thread ID: 0x2630, 2021.08.01 13:48:26.497, 1635 ms (16 ms)
{"id":1002,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2170, 2021.08.01 13:48:26.665, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:00:45.180)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 21 ms], [fan = 99%, 2948 rpm, 48°C], 28.663544 MH/s ( 98.36 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 16 ms], [fan = 99%, 2620 rpm, 52°C], 28.699796 MH/s ( 97.58 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 56 ms], [fan = 99%, 2658 rpm, 53°C], 28.717237 MH/s ( 99.05 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:00:00.185, 39 ms], [fan = 99%, 2667 rpm, 52°C], 29.103774 MH/s (100.14 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 56 ms], [fan = 99%, 3366 rpm, 54°C], 28.821236 MH/s ( 98.40 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 67 ms], [fan = 99%, 3282 rpm, 50°C], 28.708728 MH/s (100.09 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 56 ms], [fan = 99%, 2553 rpm, 54°C], 28.861905 MH/s (101.82 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 44 ms], [fan = 99%, 2688 rpm, 50°C], 29.042230 MH/s (101.72 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 34 ms], [fan = 99%, 2651 rpm, 52°C], 28.801572 MH/s ( 99.81 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 57 ms], [fan = 99%, 2674 rpm, 50°C], 28.881082 MH/s (100.59 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 10 ms], [fan = 99%, 2630 rpm, 54°C], 29.196825 MH/s (102.13 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 0, S = 0, R = 0, I = 0], [00:00:46.101, 39 ms], [fan = 99%, 2712 rpm, 55°C], 28.717869 MH/s (101.71 W) = 346.215798 MH/s (1201.39 W)

<<< thread ID: 0x24b4, 2021.08.01 13:48:26.669, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014a2d576","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2610, 2021.08.01 13:48:26.679, 182 ms
{"id":0,"jsonrpc":"2.0","result":["0xbd83fb2ca391de56637cbb519d64e3bbacaf1cdd1f0f9fcc9b06816c9959165c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b2"]}

--- thread ID: 0x2610, 2021.08.01 13:48:26.680
epoch = 431 (next epoch in 20558 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:48:26.694, 14 ms (24 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:48:29.785, 3090 ms
{"id":0,"jsonrpc":"2.0","result":["0xe385c7913adf3b00cb1e599b02a1f31fca6af8b07f62cf62d626684a89833ed5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b2"]}

--- thread ID: 0x2648, 2021.08.01 13:48:29.785
epoch = 431 (next epoch in 20558 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:48:33.021, 3236 ms
{"id":0,"jsonrpc":"2.0","result":["0x11178dfe092175fa3caa89ec4878781566b82432799f733fcddf184ed573f3fc","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b3"]}

--- thread ID: 0xedc, 2021.08.01 13:48:33.021
epoch = 431 (next epoch in 20557 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:48:33.175, 154 ms
{"id":0,"jsonrpc":"2.0","result":["0x73e3363413dc0731408ce75b633000006ca11a2c8ef762abd5844744c1c01dd3","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b3"]}

--- thread ID: 0x2628, 2021.08.01 13:48:33.175
epoch = 431 (next epoch in 20557 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:48:36.990, 3814 ms
{"id":0,"jsonrpc":"2.0","result":["0xba00807e22edda2937022e7142a8de28b5b94f1e588f2e8c06889083ae674daa","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b4"]}

--- thread ID: 0x1df0, 2021.08.01 13:48:36.990
epoch = 431 (next epoch in 20556 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:48:37.352, 362 ms
{"id":0,"jsonrpc":"2.0","result":["0x1ff6886afe7ca42ef6001487bbedee3e6ee2676e791246f8e5b9cb29af2dc329","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b4"]}

--- thread ID: 0x18b4, 2021.08.01 13:48:37.352
epoch = 431 (next epoch in 20556 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:48:38.228, 875 ms
{"id":0,"jsonrpc":"2.0","result":["0x38d650fb01fcb565f61fe1d413a324d014248f2f09b814f25e9b2da204bfc726","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b4"]}

--- thread ID: 0x2630, 2021.08.01 13:48:38.228
epoch = 431 (next epoch in 20556 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:48:38.968, 739 ms
{"id":0,"jsonrpc":"2.0","result":["0xf3b24ac379dfcea4b33be110c755e3cff1971d250c774c2b089dc372eecd3b94","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b5"]}

--- thread ID: 0x24b4, 2021.08.01 13:48:38.968
epoch = 431 (next epoch in 20555 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:48:39.205, 237 ms
{"id":0,"jsonrpc":"2.0","result":["0x03535d06123fe48cb7f515e3519eafcaf8ae8a987f7db4c07f987b35402b5d81","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b5"]}

--- thread ID: 0x2610, 2021.08.01 13:48:39.205
epoch = 431 (next epoch in 20555 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:48:41.696, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:01:00.211)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 53 ms], [fan = 99%, 2955 rpm, 48°C], 28.768088 MH/s ( 99.02 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 18 ms], [fan = 99%, 2620 rpm, 54°C], 28.896388 MH/s ( 99.36 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132,  3 ms], [fan = 99%, 2669 rpm, 55°C], 29.197353 MH/s ( 98.03 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:00:15.215, 32 ms], [fan = 99%, 2679 rpm, 53°C], 29.202715 MH/s (100.58 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 45 ms], [fan = 99%, 3335 rpm, 56°C], 28.656154 MH/s ( 97.83 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 11 ms], [fan = 99%, 3273 rpm, 52°C], 28.698782 MH/s ( 99.96 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 63 ms], [fan = 99%, 2557 rpm, 55°C], 29.088274 MH/s (101.97 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 61 ms], [fan = 99%, 2704 rpm, 51°C], 28.894442 MH/s (101.94 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 45 ms], [fan = 99%, 2654 rpm, 53°C], 28.737526 MH/s (100.79 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 22 ms], [fan = 99%, 2690 rpm, 52°C], 28.735458 MH/s (100.35 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132,  2 ms], [fan = 99%, 2629 rpm, 55°C], 29.200345 MH/s (102.62 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 0, S = 0, R = 0, I = 0], [00:01:01.132, 63 ms], [fan = 99%, 2716 rpm, 56°C], 28.718346 MH/s (102.59 W) = 346.793871 MH/s (1205.04 W)

<<< thread ID: 0x2768, 2021.08.01 13:48:41.700, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014aba78f","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2648, 2021.08.01 13:48:41.717, 2512 ms (17 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:48:43.200, 1482 ms
{"id":0,"jsonrpc":"2.0","result":["0x36925968c55eaf280fc724e47339d8b435badce7fa393a668f700a4a86939ded","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b5"]}

--- thread ID: 0xedc, 2021.08.01 13:48:43.200
epoch = 431 (next epoch in 20555 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x23a0, 2021.08.01 13:48:46.393, PCIe: 00000000:01:00.0, GPU.10 share found (search channel 0).
 nonce: 0x13d0a82094d801f6
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000ad73f7c2399d9d09782948abcbba894b5a03eb8dbcaf8285aa066ff3
   mix: 0xda435d9351de5610a4a70047c3dea5ff6288c5c92ae7661d2efab759e72450a6

<<< thread ID: 0x2628, 2021.08.01 13:48:46.393, 0 ms
{"jsonrpc":"2.0","id":1003,"method":"eth_submitWork","params":["0x13d0a82094d801f6","0x36925968c55eaf280fc724e47339d8b435badce7fa393a668f700a4a86939ded","0xda435d9351de5610a4a70047c3dea5ff6288c5c92ae7661d2efab759e72450a6"],"worker":"alphagruis"}

--- thread ID: 0x1df0, 2021.08.01 13:48:46.409, PCIe: 00000000:01:00.0, GPU.10 share accepted.

>>> thread ID: 0x1df0, 2021.08.01 13:48:46.409, 3208 ms (15 ms)
{"id":1003,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:48:49.182, 2773 ms
{"id":0,"jsonrpc":"2.0","result":["0x05cb2ae1b969a7be79abf69da7512445c16362382ce539eee2724ccbdf33a3ef","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b5"]}

--- thread ID: 0x18b4, 2021.08.01 13:48:49.182
epoch = 431 (next epoch in 20555 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:48:50.454, 1271 ms
{"id":0,"jsonrpc":"2.0","result":["0xb86b695fbc057bcfd63bf0a2cc16186f5e86bb8a629a188c75f9147159ade74b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x2630, 2021.08.01 13:48:50.454
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:48:50.704, 250 ms
{"id":0,"jsonrpc":"2.0","result":["0x50c169bb5b7c23f4c4330ba035b17fb6fb8a7fedbc34471918d2e9ef64424697","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x24b4, 2021.08.01 13:48:50.704
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:48:54.591, 3887 ms
{"id":0,"jsonrpc":"2.0","result":["0xf668a4c3eca417627d549df3d01474a3a9345868a6bd7fec00a3bfca5d2e2636","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x2610, 2021.08.01 13:48:54.591
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x4e8, 2021.08.01 13:48:56.101, PCIe: 00000000:0d:00.0, GPU.05 share found (search channel 1).
 nonce: 0x13d0a8215dc46e1a
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000004e1449814078aaaa6e626193f63b860e337239af380f7535f5a12655
   mix: 0x4178457fd789e6cb8781b4b58e16315f9a303cbdce1e867f612d0b2facb04c54

<<< thread ID: 0x2768, 2021.08.01 13:48:56.101, 0 ms
{"jsonrpc":"2.0","id":1004,"method":"eth_submitWork","params":["0x13d0a8215dc46e1a","0xf668a4c3eca417627d549df3d01474a3a9345868a6bd7fec00a3bfca5d2e2636","0x4178457fd789e6cb8781b4b58e16315f9a303cbdce1e867f612d0b2facb04c54"],"worker":"alphagruis"}

--- thread ID: 0x2648, 2021.08.01 13:48:56.117, PCIe: 00000000:0d:00.0, GPU.05 share accepted.

>>> thread ID: 0x2648, 2021.08.01 13:48:56.117, 1526 ms (15 ms)
{"id":1004,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2170, 2021.08.01 13:48:56.728, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:01:15.243)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164, 14 ms], [fan = 99%, 2940 rpm, 49°C], 28.987487 MH/s ( 99.06 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164, 22 ms], [fan = 99%, 2620 rpm, 55°C], 28.778277 MH/s ( 98.53 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164,  0 ms], [fan = 99%, 2681 rpm, 56°C], 29.193298 MH/s ( 98.18 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:00:30.247, 53 ms], [fan = 99%, 2666 rpm, 54°C], 29.126763 MH/s (100.64 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 1, S = 0, R = 0, I = 0], [00:00:00.626, 50 ms], [fan = 99%, 3326 rpm, 57°C], 29.211982 MH/s ( 98.67 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164, 18 ms], [fan = 99%, 3263 rpm, 53°C], 28.882895 MH/s (101.20 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164,  8 ms], [fan = 99%, 2560 rpm, 57°C], 28.684958 MH/s (102.23 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164, 49 ms], [fan = 99%, 2675 rpm, 52°C], 29.212977 MH/s (102.27 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164, 59 ms], [fan = 99%, 2654 rpm, 55°C], 28.664942 MH/s (101.27 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:00:10.335, 55 ms], [fan = 99%, 2661 rpm, 53°C], 29.097268 MH/s (101.68 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164, 34 ms], [fan = 99%, 2606 rpm, 56°C], 28.753559 MH/s (101.76 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 0, S = 0, R = 0, I = 0], [00:01:16.164, 14 ms], [fan = 99%, 2712 rpm, 57°C], 28.704224 MH/s (101.65 W) = 347.298630 MH/s (1207.13 W)

<<< thread ID: 0xedc, 2021.08.01 13:48:56.732, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b35b46","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2628, 2021.08.01 13:48:56.749, 631 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 13:49:00.531, 3782 ms
{"id":0,"jsonrpc":"2.0","result":["0xf8d89fb8ec2210cf83fed595b3e9de388323f77cc4e85b64e60e06b2e5753e0c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x1df0, 2021.08.01 13:49:00.531
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0xf4c, 2021.08.01 13:49:03.511, PCIe: 00000000:0c:00.0, GPU.08 share found (search channel 1).
 nonce: 0x13d0a821f71291a6
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000c5a155f5150c049d4f2303c02cd8f42765d59f62ad1f423c2c3f9159
   mix: 0x24429dfdf80234e724a5dc66002dcf415708390082702a7b801227a3c890e61e

<<< thread ID: 0x18b4, 2021.08.01 13:49:03.511, 0 ms
{"jsonrpc":"2.0","id":1005,"method":"eth_submitWork","params":["0x13d0a821f71291a6","0xf8d89fb8ec2210cf83fed595b3e9de388323f77cc4e85b64e60e06b2e5753e0c","0x24429dfdf80234e724a5dc66002dcf415708390082702a7b801227a3c890e61e"],"worker":"alphagruis"}

--- thread ID: 0x2630, 2021.08.01 13:49:03.527, PCIe: 00000000:0c:00.0, GPU.08 share accepted.

>>> thread ID: 0x2630, 2021.08.01 13:49:03.527, 2995 ms (15 ms)
{"id":1005,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:49:07.690, 4163 ms
{"id":0,"jsonrpc":"2.0","result":["0xb938d8ee9e0c53182155e918055cf220368d31d4631d3c67df5de41165eb13d8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x24b4, 2021.08.01 13:49:07.690
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:49:11.584, 3894 ms
{"id":0,"jsonrpc":"2.0","result":["0xbe17f66dd7d4c6c0d3bd539bc81306652c5dcbe50659b4e1187f0f33d4aeb4a8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x2610, 2021.08.01 13:49:11.584
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:49:11.743, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:01:30.259)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179, 18 ms], [fan = 99%, 2960 rpm, 50°C], 28.675187 MH/s ( 98.98 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179, 29 ms], [fan = 99%, 2616 rpm, 56°C], 28.712287 MH/s ( 98.20 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179, 40 ms], [fan = 99%, 2676 rpm, 57°C], 28.828701 MH/s ( 99.40 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:00:45.263, 26 ms], [fan = 99%, 2638 rpm, 55°C], 29.209010 MH/s (100.93 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 1, S = 0, R = 0, I = 0], [00:00:15.642, 21 ms], [fan = 99%, 3347 rpm, 58°C], 29.209264 MH/s ( 99.14 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179,  1 ms], [fan = 99%, 3266 rpm, 54°C], 28.722356 MH/s (100.51 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179,  2 ms], [fan = 99%, 2579 rpm, 58°C], 28.643262 MH/s (101.48 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:00:08.233, 29 ms], [fan = 99%, 2675 rpm, 53°C], 28.936442 MH/s (101.07 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179, 40 ms], [fan = 99%, 2654 rpm, 56°C], 28.645275 MH/s (100.88 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:00:25.351, 31 ms], [fan = 99%, 2677 rpm, 54°C], 29.206746 MH/s (101.75 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179, 10 ms], [fan = 99%, 2621 rpm, 57°C], 29.143891 MH/s (101.70 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 0, S = 0, R = 0, I = 0], [00:01:31.179, 61 ms], [fan = 99%, 2716 rpm, 59°C], 29.183704 MH/s (102.48 W) = 347.116125 MH/s (1206.53 W)

<<< thread ID: 0x2768, 2021.08.01 13:49:11.748, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b0925d","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2648, 2021.08.01 13:49:11.764, 179 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0x4e8, 2021.08.01 13:49:12.277, PCIe: 00000000:0d:00.0, GPU.05 share found (search channel 0).
 nonce: 0x13d0a822ac791c7f
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000074b1e3529eb7a45dbf2bf85f02b1b1498ab5a0784a111b5ad2f03012
   mix: 0x278557c7d0a49c59dfa52371f86efe80076e9efd80f1a2632c50f83123035c94

<<< thread ID: 0xedc, 2021.08.01 13:49:12.277, 0 ms
{"jsonrpc":"2.0","id":1006,"method":"eth_submitWork","params":["0x13d0a822ac791c7f","0xbe17f66dd7d4c6c0d3bd539bc81306652c5dcbe50659b4e1187f0f33d4aeb4a8","0x278557c7d0a49c59dfa52371f86efe80076e9efd80f1a2632c50f83123035c94"],"worker":"alphagruis"}

--- thread ID: 0x2628, 2021.08.01 13:49:12.294, PCIe: 00000000:0d:00.0, GPU.05 share accepted.

>>> thread ID: 0x2628, 2021.08.01 13:49:12.294, 530 ms (17 ms)
{"id":1006,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2ec, 2021.08.01 13:49:13.283, PCIe: 00000000:04:00.0, GPU.03 share found (search channel 0).
 nonce: 0x13d0a822c1535eab
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000003be072a26e80676abccc5d6b8c5a0ebf0c42c1390344c7a8684701b2
   mix: 0x5c5624d6e593adc50295d9c211e928f593e6a44a357d65446e7b3cce79403723

<<< thread ID: 0x1df0, 2021.08.01 13:49:13.283, 0 ms
{"jsonrpc":"2.0","id":1007,"method":"eth_submitWork","params":["0x13d0a822c1535eab","0xbe17f66dd7d4c6c0d3bd539bc81306652c5dcbe50659b4e1187f0f33d4aeb4a8","0x5c5624d6e593adc50295d9c211e928f593e6a44a357d65446e7b3cce79403723"],"worker":"alphagruis"}

--- thread ID: 0x18b4, 2021.08.01 13:49:13.298, PCIe: 00000000:04:00.0, GPU.03 share accepted.

>>> thread ID: 0x18b4, 2021.08.01 13:49:13.298, 1003 ms (15 ms)
{"id":1007,"jsonrpc":"2.0","result":true}

--- thread ID: 0x5e8, 2021.08.01 13:49:14.910, PCIe: 00000000:05:00.0, GPU.12 share found (search channel 1).
 nonce: 0x13d0a822e2c8fcde
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000007beb3217f98cca3a309f9cf27cb97600e2770cf2da8cd35f97b86565
   mix: 0x9a0e20d0c7a55cdaf2a4d9a94a0a4ccc40e29e11070a40420b29c765a7eaedd9

<<< thread ID: 0x2630, 2021.08.01 13:49:14.910, 0 ms
{"jsonrpc":"2.0","id":1008,"method":"eth_submitWork","params":["0x13d0a822e2c8fcde","0xbe17f66dd7d4c6c0d3bd539bc81306652c5dcbe50659b4e1187f0f33d4aeb4a8","0x9a0e20d0c7a55cdaf2a4d9a94a0a4ccc40e29e11070a40420b29c765a7eaedd9"],"worker":"alphagruis"}

--- thread ID: 0x24b4, 2021.08.01 13:49:14.926, PCIe: 00000000:05:00.0, GPU.12 share accepted.

>>> thread ID: 0x24b4, 2021.08.01 13:49:14.926, 1627 ms (15 ms)
{"id":1008,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:49:20.767, 5841 ms
{"id":0,"jsonrpc":"2.0","result":["0x15569a7a9f95b3afbdce45e62e4e1950feecdfc94d6b39321a2274dbae825d7a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x2610, 2021.08.01 13:49:20.768
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x18c8, 2021.08.01 13:49:23.319, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 1).
 nonce: 0x13d0a82391256c13
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000009c503a492484515a5bd754794db1ec244fa7626798e3d862475d05d2
   mix: 0x0f687454fd2afa611cc085718f6826739ac3588e67f1aaa386acce292f8c9dd2

<<< thread ID: 0x2768, 2021.08.01 13:49:23.319, 0 ms
{"jsonrpc":"2.0","id":1009,"method":"eth_submitWork","params":["0x13d0a82391256c13","0x15569a7a9f95b3afbdce45e62e4e1950feecdfc94d6b39321a2274dbae825d7a","0x0f687454fd2afa611cc085718f6826739ac3588e67f1aaa386acce292f8c9dd2"],"worker":"alphagruis"}

--- thread ID: 0x2648, 2021.08.01 13:49:23.335, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0x2648, 2021.08.01 13:49:23.335, 2567 ms (15 ms)
{"id":1009,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:49:24.532, 1197 ms
{"id":0,"jsonrpc":"2.0","result":["0x5d7155a4e185beac5cf1e274b278017162f37515340898985fdfb559e6440229","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0xedc, 2021.08.01 13:49:24.532
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:49:24.642, 110 ms
{"id":0,"jsonrpc":"2.0","result":["0x36ebce0df2fd7d39d03a4145a0d25fdb32d83c181b65d4b9fbbc1c06f1a368b9","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b6"]}

--- thread ID: 0x2628, 2021.08.01 13:49:24.642
epoch = 431 (next epoch in 20554 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:49:25.268, 625 ms
{"id":0,"jsonrpc":"2.0","result":["0x8766ed09b29c88208e7e8d46cfc6428b21694103e24d96f28b748d8967a46bad","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b7"]}

--- thread ID: 0x1df0, 2021.08.01 13:49:25.268
epoch = 431 (next epoch in 20553 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:49:25.391, 123 ms
{"id":0,"jsonrpc":"2.0","result":["0xaed0f105205cb462e97c12f31a59bc197f846bef9e16e7cfed07946d468317a2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b7"]}

--- thread ID: 0x18b4, 2021.08.01 13:49:25.391
epoch = 431 (next epoch in 20553 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:49:26.759, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:01:45.274)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:01:46.195, 47 ms], [fan = 99%, 2959 rpm, 50°C], 28.734374 MH/s ( 99.30 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:01:46.195, 21 ms], [fan = 99%, 2616 rpm, 57°C], 28.672796 MH/s ( 98.29 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 1, S = 0, R = 0, I = 0], [00:00:13.476,  8 ms], [fan = 99%, 2664 rpm, 57°C], 29.219294 MH/s ( 99.59 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:01:00.278,  4 ms], [fan = 99%, 2637 rpm, 56°C], 29.197119 MH/s (101.13 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 2, S = 0, R = 0, I = 0], [00:00:14.481,  5 ms], [fan = 99%, 3321 rpm, 59°C], 29.186141 MH/s ( 99.26 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:01:46.195, 65 ms], [fan = 99%, 3297 rpm, 55°C], 28.705252 MH/s (100.47 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 0, S = 0, R = 0, I = 0], [00:01:46.195, 15 ms], [fan = 99%, 2579 rpm, 59°C], 29.216580 MH/s (102.44 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:00:23.248, 25 ms], [fan = 99%, 2679 rpm, 54°C], 28.661233 MH/s (102.32 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:01:46.195, 13 ms], [fan = 99%, 2658 rpm, 57°C], 29.220605 MH/s (102.02 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:00:40.366, 11 ms], [fan = 99%, 2644 rpm, 55°C], 29.193163 MH/s (102.11 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 1, S = 0, R = 0, I = 0], [00:00:03.440, 56 ms], [fan = 99%, 2620 rpm, 58°C], 28.832256 MH/s (102.75 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:00:11.848, 55 ms], [fan = 99%, 2707 rpm, 59°C], 28.726670 MH/s (101.98 W) = 347.565483 MH/s (1211.66 W)

<<< thread ID: 0x2630, 2021.08.01 13:49:26.763, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b76dab","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:49:26.779, 1387 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:49:27.306, 527 ms
{"id":0,"jsonrpc":"2.0","result":["0x68cdc3f2a656360e7d497d8d18f6aeec3fe0c7f5ee5a59e763016e62ef9be9e3","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b7"]}

--- thread ID: 0x2610, 2021.08.01 13:49:27.306
epoch = 431 (next epoch in 20553 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:49:28.305, 998 ms
{"id":0,"jsonrpc":"2.0","result":["0xa5492cb4a7409550762120630ed3a514730e192ee4444b2ea776d4cb648c3052","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b7"]}

--- thread ID: 0x2768, 2021.08.01 13:49:28.305
epoch = 431 (next epoch in 20553 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:49:29.696, 1390 ms
{"id":0,"jsonrpc":"2.0","result":["0x7f6ed15f93151a825947dcbaffa3f4a47c4e7c9d874347affc85d98b7ac975cc","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b7"]}

--- thread ID: 0x2648, 2021.08.01 13:49:29.696
epoch = 431 (next epoch in 20553 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:49:30.751, 1055 ms
{"id":0,"jsonrpc":"2.0","result":["0x3b401ea430c22729d360a13d851427ea99a0a61b519bba876485b1f45db7504e","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b7"]}

--- thread ID: 0xedc, 2021.08.01 13:49:30.751
epoch = 431 (next epoch in 20553 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:49:30.961, 209 ms
{"id":0,"jsonrpc":"2.0","result":["0xf28429ea3c008c632fb8ef0ae314b51e95d27a5f4a209982da95f335f49d7660","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b8"]}

--- thread ID: 0x2628, 2021.08.01 13:49:30.961
epoch = 431 (next epoch in 20552 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:49:31.329, 368 ms
{"id":0,"jsonrpc":"2.0","result":["0x4d826e5ad5651786731782bcf14c72cc7b37ac2b7f330ba08346c18aae3a6d60","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b8"]}

--- thread ID: 0x1df0, 2021.08.01 13:49:31.329
epoch = 431 (next epoch in 20552 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:49:32.138, 808 ms
{"id":0,"jsonrpc":"2.0","result":["0x3c96c799e2885d7e54e420ab8609957b84ee0daf18f65d6864356d2fa431fe02","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b8"]}

--- thread ID: 0x18b4, 2021.08.01 13:49:32.138
epoch = 431 (next epoch in 20552 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x1638, 2021.08.01 13:49:32.427, PCIe: 00000000:0f:00.0, GPU.07 share found (search channel 1).
 nonce: 0x13d0a8244e07dd05
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000059f2ed30be98c1a6c2bf15a09dd5929db7d0f4b9054b8621e231d6c2
   mix: 0xe002262b1e60a9bc3e061a5bdae2a5c588eefc9ab7947783acafc1b6387bb3d2

<<< thread ID: 0x2630, 2021.08.01 13:49:32.428, 0 ms
{"jsonrpc":"2.0","id":1010,"method":"eth_submitWork","params":["0x13d0a8244e07dd05","0x3c96c799e2885d7e54e420ab8609957b84ee0daf18f65d6864356d2fa431fe02","0xe002262b1e60a9bc3e061a5bdae2a5c588eefc9ab7947783acafc1b6387bb3d2"],"worker":"alphagruis"}

--- thread ID: 0x24b4, 2021.08.01 13:49:32.443, PCIe: 00000000:0f:00.0, GPU.07 share accepted.

>>> thread ID: 0x24b4, 2021.08.01 13:49:32.443, 305 ms (15 ms)
{"id":1010,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:49:33.074, 630 ms
{"id":0,"jsonrpc":"2.0","result":["0x8c253b086b4fa3e56e7cb54db9937babc6c50ef56fc1d6c2a047c85a5e396764","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b8"]}

--- thread ID: 0x2610, 2021.08.01 13:49:33.074
epoch = 431 (next epoch in 20552 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:49:36.331, 3257 ms
{"id":0,"jsonrpc":"2.0","result":["0x84337ae1f504c94bac9c78e545b945982949eb45523ed44a6e53dae50f0b2822","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b8"]}

--- thread ID: 0x2768, 2021.08.01 13:49:36.331
epoch = 431 (next epoch in 20552 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:49:37.510, 1179 ms
{"id":0,"jsonrpc":"2.0","result":["0x8668313ba253790a37408eb508afe633e6be58080afde2a28f874c7d3438cc4f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b9"]}

--- thread ID: 0x2648, 2021.08.01 13:49:37.511
epoch = 431 (next epoch in 20551 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:49:37.763, 252 ms
{"id":0,"jsonrpc":"2.0","result":["0x55eb6c1adea11f81eb3cd19a3d678ccdec63f80e992cb93e64d6617701962431","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570b9"]}

--- thread ID: 0xedc, 2021.08.01 13:49:37.763
epoch = 431 (next epoch in 20551 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:49:40.052, 2288 ms
{"id":0,"jsonrpc":"2.0","result":["0x4f8ef565f999ec7c95378f7101a609b2faeac97203f50f587d7af6a4f218e737","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ba"]}

--- thread ID: 0x2628, 2021.08.01 13:49:40.052
epoch = 431 (next epoch in 20550 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:49:40.278, 226 ms
{"id":0,"jsonrpc":"2.0","result":["0x8640811e994d2892e7ebf5b0060fba32559b502128d8cfc7196128fba9900843","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ba"]}

--- thread ID: 0x1df0, 2021.08.01 13:49:40.279
epoch = 431 (next epoch in 20550 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:49:41.774, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:02:00.290)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:02:01.210,  0 ms], [fan = 99%, 2944 rpm, 51°C], 29.015593 MH/s (100.52 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:02:01.210,  2 ms], [fan = 99%, 2620 rpm, 58°C], 29.100047 MH/s ( 99.77 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 1, S = 0, R = 0, I = 0], [00:00:28.491,  4 ms], [fan = 99%, 2679 rpm, 58°C], 29.203443 MH/s ( 99.64 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:01:15.294,  0 ms], [fan = 99%, 2645 rpm, 57°C], 29.213681 MH/s (100.95 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 2, S = 0, R = 0, I = 0], [00:00:29.497, 54 ms], [fan = 99%, 3344 rpm, 60°C], 29.195224 MH/s ( 99.31 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:02:01.210,  2 ms], [fan = 99%, 3312 rpm, 55°C], 28.703842 MH/s (101.18 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 1, S = 0, R = 0, I = 0], [00:00:09.347,  4 ms], [fan = 99%, 2564 rpm, 59°C], 29.202873 MH/s (102.60 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:00:38.264,  0 ms], [fan = 99%, 2695 rpm, 54°C], 29.215655 MH/s (102.27 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:02:01.210,  4 ms], [fan = 99%, 2658 rpm, 58°C], 29.203849 MH/s (101.97 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:00:55.381,  0 ms], [fan = 99%, 2668 rpm, 55°C], 29.210399 MH/s (101.90 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 1, S = 0, R = 0, I = 0], [00:00:18.455, 31 ms], [fan = 99%, 2639 rpm, 59°C], 29.199580 MH/s (102.81 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:00:26.864, 55 ms], [fan = 99%, 2723 rpm, 60°C], 29.173658 MH/s (103.22 W) = 349.637844 MH/s (1216.14 W)

<<< thread ID: 0x18b4, 2021.08.01 13:49:41.779, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014d70cd4","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:49:41.795, 1516 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:49:44.317, 2521 ms
{"id":0,"jsonrpc":"2.0","result":["0x42b0af0fde38fe5b1f3f66f18d34b59093ec904606f58b12f4fdc10dbe61eb27","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ba"]}

--- thread ID: 0x24b4, 2021.08.01 13:49:44.317
epoch = 431 (next epoch in 20550 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:49:44.396, 79 ms
{"id":0,"jsonrpc":"2.0","result":["0x62c8aebc92e98260578201df71ecfdbe224e98885856dd697b147c96633cd5c3","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ba"]}

--- thread ID: 0x2610, 2021.08.01 13:49:44.397
epoch = 431 (next epoch in 20550 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x18c8, 2021.08.01 13:49:44.908, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 0).
 nonce: 0x13d0a82551f4f120
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000d1aff89d763f0ef98c92318af0721598be328a806f496cc52e28069a
   mix: 0xccc949772de6ff36f3f58aeca713b2f330f02fd0d11bf98ec5a4b7c62c4a768d

<<< thread ID: 0x2768, 2021.08.01 13:49:44.908, 0 ms
{"jsonrpc":"2.0","id":1011,"method":"eth_submitWork","params":["0x13d0a82551f4f120","0x62c8aebc92e98260578201df71ecfdbe224e98885856dd697b147c96633cd5c3","0xccc949772de6ff36f3f58aeca713b2f330f02fd0d11bf98ec5a4b7c62c4a768d"],"worker":"alphagruis"}

--- thread ID: 0x2648, 2021.08.01 13:49:44.924, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0x2648, 2021.08.01 13:49:44.924, 527 ms (15 ms)
{"id":1011,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:49:46.373, 1449 ms
{"id":0,"jsonrpc":"2.0","result":["0x9fcbb35e66e9e8237b893aac96f12d3cd524d2bcd008437fee304653dd7e4116","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bb"]}

--- thread ID: 0xedc, 2021.08.01 13:49:46.374
epoch = 431 (next epoch in 20549 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:49:46.607, 233 ms
{"id":0,"jsonrpc":"2.0","result":["0xcc0c5d7c59febe84d232b902530adb4d2468ac002be9011cf7385c82cd47e779","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bb"]}

--- thread ID: 0x2628, 2021.08.01 13:49:46.607
epoch = 431 (next epoch in 20549 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:49:47.472, 865 ms
{"id":0,"jsonrpc":"2.0","result":["0x63d95837e74b5f79f10223bf41cd28b5ef8c6258933c3a4a39d99fc782c4e9ed","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bb"]}

--- thread ID: 0x1df0, 2021.08.01 13:49:47.472
epoch = 431 (next epoch in 20549 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x4e8, 2021.08.01 13:49:50.118, PCIe: 00000000:0d:00.0, GPU.05 share found (search channel 1).
 nonce: 0x13d0a825be7dd585
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000f46221d69f5a6ca36125e020dfe5a7ec631bcfce3fffaf6a202d6aad
   mix: 0x02cabf9cc96b23c6e28da08d97e44592232099649310e5d5ea4a9602b6426161

<<< thread ID: 0x18b4, 2021.08.01 13:49:50.118, 0 ms
{"jsonrpc":"2.0","id":1012,"method":"eth_submitWork","params":["0x13d0a825be7dd585","0x63d95837e74b5f79f10223bf41cd28b5ef8c6258933c3a4a39d99fc782c4e9ed","0x02cabf9cc96b23c6e28da08d97e44592232099649310e5d5ea4a9602b6426161"],"worker":"alphagruis"}

--- thread ID: 0x2630, 2021.08.01 13:49:50.134, PCIe: 00000000:0d:00.0, GPU.05 share accepted.

>>> thread ID: 0x2630, 2021.08.01 13:49:50.134, 2661 ms (15 ms)
{"id":1012,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:49:53.503, 3369 ms
{"id":0,"jsonrpc":"2.0","result":["0xa51edec4d296fcd445fef3e0cf194c332284c1bec04804213d6fb1de0aed355d","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bb"]}

--- thread ID: 0x24b4, 2021.08.01 13:49:53.503
epoch = 431 (next epoch in 20549 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:49:56.789, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:02:15.305)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:02:16.225, 44 ms], [fan = 99%, 2924 rpm, 51°C], 29.190114 MH/s (100.61 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:02:16.225, 44 ms], [fan = 99%, 2623 rpm, 58°C], 29.215989 MH/s ( 99.56 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 1, S = 0, R = 0, I = 0], [00:00:43.506, 28 ms], [fan = 99%, 2671 rpm, 59°C], 29.218153 MH/s ( 99.81 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:01:30.309, 19 ms], [fan = 99%, 2670 rpm, 58°C], 29.220002 MH/s (101.21 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:00:06.671, 48 ms], [fan = 99%, 3344 rpm, 60°C], 29.206725 MH/s ( 99.33 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:02:16.225, 18 ms], [fan = 99%, 3289 rpm, 56°C], 28.715030 MH/s (100.73 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 1, S = 0, R = 0, I = 0], [00:00:24.362, 38 ms], [fan = 99%, 2579 rpm, 60°C], 29.206179 MH/s (102.80 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:00:53.279, 38 ms], [fan = 99%, 2686 rpm, 54°C], 29.197683 MH/s (102.66 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:02:16.225, 33 ms], [fan = 99%, 2670 rpm, 58°C], 29.217086 MH/s (102.06 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:01:10.397,  7 ms], [fan = 99%, 2667 rpm, 56°C], 28.819063 MH/s (101.03 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 2, S = 0, R = 0, I = 0], [00:00:11.881, 12 ms], [fan = 99%, 2639 rpm, 60°C], 28.684770 MH/s (101.48 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:00:41.879,  7 ms], [fan = 99%, 2727 rpm, 61°C], 29.144568 MH/s (103.68 W) = 349.035362 MH/s (1214.97 W)

<<< thread ID: 0x2610, 2021.08.01 13:49:56.794, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014cddb62","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2768, 2021.08.01 13:49:56.810, 3306 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:50:01.845, 5035 ms
{"id":0,"jsonrpc":"2.0","result":["0x3788cd407133075adc9f1f1caf2e7a0ee4438aa45d39f6d7b20b82c9951c4b55","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bb"]}

--- thread ID: 0x2648, 2021.08.01 13:50:01.845
epoch = 431 (next epoch in 20549 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:50:04.524, 2678 ms
{"id":0,"jsonrpc":"2.0","result":["0x6deb9b26e8fba82e967db92dcc85e64f271629d11d9f5a406237e2dd955a7904","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bb"]}

--- thread ID: 0xedc, 2021.08.01 13:50:04.524
epoch = 431 (next epoch in 20549 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:50:11.806, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:02:30.322)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:02:31.242, 33 ms], [fan = 99%, 2916 rpm, 51°C], 28.673051 MH/s ( 99.21 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:02:31.242, 18 ms], [fan = 99%, 2616 rpm, 59°C], 29.214301 MH/s ( 99.84 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 1, S = 0, R = 0, I = 0], [00:00:58.523,  0 ms], [fan = 99%, 2683 rpm, 60°C], 29.223761 MH/s ( 99.93 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:01:45.326, 44 ms], [fan = 99%, 2686 rpm, 58°C], 29.230355 MH/s (101.19 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:00:21.688, 25 ms], [fan = 99%, 3339 rpm, 61°C], 29.177926 MH/s ( 99.47 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:02:31.242, 23 ms], [fan = 99%, 3284 rpm, 56°C], 28.902721 MH/s (101.47 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 1, S = 0, R = 0, I = 0], [00:00:39.379,  7 ms], [fan = 99%, 2567 rpm, 61°C], 29.228026 MH/s (102.71 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:01:08.296, 15 ms], [fan = 99%, 2702 rpm, 55°C], 29.218643 MH/s (102.59 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:02:31.242,  7 ms], [fan = 99%, 2650 rpm, 59°C], 29.217075 MH/s (102.16 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:01:25.414, 40 ms], [fan = 99%, 2671 rpm, 56°C], 28.934656 MH/s (102.03 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 2, S = 0, R = 0, I = 0], [00:00:26.898, 38 ms], [fan = 99%, 2631 rpm, 60°C], 28.702189 MH/s (101.92 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:00:56.896, 27 ms], [fan = 99%, 2703 rpm, 62°C], 28.708206 MH/s (102.44 W) = 348.430910 MH/s (1214.96 W)

<<< thread ID: 0x2628, 2021.08.01 13:50:11.811, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c4a23e","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x1df0, 2021.08.01 13:50:11.826, 7302 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:50:13.502, 1675 ms
{"id":0,"jsonrpc":"2.0","result":["0x0e840d5225c73ab544681dcb03863fbd3ce734acd4c2ba8b98044e0f9d314e16","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bb"]}

--- thread ID: 0x18b4, 2021.08.01 13:50:13.502
epoch = 431 (next epoch in 20549 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:50:17.152, 3649 ms
{"id":0,"jsonrpc":"2.0","result":["0x98caeb0f6412452214476d44b0ea4b854f5b03f7f991091ece004b42fff2f6eb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bc"]}

--- thread ID: 0x2630, 2021.08.01 13:50:17.152
epoch = 431 (next epoch in 20548 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:50:17.406, 254 ms
{"id":0,"jsonrpc":"2.0","result":["0x3d4bb9d78508c671746e618c2425b40ca3feb3cf732d75296cf9f751aeb43046","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bc"]}

--- thread ID: 0x24b4, 2021.08.01 13:50:17.406
epoch = 431 (next epoch in 20548 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x25d8, 2021.08.01 13:50:19.562, PCIe: 00000000:0a:00.0, GPU.02 share found (search channel 1).
 nonce: 0x13d0a828225839cc
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000fc3c3e5b6a9cb86f407912470effb68cae90fcaa5231ce351653a53f
   mix: 0x157b39b93b6ceaef76f8872b789f9f3e023dbb2f6f34117a8c19a3c789fb8031

<<< thread ID: 0x2610, 2021.08.01 13:50:19.563, 0 ms
{"jsonrpc":"2.0","id":1013,"method":"eth_submitWork","params":["0x13d0a828225839cc","0x3d4bb9d78508c671746e618c2425b40ca3feb3cf732d75296cf9f751aeb43046","0x157b39b93b6ceaef76f8872b789f9f3e023dbb2f6f34117a8c19a3c789fb8031"],"worker":"alphagruis"}

--- thread ID: 0x2768, 2021.08.01 13:50:19.578, PCIe: 00000000:0a:00.0, GPU.02 share accepted.

>>> thread ID: 0x2768, 2021.08.01 13:50:19.578, 2172 ms (16 ms)
{"id":1013,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2ec, 2021.08.01 13:50:20.014, PCIe: 00000000:04:00.0, GPU.03 share found (search channel 1).
 nonce: 0x13d0a8282bffff61
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000072e4e337f2ff7b1dde967d147f63356f7933029fdfb1953a7fdf41a1
   mix: 0xbee65047c318e670a6b659f1852292bf6d27c99712515c6324948604f78b0afc

<<< thread ID: 0x2648, 2021.08.01 13:50:20.014, 0 ms
{"jsonrpc":"2.0","id":1014,"method":"eth_submitWork","params":["0x13d0a8282bffff61","0x3d4bb9d78508c671746e618c2425b40ca3feb3cf732d75296cf9f751aeb43046","0xbee65047c318e670a6b659f1852292bf6d27c99712515c6324948604f78b0afc"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:50:20.031, PCIe: 00000000:04:00.0, GPU.03 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:50:20.031, 452 ms (16 ms)
{"id":1014,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:50:23.660, 3629 ms
{"id":0,"jsonrpc":"2.0","result":["0x7d8de7c70b1a8711f24b0d2fb1dd1837ebab94e40446da0e2a5627b185439a11","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bd"]}

--- thread ID: 0x2628, 2021.08.01 13:50:23.660
epoch = 431 (next epoch in 20547 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:50:23.892, 231 ms
{"id":0,"jsonrpc":"2.0","result":["0x1e1d71bea27d6f19b864e5b41bb0879da697941e35b605ee5bcb3e8455dd5286","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bd"]}

--- thread ID: 0x1df0, 2021.08.01 13:50:23.892
epoch = 431 (next epoch in 20547 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:50:25.868, 1976 ms
{"id":0,"jsonrpc":"2.0","result":["0x596e6f04234796e160bb06bc9d901852f7fbddc38e71dd2522f1ed7bed41f6eb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bd"]}

--- thread ID: 0x18b4, 2021.08.01 13:50:25.868
epoch = 431 (next epoch in 20547 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:50:26.837, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:02:45.352)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:02:46.273, 11 ms], [fan = 99%, 2936 rpm, 51°C], 28.650736 MH/s ( 99.35 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:00:07.275,  4 ms], [fan = 99%, 2631 rpm, 60°C], 29.218413 MH/s ( 99.79 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:00:06.823, 43 ms], [fan = 99%, 2686 rpm, 60°C], 29.216113 MH/s ( 99.91 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:02:00.356, 43 ms], [fan = 99%, 2677 rpm, 59°C], 29.089699 MH/s (101.29 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:00:36.718,  6 ms], [fan = 99%, 3352 rpm, 61°C], 29.218032 MH/s ( 99.48 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:02:46.273,  8 ms], [fan = 99%, 3268 rpm, 57°C], 29.217643 MH/s (101.59 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 1, S = 0, R = 0, I = 0], [00:00:54.409, 39 ms], [fan = 99%, 2563 rpm, 61°C], 29.217015 MH/s (102.34 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:01:23.326,  0 ms], [fan = 99%, 2690 rpm, 56°C], 29.218155 MH/s (102.54 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:02:46.273, 39 ms], [fan = 99%, 2641 rpm, 59°C], 29.218746 MH/s (102.43 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:01:40.444,  1 ms], [fan = 99%, 2679 rpm, 57°C], 28.892659 MH/s (101.61 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 2, S = 0, R = 0, I = 0], [00:00:41.929, 35 ms], [fan = 99%, 2635 rpm, 61°C], 28.852771 MH/s (103.16 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:01:11.927, 63 ms], [fan = 99%, 2719 rpm, 62°C], 28.588884 MH/s (102.37 W) = 348.598866 MH/s (1215.87 W)

<<< thread ID: 0x2630, 2021.08.01 13:50:26.841, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c73252","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:50:26.857, 989 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:50:27.809, 951 ms
{"id":0,"jsonrpc":"2.0","result":["0x8d1cbee7da1402e8b439ec31f2a9f1b140aabd39912ecf53a85a6fa1715e6d5b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bd"]}

--- thread ID: 0x2610, 2021.08.01 13:50:27.809
epoch = 431 (next epoch in 20547 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:50:29.817, 2008 ms
{"id":0,"jsonrpc":"2.0","result":["0x4bed9af3213993ac4ede536dd6454ade712014314ae881318f06b368db886cba","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bd"]}

--- thread ID: 0x2768, 2021.08.01 13:50:29.817
epoch = 431 (next epoch in 20547 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:50:31.354, 1537 ms
{"id":0,"jsonrpc":"2.0","result":["0xff2b563d82fe8ded363ee426785b55f693a475cd0872b7ac9ac29ad2492c5a0e","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570be"]}

--- thread ID: 0x2648, 2021.08.01 13:50:31.354
epoch = 431 (next epoch in 20546 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:50:31.480, 126 ms
{"id":0,"jsonrpc":"2.0","result":["0xd9f1467c98aec060173a57da6befbbcfb482ed11e5d681a3ec3374008b129c99","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570be"]}

--- thread ID: 0xedc, 2021.08.01 13:50:31.480
epoch = 431 (next epoch in 20546 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x1638, 2021.08.01 13:50:31.670, PCIe: 00000000:0f:00.0, GPU.07 share found (search channel 1).
 nonce: 0x13d0a8291e2fa64a
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000003b6a3495d7348667655d2f8fb81e3da95c90ef8c361f456e8eb71471
   mix: 0xa6ac81171641f0cb21c0b4530303c156634623241b418141e0abf1867a8fd089

<<< thread ID: 0x2628, 2021.08.01 13:50:31.670, 0 ms
{"jsonrpc":"2.0","id":1015,"method":"eth_submitWork","params":["0x13d0a8291e2fa64a","0xd9f1467c98aec060173a57da6befbbcfb482ed11e5d681a3ec3374008b129c99","0xa6ac81171641f0cb21c0b4530303c156634623241b418141e0abf1867a8fd089"],"worker":"alphagruis"}

--- thread ID: 0x1df0, 2021.08.01 13:50:31.688, PCIe: 00000000:0f:00.0, GPU.07 share accepted.

>>> thread ID: 0x1df0, 2021.08.01 13:50:31.688, 207 ms (17 ms)
{"id":1015,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:50:35.562, 3874 ms
{"id":0,"jsonrpc":"2.0","result":["0x346cb65a171ff1faf8564332cbe89b5e9d645d95759333d9dfe07b7983e92988","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570be"]}

--- thread ID: 0x18b4, 2021.08.01 13:50:35.562
epoch = 431 (next epoch in 20546 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:50:39.402, 3840 ms
{"id":0,"jsonrpc":"2.0","result":["0x09142ec2ab1f07c707abea43219e924995c581b02bccdc5dcde77049917f1cdf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570be"]}

--- thread ID: 0x2630, 2021.08.01 13:50:39.402
epoch = 431 (next epoch in 20546 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:50:40.190, 788 ms
{"id":0,"jsonrpc":"2.0","result":["0xb40f694a38f10aa56465b4fd146aa7cd847ad60f40b42cf367e91e04fc108d0b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bf"]}

--- thread ID: 0x24b4, 2021.08.01 13:50:40.190
epoch = 431 (next epoch in 20545 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:50:40.319, 128 ms
{"id":0,"jsonrpc":"2.0","result":["0x3c0b4b8a2a1d2aac2221f1a2ba8c7a8f2a5abce6bf53968051a8227fd3feb3a6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570bf"]}

--- thread ID: 0x2610, 2021.08.01 13:50:40.319
epoch = 431 (next epoch in 20545 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:50:41.852, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:03:00.368)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:03:01.288, 62 ms], [fan = 99%, 2956 rpm, 52°C], 29.169269 MH/s ( 99.60 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:00:22.290, 13 ms], [fan = 99%, 2620 rpm, 60°C], 29.196585 MH/s ( 99.80 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:00:21.838, 14 ms], [fan = 99%, 2670 rpm, 61°C], 28.689517 MH/s ( 98.65 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:02:15.372, 30 ms], [fan = 99%, 2657 rpm, 59°C], 28.981661 MH/s (101.42 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:00:51.734, 18 ms], [fan = 99%, 3330 rpm, 62°C], 29.231093 MH/s ( 99.58 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:03:01.288,  9 ms], [fan = 99%, 3322 rpm, 57°C], 29.200367 MH/s (101.68 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:00:10.182, 32 ms], [fan = 99%, 2563 rpm, 62°C], 28.892857 MH/s (101.36 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:01:38.342, 18 ms], [fan = 99%, 2674 rpm, 56°C], 29.230289 MH/s (102.54 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:03:01.288, 28 ms], [fan = 99%, 2633 rpm, 60°C], 29.097865 MH/s (102.49 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:01:55.459, 16 ms], [fan = 99%, 2663 rpm, 57°C], 28.728388 MH/s (102.13 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 2, S = 0, R = 0, I = 0], [00:00:56.944, 13 ms], [fan = 99%, 2623 rpm, 61°C], 29.190581 MH/s (103.11 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:01:26.942, 18 ms], [fan = 99%, 2715 rpm, 63°C], 29.005799 MH/s (103.68 W) = 348.614271 MH/s (1216.04 W)

<<< thread ID: 0x2768, 2021.08.01 13:50:41.857, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c76e7f","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2648, 2021.08.01 13:50:41.871, 1552 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:50:41.965, 93 ms
{"id":0,"jsonrpc":"2.0","result":["0x710e14206122a6bd078672b61ce0a0ed69561797e36b6c1ede8589b1f90237e7","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c0"]}

--- thread ID: 0xedc, 2021.08.01 13:50:41.965
epoch = 431 (next epoch in 20544 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:50:42.047, 82 ms
{"id":0,"jsonrpc":"2.0","result":["0x02db591780368c84e4d59fad7d975a6100caf1bfad47623453ab7224bad9110c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c0"]}

--- thread ID: 0x2628, 2021.08.01 13:50:42.047
epoch = 431 (next epoch in 20544 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:50:46.045, 3997 ms
{"id":0,"jsonrpc":"2.0","result":["0x59d2dd3a29066068c75e490afa7604a76fbca92b66003f2607d401012d7056e7","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c0"]}

--- thread ID: 0x1df0, 2021.08.01 13:50:46.045
epoch = 431 (next epoch in 20544 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:50:49.025, 2980 ms
{"id":0,"jsonrpc":"2.0","result":["0xd7901d4fcc7c5460c483a7f2e24bb07eff7e15bb5e3eb94724a3535b3294dc23","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c0"]}

--- thread ID: 0x18b4, 2021.08.01 13:50:49.025
epoch = 431 (next epoch in 20544 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:50:51.126, 2100 ms
{"id":0,"jsonrpc":"2.0","result":["0xd0b86063c4bf56f4d81e14991cd47ca97911e15317bc30aac8972c9d194007e4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c0"]}

--- thread ID: 0x2630, 2021.08.01 13:50:51.126
epoch = 431 (next epoch in 20544 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:50:55.048, 3922 ms
{"id":0,"jsonrpc":"2.0","result":["0x103414d1f74e612836baee37f8d9bfb988dde38647515ac6518db6db5a9798cf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c0"]}

--- thread ID: 0x24b4, 2021.08.01 13:50:55.048
epoch = 431 (next epoch in 20544 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:50:56.868, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:03:15.383)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:03:16.304, 18 ms], [fan = 99%, 2960 rpm, 52°C], 28.608702 MH/s ( 99.70 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:00:37.306, 37 ms], [fan = 99%, 2612 rpm, 60°C], 29.195493 MH/s ( 99.79 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:00:36.854,  5 ms], [fan = 99%, 2678 rpm, 61°C], 29.229541 MH/s (100.09 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:02:30.388, 23 ms], [fan = 99%, 2669 rpm, 60°C], 29.227530 MH/s (101.45 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:01:06.750, 20 ms], [fan = 99%, 3322 rpm, 63°C], 29.185257 MH/s ( 99.49 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:03:16.304, 37 ms], [fan = 99%, 3265 rpm, 58°C], 29.199629 MH/s (101.61 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:00:25.198, 47 ms], [fan = 99%, 2567 rpm, 62°C], 28.578721 MH/s (101.96 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:01:53.357, 49 ms], [fan = 99%, 2694 rpm, 56°C], 29.006622 MH/s (101.29 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:03:16.304,  5 ms], [fan = 99%, 2649 rpm, 60°C], 29.184398 MH/s (102.59 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:02:10.475, 47 ms], [fan = 99%, 2651 rpm, 58°C], 28.734851 MH/s (101.32 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 2, S = 0, R = 0, I = 0], [00:01:11.960, 42 ms], [fan = 99%, 2630 rpm, 62°C], 29.168985 MH/s (102.15 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:01:41.958, 11 ms], [fan = 99%, 2715 rpm, 63°C], 28.940102 MH/s (103.96 W) = 348.259831 MH/s (1215.42 W)

<<< thread ID: 0x2610, 2021.08.01 13:50:56.872, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c205f7","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2768, 2021.08.01 13:50:56.888, 1839 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:50:59.071, 2183 ms
{"id":0,"jsonrpc":"2.0","result":["0x47840feb754be4acbe73fbf245d942411f3ff508cac1cebbbdcdee96fe615341","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c1"]}

--- thread ID: 0x2648, 2021.08.01 13:50:59.071
epoch = 431 (next epoch in 20543 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:50:59.172, 100 ms
{"id":0,"jsonrpc":"2.0","result":["0xbd2100ed59dc65ece673d8c6c3b2ce1ecb14d2afe42e967cae5a280606e01858","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c1"]}

--- thread ID: 0xedc, 2021.08.01 13:50:59.172
epoch = 431 (next epoch in 20543 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:51:02.127, 2955 ms
{"id":0,"jsonrpc":"2.0","result":["0x2be4d0a3b536a0c61e8305eaf0e558d164796131b5b7c5d54b58f8dae56fad8f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c1"]}

--- thread ID: 0x2628, 2021.08.01 13:51:02.128
epoch = 431 (next epoch in 20543 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:51:03.157, 1029 ms
{"id":0,"jsonrpc":"2.0","result":["0xbb60a6f3446d57eaf1675381d0043d62002370ab0840392dfc2065394c3401c5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c1"]}

--- thread ID: 0x1df0, 2021.08.01 13:51:03.157
epoch = 431 (next epoch in 20543 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:51:05.813, 2656 ms
{"id":0,"jsonrpc":"2.0","result":["0x0b274660781c51e3896b98692a3073239f6dd3308264958b6baae5ed5bd02193","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c2"]}

--- thread ID: 0x18b4, 2021.08.01 13:51:05.813
epoch = 431 (next epoch in 20542 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:51:05.934, 121 ms
{"id":0,"jsonrpc":"2.0","result":["0xf8cd71852b9db4a975df4ae573b37736dada42860a57d2eab1cc245c51d9c76a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c2"]}

--- thread ID: 0x2630, 2021.08.01 13:51:05.934
epoch = 431 (next epoch in 20542 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:51:09.024, 3089 ms
{"id":0,"jsonrpc":"2.0","result":["0x905f5855ef485136d15950cf0426092b7d4e9e4df3a15eaf460b50aa2828f7d3","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c2"]}

--- thread ID: 0x24b4, 2021.08.01 13:51:09.024
epoch = 431 (next epoch in 20542 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:51:09.108, 83 ms
{"id":0,"jsonrpc":"2.0","result":["0xe026fd64960ecc940ed616749532c59f9327c6bc1731dc3d6aa3f68d2146258b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c3"]}

--- thread ID: 0x2610, 2021.08.01 13:51:09.108
epoch = 431 (next epoch in 20541 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:51:09.407, 299 ms
{"id":0,"jsonrpc":"2.0","result":["0xabbee04c731bd3834f00731a32c000c8ee7e7b31bd7061f909eadb18745c9a7d","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c3"]}

--- thread ID: 0x2768, 2021.08.01 13:51:09.407
epoch = 431 (next epoch in 20541 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:51:11.244, 1836 ms
{"id":0,"jsonrpc":"2.0","result":["0x0522f2ea84f20b5f7e407a948cf6314b4eb930f43beb672cfb157d1ee1b1ed1d","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c3"]}

--- thread ID: 0x2648, 2021.08.01 13:51:11.244
epoch = 431 (next epoch in 20541 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:51:11.884, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:03:30.399)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:03:31.320, 31 ms], [fan = 99%, 2947 rpm, 52°C], 28.806263 MH/s (100.71 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:00:52.322, 11 ms], [fan = 99%, 2619 rpm, 61°C], 29.211005 MH/s ( 99.81 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:00:51.870, 56 ms], [fan = 99%, 2665 rpm, 61°C], 29.198097 MH/s (100.09 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:02:45.404,  8 ms], [fan = 99%, 2657 rpm, 60°C], 29.223088 MH/s (101.59 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:01:21.766,  0 ms], [fan = 99%, 3361 rpm, 63°C], 29.198663 MH/s ( 99.61 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 0, S = 0, R = 0, I = 0], [00:03:31.320, 12 ms], [fan = 99%, 3252 rpm, 58°C], 29.213287 MH/s (101.77 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:00:40.214, 27 ms], [fan = 99%, 2552 rpm, 63°C], 29.216047 MH/s (102.68 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:02:08.373, 31 ms], [fan = 99%, 2694 rpm, 57°C], 29.107375 MH/s (102.74 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:03:31.320, 56 ms], [fan = 99%, 2666 rpm, 60°C], 29.194566 MH/s (102.44 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:02:25.491, 30 ms], [fan = 99%, 2679 rpm, 58°C], 29.038485 MH/s (102.31 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 2, S = 0, R = 0, I = 0], [00:01:26.976,  8 ms], [fan = 99%, 2630 rpm, 62°C], 29.224010 MH/s (102.95 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:01:56.974, 21 ms], [fan = 99%, 2707 rpm, 63°C], 28.491975 MH/s (102.39 W) = 349.122861 MH/s (1219.09 W)

<<< thread ID: 0xedc, 2021.08.01 13:51:11.888, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014cf312d","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2628, 2021.08.01 13:51:11.904, 660 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 13:51:14.206, 2302 ms
{"id":0,"jsonrpc":"2.0","result":["0x55029126400878a821732d7ae793d4fcb08126eb9993ce48e8bfa0ecaab5f23a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c3"]}

--- thread ID: 0x1df0, 2021.08.01 13:51:14.206
epoch = 431 (next epoch in 20541 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:51:16.267, 2060 ms
{"id":0,"jsonrpc":"2.0","result":["0xcd3a60851b9a412fcf879d80a562a940140d9ff9a575474c098b714c7e753e77","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c3"]}

--- thread ID: 0x18b4, 2021.08.01 13:51:16.267
epoch = 431 (next epoch in 20541 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x10c4, 2021.08.01 13:51:18.709, PCIe: 00000000:02:00.0, GPU.06 share found (search channel 1).
 nonce: 0x13d0a82cefd5540e
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000a272c0f9a528fd3c1f09639e5fb1a5d74337f8af7ad194b375f6a60f
   mix: 0xf344744eab17a2c3331f9635c1573630ec4d0871c706d366e0128cbb46d3d6cc

<<< thread ID: 0x2630, 2021.08.01 13:51:18.710, 0 ms
{"jsonrpc":"2.0","id":1016,"method":"eth_submitWork","params":["0x13d0a82cefd5540e","0xcd3a60851b9a412fcf879d80a562a940140d9ff9a575474c098b714c7e753e77","0xf344744eab17a2c3331f9635c1573630ec4d0871c706d366e0128cbb46d3d6cc"],"worker":"alphagruis"}

--- thread ID: 0x24b4, 2021.08.01 13:51:18.725, PCIe: 00000000:02:00.0, GPU.06 share accepted.

>>> thread ID: 0x24b4, 2021.08.01 13:51:18.725, 2458 ms (15 ms)
{"id":1016,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:51:19.218, 493 ms
{"id":0,"jsonrpc":"2.0","result":["0xeac960c359138f7b207b5c15aca74596de08dd1a47cfcd0b5470bda395482b3a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c4"]}

--- thread ID: 0x2610, 2021.08.01 13:51:19.218
epoch = 431 (next epoch in 20540 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:51:19.463, 245 ms
{"id":0,"jsonrpc":"2.0","result":["0x921baacfd12a6b9ebc66db8a26b79b244f6cb25f45b4dd6e10168145a09b201a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c4"]}

--- thread ID: 0x2768, 2021.08.01 13:51:19.464
epoch = 431 (next epoch in 20540 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:51:20.366, 902 ms
{"id":0,"jsonrpc":"2.0","result":["0x5d2a217942f2c82bb714c7642e8d93095d0f6d4668594e796a620d26ebdd42e6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c4"]}

--- thread ID: 0x2648, 2021.08.01 13:51:20.366
epoch = 431 (next epoch in 20540 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:51:21.317, 951 ms
{"id":0,"jsonrpc":"2.0","result":["0x0f683d25d71c2c10f7575e0203bc4efa7bef80994c9d664aecc5cb99612d57f0","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c4"]}

--- thread ID: 0xedc, 2021.08.01 13:51:21.317
epoch = 431 (next epoch in 20540 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:51:22.321, 1004 ms
{"id":0,"jsonrpc":"2.0","result":["0xa65649faf4a4e7c3c237bea48b44fa301d322d41f5b50504ddf9821ad6d22431","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c4"]}

--- thread ID: 0x2628, 2021.08.01 13:51:22.321
epoch = 431 (next epoch in 20540 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:51:22.425, 103 ms
{"id":0,"jsonrpc":"2.0","result":["0xf79d8e1e52212aa0de956a68d07bd4dbfdd29bec1d4a83684b63d6672a07e913","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c5"]}

--- thread ID: 0x1df0, 2021.08.01 13:51:22.425
epoch = 431 (next epoch in 20539 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:51:22.604, 179 ms
{"id":0,"jsonrpc":"2.0","result":["0x5ad1cf072a2433ec1f2779ff2cb91ea30f80a547c5da3c673b29ff46bb336742","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c5"]}

--- thread ID: 0x18b4, 2021.08.01 13:51:22.604
epoch = 431 (next epoch in 20539 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:51:23.380, 776 ms
{"id":0,"jsonrpc":"2.0","result":["0xe24f8789153669f8e47735545e4210567ebf48eb965714916f2021e9ec365e18","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c5"]}

--- thread ID: 0x2630, 2021.08.01 13:51:23.380
epoch = 431 (next epoch in 20539 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:51:24.662, 1281 ms
{"id":0,"jsonrpc":"2.0","result":["0xa021e11c0648f1a4657a6d6ae95871ac0337beab0ef945173abc94d0a4914bca","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c5"]}

--- thread ID: 0x24b4, 2021.08.01 13:51:24.662
epoch = 431 (next epoch in 20539 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:51:25.693, 1030 ms
{"id":0,"jsonrpc":"2.0","result":["0x5c2b884b328ca3262a7a012b4ce58b54096bd6e479786404af7a6ffe702a1ee1","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c5"]}

--- thread ID: 0x2610, 2021.08.01 13:51:25.693
epoch = 431 (next epoch in 20539 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:51:26.897, 1203 ms
{"id":0,"jsonrpc":"2.0","result":["0x8537b1893950dd9061bd0d8addad103be1e42187b0a0501a60280bc3be79443e","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2768, 2021.08.01 13:51:26.897
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:51:26.915, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:03:45.430)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:03:46.351, 57 ms], [fan = 99%, 2924 rpm, 52°C], 28.800980 MH/s (100.77 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:01:07.353,  5 ms], [fan = 99%, 2615 rpm, 61°C], 29.197718 MH/s ( 99.89 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:01:06.901, 53 ms], [fan = 99%, 2677 rpm, 62°C], 29.193431 MH/s (100.03 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:03:00.435, 37 ms], [fan = 99%, 2665 rpm, 61°C], 29.184834 MH/s (101.44 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:01:36.797, 37 ms], [fan = 99%, 3354 rpm, 64°C], 29.226190 MH/s ( 99.34 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 1, S = 0, R = 0, I = 0], [00:00:08.206,  0 ms], [fan = 99%, 3262 rpm, 59°C], 29.215878 MH/s (101.58 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:00:55.245, 12 ms], [fan = 99%, 2571 rpm, 63°C], 29.222783 MH/s (102.87 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 1, S = 0, R = 0, I = 0], [00:02:23.404, 38 ms], [fan = 99%, 2685 rpm, 57°C], 28.788081 MH/s (101.00 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:03:46.351,  0 ms], [fan = 99%, 2657 rpm, 61°C], 28.637663 MH/s (101.51 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:02:40.522, 26 ms], [fan = 99%, 2658 rpm, 58°C], 29.197766 MH/s (101.81 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 2, S = 0, R = 0, I = 0], [00:01:42.007,  0 ms], [fan = 99%, 2645 rpm, 62°C], 29.201143 MH/s (103.15 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:02:12.005, 13 ms], [fan = 99%, 2710 rpm, 63°C], 28.392186 MH/s (102.81 W) = 348.258653 MH/s (1216.18 W)

<<< thread ID: 0x2648, 2021.08.01 13:51:26.921, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c2015d","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0xedc, 2021.08.01 13:51:26.936, 39 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:51:27.065, 128 ms
{"id":0,"jsonrpc":"2.0","result":["0x1d2ef667d605bf19ed9a460fc44ce116e10ac01b923b2d0fc5884e0dcad904b6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2628, 2021.08.01 13:51:27.065
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:51:28.930, 1865 ms
{"id":0,"jsonrpc":"2.0","result":["0x081766b6463e840d25b78d4d3a706789030213f8993ff4d24aa72720ec604fe8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x1df0, 2021.08.01 13:51:28.930
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0xf4c, 2021.08.01 13:51:29.221, PCIe: 00000000:0c:00.0, GPU.08 share found (search channel 0).
 nonce: 0x13d0a82dc9c5e1f1
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000001458884a7ab06432e0921eea2b349242fe85bb25896c847427600e19
   mix: 0xbf52f5a344248fb44772ab3dcf3072ce9f3fb1243234d84d9a83d75f1833acc4

<<< thread ID: 0x18b4, 2021.08.01 13:51:29.221, 0 ms
{"jsonrpc":"2.0","id":1017,"method":"eth_submitWork","params":["0x13d0a82dc9c5e1f1","0x081766b6463e840d25b78d4d3a706789030213f8993ff4d24aa72720ec604fe8","0xbf52f5a344248fb44772ab3dcf3072ce9f3fb1243234d84d9a83d75f1833acc4"],"worker":"alphagruis"}

--- thread ID: 0x2630, 2021.08.01 13:51:29.236, PCIe: 00000000:0c:00.0, GPU.08 share accepted.

>>> thread ID: 0x2630, 2021.08.01 13:51:29.236, 306 ms (15 ms)
{"id":1017,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:51:30.958, 1721 ms
{"id":0,"jsonrpc":"2.0","result":["0xf1ff2dd2c2e61e0cbf96d242afb54c7c91e1e90f3bec3167edd82267ef80fdfc","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x24b4, 2021.08.01 13:51:30.958
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:51:34.057, 3099 ms
{"id":0,"jsonrpc":"2.0","result":["0x8774ba6edcbaaada8847833229c15f9e6b19defaa4b4ede52eb16a8601f55a90","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2610, 2021.08.01 13:51:34.058
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:51:36.950, 2892 ms
{"id":0,"jsonrpc":"2.0","result":["0x87fcc6fa3f49a8af001d3ccbad38e8b913352bbd9974b0060d8887557244a9c5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2768, 2021.08.01 13:51:36.950
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x18c8, 2021.08.01 13:51:38.436, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 1).
 nonce: 0x13d0a82e88d1afbe
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000015ea2108d7354e9702f29c9901393cdd838e914c49c05bfd7691a2c9
   mix: 0x604a7bc4e026a849be7d16d685e8d2cc1e9c5f00042efbe0df5826e73c46d83d

<<< thread ID: 0x2648, 2021.08.01 13:51:38.436, 0 ms
{"jsonrpc":"2.0","id":1018,"method":"eth_submitWork","params":["0x13d0a82e88d1afbe","0x87fcc6fa3f49a8af001d3ccbad38e8b913352bbd9974b0060d8887557244a9c5","0x604a7bc4e026a849be7d16d685e8d2cc1e9c5f00042efbe0df5826e73c46d83d"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:51:38.451, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:51:38.451, 1500 ms (14 ms)
{"id":1018,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2170, 2021.08.01 13:51:41.930, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:04:00.445)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:04:01.366, 37 ms], [fan = 99%, 2950 rpm, 52°C], 28.865916 MH/s (100.94 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:01:22.368, 58 ms], [fan = 99%, 2608 rpm, 61°C], 29.186572 MH/s (100.07 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:01:21.916, 24 ms], [fan = 99%, 2673 rpm, 62°C], 29.223311 MH/s (100.15 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 2, S = 0, R = 0, I = 0], [00:03:15.450, 18 ms], [fan = 99%, 2665 rpm, 61°C], 29.193683 MH/s (101.60 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:01:51.812, 18 ms], [fan = 99%, 3353 rpm, 64°C], 29.092661 MH/s ( 99.63 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 1, S = 0, R = 0, I = 0], [00:00:23.221, 19 ms], [fan = 99%, 3253 rpm, 59°C], 29.214667 MH/s (102.10 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:01:10.260, 15 ms], [fan = 99%, 2544 rpm, 63°C], 29.204365 MH/s (103.12 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 2, S = 0, R = 0, I = 0], [00:00:12.709, 36 ms], [fan = 99%, 2689 rpm, 57°C], 28.827485 MH/s (102.74 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:04:01.366, 28 ms], [fan = 99%, 2657 rpm, 61°C], 29.222670 MH/s (102.73 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:02:55.537, 46 ms], [fan = 99%, 2674 rpm, 59°C], 28.720247 MH/s (101.69 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 3, S = 0, R = 0, I = 0], [00:00:03.494, 68 ms], [fan = 99%, 2641 rpm, 63°C], 28.785463 MH/s (102.53 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:02:27.020, 56 ms], [fan = 99%, 2706 rpm, 64°C], 28.326874 MH/s (102.37 W) = 347.863914 MH/s (1219.67 W)

<<< thread ID: 0x2628, 2021.08.01 13:51:41.934, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014bbfb6a","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x1df0, 2021.08.01 13:51:41.954, 3502 ms
{"id":0,"jsonrpc":"2.0","result":["0x5b1918740aa25899b11df836521d53007272aa9edbc8f745103a45cd44c8f5cf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x1df0, 2021.08.01 13:51:41.954
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:51:41.977, 23 ms (42 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2630, 2021.08.01 13:51:49.034, 7056 ms
{"id":0,"jsonrpc":"2.0","result":["0x1dab276c932e000001be9725324d7464bdbfe48d34e6a5e2479733b7ce3406a6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2630, 2021.08.01 13:51:49.034
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2fc, 2021.08.01 13:51:51.460, PCIe: 00000000:0e:00.0, GPU.04 share found (search channel 1).
 nonce: 0x13d0a82f978dd6b0
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000287a09ae415b1ceade2b4c5d95a3b39ab7b15b7bfd33f5b374b0c74b
   mix: 0xe04382009de573a4bf7c682832841bfb852c2c2559b502ea3829f8df21b0e9aa

<<< thread ID: 0x24b4, 2021.08.01 13:51:51.460, 0 ms
{"jsonrpc":"2.0","id":1019,"method":"eth_submitWork","params":["0x13d0a82f978dd6b0","0x1dab276c932e000001be9725324d7464bdbfe48d34e6a5e2479733b7ce3406a6","0xe04382009de573a4bf7c682832841bfb852c2c2559b502ea3829f8df21b0e9aa"],"worker":"alphagruis"}

--- thread ID: 0x2610, 2021.08.01 13:51:51.476, PCIe: 00000000:0e:00.0, GPU.04 share accepted.

>>> thread ID: 0x2610, 2021.08.01 13:51:51.476, 2441 ms (15 ms)
{"id":1019,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2768, 2021.08.01 13:51:56.229, 4753 ms
{"id":0,"jsonrpc":"2.0","result":["0x58008d3953f71c2a9026ba798db2ab7d450a0ee2526563f9d6b411c95d01ea5e","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2768, 2021.08.01 13:51:56.229
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:51:56.946, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:04:15.462)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:04:16.382, 11 ms], [fan = 99%, 2964 rpm, 52°C], 29.209087 MH/s (100.67 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:01:37.384, 41 ms], [fan = 99%, 2619 rpm, 62°C], 29.194015 MH/s ( 99.95 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:01:36.933,  0 ms], [fan = 99%, 2673 rpm, 63°C], 29.193150 MH/s (100.13 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:00:05.486, 19 ms], [fan = 99%, 2669 rpm, 61°C], 29.210478 MH/s (101.47 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 3, S = 0, R = 0, I = 0], [00:02:06.828, 11 ms], [fan = 99%, 3355 rpm, 64°C], 29.209506 MH/s ( 99.69 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 1, S = 0, R = 0, I = 0], [00:00:38.237,  0 ms], [fan = 99%, 3243 rpm, 59°C], 29.212961 MH/s (101.83 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:01:25.276, 36 ms], [fan = 99%, 2555 rpm, 64°C], 29.202836 MH/s (102.96 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 2, S = 0, R = 0, I = 0], [00:00:27.725,  0 ms], [fan = 99%, 2665 rpm, 57°C], 28.880444 MH/s (102.73 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:04:16.382,  0 ms], [fan = 99%, 2653 rpm, 61°C], 29.213017 MH/s (102.57 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:03:10.554,  0 ms], [fan = 99%, 2646 rpm, 59°C], 28.974462 MH/s (102.41 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 3, S = 0, R = 0, I = 0], [00:00:18.510,  9 ms], [fan = 99%, 2621 rpm, 63°C], 28.714129 MH/s (103.50 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:02:42.036,  2 ms], [fan = 99%, 2702 rpm, 64°C], 28.522093 MH/s (102.98 W) = 348.736178 MH/s (1220.92 W)

<<< thread ID: 0x2648, 2021.08.01 13:51:56.951, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c94ab2","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0xedc, 2021.08.01 13:51:56.966, 736 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:51:57.064, 97 ms
{"id":0,"jsonrpc":"2.0","result":["0x3def5b091b6e64cf9195a4528df200258ccd4431315230d7e893048d5a8241af","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2628, 2021.08.01 13:51:57.064
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x4e8, 2021.08.01 13:52:02.255, PCIe: 00000000:0d:00.0, GPU.05 share found (search channel 1).
 nonce: 0x13d0a830782758c9
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000003bd6b7b54d12728d20842c9de6dfebe4fdb3809e1fb30a34d000bf73
   mix: 0x64193b77f5d11882cdce35452fcf2d08c19ed6ea0fbdf29295136f417579fa44

<<< thread ID: 0x1df0, 2021.08.01 13:52:02.255, 0 ms
{"jsonrpc":"2.0","id":1020,"method":"eth_submitWork","params":["0x13d0a830782758c9","0x3def5b091b6e64cf9195a4528df200258ccd4431315230d7e893048d5a8241af","0x64193b77f5d11882cdce35452fcf2d08c19ed6ea0fbdf29295136f417579fa44"],"worker":"alphagruis"}

--- thread ID: 0x18b4, 2021.08.01 13:52:02.271, PCIe: 00000000:0d:00.0, GPU.05 share accepted.

>>> thread ID: 0x18b4, 2021.08.01 13:52:02.271, 5207 ms (16 ms)
{"id":1020,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2630, 2021.08.01 13:52:03.971, 1699 ms
{"id":0,"jsonrpc":"2.0","result":["0x7bf2ac1fd4b62843fe6833483a05f885999f5b6c941dc46380bfb8e6842fcc59","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x2630, 2021.08.01 13:52:03.971
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:52:11.965, 7993 ms
{"id":0,"jsonrpc":"2.0","result":["0xf3f3e927785f7c8f25f706f0c6bbd26ddce5a863a7bcf1c281e7e0f28e64c068","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c6"]}

--- thread ID: 0x24b4, 2021.08.01 13:52:11.965
epoch = 431 (next epoch in 20538 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:52:11.964, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:04:30.479)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:04:31.399, 60 ms], [fan = 99%, 2955 rpm, 52°C], 29.210234 MH/s (100.96 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:01:52.401, 16 ms], [fan = 99%, 2604 rpm, 62°C], 29.196356 MH/s ( 99.88 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 2, S = 0, R = 0, I = 0], [00:01:51.950, 52 ms], [fan = 99%, 2677 rpm, 63°C], 29.205665 MH/s (100.21 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:00:20.503, 46 ms], [fan = 99%, 2673 rpm, 62°C], 29.199596 MH/s (101.59 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:00:09.709, 66 ms], [fan = 99%, 3341 rpm, 65°C], 28.720616 MH/s ( 98.98 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 1, S = 0, R = 0, I = 0], [00:00:53.254, 56 ms], [fan = 99%, 3300 rpm, 60°C], 29.212790 MH/s (101.72 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:01:40.293,  5 ms], [fan = 99%, 2586 rpm, 64°C], 29.220713 MH/s (102.97 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 2, S = 0, R = 0, I = 0], [00:00:42.742, 44 ms], [fan = 99%, 2701 rpm, 58°C], 29.206566 MH/s (102.84 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:04:31.399,  0 ms], [fan = 99%, 2637 rpm, 62°C], 29.192979 MH/s (102.51 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:03:25.571, 46 ms], [fan = 99%, 2654 rpm, 59°C], 29.207370 MH/s (102.43 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 3, S = 0, R = 0, I = 0], [00:00:33.527, 57 ms], [fan = 99%, 2644 rpm, 64°C], 29.207287 MH/s (103.29 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:02:57.053, 27 ms], [fan = 99%, 2706 rpm, 64°C], 28.570089 MH/s (102.79 W) = 349.350261 MH/s (1220.18 W)

<<< thread ID: 0x2610, 2021.08.01 13:52:11.969, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014d2a975","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2768, 2021.08.01 13:52:12.008, 43 ms (38 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:52:13.150, 1141 ms
{"id":0,"jsonrpc":"2.0","result":["0x18dc3ced2b63f0313415ef8b1bfac660d581a938e7b0a3c73e335b7bf1ff7415","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c7"]}

--- thread ID: 0x2648, 2021.08.01 13:52:13.150
epoch = 431 (next epoch in 20537 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:52:13.248, 98 ms
{"id":0,"jsonrpc":"2.0","result":["0x146598262af832c872801a51c2389d54fa4ebd86114721ab9e3abd5249574ae6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c7"]}

--- thread ID: 0xedc, 2021.08.01 13:52:13.248
epoch = 431 (next epoch in 20537 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2ec, 2021.08.01 13:52:15.707, PCIe: 00000000:04:00.0, GPU.03 share found (search channel 1).
 nonce: 0x13d0a831902b2535
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000080ad298645afd4046b320276c337aed6fd0be2bf3aec5796348ef6b2
   mix: 0x0522f1ba61798876fc1cdf28dbb6795b4aa8e924eeb585d7ae934c3f13c33490

<<< thread ID: 0x2628, 2021.08.01 13:52:15.707, 0 ms
{"jsonrpc":"2.0","id":1021,"method":"eth_submitWork","params":["0x13d0a831902b2535","0x146598262af832c872801a51c2389d54fa4ebd86114721ab9e3abd5249574ae6","0x0522f1ba61798876fc1cdf28dbb6795b4aa8e924eeb585d7ae934c3f13c33490"],"worker":"alphagruis"}

--- thread ID: 0x1df0, 2021.08.01 13:52:15.723, PCIe: 00000000:04:00.0, GPU.03 share accepted.

>>> thread ID: 0x1df0, 2021.08.01 13:52:15.723, 2474 ms (15 ms)
{"id":1021,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:52:16.510, 787 ms
{"id":0,"jsonrpc":"2.0","result":["0x11de1cb9d0c79b9c888c2dab67818ac66bf17e8a2b51afdc4c336ac47ba1dd7c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c7"]}

--- thread ID: 0x18b4, 2021.08.01 13:52:16.510
epoch = 431 (next epoch in 20537 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:52:16.596, 85 ms
{"id":0,"jsonrpc":"2.0","result":["0x1947d71fd91a0961d3c0501e1132eee627e81e0f9d96bc933d2793c0382bf87b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c7"]}

--- thread ID: 0x2630, 2021.08.01 13:52:16.596
epoch = 431 (next epoch in 20537 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0xf4c, 2021.08.01 13:52:17.599, PCIe: 00000000:0c:00.0, GPU.08 share found (search channel 1).
 nonce: 0x13d0a831b80c4fcc
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000000526f3f5c04ecd05b9c435f1adbb483f35db0610c1d19280cc075fc1
   mix: 0x6f6395c1286dcb1e4b1259fb395cd9942e4302876650ab3d3fb83776111a7997

<<< thread ID: 0x24b4, 2021.08.01 13:52:17.599, 0 ms
{"jsonrpc":"2.0","id":1022,"method":"eth_submitWork","params":["0x13d0a831b80c4fcc","0x1947d71fd91a0961d3c0501e1132eee627e81e0f9d96bc933d2793c0382bf87b","0x6f6395c1286dcb1e4b1259fb395cd9942e4302876650ab3d3fb83776111a7997"],"worker":"alphagruis"}

--- thread ID: 0x2610, 2021.08.01 13:52:17.614, PCIe: 00000000:0c:00.0, GPU.08 share accepted.

>>> thread ID: 0x2610, 2021.08.01 13:52:17.614, 1018 ms (15 ms)
{"id":1022,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2768, 2021.08.01 13:52:18.599, 984 ms
{"id":0,"jsonrpc":"2.0","result":["0xfaed6c81451f6d2ff3d192dbe8bd15c7746046ecb2db43fd528c4427a2991ab8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c7"]}

--- thread ID: 0x2768, 2021.08.01 13:52:18.599
epoch = 431 (next epoch in 20537 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:52:19.340, 740 ms
{"id":0,"jsonrpc":"2.0","result":["0xf159cbc3876b69e775ab560d0f7460ebc6e0056e0b61f637e1c3f228ba095768","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c7"]}

--- thread ID: 0x2648, 2021.08.01 13:52:19.340
epoch = 431 (next epoch in 20537 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:52:20.498, 1158 ms
{"id":0,"jsonrpc":"2.0","result":["0xdc0613ab0da3dca53ba074953486b76e15b725ffa15980d0425538f70ab56641","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c8"]}

--- thread ID: 0xedc, 2021.08.01 13:52:20.498
epoch = 431 (next epoch in 20536 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:52:20.690, 192 ms
{"id":0,"jsonrpc":"2.0","result":["0xb54382edf54e2b4c1f8cf97333e84bda3cbe9539e6fbf3309735f8550e657218","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c8"]}

--- thread ID: 0x2628, 2021.08.01 13:52:20.690
epoch = 431 (next epoch in 20536 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:52:22.706, 2015 ms
{"id":0,"jsonrpc":"2.0","result":["0x5e17fa2d1531bd6b7eb0cc13eca8f4148fe988f62d28c6c072f406de6deaf31c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c8"]}

--- thread ID: 0x1df0, 2021.08.01 13:52:22.706
epoch = 431 (next epoch in 20536 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:52:24.569, 1863 ms
{"id":0,"jsonrpc":"2.0","result":["0x3ab089f297966adbc8e9171a147a7c63b28213cdf4b24a5fefcb608410f1bc35","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c8"]}

--- thread ID: 0x18b4, 2021.08.01 13:52:24.569
epoch = 431 (next epoch in 20536 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:52:26.993, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:04:45.509)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:04:46.429, 53 ms], [fan = 99%, 2937 rpm, 53°C], 29.198331 MH/s (100.86 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:02:07.431,  3 ms], [fan = 99%, 2608 rpm, 62°C], 29.189753 MH/s ( 99.89 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:00:11.286, 37 ms], [fan = 99%, 2680 rpm, 63°C], 29.208349 MH/s (100.28 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:00:35.533, 38 ms], [fan = 99%, 2693 rpm, 62°C], 29.202382 MH/s (101.76 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:00:24.738, 34 ms], [fan = 99%, 3342 rpm, 65°C], 29.181877 MH/s ( 99.77 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 1, S = 0, R = 0, I = 0], [00:01:08.284, 49 ms], [fan = 99%, 3284 rpm, 60°C], 29.192370 MH/s (101.84 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:01:55.323, 41 ms], [fan = 99%, 2551 rpm, 64°C], 29.197287 MH/s (103.13 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:00:09.394, 61 ms], [fan = 99%, 2693 rpm, 58°C], 29.026101 MH/s (102.72 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:04:46.429, 47 ms], [fan = 99%, 2645 rpm, 62°C], 29.203700 MH/s (102.62 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:03:40.600, 39 ms], [fan = 99%, 2662 rpm, 60°C], 29.203784 MH/s (101.82 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 3, S = 0, R = 0, I = 0], [00:00:48.557, 49 ms], [fan = 99%, 2621 rpm, 64°C], 29.194576 MH/s (103.36 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:03:12.083, 37 ms], [fan = 99%, 2706 rpm, 64°C], 28.386100 MH/s (103.10 W) = 349.384610 MH/s (1221.15 W)

<<< thread ID: 0x2630, 2021.08.01 13:52:26.998, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014d32fa2","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:52:27.013, 2444 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:52:28.579, 1565 ms
{"id":0,"jsonrpc":"2.0","result":["0x5226f69669dd9c7b57ae46577648408442474ab39e5fc4198d53e1b45fbec05b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c8"]}

--- thread ID: 0x2610, 2021.08.01 13:52:28.579
epoch = 431 (next epoch in 20536 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:52:31.179, 2600 ms
{"id":0,"jsonrpc":"2.0","result":["0x200a12462dddfe05f82293b824222e011fd5762eee8a39b092068a3da865bf8e","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c9"]}

--- thread ID: 0x2768, 2021.08.01 13:52:31.179
epoch = 431 (next epoch in 20535 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:52:31.441, 262 ms
{"id":0,"jsonrpc":"2.0","result":["0x4f054e0c8b0b5d8e38450cd63af3d7b42972810d363ecde909425bfa5aba59d0","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c9"]}

--- thread ID: 0x2648, 2021.08.01 13:52:31.442
epoch = 431 (next epoch in 20535 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:52:32.295, 853 ms
{"id":0,"jsonrpc":"2.0","result":["0x249978ddbc6b2516a303a75122764c8bd567734db64efd9bef4fc58bdefdee32","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570c9"]}

--- thread ID: 0xedc, 2021.08.01 13:52:32.295
epoch = 431 (next epoch in 20535 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:52:35.420, 3124 ms
{"id":0,"jsonrpc":"2.0","result":["0x0b02abc49323b43a4552c67a072573ba89dc8aed7bee976b6435b93b5e26c46c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ca"]}

--- thread ID: 0x2628, 2021.08.01 13:52:35.420
epoch = 431 (next epoch in 20534 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:52:35.529, 108 ms
{"id":0,"jsonrpc":"2.0","result":["0xd81f613341da4e816813fc409587a48bb57eabc384b5dc44f7b301a7ec36d1d0","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ca"]}

--- thread ID: 0x1df0, 2021.08.01 13:52:35.529
epoch = 431 (next epoch in 20534 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:52:37.385, 1856 ms
{"id":0,"jsonrpc":"2.0","result":["0xafe09c0c2fd9b9b4c1d35fedda35eecc6fcf16f2e29546b769172c0454f225b1","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cb"]}

--- thread ID: 0x18b4, 2021.08.01 13:52:37.385
epoch = 431 (next epoch in 20533 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:52:37.504, 118 ms
{"id":0,"jsonrpc":"2.0","result":["0x94f6b0cd144fb0a296f0e5daad424d9f062d9dbc4a26807eeed94698cd20a1cb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cb"]}

--- thread ID: 0x2630, 2021.08.01 13:52:37.504
epoch = 431 (next epoch in 20533 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:52:38.586, 1082 ms
{"id":0,"jsonrpc":"2.0","result":["0x0932c0619ed60e671dc787a51bd63fee54cf01cc417703950745a58a25e9a399","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cb"]}

--- thread ID: 0x24b4, 2021.08.01 13:52:38.586
epoch = 431 (next epoch in 20533 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:52:39.465, 878 ms
{"id":0,"jsonrpc":"2.0","result":["0x19f213035528931c4fcca3c37eb559716b38ff6d89752e080adbaecdb4609371","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cb"]}

--- thread ID: 0x2610, 2021.08.01 13:52:39.465
epoch = 431 (next epoch in 20533 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:52:42.009, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:05:00.524)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:05:01.444, 26 ms], [fan = 99%, 2916 rpm, 53°C], 28.641614 MH/s ( 99.46 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:02:22.446, 31 ms], [fan = 99%, 2608 rpm, 62°C], 29.197049 MH/s (100.05 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:00:26.301, 16 ms], [fan = 99%, 2676 rpm, 63°C], 29.203647 MH/s (100.34 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:00:50.548, 16 ms], [fan = 99%, 2672 rpm, 62°C], 29.200555 MH/s (101.75 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:00:39.754,  6 ms], [fan = 99%, 3324 rpm, 65°C], 29.204708 MH/s ( 99.85 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 1, S = 0, R = 0, I = 0], [00:01:23.299, 23 ms], [fan = 99%, 3254 rpm, 60°C], 28.917194 MH/s (100.44 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:02:10.338, 25 ms], [fan = 99%, 2547 rpm, 65°C], 29.218321 MH/s (103.08 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:00:24.410, 23 ms], [fan = 99%, 2685 rpm, 58°C], 29.151680 MH/s (102.96 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 0, S = 0, R = 0, I = 0], [00:05:01.444, 23 ms], [fan = 99%, 2657 rpm, 62°C], 29.201358 MH/s (102.65 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:03:55.616, 26 ms], [fan = 99%, 2646 rpm, 60°C], 28.756628 MH/s (101.16 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 3, S = 0, R = 0, I = 0], [00:01:03.573, 36 ms], [fan = 99%, 2648 rpm, 64°C], 28.972278 MH/s (103.47 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:03:27.098, 66 ms], [fan = 99%, 2706 rpm, 65°C], 28.181064 MH/s (102.09 W) = 347.846096 MH/s (1217.30 W)

<<< thread ID: 0x2768, 2021.08.01 13:52:42.013, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014bbb5d0","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2648, 2021.08.01 13:52:42.029, 2564 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:52:43.672, 1642 ms
{"id":0,"jsonrpc":"2.0","result":["0x7edaa0dd1a22c909dde90bae73278eda7135e95306b9e3fa13e2822561cbd2e5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cb"]}

--- thread ID: 0xedc, 2021.08.01 13:52:43.672
epoch = 431 (next epoch in 20533 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2420, 2021.08.01 13:52:45.857, PCIe: 00000000:06:00.0, GPU.09 share found (search channel 1).
 nonce: 0x13d0a8340291caa7
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000b416102f098b33a015a4f30bdc1ff2cdff73f6ba615cd563b8d363ac
   mix: 0x8e54fa10b2b6e4326b19b4311d485f6e6be0423fa9553df6748651b385200d87

<<< thread ID: 0x2628, 2021.08.01 13:52:45.857, 0 ms
{"jsonrpc":"2.0","id":1023,"method":"eth_submitWork","params":["0x13d0a8340291caa7","0x7edaa0dd1a22c909dde90bae73278eda7135e95306b9e3fa13e2822561cbd2e5","0x8e54fa10b2b6e4326b19b4311d485f6e6be0423fa9553df6748651b385200d87"],"worker":"alphagruis"}

--- thread ID: 0x1df0, 2021.08.01 13:52:45.873, PCIe: 00000000:06:00.0, GPU.09 share accepted.

>>> thread ID: 0x1df0, 2021.08.01 13:52:45.873, 2201 ms (16 ms)
{"id":1023,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:52:47.634, 1760 ms
{"id":0,"jsonrpc":"2.0","result":["0x389c147b1fc81ad24af348957cffce780ef2ac0173a41d8bac8d2444ad917988","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cb"]}

--- thread ID: 0x18b4, 2021.08.01 13:52:47.634
epoch = 431 (next epoch in 20533 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:52:57.030, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:05:15.545)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:05:16.466, 49 ms], [fan = 99%, 2947 rpm, 53°C], 29.184846 MH/s ( 99.61 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:02:37.467,  7 ms], [fan = 99%, 2615 rpm, 63°C], 29.013989 MH/s (100.02 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:00:41.323,  3 ms], [fan = 99%, 2676 rpm, 64°C], 29.196152 MH/s (100.21 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:01:05.570,  5 ms], [fan = 99%, 2676 rpm, 62°C], 29.193294 MH/s (101.55 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:00:54.775,  3 ms], [fan = 99%, 3340 rpm, 66°C], 29.201862 MH/s ( 99.67 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 1, S = 0, R = 0, I = 0], [00:01:38.320, 67 ms], [fan = 99%, 3297 rpm, 61°C], 28.705909 MH/s (101.02 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:02:25.360, 12 ms], [fan = 99%, 2551 rpm, 65°C], 29.088734 MH/s (103.04 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:00:39.431,  2 ms], [fan = 99%, 2673 rpm, 58°C], 29.207652 MH/s (103.08 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:00:11.173, 30 ms], [fan = 99%, 2657 rpm, 62°C], 28.686662 MH/s (101.82 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:04:10.637, 58 ms], [fan = 99%, 2657 rpm, 60°C], 28.988326 MH/s (102.64 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 3, S = 0, R = 0, I = 0], [00:01:18.594,  4 ms], [fan = 99%, 2620 rpm, 64°C], 29.214099 MH/s (103.35 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:03:42.119, 59 ms], [fan = 99%, 2706 rpm, 65°C], 28.087795 MH/s (102.87 W) = 347.769320 MH/s (1218.88 W)

<<< thread ID: 0x2630, 2021.08.01 13:52:57.034, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014ba89e8","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:52:57.050, 9416 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0x10c4, 2021.08.01 13:53:00.623, PCIe: 00000000:02:00.0, GPU.06 share found (search channel 1).
 nonce: 0x13d0a83534a53a0d
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000ffad9c6a72af179114824bb040a1082f60e3c3e8f924d64172074f07
   mix: 0xd3422bb003134b6c8ebd44aafc8e74ce37cbcebaf0bf5a1c384222b0cf5e79d9

<<< thread ID: 0x2610, 2021.08.01 13:53:00.623, 0 ms
{"jsonrpc":"2.0","id":1024,"method":"eth_submitWork","params":["0x13d0a83534a53a0d","0x389c147b1fc81ad24af348957cffce780ef2ac0173a41d8bac8d2444ad917988","0xd3422bb003134b6c8ebd44aafc8e74ce37cbcebaf0bf5a1c384222b0cf5e79d9"],"worker":"alphagruis"}

--- thread ID: 0x2768, 2021.08.01 13:53:00.640, PCIe: 00000000:02:00.0, GPU.06 share accepted.

>>> thread ID: 0x2768, 2021.08.01 13:53:00.640, 3589 ms (16 ms)
{"id":1024,"jsonrpc":"2.0","result":true}

--- thread ID: 0x18c8, 2021.08.01 13:53:06.737, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 1).
 nonce: 0x13d0a835b35e3089
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000004d36ce8abedccfd424bf24f2893f0a62ccde9d4a3eaddfb6659c3bfb
   mix: 0x7b90dec9bc2662f2a252ad515c9d0b412695cb917cd95b6dd35a69a1619da377

<<< thread ID: 0x2648, 2021.08.01 13:53:06.738, 0 ms
{"jsonrpc":"2.0","id":1025,"method":"eth_submitWork","params":["0x13d0a835b35e3089","0x389c147b1fc81ad24af348957cffce780ef2ac0173a41d8bac8d2444ad917988","0x7b90dec9bc2662f2a252ad515c9d0b412695cb917cd95b6dd35a69a1619da377"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:53:06.756, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:53:06.756, 6115 ms (18 ms)
{"id":1025,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:53:09.990, 3234 ms
{"id":0,"jsonrpc":"2.0","result":["0x99f3cdb08ff5016684956d181a1494ed65a8bc44517373196f71ce233517a40b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cc"]}

--- thread ID: 0x2628, 2021.08.01 13:53:09.990
epoch = 431 (next epoch in 20532 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:53:10.073, 83 ms
{"id":0,"jsonrpc":"2.0","result":["0x3906c750576411525013bb4f3fb0ba938b9d1a1787488e5ff41c832a8ab1b8e6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cc"]}

--- thread ID: 0x1df0, 2021.08.01 13:53:10.074
epoch = 431 (next epoch in 20532 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:53:12.040, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:05:30.555)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:05:31.476, 34 ms], [fan = 99%, 2957 rpm, 52°C], 28.675875 MH/s ( 99.98 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:02:52.477, 17 ms], [fan = 99%, 2619 rpm, 63°C], 28.771282 MH/s ( 98.90 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:00:56.333, 53 ms], [fan = 99%, 2676 rpm, 64°C], 29.188460 MH/s (100.36 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:01:20.580, 51 ms], [fan = 99%, 2672 rpm, 63°C], 29.194718 MH/s (101.77 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:01:09.785, 19 ms], [fan = 99%, 3360 rpm, 66°C], 29.210685 MH/s (100.11 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 2, S = 0, R = 0, I = 0], [00:00:11.417,  0 ms], [fan = 99%, 3252 rpm, 61°C], 29.204684 MH/s (101.62 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:02:40.370, 15 ms], [fan = 99%, 2555 rpm, 65°C], 28.809101 MH/s (101.78 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:00:54.441,  3 ms], [fan = 99%, 2688 rpm, 58°C], 28.813632 MH/s (101.81 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:00:26.183,  0 ms], [fan = 99%, 2653 rpm, 63°C], 29.185956 MH/s (102.65 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:04:25.647, 13 ms], [fan = 99%, 2649 rpm, 60°C], 28.759281 MH/s (101.20 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 4, S = 0, R = 0, I = 0], [00:00:05.302, 50 ms], [fan = 99%, 2640 rpm, 65°C], 29.192440 MH/s (103.38 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:03:57.129, 65 ms], [fan = 99%, 2714 rpm, 65°C], 28.231655 MH/s (102.45 W) = 347.237769 MH/s (1216.00 W)

<<< thread ID: 0x18b4, 2021.08.01 13:53:12.044, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b26d89","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:53:12.059, 1985 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:53:13.810, 1750 ms
{"id":0,"jsonrpc":"2.0","result":["0x97d238c9852c8b74e91a30eb0bd211e0d704f11f74daf3755d2051849fef4ff6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cc"]}

--- thread ID: 0x24b4, 2021.08.01 13:53:13.810
epoch = 431 (next epoch in 20532 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x18c8, 2021.08.01 13:53:14.290, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 0).
 nonce: 0x13d0a8364f3a8606
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000744ebe4f16f25dc23d5b4179a8653ea50ee70e3eaad833cfa52a86f1
   mix: 0x8d3961d3e6c1041590fe429f4cb564f1a487e401cba3d951febfb184360d3eca

<<< thread ID: 0x2610, 2021.08.01 13:53:14.290, 0 ms
{"jsonrpc":"2.0","id":1026,"method":"eth_submitWork","params":["0x13d0a8364f3a8606","0x97d238c9852c8b74e91a30eb0bd211e0d704f11f74daf3755d2051849fef4ff6","0x8d3961d3e6c1041590fe429f4cb564f1a487e401cba3d951febfb184360d3eca"],"worker":"alphagruis"}

--- thread ID: 0x2768, 2021.08.01 13:53:14.313, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0x2768, 2021.08.01 13:53:14.313, 503 ms (23 ms)
{"id":1026,"jsonrpc":"2.0","result":true}

--- thread ID: 0x25d8, 2021.08.01 13:53:18.595, PCIe: 00000000:0a:00.0, GPU.02 share found (search channel 0).
 nonce: 0x13d0a836a8334ec6
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000d1d089c0fa906a93048a37a661b7132d091881f190c8652809cd2918
   mix: 0x55213a83634427718215ef9ffb337a6d707e54c12fdd2919eeb3c12505e18add

<<< thread ID: 0x2648, 2021.08.01 13:53:18.595, 0 ms
{"jsonrpc":"2.0","id":1027,"method":"eth_submitWork","params":["0x13d0a836a8334ec6","0x97d238c9852c8b74e91a30eb0bd211e0d704f11f74daf3755d2051849fef4ff6","0x55213a83634427718215ef9ffb337a6d707e54c12fdd2919eeb3c12505e18add"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:53:18.610, PCIe: 00000000:0a:00.0, GPU.02 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:53:18.610, 4296 ms (15 ms)
{"id":1027,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:53:22.076, 3466 ms
{"id":0,"jsonrpc":"2.0","result":["0xabde683fb93ac5638079a4bae74235b1dccec0d48a7a88ab77c461601bf01e25","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cc"]}

--- thread ID: 0x2628, 2021.08.01 13:53:22.076
epoch = 431 (next epoch in 20532 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:53:24.094, 2017 ms
{"id":0,"jsonrpc":"2.0","result":["0x9f42d0866624c7af4042712f737a41b46a2b57d53db7992cfa28bd1c471e91a4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cc"]}

--- thread ID: 0x1df0, 2021.08.01 13:53:24.094
epoch = 431 (next epoch in 20532 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:53:26.065, 1970 ms
{"id":0,"jsonrpc":"2.0","result":["0x2ac19698958512ed2aa8f68a8763968fd0e9baa9a3500d823dcf1803c2471027","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cc"]}

--- thread ID: 0x18b4, 2021.08.01 13:53:26.065
epoch = 431 (next epoch in 20532 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:53:27.056, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:05:45.571)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:05:46.491, 11 ms], [fan = 99%, 2939 rpm, 52°C], 28.650459 MH/s ( 99.99 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:00:08.461, 65 ms], [fan = 99%, 2611 rpm, 63°C], 28.791687 MH/s ( 99.81 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:01:11.349, 21 ms], [fan = 99%, 2676 rpm, 64°C], 29.198001 MH/s (100.39 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:01:35.595, 42 ms], [fan = 99%, 2672 rpm, 63°C], 28.695035 MH/s (101.39 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:01:24.801, 29 ms], [fan = 99%, 3347 rpm, 66°C], 29.199540 MH/s (100.12 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 2, S = 0, R = 0, I = 0], [00:00:26.433, 47 ms], [fan = 99%, 3297 rpm, 61°C], 29.207002 MH/s (101.60 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:02:55.386, 56 ms], [fan = 99%, 2566 rpm, 65°C], 28.602707 MH/s (102.25 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:01:09.457, 55 ms], [fan = 99%, 2688 rpm, 58°C], 28.629112 MH/s (102.36 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:00:41.199, 44 ms], [fan = 99%, 2644 rpm, 63°C], 29.207274 MH/s (102.70 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 1, S = 0, R = 0, I = 0], [00:04:40.663, 44 ms], [fan = 99%, 2661 rpm, 60°C], 28.752137 MH/s (102.17 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:00:12.766, 56 ms], [fan = 99%, 2624 rpm, 65°C], 28.754021 MH/s (102.78 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:04:12.145, 44 ms], [fan = 99%, 2702 rpm, 65°C], 27.949181 MH/s (101.96 W) = 345.636156 MH/s (1217.54 W)

<<< thread ID: 0x2630, 2021.08.01 13:53:27.060, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x000000000000000000000000000000000000000000000000000000001499fd3c","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:53:27.075, 1010 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:53:29.157, 2081 ms
{"id":0,"jsonrpc":"2.0","result":["0x0a06dc8a86de66bfac52f2a6f88243d9f599fc10f7780df27b291dbc01a11aac","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cc"]}

--- thread ID: 0x2610, 2021.08.01 13:53:29.157
epoch = 431 (next epoch in 20532 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x23a0, 2021.08.01 13:53:30.222, PCIe: 00000000:01:00.0, GPU.10 share found (search channel 1).
 nonce: 0x13d0a83797d8d202
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000aa17305df153b6c1f6ecb298e894d2228fe110f79c0dc5c3833cad4a
   mix: 0x278d3c7f6b5948cd256e21c58f897866ae11641f4a800041a4eb755bca03f830

<<< thread ID: 0x2768, 2021.08.01 13:53:30.222, 0 ms
{"jsonrpc":"2.0","id":1028,"method":"eth_submitWork","params":["0x13d0a83797d8d202","0x0a06dc8a86de66bfac52f2a6f88243d9f599fc10f7780df27b291dbc01a11aac","0x278d3c7f6b5948cd256e21c58f897866ae11641f4a800041a4eb755bca03f830"],"worker":"alphagruis"}

--- thread ID: 0x2648, 2021.08.01 13:53:30.252, PCIe: 00000000:01:00.0, GPU.10 share accepted.

>>> thread ID: 0x2648, 2021.08.01 13:53:30.252, 1095 ms (30 ms)
{"id":1028,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:53:38.394, 8141 ms
{"id":0,"jsonrpc":"2.0","result":["0xb3270068e0cd7f85d230441ec7beec883252480c4c421f524747cc7309afdff4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cd"]}

--- thread ID: 0xedc, 2021.08.01 13:53:38.394
epoch = 431 (next epoch in 20531 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:53:38.630, 236 ms
{"id":0,"jsonrpc":"2.0","result":["0xc2b13cea54b4131d6c0d20f72d2522a9ec9719ddf50fc9133a50d5da83392828","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cd"]}

--- thread ID: 0x2628, 2021.08.01 13:53:38.630
epoch = 431 (next epoch in 20531 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:53:42.071, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:06:00.586)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:06:01.507, 25 ms], [fan = 99%, 2935 rpm, 53°C], 29.190173 MH/s (100.91 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:00:23.476, 10 ms], [fan = 99%, 2623 rpm, 63°C], 28.893545 MH/s ( 98.80 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:01:26.364, 47 ms], [fan = 99%, 2671 rpm, 64°C], 29.139683 MH/s ( 99.56 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:01:50.611, 68 ms], [fan = 99%, 2664 rpm, 63°C], 29.035086 MH/s (102.00 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:01:39.816,  6 ms], [fan = 99%, 3348 rpm, 66°C], 29.201976 MH/s (100.01 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 2, S = 0, R = 0, I = 0], [00:00:41.448, 20 ms], [fan = 99%, 3273 rpm, 61°C], 29.216895 MH/s (101.78 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:03:10.401,  0 ms], [fan = 99%, 2551 rpm, 66°C], 28.978276 MH/s (102.04 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:01:24.472, 68 ms], [fan = 99%, 2661 rpm, 58°C], 28.962352 MH/s (102.96 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:00:56.214, 16 ms], [fan = 99%, 2648 rpm, 63°C], 29.216496 MH/s (102.91 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 2, S = 0, R = 0, I = 0], [00:00:11.849, 39 ms], [fan = 99%, 2665 rpm, 60°C], 28.733893 MH/s (101.42 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:00:27.781,  0 ms], [fan = 99%, 2635 rpm, 65°C], 29.212668 MH/s (103.41 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:04:27.160, 51 ms], [fan = 99%, 2706 rpm, 66°C], 28.058537 MH/s (102.02 W) = 347.839580 MH/s (1217.82 W)

<<< thread ID: 0x1df0, 2021.08.01 13:53:42.076, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014bb9c5c","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x18b4, 2021.08.01 13:53:42.092, 3462 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2630, 2021.08.01 13:53:42.375, 282 ms
{"id":0,"jsonrpc":"2.0","result":["0x7c7c35d413f30cc972c4f9742b6cacc25e6b31c742d9706f2644d1a94d10a013","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cd"]}

--- thread ID: 0x2630, 2021.08.01 13:53:42.375
epoch = 431 (next epoch in 20531 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x23a0, 2021.08.01 13:53:45.421, PCIe: 00000000:01:00.0, GPU.10 share found (search channel 1).
 nonce: 0x13d0a838d2ccdda2
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000006777711aced00f22255896af5bd867756c5c5685b30a564d3db4a38d
   mix: 0x1c847c76bc9ec3cf60dcfad332c143042936ce08ea999d3ea04e6f160e345c5a

<<< thread ID: 0x24b4, 2021.08.01 13:53:45.421, 0 ms
{"jsonrpc":"2.0","id":1029,"method":"eth_submitWork","params":["0x13d0a838d2ccdda2","0x7c7c35d413f30cc972c4f9742b6cacc25e6b31c742d9706f2644d1a94d10a013","0x1c847c76bc9ec3cf60dcfad332c143042936ce08ea999d3ea04e6f160e345c5a"],"worker":"alphagruis"}

--- thread ID: 0x2610, 2021.08.01 13:53:45.436, PCIe: 00000000:01:00.0, GPU.10 share accepted.

>>> thread ID: 0x2610, 2021.08.01 13:53:45.436, 3061 ms (15 ms)
{"id":1029,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2768, 2021.08.01 13:53:47.686, 2249 ms
{"id":0,"jsonrpc":"2.0","result":["0x61dbdaa8645092846ae24a802f57c300acca83003e0eee22491077e9bb366bed","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ce"]}

--- thread ID: 0x2768, 2021.08.01 13:53:47.686
epoch = 431 (next epoch in 20530 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:53:47.758, 71 ms
{"id":0,"jsonrpc":"2.0","result":["0x8b9b57c52020e2cee43b43c66e8279b81545349d20df84b8b9656e33dbd09ea1","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ce"]}

--- thread ID: 0x2648, 2021.08.01 13:53:47.758
epoch = 431 (next epoch in 20530 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:53:50.866, 3108 ms
{"id":0,"jsonrpc":"2.0","result":["0x0706bd0a5b7a030eb461b04ae636f745f0bb6bcdda1084970f63a39f066ba4cf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ce"]}

--- thread ID: 0xedc, 2021.08.01 13:53:50.866
epoch = 431 (next epoch in 20530 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:53:53.761, 2894 ms
{"id":0,"jsonrpc":"2.0","result":["0x5d7a7b002540f6774451322c80748f6fa7e0d5dc282702b15139926439eff5ba","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ce"]}

--- thread ID: 0x2628, 2021.08.01 13:53:53.761
epoch = 431 (next epoch in 20530 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:53:55.776, 2014 ms
{"id":0,"jsonrpc":"2.0","result":["0x01b942e6c65efe837bf8cf09a275fd116c7fecf0265219bc50e0efae27634a1a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ce"]}

--- thread ID: 0x1df0, 2021.08.01 13:53:55.776
epoch = 431 (next epoch in 20530 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:53:56.779, 1002 ms
{"id":0,"jsonrpc":"2.0","result":["0x58efcf3dd44bb177be40e78ee6cbe86b868c74c87a6ec8d890bd16274bac5425","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ce"]}

--- thread ID: 0x18b4, 2021.08.01 13:53:56.779
epoch = 431 (next epoch in 20530 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:53:57.072, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:06:15.587)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:06:16.507, 62 ms], [fan = 99%, 2970 rpm, 53°C], 29.178401 MH/s (100.94 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:00:38.477, 58 ms], [fan = 99%, 2607 rpm, 63°C], 28.758273 MH/s ( 99.81 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:01:41.364, 22 ms], [fan = 99%, 2659 rpm, 65°C], 29.201657 MH/s (100.43 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:02:05.611,  8 ms], [fan = 99%, 2668 rpm, 63°C], 29.226380 MH/s (101.82 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:01:54.817,  9 ms], [fan = 99%, 3329 rpm, 66°C], 29.173299 MH/s ( 99.86 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 2, S = 0, R = 0, I = 0], [00:00:56.448, 61 ms], [fan = 99%, 3266 rpm, 61°C], 29.182252 MH/s (101.95 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:03:25.401, 59 ms], [fan = 99%, 2551 rpm, 66°C], 28.749724 MH/s (103.32 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:01:39.473, 48 ms], [fan = 99%, 2668 rpm, 59°C], 29.012697 MH/s (102.89 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:01:11.214,  8 ms], [fan = 99%, 2652 rpm, 63°C], 29.226904 MH/s (102.89 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:00:11.651,  5 ms], [fan = 99%, 2645 rpm, 61°C], 29.212670 MH/s (102.61 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:00:42.782, 27 ms], [fan = 99%, 2631 rpm, 65°C], 29.196646 MH/s (103.41 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:04:42.161, 20 ms], [fan = 99%, 2701 rpm, 66°C], 27.805232 MH/s (101.95 W) = 347.924135 MH/s (1221.86 W)

<<< thread ID: 0x2630, 2021.08.01 13:53:57.076, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014bce6a7","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:53:57.092, 312 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:54:01.815, 4723 ms
{"id":0,"jsonrpc":"2.0","result":["0x797ed502051158e769a93248ef7600696327fcd625b80bfbd553546304d31d84","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cf"]}

--- thread ID: 0x2610, 2021.08.01 13:54:01.815
epoch = 431 (next epoch in 20529 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:54:01.863, 47 ms
{"id":0,"jsonrpc":"2.0","result":["0x8a65e296ff731d64ad74a0fb704e4128e062a588a7d6613385c3f2ccdbd18ebb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ce"]}

--- thread ID: 0x2768, 2021.08.01 13:54:01.863
epoch = 431 (next epoch in 20530 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:54:01.905, 42 ms
{"id":0,"jsonrpc":"2.0","result":["0x2b3a3961fa5832df3f572dec6f5eae2acc1c03965a46bbbf104636c9e2ae2f93","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cf"]}

--- thread ID: 0x2648, 2021.08.01 13:54:01.905
epoch = 431 (next epoch in 20529 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:54:06.035, 4129 ms
{"id":0,"jsonrpc":"2.0","result":["0xbe68da7d53c071c07ef4d3775d038248b4fe48818bd28a444cf98f71a4631bfb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570cf"]}

--- thread ID: 0xedc, 2021.08.01 13:54:06.035
epoch = 431 (next epoch in 20529 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:54:07.418, 1383 ms
{"id":0,"jsonrpc":"2.0","result":["0xabbb4a8d659de2516336937604a478ae64eb932f6f21bca9c2662955f9f9306c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0x2628, 2021.08.01 13:54:07.418
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:54:07.513, 94 ms
{"id":0,"jsonrpc":"2.0","result":["0x21f415936c5ea408960c6b8ae37357f1446cab63bc1e049402b36610996f3fd2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0x1df0, 2021.08.01 13:54:07.513
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:54:11.650, 4136 ms
{"id":0,"jsonrpc":"2.0","result":["0x24d00e42f5048db863ab375cbb83ca2cb23a31efcb97e63120b86b9e389a8e0a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0x18b4, 2021.08.01 13:54:11.650
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:54:12.087, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:06:30.603)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:06:31.523, 38 ms], [fan = 99%, 2955 rpm, 53°C], 28.735436 MH/s (100.94 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:00:53.492, 32 ms], [fan = 99%, 2611 rpm, 63°C], 29.191699 MH/s ( 99.99 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:01:56.380,  0 ms], [fan = 99%, 2667 rpm, 65°C], 29.199006 MH/s (100.21 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:02:20.627, 46 ms], [fan = 99%, 2672 rpm, 64°C], 29.187390 MH/s (101.87 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:02:09.832,  3 ms], [fan = 99%, 3352 rpm, 66°C], 29.193398 MH/s ( 99.96 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 2, S = 0, R = 0, I = 0], [00:01:11.464, 36 ms], [fan = 99%, 3293 rpm, 61°C], 28.660239 MH/s (101.27 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:03:40.417, 21 ms], [fan = 99%, 2555 rpm, 66°C], 28.734611 MH/s (103.31 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 3, S = 0, R = 0, I = 0], [00:01:54.488, 17 ms], [fan = 99%, 2684 rpm, 59°C], 29.217670 MH/s (103.01 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:01:26.230, 12 ms], [fan = 99%, 2644 rpm, 63°C], 29.204628 MH/s (102.85 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:00:26.667, 44 ms], [fan = 99%, 2641 rpm, 61°C], 28.928893 MH/s (101.51 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:00:57.798, 29 ms], [fan = 99%, 2624 rpm, 65°C], 29.033076 MH/s (102.95 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:04:57.177, 60 ms], [fan = 99%, 2702 rpm, 66°C], 28.003221 MH/s (102.24 W) = 347.289267 MH/s (1220.12 W)

<<< thread ID: 0x2630, 2021.08.01 13:54:12.092, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b336b3","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:54:12.106, 456 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:54:13.568, 1462 ms
{"id":0,"jsonrpc":"2.0","result":["0x1a8e05eaab0d386ddaa5f750e92d46b476bb126f0ac7637e1f7b2e5a68a3dffd","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0x2610, 2021.08.01 13:54:13.568
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0xf4c, 2021.08.01 13:54:14.950, PCIe: 00000000:0c:00.0, GPU.08 share found (search channel 0).
 nonce: 0x13d0a83b369c562d
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000857805f0168ab35fc838305932b20972ad26d67197a07d4d31da3140
   mix: 0xf469474d27c08ba493e40370f5803218dc3526432d65cb2c56afae73938da1fa

<<< thread ID: 0x2768, 2021.08.01 13:54:14.950, 0 ms
{"jsonrpc":"2.0","id":1030,"method":"eth_submitWork","params":["0x13d0a83b369c562d","0x1a8e05eaab0d386ddaa5f750e92d46b476bb126f0ac7637e1f7b2e5a68a3dffd","0xf469474d27c08ba493e40370f5803218dc3526432d65cb2c56afae73938da1fa"],"worker":"alphagruis"}

--- thread ID: 0x2648, 2021.08.01 13:54:14.966, PCIe: 00000000:0c:00.0, GPU.08 share accepted.

>>> thread ID: 0x2648, 2021.08.01 13:54:14.966, 1397 ms (15 ms)
{"id":1030,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:54:16.548, 1582 ms
{"id":0,"jsonrpc":"2.0","result":["0xc1727bbfe3348e451a585c1f193e00f91f68e8aac76ad60fbeb269396a031d10","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0xedc, 2021.08.01 13:54:16.548
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:54:19.601, 3052 ms
{"id":0,"jsonrpc":"2.0","result":["0x11d5b6f5f1c5576783ee5c6357f3d4f29cc9cd5daa39064e7857b1d95c82f66c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0x2628, 2021.08.01 13:54:19.601
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:54:19.735, 134 ms
{"id":0,"jsonrpc":"2.0","result":["0xd7b8a57067acab6040f75cb7b0e9ea950ba5181d5e6b05ea5b180c7da0de5b63","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0x1df0, 2021.08.01 13:54:19.735
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:54:21.530, 1794 ms
{"id":0,"jsonrpc":"2.0","result":["0x2143cf2aff00cfb53f3dc9d3b241c8132970f7234e25b3069f6a30511d361395","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d0"]}

--- thread ID: 0x18b4, 2021.08.01 13:54:21.530
epoch = 431 (next epoch in 20528 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:54:22.682, 1152 ms
{"id":0,"jsonrpc":"2.0","result":["0xd236dc0b5bf60f967f64241a93a50359796ca6231cb59bd3f093369c06ed2957","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d1"]}

--- thread ID: 0x2630, 2021.08.01 13:54:22.682
epoch = 431 (next epoch in 20527 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:54:22.805, 122 ms
{"id":0,"jsonrpc":"2.0","result":["0x521d877a42dbaf316b38b447ce5867cc2419b87048b43792772c79fffcbdea4c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d1"]}

--- thread ID: 0x24b4, 2021.08.01 13:54:22.805
epoch = 431 (next epoch in 20527 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:54:23.780, 975 ms
{"id":0,"jsonrpc":"2.0","result":["0x678bd7a4b70b28f16e7f6b3476167ae5a794114dd3e55fa3037f1f49c1632f4f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d2"]}

--- thread ID: 0x2610, 2021.08.01 13:54:23.780
epoch = 431 (next epoch in 20526 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0xf4c, 2021.08.01 13:54:23.876, PCIe: 00000000:0c:00.0, GPU.08 share found (search channel 0).
 nonce: 0x13d0a83bef2db86f
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000039a797a23cf31981fccfe550f71de4d58ad638313e9d6b4ba2cb40bc
   mix: 0xd37c52d1f80205f4958b00b3dce6101dc6e79a028a1cd5db331fa2345f07373b

<<< thread ID: 0x2768, 2021.08.01 13:54:23.876, 0 ms
{"jsonrpc":"2.0","id":1031,"method":"eth_submitWork","params":["0x13d0a83bef2db86f","0x678bd7a4b70b28f16e7f6b3476167ae5a794114dd3e55fa3037f1f49c1632f4f","0xd37c52d1f80205f4958b00b3dce6101dc6e79a028a1cd5db331fa2345f07373b"],"worker":"alphagruis"}

--- thread ID: 0x2648, 2021.08.01 13:54:23.909, PCIe: 00000000:0c:00.0, GPU.08 share accepted.

>>> thread ID: 0x2648, 2021.08.01 13:54:23.909, 129 ms (33 ms)
{"id":1031,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:54:23.910, 0 ms
{"id":0,"jsonrpc":"2.0","result":["0x0e8405ee14c50baa9720824cdd4baaad86b327f8835424b0ef465f3356ef3696","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d2"]}

--- thread ID: 0xedc, 2021.08.01 13:54:23.910
epoch = 431 (next epoch in 20526 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:54:25.088, 1178 ms
{"id":0,"jsonrpc":"2.0","result":["0x255b8ece4543e7caca64cb405c021d6f598bb7142a5838f945092ab4f0f586bd","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d2"]}

--- thread ID: 0x2628, 2021.08.01 13:54:25.088
epoch = 431 (next epoch in 20526 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:54:25.440, 351 ms
{"id":0,"jsonrpc":"2.0","result":["0x365de30a74de63e6b43f49dcfb1e98346fdbe6cb2a1cd47bfd19c09e35a90bbd","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d3"]}

--- thread ID: 0x1df0, 2021.08.01 13:54:25.440
epoch = 431 (next epoch in 20525 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:54:25.648, 207 ms
{"id":0,"jsonrpc":"2.0","result":["0x766ea3f478e37697e5008f8e4698863ddd3001e3fc028eae1ce960833ff19d16","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d3"]}

--- thread ID: 0x18b4, 2021.08.01 13:54:25.648
epoch = 431 (next epoch in 20525 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:54:26.728, 1080 ms
{"id":0,"jsonrpc":"2.0","result":["0x68d593314d8be07aa7f6bb8f7d7a9d64254f84dda49ae293e899cdc89e426ed5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d3"]}

--- thread ID: 0x2630, 2021.08.01 13:54:26.728
epoch = 431 (next epoch in 20525 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:54:26.829, 101 ms
{"id":0,"jsonrpc":"2.0","result":["0x6660a712f827f2cef0d710636cc1bcab0b77b67bbaaf7b53a1ce1ab3c677553e","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d3"]}

--- thread ID: 0x24b4, 2021.08.01 13:54:26.830
epoch = 431 (next epoch in 20525 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:54:27.103, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:06:45.618)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:06:46.539, 40 ms], [fan = 99%, 2937 rpm, 53°C], 28.653999 MH/s (100.29 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:01:08.508, 17 ms], [fan = 99%, 2615 rpm, 63°C], 28.990188 MH/s ( 98.78 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:02:11.396, 18 ms], [fan = 99%, 2659 rpm, 65°C], 29.211606 MH/s (100.55 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 3, S = 0, R = 0, I = 0], [00:02:35.642, 55 ms], [fan = 99%, 2680 rpm, 64°C], 28.689534 MH/s (101.94 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:02:24.848, 40 ms], [fan = 99%, 3357 rpm, 66°C], 29.187859 MH/s ( 99.89 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 2, S = 0, R = 0, I = 0], [00:01:26.480, 56 ms], [fan = 99%, 3264 rpm, 62°C], 28.962527 MH/s (101.55 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:03:55.433, 58 ms], [fan = 99%, 2536 rpm, 66°C], 28.941351 MH/s (102.62 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 5, S = 0, R = 0, I = 0], [00:00:03.227, 29 ms], [fan = 99%, 2684 rpm, 59°C], 29.213234 MH/s (102.73 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:01:41.246, 39 ms], [fan = 99%, 2652 rpm, 63°C], 29.210774 MH/s (102.76 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:00:41.682, 22 ms], [fan = 99%, 2657 rpm, 61°C], 29.213365 MH/s (102.57 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:01:12.813, 37 ms], [fan = 99%, 2643 rpm, 65°C], 28.685813 MH/s (103.31 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:05:12.192, 53 ms], [fan = 99%, 2705 rpm, 66°C], 27.701279 MH/s (101.85 W) = 346.661529 MH/s (1218.84 W)

<<< thread ID: 0x2610, 2021.08.01 13:54:27.107, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014a9a299","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2768, 2021.08.01 13:54:27.123, 293 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:54:30.619, 3495 ms
{"id":0,"jsonrpc":"2.0","result":["0x73318ae87005628c3e0326b37a29c404df3158f44ff3a7a8a7079c9cb28d9dbf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d3"]}

--- thread ID: 0x2648, 2021.08.01 13:54:30.619
epoch = 431 (next epoch in 20525 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2fc, 2021.08.01 13:54:30.718, PCIe: 00000000:0e:00.0, GPU.04 share found (search channel 0).
 nonce: 0x13d0a83c7ca0b554
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000091f5a35b59375218ad2595ab2cc11fa0fd866db9a4700f24acbd1dc9
   mix: 0x2ed3a3ba6a1db99deb58a70c462db966f03bffc89512fde3deee4106cc3f334c

<<< thread ID: 0xedc, 2021.08.01 13:54:30.718, 0 ms
{"jsonrpc":"2.0","id":1032,"method":"eth_submitWork","params":["0x13d0a83c7ca0b554","0x73318ae87005628c3e0326b37a29c404df3158f44ff3a7a8a7079c9cb28d9dbf","0x2ed3a3ba6a1db99deb58a70c462db966f03bffc89512fde3deee4106cc3f334c"],"worker":"alphagruis"}

--- thread ID: 0x2628, 2021.08.01 13:54:30.735, PCIe: 00000000:0e:00.0, GPU.04 share accepted.

>>> thread ID: 0x2628, 2021.08.01 13:54:30.735, 116 ms (17 ms)
{"id":1032,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 13:54:36.639, 5903 ms
{"id":0,"jsonrpc":"2.0","result":["0xcd1aa667fbad76704fa6768b52459e2c5403aa402653ea447406f92ca0183842","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d3"]}

--- thread ID: 0x1df0, 2021.08.01 13:54:36.639
epoch = 431 (next epoch in 20525 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:54:36.706, 67 ms
{"id":0,"jsonrpc":"2.0","result":["0x72b2caa4c589bca52c6de77317e048fd362eb8211f0d74521da6945bce3e63ef","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d3"]}

--- thread ID: 0x18b4, 2021.08.01 13:54:36.706
epoch = 431 (next epoch in 20525 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:54:42.122, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:07:00.637)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:07:01.558, 19 ms], [fan = 99%, 2952 rpm, 53°C], 28.649243 MH/s ( 99.89 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:01:23.527,  6 ms], [fan = 99%, 2611 rpm, 64°C], 28.779314 MH/s ( 98.68 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:02:26.415, 12 ms], [fan = 99%, 2659 rpm, 65°C], 29.204539 MH/s (100.45 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:00:11.404, 35 ms], [fan = 99%, 2659 rpm, 64°C], 29.197436 MH/s (102.19 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:02:39.867,  9 ms], [fan = 99%, 3315 rpm, 67°C], 29.148628 MH/s (100.04 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 2, S = 0, R = 0, I = 0], [00:01:41.499, 34 ms], [fan = 99%, 3249 rpm, 62°C], 29.205956 MH/s (101.88 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:04:10.452, 34 ms], [fan = 99%, 2543 rpm, 66°C], 29.046116 MH/s (103.11 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 5, S = 0, R = 0, I = 0], [00:00:18.246, 12 ms], [fan = 99%, 2656 rpm, 59°C], 29.202326 MH/s (102.86 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:01:56.265, 21 ms], [fan = 99%, 2661 rpm, 63°C], 29.196343 MH/s (103.00 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:00:56.701,  4 ms], [fan = 99%, 2653 rpm, 61°C], 29.200561 MH/s (102.55 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:01:27.832, 18 ms], [fan = 99%, 2620 rpm, 66°C], 29.196203 MH/s (103.48 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:05:27.211, 23 ms], [fan = 99%, 2701 rpm, 66°C], 27.597778 MH/s (101.39 W) = 347.624443 MH/s (1219.53 W)

<<< thread ID: 0x2630, 2021.08.01 13:54:42.126, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b853fb","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:54:42.141, 5435 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0xf4c, 2021.08.01 13:54:44.915, PCIe: 00000000:0c:00.0, GPU.08 share found (search channel 1).
 nonce: 0x13d0a83da3058822
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000078bf032aff51a66e751493dbff9e13995eb9d20461e08e016e64568b
   mix: 0xe150d47f18ceaf0a37ab4ced0a29f64b5e93263a48a85817b9c0b3717998a9e0

<<< thread ID: 0x2610, 2021.08.01 13:54:44.915, 0 ms
{"jsonrpc":"2.0","id":1033,"method":"eth_submitWork","params":["0x13d0a83da3058822","0x72b2caa4c589bca52c6de77317e048fd362eb8211f0d74521da6945bce3e63ef","0xe150d47f18ceaf0a37ab4ced0a29f64b5e93263a48a85817b9c0b3717998a9e0"],"worker":"alphagruis"}

--- thread ID: 0x2768, 2021.08.01 13:54:44.930, PCIe: 00000000:0c:00.0, GPU.08 share accepted.

>>> thread ID: 0x2768, 2021.08.01 13:54:44.930, 2788 ms (15 ms)
{"id":1033,"jsonrpc":"2.0","result":true}

--- thread ID: 0x10c4, 2021.08.01 13:54:45.900, PCIe: 00000000:02:00.0, GPU.06 share found (search channel 0).
 nonce: 0x13d0a83db7303ea0
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000076f3db76270225945a03030b099c55bd2049aac62f85c92efe59d1d1
   mix: 0x900355f7d7e622dcc1b7e9b3014d325642fb00355b32ed565d0a0f4514d13355

<<< thread ID: 0x2648, 2021.08.01 13:54:45.900, 0 ms
{"jsonrpc":"2.0","id":1034,"method":"eth_submitWork","params":["0x13d0a83db7303ea0","0x72b2caa4c589bca52c6de77317e048fd362eb8211f0d74521da6945bce3e63ef","0x900355f7d7e622dcc1b7e9b3014d325642fb00355b32ed565d0a0f4514d13355"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:54:45.916, PCIe: 00000000:02:00.0, GPU.06 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:54:45.916, 985 ms (16 ms)
{"id":1034,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:54:47.127, 1210 ms
{"id":0,"jsonrpc":"2.0","result":["0x2c7ab76bcfe0f40273e53cb05f11a9ab126a999866c2c862ba2a4497b4b75c3a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x2628, 2021.08.01 13:54:47.127
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:54:47.242, 115 ms
{"id":0,"jsonrpc":"2.0","result":["0x0af26aa431663f9b637e0b635a6442229e3396763ea96d37cfeaf92f9bf8c301","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x1df0, 2021.08.01 13:54:47.243
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:54:52.189, 4946 ms
{"id":0,"jsonrpc":"2.0","result":["0xc531344526bea13810b629ca47f8ea1217e9bf468da21db631e3c898855038af","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x18b4, 2021.08.01 13:54:52.189
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:54:57.133, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:07:15.649)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:07:16.569, 11 ms], [fan = 99%, 2956 rpm, 53°C], 28.920046 MH/s ( 99.84 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:01:38.538,  9 ms], [fan = 99%, 2607 rpm, 64°C], 29.177321 MH/s (100.06 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:02:41.426, 41 ms], [fan = 99%, 2655 rpm, 65°C], 29.198321 MH/s (100.48 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:00:26.415, 48 ms], [fan = 99%, 2671 rpm, 64°C], 28.650672 MH/s (101.36 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:02:54.878, 52 ms], [fan = 99%, 3331 rpm, 67°C], 29.196900 MH/s (100.29 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:00:11.233,  6 ms], [fan = 99%, 3270 rpm, 62°C], 29.206951 MH/s (101.78 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:04:25.463,  8 ms], [fan = 99%, 2539 rpm, 66°C], 29.193835 MH/s (103.12 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 6, S = 0, R = 0, I = 0], [00:00:12.218, 10 ms], [fan = 99%, 2680 rpm, 59°C], 29.193404 MH/s (102.77 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:02:11.276, 14 ms], [fan = 99%, 2652 rpm, 64°C], 29.197984 MH/s (102.96 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:01:11.713, 52 ms], [fan = 99%, 2669 rpm, 61°C], 29.197445 MH/s (102.46 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:01:42.844,  6 ms], [fan = 99%, 2612 rpm, 66°C], 28.685169 MH/s (102.18 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:05:42.223, 26 ms], [fan = 99%, 2701 rpm, 66°C], 27.791017 MH/s (102.40 W) = 347.609065 MH/s (1219.70 W)

<<< thread ID: 0x2630, 2021.08.01 13:54:57.138, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b817e9","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:54:57.152, 4963 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:55:00.231, 3079 ms
{"id":0,"jsonrpc":"2.0","result":["0x907848fea70884f6294f749cf672d3b93fa641144771b1fb0d358d93bf652f0f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x2610, 2021.08.01 13:55:00.231
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:55:06.282, 6050 ms
{"id":0,"jsonrpc":"2.0","result":["0x04a64e604eaca937804e2c451eaa37f2cdfe9e09f7ded584746a00f0acdae523","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x2768, 2021.08.01 13:55:06.282
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:55:10.242, 3960 ms
{"id":0,"jsonrpc":"2.0","result":["0xda9a90c81bdf4785812b2e61ae8bdd69ad13ed892c6de3f3549893a802f83bb4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x2648, 2021.08.01 13:55:10.243
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:55:12.134, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:07:30.649)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:07:31.569,  2 ms], [fan = 99%, 2939 rpm, 52°C], 28.719950 MH/s (100.58 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:01:53.539, 24 ms], [fan = 99%, 2615 rpm, 64°C], 29.057855 MH/s ( 98.51 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:02:56.426,  4 ms], [fan = 99%, 2670 rpm, 65°C], 29.202606 MH/s (100.38 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:00:41.416, 68 ms], [fan = 99%, 2655 rpm, 64°C], 28.626509 MH/s (101.26 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:03:09.879, 24 ms], [fan = 99%, 3354 rpm, 67°C], 28.814440 MH/s ( 98.78 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:00:26.234, 44 ms], [fan = 99%, 3304 rpm, 62°C], 29.200890 MH/s (101.93 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:04:40.463,  0 ms], [fan = 99%, 2532 rpm, 67°C], 29.053819 MH/s (102.17 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 6, S = 0, R = 0, I = 0], [00:00:27.219, 19 ms], [fan = 99%, 2668 rpm, 59°C], 29.211488 MH/s (102.85 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:02:26.277, 27 ms], [fan = 99%, 2644 rpm, 64°C], 29.204819 MH/s (103.05 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:01:26.713,  2 ms], [fan = 99%, 2649 rpm, 61°C], 29.197668 MH/s (101.70 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:01:57.844,  5 ms], [fan = 99%, 2631 rpm, 66°C], 28.730293 MH/s (103.38 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:05:57.223,  2 ms], [fan = 99%, 2698 rpm, 66°C], 27.664999 MH/s (101.66 W) = 346.685336 MH/s (1216.25 W)

<<< thread ID: 0xedc, 2021.08.01 13:55:12.138, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014a9ff98","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2628, 2021.08.01 13:55:12.153, 1910 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 13:55:17.279, 5125 ms
{"id":0,"jsonrpc":"2.0","result":["0x83957b04f977240ed72572c343bfeaf6cecd3020f727799e8963e7a6aed424ae","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x1df0, 2021.08.01 13:55:17.279
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:55:19.227, 1948 ms
{"id":0,"jsonrpc":"2.0","result":["0xaa8562888b24291bfcefafd166fb5b57d891d7376298223dd0dbc4cff2b00702","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d4"]}

--- thread ID: 0x18b4, 2021.08.01 13:55:19.227
epoch = 431 (next epoch in 20524 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:55:19.792, 564 ms
{"id":0,"jsonrpc":"2.0","result":["0x439430392a0a36b6c42188190deae41ae599d13daafd60122a67db97a559ad0d","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d5"]}

--- thread ID: 0x2630, 2021.08.01 13:55:19.792
epoch = 431 (next epoch in 20523 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:55:19.925, 132 ms
{"id":0,"jsonrpc":"2.0","result":["0xe7a461771e5af276b10ae3aecfea20f6de7ddb9facf708d90fd4d37481dc8f56","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d5"]}

--- thread ID: 0x24b4, 2021.08.01 13:55:19.925
epoch = 431 (next epoch in 20523 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:55:21.870, 1944 ms
{"id":0,"jsonrpc":"2.0","result":["0x3e7880677ebdbf3abe8bcab9cf9e6f6b1c2177857aeefb7f4de108ab05dd3efb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d5"]}

--- thread ID: 0x2610, 2021.08.01 13:55:21.870
epoch = 431 (next epoch in 20523 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:55:21.905, 35 ms
{"id":0,"jsonrpc":"2.0","result":["0xa22cd3d9e1a630eafb4427e23dceaef750afa0ab13b59eb168411072fa8f1d23","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d5"]}

--- thread ID: 0x2768, 2021.08.01 13:55:21.905
epoch = 431 (next epoch in 20523 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:55:24.187, 2282 ms
{"id":0,"jsonrpc":"2.0","result":["0x579a5e18268fe7e9ee388ad8e439f0323a8e6cd879f678efb612c67e191d4cd4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d5"]}

--- thread ID: 0x2648, 2021.08.01 13:55:24.188
epoch = 431 (next epoch in 20523 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:55:24.315, 127 ms
{"id":0,"jsonrpc":"2.0","result":["0x21bc9af5a21e854240727f3d2da59fd06f25d9f03292c8e2588ea79e30b9f8fa","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d5"]}

--- thread ID: 0xedc, 2021.08.01 13:55:24.315
epoch = 431 (next epoch in 20523 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:55:25.894, 1579 ms
{"id":0,"jsonrpc":"2.0","result":["0x65b1275a996e5315bc412290f21c78032d8c038ed068030d0711ab73e6664d7c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d5"]}

--- thread ID: 0x2628, 2021.08.01 13:55:25.894
epoch = 431 (next epoch in 20523 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:55:27.150, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:07:45.665)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:07:46.585, 14 ms], [fan = 99%, 2897 rpm, 52°C], 28.953089 MH/s (100.90 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:02:08.555, 22 ms], [fan = 99%, 2603 rpm, 64°C], 28.881803 MH/s ( 99.74 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 3, S = 0, R = 0, I = 0], [00:03:11.442,  0 ms], [fan = 99%, 2662 rpm, 65°C], 29.218045 MH/s (100.46 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:00:56.432, 25 ms], [fan = 99%, 2676 rpm, 64°C], 28.653836 MH/s (100.60 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:03:24.895, 11 ms], [fan = 99%, 3345 rpm, 67°C], 28.935380 MH/s ( 99.05 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:00:41.250, 16 ms], [fan = 99%, 3332 rpm, 62°C], 29.216523 MH/s (101.93 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:04:55.479, 25 ms], [fan = 99%, 2566 rpm, 67°C], 28.767921 MH/s (103.21 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 6, S = 0, R = 0, I = 0], [00:00:42.235,  0 ms], [fan = 99%, 2668 rpm, 59°C], 29.216938 MH/s (102.73 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:02:41.292,  0 ms], [fan = 99%, 2640 rpm, 64°C], 29.188356 MH/s (102.75 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:01:41.729, 19 ms], [fan = 99%, 2641 rpm, 61°C], 29.218980 MH/s (102.51 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:02:12.860, 24 ms], [fan = 99%, 2631 rpm, 66°C], 29.204344 MH/s (103.39 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:06:12.239, 50 ms], [fan = 99%, 2701 rpm, 66°C], 27.627310 MH/s (101.82 W) = 347.082525 MH/s (1219.10 W)

<<< thread ID: 0x1df0, 2021.08.01 13:55:27.154, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b00f1d","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x18b4, 2021.08.01 13:55:27.170, 1275 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2630, 2021.08.01 13:55:32.860, 5690 ms
{"id":0,"jsonrpc":"2.0","result":["0x114aa22bcabb540aeb24ada03712e6a5e01d9f3c1f180f177419ede2c4c4f026","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d6"]}

--- thread ID: 0x2630, 2021.08.01 13:55:32.860
epoch = 431 (next epoch in 20522 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:55:33.104, 243 ms
{"id":0,"jsonrpc":"2.0","result":["0x8f080240cf2f9930d50d1db2c41be94a9d77196ce5b704402cfedcc3841bffd2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d6"]}

--- thread ID: 0x24b4, 2021.08.01 13:55:33.104
epoch = 431 (next epoch in 20522 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2ec, 2021.08.01 13:55:34.726, PCIe: 00000000:04:00.0, GPU.03 share found (search channel 0).
 nonce: 0x13d0a841a9458c6f
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000093d15f3583598fae2c1d2ebb4948ac8637d0ff405ee5207b65e74437
   mix: 0x78683e0dbfb9e7579700374e70f706e8d084083c53e0935ab2cff8c7239e67c7

<<< thread ID: 0x2610, 2021.08.01 13:55:34.727, 0 ms
{"jsonrpc":"2.0","id":1035,"method":"eth_submitWork","params":["0x13d0a841a9458c6f","0x8f080240cf2f9930d50d1db2c41be94a9d77196ce5b704402cfedcc3841bffd2","0x78683e0dbfb9e7579700374e70f706e8d084083c53e0935ab2cff8c7239e67c7"],"worker":"alphagruis"}

--- thread ID: 0x2768, 2021.08.01 13:55:34.743, PCIe: 00000000:04:00.0, GPU.03 share accepted.

>>> thread ID: 0x2768, 2021.08.01 13:55:34.743, 1638 ms (16 ms)
{"id":1035,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:55:35.959, 1216 ms
{"id":0,"jsonrpc":"2.0","result":["0x3b1a68bb0b9650fb9ca7149dcd540739e739d962096accd1cb43be1c142952cf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d6"]}

--- thread ID: 0x2648, 2021.08.01 13:55:35.959
epoch = 431 (next epoch in 20522 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:55:39.965, 4006 ms
{"id":0,"jsonrpc":"2.0","result":["0x496355dcf25d59b9c79305a1364015b0821a09c01b3ee5492b827af306a4beaa","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d6"]}

--- thread ID: 0xedc, 2021.08.01 13:55:39.965
epoch = 431 (next epoch in 20522 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:55:41.108, 1142 ms
{"id":0,"jsonrpc":"2.0","result":["0x7e6d4af320bf7c51f373727d9d61c1fc9f8822fb0100df79c01b197349c8103a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d7"]}

--- thread ID: 0x2628, 2021.08.01 13:55:41.108
epoch = 431 (next epoch in 20521 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:55:41.266, 158 ms
{"id":0,"jsonrpc":"2.0","result":["0xaa6c885a2f70698f90073b6c91441c6fc3167e380709f5996c18349b573c9efd","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d7"]}

--- thread ID: 0x1df0, 2021.08.01 13:55:41.266
epoch = 431 (next epoch in 20521 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:55:42.150, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:08:00.665)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:08:01.586, 46 ms], [fan = 99%, 2933 rpm, 53°C], 29.204245 MH/s (100.91 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:02:23.555,  2 ms], [fan = 99%, 2607 rpm, 64°C], 28.760337 MH/s ( 99.26 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:00:07.424,  9 ms], [fan = 99%, 2658 rpm, 65°C], 29.208845 MH/s (100.48 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:01:11.432, 49 ms], [fan = 99%, 2676 rpm, 64°C], 28.613923 MH/s (101.63 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:03:39.895, 31 ms], [fan = 99%, 3328 rpm, 67°C], 29.092190 MH/s (100.09 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:00:56.250, 51 ms], [fan = 99%, 3250 rpm, 62°C], 29.200987 MH/s (101.77 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:05:10.480, 46 ms], [fan = 99%, 2547 rpm, 67°C], 28.677102 MH/s (102.55 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 6, S = 0, R = 0, I = 0], [00:00:57.235, 32 ms], [fan = 99%, 2672 rpm, 59°C], 29.200246 MH/s (102.68 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:02:56.293, 32 ms], [fan = 99%, 2636 rpm, 64°C], 29.206437 MH/s (102.88 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:01:56.729, 56 ms], [fan = 99%, 2633 rpm, 61°C], 29.199006 MH/s (102.39 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:02:27.860, 56 ms], [fan = 99%, 2623 rpm, 66°C], 29.194879 MH/s (103.55 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:06:27.239, 67 ms], [fan = 99%, 2697 rpm, 66°C], 27.817840 MH/s (102.23 W) = 347.376037 MH/s (1220.43 W)

<<< thread ID: 0x18b4, 2021.08.01 13:55:42.154, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b489a5","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:55:42.169, 903 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:55:46.267, 4097 ms
{"id":0,"jsonrpc":"2.0","result":["0xe51c4b0e3ca5c7f7278028e3ac8f72e4900aa7ce983f19eb534a28dab5046fe8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d7"]}

--- thread ID: 0x24b4, 2021.08.01 13:55:46.267
epoch = 431 (next epoch in 20521 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:55:46.606, 338 ms
{"id":0,"jsonrpc":"2.0","result":["0x975a6dc383c295e8c059ac4178363283aff544f3808a4730d81bc7cb76cb7df2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d8"]}

--- thread ID: 0x2610, 2021.08.01 13:55:46.606
epoch = 431 (next epoch in 20520 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:55:46.713, 106 ms
{"id":0,"jsonrpc":"2.0","result":["0xf33a7a1ed2cccdcb503481c3662f0a1cef466c763990226b38446b53395d611c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d8"]}

--- thread ID: 0x2768, 2021.08.01 13:55:46.713
epoch = 431 (next epoch in 20520 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:55:49.900, 3187 ms
{"id":0,"jsonrpc":"2.0","result":["0x064af4b4775afd82b72ca047bc87ef14184e9a038d74f33a628df21bef1fbfcf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d8"]}

--- thread ID: 0x2648, 2021.08.01 13:55:49.900
epoch = 431 (next epoch in 20520 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:55:51.826, 1925 ms
{"id":0,"jsonrpc":"2.0","result":["0x5ecdafae96b1da99f5af83796fae8fadc22382620a18657302d9e032f3b28459","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d8"]}

--- thread ID: 0xedc, 2021.08.01 13:55:51.826
epoch = 431 (next epoch in 20520 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:55:56.959, 5133 ms
{"id":0,"jsonrpc":"2.0","result":["0xe1ffe8d653cd9476d5b3df781ef732cf8f630c80a7e56c40668cffc7399baf1f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d8"]}

--- thread ID: 0x2628, 2021.08.01 13:55:56.959
epoch = 431 (next epoch in 20520 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:55:57.165, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:08:15.681)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:08:16.601, 23 ms], [fan = 99%, 2949 rpm, 52°C], 29.190382 MH/s (100.79 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:02:38.570, 21 ms], [fan = 99%, 2611 rpm, 64°C], 29.203673 MH/s ( 99.96 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:00:22.439, 23 ms], [fan = 99%, 2670 rpm, 65°C], 29.226300 MH/s (100.48 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:01:26.447, 15 ms], [fan = 99%, 2672 rpm, 64°C], 29.219623 MH/s (101.99 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:03:54.910, 23 ms], [fan = 99%, 3336 rpm, 67°C], 29.227363 MH/s (100.15 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:01:11.265, 28 ms], [fan = 99%, 3263 rpm, 62°C], 29.201539 MH/s (101.73 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:05:25.495, 32 ms], [fan = 99%, 2543 rpm, 67°C], 28.943553 MH/s (103.32 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 6, S = 0, R = 0, I = 0], [00:01:12.250,  0 ms], [fan = 99%, 2680 rpm, 59°C], 29.183006 MH/s (103.12 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:03:11.308,  6 ms], [fan = 99%, 2648 rpm, 64°C], 29.202752 MH/s (102.69 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:02:11.745, 22 ms], [fan = 99%, 2645 rpm, 61°C], 29.141552 MH/s (101.56 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 5, S = 0, R = 0, I = 0], [00:02:42.876, 24 ms], [fan = 99%, 2623 rpm, 66°C], 29.224956 MH/s (103.22 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:06:42.255, 68 ms], [fan = 99%, 2701 rpm, 67°C], 27.626850 MH/s (101.67 W) = 348.591549 MH/s (1220.68 W)

<<< thread ID: 0x1df0, 2021.08.01 13:55:57.170, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c715bd","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x18b4, 2021.08.01 13:55:57.186, 226 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2630, 2021.08.01 13:56:02.065, 4879 ms
{"id":0,"jsonrpc":"2.0","result":["0xd2d1ebebef2fcecb087c6b092997afacbef7236f2cf9631c7c1da72f3780abfa","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d9"]}

--- thread ID: 0x2630, 2021.08.01 13:56:02.065
epoch = 431 (next epoch in 20519 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:56:02.223, 158 ms
{"id":0,"jsonrpc":"2.0","result":["0xf99eb752f9a0bf4d3e781257b26c2401695b08509bd936f52adf0bc25b997f6d","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d9"]}

--- thread ID: 0x24b4, 2021.08.01 13:56:02.224
epoch = 431 (next epoch in 20519 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:56:03.215, 991 ms
{"id":0,"jsonrpc":"2.0","result":["0x759d76fe7cefd3f60895fefd34330ec3efa88c52bbf7552187c9c39f829991e4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d9"]}

--- thread ID: 0x2610, 2021.08.01 13:56:03.215
epoch = 431 (next epoch in 20519 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:56:05.405, 2190 ms
{"id":0,"jsonrpc":"2.0","result":["0xcda345b9807fe48d62a632d7a43587dfe09923b71e651867a755b2b6905118b4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570d9"]}

--- thread ID: 0x2768, 2021.08.01 13:56:05.406
epoch = 431 (next epoch in 20519 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x18c8, 2021.08.01 13:56:10.297, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 0).
 nonce: 0x13d0a8448bbb78ef
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000a86fb7985f10045ae6dafc5075979f537f63ad5c83d3b5ab47a69f9f
   mix: 0x45713bfa48e700c6d5cd846ca5febfcbe514b321aafd3ea5063031d98daf592f

<<< thread ID: 0x2648, 2021.08.01 13:56:10.298, 0 ms
{"jsonrpc":"2.0","id":1036,"method":"eth_submitWork","params":["0x13d0a8448bbb78ef","0xcda345b9807fe48d62a632d7a43587dfe09923b71e651867a755b2b6905118b4","0x45713bfa48e700c6d5cd846ca5febfcbe514b321aafd3ea5063031d98daf592f"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:56:10.313, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:56:10.313, 4907 ms (15 ms)
{"id":1036,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:56:10.603, 289 ms
{"id":0,"jsonrpc":"2.0","result":["0xc8187381aa9578b079c431b0d8533523e8377627be72ed4244b597da3b9145f3","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570da"]}

--- thread ID: 0x2628, 2021.08.01 13:56:10.603
epoch = 431 (next epoch in 20518 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:56:10.699, 96 ms
{"id":0,"jsonrpc":"2.0","result":["0x7eb84867d1cf57912911cf2fff40109d9f4ac26d34941bb9ecbfb4e1f3de317f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570da"]}

--- thread ID: 0x1df0, 2021.08.01 13:56:10.699
epoch = 431 (next epoch in 20518 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:56:12.181, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:08:30.696)
PCIe: 00000000:09:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:08:31.616,  8 ms], [fan = 99%, 2943 rpm, 53°C], 29.014114 MH/s ( 99.78 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:02:53.586,  1 ms], [fan = 99%, 2607 rpm, 64°C], 29.191307 MH/s ( 99.91 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:00:37.455,  1 ms], [fan = 99%, 2650 rpm, 65°C], 29.187277 MH/s (100.37 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:01:41.463, 10 ms], [fan = 99%, 2676 rpm, 64°C], 29.198538 MH/s (102.05 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:04:09.926,  5 ms], [fan = 99%, 3321 rpm, 67°C], 29.204614 MH/s (100.14 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:01:26.281,  4 ms], [fan = 99%, 3234 rpm, 62°C], 29.216049 MH/s (101.88 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:05:40.511,  8 ms], [fan = 99%, 2562 rpm, 67°C], 29.200137 MH/s (103.43 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 6, S = 0, R = 0, I = 0], [00:01:27.266, 24 ms], [fan = 99%, 2664 rpm, 59°C], 29.180519 MH/s (103.03 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:03:26.324, 24 ms], [fan = 99%, 2644 rpm, 64°C], 29.182429 MH/s (102.73 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:02:26.760, 38 ms], [fan = 99%, 2664 rpm, 62°C], 29.108869 MH/s (101.73 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:00:01.884,  5 ms], [fan = 99%, 2634 rpm, 66°C], 29.186969 MH/s (103.46 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:06:57.270, 71 ms], [fan = 99%, 2697 rpm, 66°C], 27.597050 MH/s (101.21 W) = 348.467872 MH/s (1219.72 W)

<<< thread ID: 0x18b4, 2021.08.01 13:56:12.185, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014c532a0","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:56:12.202, 1502 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:56:13.735, 1533 ms
{"id":0,"jsonrpc":"2.0","result":["0x8ef57125ed39c829ce0dfaf15838f2589f010bc72858fa5c5d4a3130fb187b3a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570da"]}

--- thread ID: 0x24b4, 2021.08.01 13:56:13.735
epoch = 431 (next epoch in 20518 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:56:13.850, 115 ms
{"id":0,"jsonrpc":"2.0","result":["0x3f255ff026702becabaf6122a5d52ba8385bed802e254f134f5e23bd934e6ca6","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x2610, 2021.08.01 13:56:13.850
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:56:13.958, 107 ms
{"id":0,"jsonrpc":"2.0","result":["0xcb09619a127a79fdc2e8e9be562e46f6e831b9651a7e51dcbe0685c062e7ee70","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x2768, 2021.08.01 13:56:13.958
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x1970, 2021.08.01 13:56:15.472, PCIe: 00000000:09:00.0, GPU.01 share found (search channel 0).
 nonce: 0x13d0a844f6e90548
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000007e2e5049eb239e01c30c6a1d785418f0b988be8a9b177c6e2edf851a
   mix: 0xcd949e2807514e62653a57eef7e0d3e75452cbba013f812e27d1124080a24fb9

<<< thread ID: 0x2648, 2021.08.01 13:56:15.473, 0 ms
{"jsonrpc":"2.0","id":1037,"method":"eth_submitWork","params":["0x13d0a844f6e90548","0xcb09619a127a79fdc2e8e9be562e46f6e831b9651a7e51dcbe0685c062e7ee70","0xcd949e2807514e62653a57eef7e0d3e75452cbba013f812e27d1124080a24fb9"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:56:15.488, PCIe: 00000000:09:00.0, GPU.01 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:56:15.488, 1530 ms (15 ms)
{"id":1037,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:56:15.894, 406 ms
{"id":0,"jsonrpc":"2.0","result":["0x4c9d65ea477cbe54d05e179237a984903a4910decd61055ed67edf0efe144a72","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x2628, 2021.08.01 13:56:15.894
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:56:16.916, 1021 ms
{"id":0,"jsonrpc":"2.0","result":["0xf6a814a52a7554ee9c56388b9f5247094cbd935dd56fb4b3a7d9b28af4cb13a4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x1df0, 2021.08.01 13:56:16.916
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:56:19.014, 2098 ms
{"id":0,"jsonrpc":"2.0","result":["0x67acce5bf863d11392814210fd6d0b1fbac88e053d7b389589eb88b6cd2d0e41","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x18b4, 2021.08.01 13:56:19.014
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:56:20.928, 1913 ms
{"id":0,"jsonrpc":"2.0","result":["0xc5425e7eb3c7cf61046e2f2838426a96e25d2c9fb59110b0d238aa7bc72af36b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x2630, 2021.08.01 13:56:20.928
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:56:22.968, 2040 ms
{"id":0,"jsonrpc":"2.0","result":["0x6761a395ab6b46a263cd91d465bbdee8bfa9b4bd83373131a75e034fb36c5839","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x24b4, 2021.08.01 13:56:22.968
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:56:27.184, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:08:45.699)
PCIe: 00000000:09:00.0, GPU.01: [A = 1, S = 0, R = 0, I = 0], [00:00:11.711, 23 ms], [fan = 99%, 2935 rpm, 53°C], 28.834533 MH/s (100.88 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:03:08.588, 35 ms], [fan = 99%, 2596 rpm, 64°C], 29.211923 MH/s ( 99.91 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:00:52.457, 42 ms], [fan = 99%, 2670 rpm, 65°C], 29.212094 MH/s (100.33 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 4, S = 0, R = 0, I = 0], [00:01:56.465, 33 ms], [fan = 99%, 2672 rpm, 64°C], 29.197203 MH/s (101.86 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:04:24.928, 44 ms], [fan = 99%, 3314 rpm, 67°C], 29.214716 MH/s ( 99.97 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:01:41.283, 42 ms], [fan = 99%, 3282 rpm, 63°C], 29.195881 MH/s (101.81 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:05:55.513, 44 ms], [fan = 99%, 2554 rpm, 67°C], 29.196283 MH/s (103.20 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 6, S = 0, R = 0, I = 0], [00:01:42.269, 66 ms], [fan = 99%, 2668 rpm, 59°C], 29.189323 MH/s (102.88 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:03:41.326, 10 ms], [fan = 99%, 2652 rpm, 64°C], 29.190127 MH/s (102.93 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 3, S = 0, R = 0, I = 0], [00:02:41.763, 23 ms], [fan = 99%, 2652 rpm, 62°C], 28.870192 MH/s (102.43 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:00:16.886, 15 ms], [fan = 99%, 2634 rpm, 66°C], 29.148142 MH/s (102.46 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:07:12.273, 14 ms], [fan = 99%, 2693 rpm, 67°C], 27.422468 MH/s (101.31 W) = 347.882885 MH/s (1219.98 W)

<<< thread ID: 0x2610, 2021.08.01 13:56:27.188, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014bc4585","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2768, 2021.08.01 13:56:27.203, 4234 ms (14 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:56:29.926, 2723 ms
{"id":0,"jsonrpc":"2.0","result":["0x6ca7b87a9cddb5e905b9bbf9f2b402025b5035f7e8a46867589b5cdcdcac1910","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x2648, 2021.08.01 13:56:29.926
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0xf4c, 2021.08.01 13:56:32.459, PCIe: 00000000:0c:00.0, GPU.08 share found (search channel 1).
 nonce: 0x13d0a84656fc8cf9
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000002cfe398a546bf606c7da61f90d56de82044a5f57221424f669b1a528
   mix: 0x68c075cd93ce853fa694224820c58d054e8de2abd098383feb3f8061c9e7dfbd

<<< thread ID: 0xedc, 2021.08.01 13:56:32.459, 0 ms
{"jsonrpc":"2.0","id":1038,"method":"eth_submitWork","params":["0x13d0a84656fc8cf9","0x6ca7b87a9cddb5e905b9bbf9f2b402025b5035f7e8a46867589b5cdcdcac1910","0x68c075cd93ce853fa694224820c58d054e8de2abd098383feb3f8061c9e7dfbd"],"worker":"alphagruis"}

--- thread ID: 0x2628, 2021.08.01 13:56:32.474, PCIe: 00000000:0c:00.0, GPU.08 share accepted.

>>> thread ID: 0x2628, 2021.08.01 13:56:32.474, 2548 ms (15 ms)
{"id":1038,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2fc, 2021.08.01 13:56:35.787, PCIe: 00000000:0e:00.0, GPU.04 share found (search channel 0).
 nonce: 0x13d0a8469c9b4ea8
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000e0015b19297742c47001d64894bb762b0f4920a1c6759929e1471e91
   mix: 0x0e00a3cd4e22ea2387c1139b95812076976c699c5342e2d0bd6a2ac570566517

<<< thread ID: 0x1df0, 2021.08.01 13:56:35.788, 0 ms
{"jsonrpc":"2.0","id":1039,"method":"eth_submitWork","params":["0x13d0a8469c9b4ea8","0x6ca7b87a9cddb5e905b9bbf9f2b402025b5035f7e8a46867589b5cdcdcac1910","0x0e00a3cd4e22ea2387c1139b95812076976c699c5342e2d0bd6a2ac570566517"],"worker":"alphagruis"}

--- thread ID: 0x18b4, 2021.08.01 13:56:35.804, PCIe: 00000000:0e:00.0, GPU.04 share accepted.

>>> thread ID: 0x18b4, 2021.08.01 13:56:35.804, 3329 ms (16 ms)
{"id":1039,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2630, 2021.08.01 13:56:37.985, 2180 ms
{"id":0,"jsonrpc":"2.0","result":["0xce643a5597a031d055fb03c7ecab905dbf28532815961417ff32e1c69c802aea","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570db"]}

--- thread ID: 0x2630, 2021.08.01 13:56:37.985
epoch = 431 (next epoch in 20517 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x23a0, 2021.08.01 13:56:39.267, PCIe: 00000000:01:00.0, GPU.10 share found (search channel 0).
 nonce: 0x13d0a846e449b88f
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000001375770c3a9f6dab0e82a1e24b3b0094d0ab4402b34332ea5f40ebed
   mix: 0xdac543f3c705dabc08d2288f06cfd0b8ac8b32c9dfe93afba0e7088b1c9a15f9

<<< thread ID: 0x24b4, 2021.08.01 13:56:39.267, 0 ms
{"jsonrpc":"2.0","id":1040,"method":"eth_submitWork","params":["0x13d0a846e449b88f","0xce643a5597a031d055fb03c7ecab905dbf28532815961417ff32e1c69c802aea","0xdac543f3c705dabc08d2288f06cfd0b8ac8b32c9dfe93afba0e7088b1c9a15f9"],"worker":"alphagruis"}

--- thread ID: 0x2610, 2021.08.01 13:56:39.282, PCIe: 00000000:01:00.0, GPU.10 share accepted.

>>> thread ID: 0x2610, 2021.08.01 13:56:39.282, 1296 ms (14 ms)
{"id":1040,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2170, 2021.08.01 13:56:42.197, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:09:00.712)
PCIe: 00000000:09:00.0, GPU.01: [A = 1, S = 0, R = 0, I = 0], [00:00:26.724, 31 ms], [fan = 99%, 2927 rpm, 53°C], 28.978677 MH/s (100.89 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:03:23.601, 10 ms], [fan = 99%, 2607 rpm, 64°C], 29.199300 MH/s ( 99.89 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:01:07.470, 65 ms], [fan = 99%, 2654 rpm, 65°C], 28.989786 MH/s (100.00 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 5, S = 0, R = 0, I = 0], [00:00:06.409,  4 ms], [fan = 99%, 2675 rpm, 64°C], 29.203490 MH/s (101.96 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:04:39.941, 23 ms], [fan = 99%, 3324 rpm, 67°C], 29.222191 MH/s (100.14 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:01:56.296, 23 ms], [fan = 99%, 3222 rpm, 62°C], 29.180031 MH/s (101.86 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:06:10.526, 16 ms], [fan = 99%, 2558 rpm, 67°C], 29.194308 MH/s (103.21 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:00:09.738, 15 ms], [fan = 99%, 2676 rpm, 59°C], 29.203545 MH/s (103.06 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 1, S = 0, R = 0, I = 0], [00:03:56.339, 42 ms], [fan = 99%, 2648 rpm, 64°C], 29.199076 MH/s (102.91 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:00:02.930,  4 ms], [fan = 99%, 2656 rpm, 62°C], 28.824831 MH/s (101.74 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:00:31.899, 32 ms], [fan = 99%, 2615 rpm, 66°C], 28.766823 MH/s (102.47 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:07:27.286, 43 ms], [fan = 99%, 2709 rpm, 67°C], 27.443813 MH/s (101.77 W) = 347.405871 MH/s (1219.88 W)

<<< thread ID: 0x2768, 2021.08.01 13:56:42.201, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b4fe2f","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2648, 2021.08.01 13:56:42.216, 2934 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:56:42.697, 481 ms
{"id":0,"jsonrpc":"2.0","result":["0x560938777a307ebda5fa96a2d0159179ebef4b74f3792199a58058b87b868ed2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dc"]}

--- thread ID: 0xedc, 2021.08.01 13:56:42.697
epoch = 431 (next epoch in 20516 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:56:42.877, 179 ms
{"id":0,"jsonrpc":"2.0","result":["0x7f5d060775bb34e1c28e66cc8c707743fa0d1df8a8b6da8e13f7d29afc4d623a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dc"]}

--- thread ID: 0x2628, 2021.08.01 13:56:42.877
epoch = 431 (next epoch in 20516 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2fc, 2021.08.01 13:56:43.035, PCIe: 00000000:0e:00.0, GPU.04 share found (search channel 1).
 nonce: 0x13d0a847324bb8b2
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000b300084b107779c45676ae555763ce4fb219821307ffa092da272c47
   mix: 0x70119da2cfe203e9c8e34d364d1d145c63e04bd3eaac6db40e4c3fb0e8487e24

<<< thread ID: 0x1df0, 2021.08.01 13:56:43.036, 0 ms
{"jsonrpc":"2.0","id":1041,"method":"eth_submitWork","params":["0x13d0a847324bb8b2","0x7f5d060775bb34e1c28e66cc8c707743fa0d1df8a8b6da8e13f7d29afc4d623a","0x70119da2cfe203e9c8e34d364d1d145c63e04bd3eaac6db40e4c3fb0e8487e24"],"worker":"alphagruis"}

--- thread ID: 0x18b4, 2021.08.01 13:56:43.052, PCIe: 00000000:0e:00.0, GPU.04 share accepted.

>>> thread ID: 0x18b4, 2021.08.01 13:56:43.052, 175 ms (16 ms)
{"id":1041,"jsonrpc":"2.0","result":true}

--- thread ID: 0x2420, 2021.08.01 13:56:46.246, PCIe: 00000000:06:00.0, GPU.09 share found (search channel 1).
 nonce: 0x13d0a84774c4722b
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000038e45c466b4cdcf15df8cdad0bd79e3c99509944af081ef475df7aa0
   mix: 0xc52f338fa08d0651bc59b78c04bb73cad5ea034e1cef0bf010015318c2057f77

<<< thread ID: 0x2630, 2021.08.01 13:56:46.246, 0 ms
{"jsonrpc":"2.0","id":1042,"method":"eth_submitWork","params":["0x13d0a84774c4722b","0x7f5d060775bb34e1c28e66cc8c707743fa0d1df8a8b6da8e13f7d29afc4d623a","0xc52f338fa08d0651bc59b78c04bb73cad5ea034e1cef0bf010015318c2057f77"],"worker":"alphagruis"}

--- thread ID: 0x24b4, 2021.08.01 13:56:46.262, PCIe: 00000000:06:00.0, GPU.09 share accepted.

>>> thread ID: 0x24b4, 2021.08.01 13:56:46.262, 3209 ms (15 ms)
{"id":1042,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:56:46.746, 484 ms
{"id":0,"jsonrpc":"2.0","result":["0x551ab6708209c2b8d08b5b39f15658e021695d6e22864d0b4b07b5699ce805cf","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dc"]}

--- thread ID: 0x2610, 2021.08.01 13:56:46.746
epoch = 431 (next epoch in 20516 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:56:48.054, 1307 ms
{"id":0,"jsonrpc":"2.0","result":["0xcae30e609a1f19432269d685b5723c68c81ee35386434a7df74553ceecccf132","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dc"]}

--- thread ID: 0x2768, 2021.08.01 13:56:48.054
epoch = 431 (next epoch in 20516 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x1970, 2021.08.01 13:56:48.066, PCIe: 00000000:09:00.0, GPU.01 share found (search channel 1, stale: 12 ms of delay).
 nonce: 0x13d0a8479a6aff21
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000e8b2680a99cb7a4d1eb59060279b871a98f559c50fc4351034ef498b
   mix: 0xbd066c3ed91eee3e0aa2683ae1fd0ed85d114721188535961c970f69024b8fc3

<<< thread ID: 0x2648, 2021.08.01 13:56:48.066, 0 ms
{"jsonrpc":"2.0","id":1043,"method":"eth_submitWork","params":["0x13d0a8479a6aff21","0x551ab6708209c2b8d08b5b39f15658e021695d6e22864d0b4b07b5699ce805cf","0xbd066c3ed91eee3e0aa2683ae1fd0ed85d114721188535961c970f69024b8fc3"],"worker":"alphagruis"}

>>> thread ID: 0xedc, 2021.08.01 13:56:48.112, 57 ms
{"id":0,"jsonrpc":"2.0","result":["0x3471d701ac7a1dc57aa4b7f3264238f98a0313f9373d6e6057aaec790d302454","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dc"]}

--- thread ID: 0xedc, 2021.08.01 13:56:48.112
epoch = 431 (next epoch in 20516 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2628, 2021.08.01 13:56:48.153, PCIe: 00000000:09:00.0, GPU.01 share accepted.

>>> thread ID: 0x2628, 2021.08.01 13:56:48.153, 40 ms (86 ms)
{"id":1043,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 13:56:54.960, 6807 ms
{"id":0,"jsonrpc":"2.0","result":["0x3e6b4e926727ecf96dffa691eb61b020e81b5b947ae6f27f707806a0a4a83380","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dc"]}

--- thread ID: 0x1df0, 2021.08.01 13:56:54.960
epoch = 431 (next epoch in 20516 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:56:57.212, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:09:15.727)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:00:09.146,  4 ms], [fan = 99%, 2955 rpm, 53°C], 28.729687 MH/s ( 99.76 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:03:38.617, 61 ms], [fan = 99%, 2607 rpm, 64°C], 29.192799 MH/s (100.03 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:01:22.486, 36 ms], [fan = 99%, 2658 rpm, 65°C], 28.729503 MH/s ( 99.45 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:00:14.177,  5 ms], [fan = 99%, 2647 rpm, 64°C], 29.216135 MH/s (102.21 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:04:54.957,  0 ms], [fan = 99%, 3313 rpm, 67°C], 29.193143 MH/s (100.23 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:02:11.312,  1 ms], [fan = 99%, 3265 rpm, 63°C], 29.202569 MH/s (101.70 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:06:25.542, 57 ms], [fan = 99%, 2550 rpm, 67°C], 28.700509 MH/s (102.77 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:00:24.754, 65 ms], [fan = 99%, 2664 rpm, 59°C], 29.194021 MH/s (102.38 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:00:10.966, 58 ms], [fan = 99%, 2640 rpm, 64°C], 29.057865 MH/s (103.01 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:00:17.945,  3 ms], [fan = 99%, 2644 rpm, 62°C], 28.903787 MH/s (102.47 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:00:46.915, 26 ms], [fan = 99%, 2607 rpm, 66°C], 28.674340 MH/s (102.07 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:07:42.301, 49 ms], [fan = 99%, 2705 rpm, 67°C], 27.436482 MH/s (101.37 W) = 346.230840 MH/s (1217.45 W)

<<< thread ID: 0x18b4, 2021.08.01 13:56:57.216, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014a31038","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:56:57.233, 2272 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:57:04.880, 7647 ms
{"id":0,"jsonrpc":"2.0","result":["0x33bd09d799c84f1a718952baef122946f02cdc3d64041f1435e07129846e30c3","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dc"]}

--- thread ID: 0x24b4, 2021.08.01 13:57:04.881
epoch = 431 (next epoch in 20516 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:57:08.098, 3217 ms
{"id":0,"jsonrpc":"2.0","result":["0xc01fd501e7c81848a0fc4dc6e235e1e6984c6b5e4366ce8732eb6a70d3932e28","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dd"]}

--- thread ID: 0x2610, 2021.08.01 13:57:08.098
epoch = 431 (next epoch in 20515 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:57:08.160, 61 ms
{"id":0,"jsonrpc":"2.0","result":["0x97a7d0944491fa23963a8300a466609205ff995e811f99e1e030f61545f2e445","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dd"]}

--- thread ID: 0x2768, 2021.08.01 13:57:08.160
epoch = 431 (next epoch in 20515 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:57:11.149, 2989 ms
{"id":0,"jsonrpc":"2.0","result":["0x50c839ff6ef757d0b5b4b38b83eab938d10f426f7a15cac13f7958701c360f8c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dd"]}

--- thread ID: 0x2648, 2021.08.01 13:57:11.149
epoch = 431 (next epoch in 20515 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:57:12.160, 1011 ms
{"id":0,"jsonrpc":"2.0","result":["0x019933dd00d145de3366192a143e11e35750e2785d1cb5d0a453e1ad4f619fe7","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dd"]}

--- thread ID: 0xedc, 2021.08.01 13:57:12.160
epoch = 431 (next epoch in 20515 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:57:12.228, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:09:30.744)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:00:24.162, 45 ms], [fan = 99%, 2924 rpm, 53°C], 29.210503 MH/s (100.92 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:03:53.633, 37 ms], [fan = 99%, 2603 rpm, 64°C], 29.200740 MH/s ( 99.89 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:01:37.502, 38 ms], [fan = 99%, 2658 rpm, 65°C], 28.910542 MH/s ( 99.54 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:00:29.193, 27 ms], [fan = 99%, 2651 rpm, 64°C], 29.206770 MH/s (102.01 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:05:09.973, 41 ms], [fan = 99%, 3331 rpm, 67°C], 28.906725 MH/s (100.05 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:02:26.328, 51 ms], [fan = 99%, 3233 rpm, 63°C], 29.209664 MH/s (101.80 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:06:40.558, 35 ms], [fan = 99%, 2566 rpm, 67°C], 28.658894 MH/s (102.15 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:00:39.770, 45 ms], [fan = 99%, 2688 rpm, 59°C], 28.653629 MH/s (102.10 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:00:25.982, 47 ms], [fan = 99%, 2656 rpm, 64°C], 29.157164 MH/s (102.75 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:00:32.961, 51 ms], [fan = 99%, 2649 rpm, 62°C], 29.195071 MH/s (102.78 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:01:01.931, 18 ms], [fan = 99%, 2622 rpm, 66°C], 28.684241 MH/s (103.43 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:07:57.317,  1 ms], [fan = 99%, 2689 rpm, 67°C], 27.625758 MH/s (100.88 W) = 346.619701 MH/s (1218.31 W)

<<< thread ID: 0x2628, 2021.08.01 13:57:12.233, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014a8ff35","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x1df0, 2021.08.01 13:57:12.248, 88 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:57:14.291, 2042 ms
{"id":0,"jsonrpc":"2.0","result":["0xbd49eb70f59b37a1ae0f8eea7d07c4b910ab99bbc7b97437b5415d5ea6d8f330","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dd"]}

--- thread ID: 0x18b4, 2021.08.01 13:57:14.291
epoch = 431 (next epoch in 20515 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:57:16.291, 1999 ms
{"id":0,"jsonrpc":"2.0","result":["0x4e6f2bccae7a8eedda55a2dfb04a5932457b3574006c5114047835d918e023dc","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570dd"]}

--- thread ID: 0x2630, 2021.08.01 13:57:16.291
epoch = 431 (next epoch in 20515 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:57:17.778, 1487 ms
{"id":0,"jsonrpc":"2.0","result":["0xea6ea8c8d1663a1ff7ff6ddb3f28a7fc53068c1de092fde3950945de10972fc0","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570de"]}

--- thread ID: 0x24b4, 2021.08.01 13:57:17.778
epoch = 431 (next epoch in 20514 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:57:17.843, 64 ms
{"id":0,"jsonrpc":"2.0","result":["0x4079ab3bfa33ae89dc6c783bf6406f423e4df2ed36d14abae0cfac68b6d7100a","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570de"]}

--- thread ID: 0x2610, 2021.08.01 13:57:17.843
epoch = 431 (next epoch in 20514 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:57:18.933, 1089 ms
{"id":0,"jsonrpc":"2.0","result":["0xa3fbb4d10c788c5baaebbdf9bbde3bc7994d171a8e922bcf31185c102c8af434","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570df"]}

--- thread ID: 0x2768, 2021.08.01 13:57:18.933
epoch = 431 (next epoch in 20513 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:57:19.004, 70 ms
{"id":0,"jsonrpc":"2.0","result":["0x1faeebd6cdb15cf60f2df14a2e6f0be6b72212da2bf917bcdcadd747c3c2ef8b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570df"]}

--- thread ID: 0x2648, 2021.08.01 13:57:19.004
epoch = 431 (next epoch in 20513 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:57:20.039, 1035 ms
{"id":0,"jsonrpc":"2.0","result":["0x64e658168b4801a00f8ddaf258929e887f2b620dbfb116e0dfbbed2bdb4eefcb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570df"]}

--- thread ID: 0xedc, 2021.08.01 13:57:20.039
epoch = 431 (next epoch in 20513 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:57:21.008, 969 ms
{"id":0,"jsonrpc":"2.0","result":["0x6c4957d348617dd3f0171a46ac5a5238a9745db755769826eea60c9c28cce243","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570df"]}

--- thread ID: 0x2628, 2021.08.01 13:57:21.008
epoch = 431 (next epoch in 20513 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:57:23.243, 2235 ms
{"id":0,"jsonrpc":"2.0","result":["0x8370f36e8fc76e58381806725ed655101982e470ba3f83dd3228211d1f5668f3","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570df"]}

--- thread ID: 0x1df0, 2021.08.01 13:57:23.243
epoch = 431 (next epoch in 20513 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:57:24.220, 976 ms
{"id":0,"jsonrpc":"2.0","result":["0x0dd7d96a0557289c8b63daaa93280d2fcc3a4a7ad3bed3328742d26b2d5b7f44","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570df"]}

--- thread ID: 0x18b4, 2021.08.01 13:57:24.220
epoch = 431 (next epoch in 20513 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:57:27.259, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:09:45.774)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:00:39.193, 34 ms], [fan = 99%, 2918 rpm, 53°C], 29.204457 MH/s (100.85 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:04:08.664, 63 ms], [fan = 99%, 2599 rpm, 64°C], 29.201431 MH/s (100.00 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:01:52.532, 54 ms], [fan = 99%, 2662 rpm, 65°C], 28.656561 MH/s ( 99.60 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:00:44.223, 18 ms], [fan = 99%, 2663 rpm, 64°C], 29.203665 MH/s (102.01 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:05:25.003, 18 ms], [fan = 99%, 3343 rpm, 67°C], 28.736632 MH/s ( 98.40 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:02:41.359, 46 ms], [fan = 99%, 3268 rpm, 63°C], 29.199112 MH/s (101.73 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:06:55.588,  0 ms], [fan = 99%, 2554 rpm, 67°C], 28.787763 MH/s (102.47 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:00:54.800, 60 ms], [fan = 99%, 2664 rpm, 59°C], 28.688916 MH/s (101.86 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:00:41.013, 37 ms], [fan = 99%, 2632 rpm, 64°C], 29.205475 MH/s (102.93 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:00:47.992, 44 ms], [fan = 99%, 2629 rpm, 62°C], 29.206278 MH/s (102.68 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:01:16.961, 60 ms], [fan = 99%, 2630 rpm, 66°C], 28.676376 MH/s (102.80 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:08:12.348, 11 ms], [fan = 99%, 2689 rpm, 67°C], 27.405693 MH/s (100.84 W) = 346.172359 MH/s (1216.18 W)

<<< thread ID: 0x2630, 2021.08.01 13:57:27.263, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014a22bc7","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:57:27.279, 3059 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2610, 2021.08.01 13:57:27.811, 532 ms
{"id":0,"jsonrpc":"2.0","result":["0x22de1762fb8467c167435e736873ba4f62461c632217385b2ed059a05681880f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e0"]}

--- thread ID: 0x2610, 2021.08.01 13:57:27.811
epoch = 431 (next epoch in 20512 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:57:27.889, 77 ms
{"id":0,"jsonrpc":"2.0","result":["0x19c40e2ca714c1556fe2a2d32e441656528dc35c5e206a9b867408f047412565","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e0"]}

--- thread ID: 0x2768, 2021.08.01 13:57:27.889
epoch = 431 (next epoch in 20512 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:57:28.852, 962 ms
{"id":0,"jsonrpc":"2.0","result":["0x5c4618ae5c699d39da41d5ab169d818a999a41d4bc52fa2d7c4863b9f786e466","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e0"]}

--- thread ID: 0x2648, 2021.08.01 13:57:28.852
epoch = 431 (next epoch in 20512 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:57:32.055, 3202 ms
{"id":0,"jsonrpc":"2.0","result":["0x3c5c146e29fd617bcf5969e4afaf4f3ba29dbf52943d9de01a5b2bc1e20d8233","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e0"]}

--- thread ID: 0xedc, 2021.08.01 13:57:32.055
epoch = 431 (next epoch in 20512 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:57:35.947, 3892 ms
{"id":0,"jsonrpc":"2.0","result":["0x917025c7d24f9c8d6fbffae86f4d860f1887c1f4227b34cf2557a165d5e78725","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e0"]}

--- thread ID: 0x2628, 2021.08.01 13:57:35.947
epoch = 431 (next epoch in 20512 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:57:37.517, 1569 ms
{"id":0,"jsonrpc":"2.0","result":["0x4866a4fe8e01c09d69f419d6d6ab29012f59afb918bf33137580fc270005d5a7","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e1"]}

--- thread ID: 0x1df0, 2021.08.01 13:57:37.517
epoch = 431 (next epoch in 20511 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:57:37.581, 63 ms
{"id":0,"jsonrpc":"2.0","result":["0x1ada981dd72f5703e3aa0858a6f8a7527be01b1c0bf1ba2bafc6296601a3e082","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e1"]}

--- thread ID: 0x18b4, 2021.08.01 13:57:37.581
epoch = 431 (next epoch in 20511 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:57:42.260, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:10:00.775)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:00:54.194, 69 ms], [fan = 99%, 2938 rpm, 53°C], 29.184616 MH/s (100.09 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:04:23.665, 22 ms], [fan = 99%, 2596 rpm, 64°C], 29.208205 MH/s (100.24 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:02:07.534,  1 ms], [fan = 99%, 2654 rpm, 66°C], 29.209889 MH/s (100.56 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:00:59.225, 12 ms], [fan = 99%, 2667 rpm, 65°C], 29.201042 MH/s (102.17 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 4, S = 0, R = 0, I = 0], [00:05:40.005, 49 ms], [fan = 99%, 3319 rpm, 67°C], 29.106316 MH/s (100.21 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:02:56.360, 49 ms], [fan = 99%, 3265 rpm, 63°C], 29.207385 MH/s (101.84 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:07:10.589,  3 ms], [fan = 99%, 2535 rpm, 68°C], 29.209375 MH/s (103.45 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:01:09.801, 24 ms], [fan = 99%, 2680 rpm, 59°C], 29.210767 MH/s (102.88 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:00:56.014,  0 ms], [fan = 99%, 2640 rpm, 64°C], 29.210017 MH/s (103.09 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:01:02.993, 31 ms], [fan = 99%, 2644 rpm, 62°C], 28.883275 MH/s (101.89 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:01:31.963, 36 ms], [fan = 99%, 2599 rpm, 66°C], 28.677035 MH/s (102.39 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:08:27.349, 69 ms], [fan = 99%, 2709 rpm, 67°C], 27.490204 MH/s (101.86 W) = 347.798126 MH/s (1220.64 W)

<<< thread ID: 0x2630, 2021.08.01 13:57:42.265, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014bafa6e","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x24b4, 2021.08.01 13:57:42.280, 4699 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0x4e8, 2021.08.01 13:57:43.428, PCIe: 00000000:0d:00.0, GPU.05 share found (search channel 0).
 nonce: 0x13d0a84c122c6a5c
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000000fba167dc7fba479a94a538f3437c8fba0cb4d2913ecfd5d1255db92
   mix: 0x9f95e688b31db8351c6600ff94e439552b22266d99d7872c00d7ef6f400a7ad9

<<< thread ID: 0x2610, 2021.08.01 13:57:43.428, 0 ms
{"jsonrpc":"2.0","id":1044,"method":"eth_submitWork","params":["0x13d0a84c122c6a5c","0x1ada981dd72f5703e3aa0858a6f8a7527be01b1c0bf1ba2bafc6296601a3e082","0x9f95e688b31db8351c6600ff94e439552b22266d99d7872c00d7ef6f400a7ad9"],"worker":"alphagruis"}

--- thread ID: 0x2768, 2021.08.01 13:57:43.443, PCIe: 00000000:0d:00.0, GPU.05 share accepted.

>>> thread ID: 0x2768, 2021.08.01 13:57:43.443, 1162 ms (14 ms)
{"id":1044,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:57:43.599, 155 ms
{"id":0,"jsonrpc":"2.0","result":["0x0671f0d1f669182308d24de33c989fc57bc45fe3186e1e322b4e21df073dcb62","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e1"]}

--- thread ID: 0x2648, 2021.08.01 13:57:43.599
epoch = 431 (next epoch in 20511 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:57:47.651, 4052 ms
{"id":0,"jsonrpc":"2.0","result":["0xd27d6007011f964044fc85e7926aa2e44d1d147f5632e2e5bea3d2e5eaa67f72","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e1"]}

--- thread ID: 0xedc, 2021.08.01 13:57:47.651
epoch = 431 (next epoch in 20511 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:57:48.874, 1222 ms
{"id":0,"jsonrpc":"2.0","result":["0xc12fffa35389a5590ed6b5c3f5204c93cec3ef7150a0bf6075b2b02fa762d6e8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e2"]}

--- thread ID: 0x2628, 2021.08.01 13:57:48.874
epoch = 431 (next epoch in 20510 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:57:49.051, 176 ms
{"id":0,"jsonrpc":"2.0","result":["0x9f79494c97bbdad6976082d72df28900faa5951befc415e08997e24be7adc153","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e2"]}

--- thread ID: 0x1df0, 2021.08.01 13:57:49.051
epoch = 431 (next epoch in 20510 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:57:51.889, 2837 ms
{"id":0,"jsonrpc":"2.0","result":["0xe571b440fc6616333e01f6cfb9f88ff1a3cb203006a0933c672e9536b1c2bba8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e2"]}

--- thread ID: 0x18b4, 2021.08.01 13:57:51.889
epoch = 431 (next epoch in 20510 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:57:51.956, 67 ms
{"id":0,"jsonrpc":"2.0","result":["0x3d5fa3ad2054d7877ecdda63c84782be81894da8fbbb06f2a85edeedd2ae3972","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e2"]}

--- thread ID: 0x2630, 2021.08.01 13:57:51.956
epoch = 431 (next epoch in 20510 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:57:52.876, 919 ms
{"id":0,"jsonrpc":"2.0","result":["0x9ee59e945e64a80024928ff2375142b32f2d086ddce4abdf338fa13a3439a99b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e2"]}

--- thread ID: 0x24b4, 2021.08.01 13:57:52.876
epoch = 431 (next epoch in 20510 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:57:57.290, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:10:15.805)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:01:09.224, 44 ms], [fan = 99%, 2968 rpm, 53°C], 28.856713 MH/s ( 99.70 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:04:38.695, 10 ms], [fan = 99%, 2611 rpm, 64°C], 29.205805 MH/s ( 99.96 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:02:22.563, 12 ms], [fan = 99%, 2658 rpm, 66°C], 29.219172 MH/s (100.45 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:01:14.254, 12 ms], [fan = 99%, 2663 rpm, 65°C], 29.218748 MH/s (102.11 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 5, S = 0, R = 0, I = 0], [00:00:13.862, 23 ms], [fan = 99%, 3356 rpm, 68°C], 28.674363 MH/s ( 99.79 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:03:11.390, 58 ms], [fan = 99%, 3297 rpm, 63°C], 28.997028 MH/s (101.55 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:07:25.619,  0 ms], [fan = 99%, 2547 rpm, 68°C], 29.191641 MH/s (103.43 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:01:24.831, 13 ms], [fan = 99%, 2672 rpm, 60°C], 29.205340 MH/s (102.86 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:01:11.044, 12 ms], [fan = 99%, 2644 rpm, 64°C], 29.221100 MH/s (102.89 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:01:18.023, 65 ms], [fan = 99%, 2648 rpm, 62°C], 28.740038 MH/s (102.11 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:01:46.992, 49 ms], [fan = 99%, 2626 rpm, 67°C], 29.169885 MH/s (103.44 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:08:42.379,  0 ms], [fan = 99%, 2697 rpm, 67°C], 27.386275 MH/s (101.75 W) = 347.086108 MH/s (1220.03 W)

<<< thread ID: 0x2610, 2021.08.01 13:57:57.294, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b01d1c","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2768, 2021.08.01 13:57:57.310, 4434 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:57:57.903, 592 ms
{"id":0,"jsonrpc":"2.0","result":["0xb5784e45f95662d547fd101054e36f2f7fdb62271f3f37c01755cb0c41b1b5f2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e2"]}

--- thread ID: 0x2648, 2021.08.01 13:57:57.903
epoch = 431 (next epoch in 20510 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:58:02.014, 4111 ms
{"id":0,"jsonrpc":"2.0","result":["0x1c1245017ec0f19b4e672d29778b334fd2edb69db723c4636463b117e0e32197","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e2"]}

--- thread ID: 0xedc, 2021.08.01 13:58:02.014
epoch = 431 (next epoch in 20510 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:58:02.743, 728 ms
{"id":0,"jsonrpc":"2.0","result":["0x1b56782e99e659552836a0d6c220f67b01482fbed5b7d5fc8d2fe3e7d27fff9f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e3"]}

--- thread ID: 0x2628, 2021.08.01 13:58:02.743
epoch = 431 (next epoch in 20509 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:58:02.871, 128 ms
{"id":0,"jsonrpc":"2.0","result":["0x94d4c3944519e851072344de1ee6b7f6467f3dee5989f5fdb7a87fbf4c98ae5b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e3"]}

--- thread ID: 0x1df0, 2021.08.01 13:58:02.871
epoch = 431 (next epoch in 20509 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:58:05.132, 2260 ms
{"id":0,"jsonrpc":"2.0","result":["0xd2e685178862f1256568791af89ceb4c2a1ec63e9d2467385b4dfe6b145f570f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e4"]}

--- thread ID: 0x18b4, 2021.08.01 13:58:05.132
epoch = 431 (next epoch in 20508 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:58:05.272, 139 ms
{"id":0,"jsonrpc":"2.0","result":["0x21b3aa0b043528f1f371874f75e04e547a02f4079a13ea051d4ec65d4be71260","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e4"]}

--- thread ID: 0x2630, 2021.08.01 13:58:05.272
epoch = 431 (next epoch in 20508 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:58:08.238, 2966 ms
{"id":0,"jsonrpc":"2.0","result":["0xe4a5dc01c4ebb1ea73fe5ba97b5f74f38c6e4911b13efb326a6fd6ea036ec88b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e4"]}

--- thread ID: 0x24b4, 2021.08.01 13:58:08.238
epoch = 431 (next epoch in 20508 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:58:12.263, 4024 ms
{"id":0,"jsonrpc":"2.0","result":["0x6b69cb0ebfc3a15f97cc75d760d6601420b222570716b571e6a237f2f9b512d5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e4"]}

--- thread ID: 0x2610, 2021.08.01 13:58:12.263
epoch = 431 (next epoch in 20508 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:58:12.307, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:10:30.822)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:01:24.241, 37 ms], [fan = 99%, 2916 rpm, 53°C], 28.901150 MH/s ( 99.71 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:04:53.711, 62 ms], [fan = 99%, 2599 rpm, 64°C], 29.194490 MH/s (100.06 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:02:37.580, 30 ms], [fan = 99%, 2654 rpm, 66°C], 29.207879 MH/s (100.69 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:01:29.271, 14 ms], [fan = 99%, 2650 rpm, 65°C], 29.214505 MH/s (101.90 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 5, S = 0, R = 0, I = 0], [00:00:28.878, 58 ms], [fan = 99%, 3337 rpm, 67°C], 28.734708 MH/s ( 99.74 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:03:26.406,  0 ms], [fan = 99%, 3237 rpm, 63°C], 29.180845 MH/s (101.98 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:07:40.636, 28 ms], [fan = 99%, 2539 rpm, 68°C], 28.913703 MH/s (102.02 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:01:39.848,  0 ms], [fan = 99%, 2660 rpm, 60°C], 29.188262 MH/s (103.06 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:01:26.061, 29 ms], [fan = 99%, 2640 rpm, 64°C], 29.211955 MH/s (102.88 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:01:33.040, 58 ms], [fan = 99%, 2644 rpm, 62°C], 28.878492 MH/s (102.78 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 6, S = 0, R = 0, I = 0], [00:02:02.009, 42 ms], [fan = 99%, 2622 rpm, 67°C], 28.661129 MH/s (102.11 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:08:57.396,  2 ms], [fan = 99%, 2705 rpm, 67°C], 27.536572 MH/s (101.77 W) = 346.823690 MH/s (1218.70 W)

<<< thread ID: 0x2768, 2021.08.01 13:58:12.311, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014ac1c0a","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2648, 2021.08.01 13:58:12.328, 65 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0x18c8, 2021.08.01 13:58:14.904, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 0).
 nonce: 0x13d0a84e9ceb21c5
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000f497dacaec8868edbdd13eec19fd6a8c2265f57ad8d44508e54007e1
   mix: 0x2acf5cf23da7832c47756ee18edd5f8c259f5b498aa9d62dbe11fde0d6bd7fa8

<<< thread ID: 0xedc, 2021.08.01 13:58:14.904, 0 ms
{"jsonrpc":"2.0","id":1045,"method":"eth_submitWork","params":["0x13d0a84e9ceb21c5","0x6b69cb0ebfc3a15f97cc75d760d6601420b222570716b571e6a237f2f9b512d5","0x2acf5cf23da7832c47756ee18edd5f8c259f5b498aa9d62dbe11fde0d6bd7fa8"],"worker":"alphagruis"}

--- thread ID: 0x2628, 2021.08.01 13:58:14.921, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0x2628, 2021.08.01 13:58:14.921, 2592 ms (16 ms)
{"id":1045,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 13:58:16.252, 1330 ms
{"id":0,"jsonrpc":"2.0","result":["0xb9810b862c6b436090bafa22943e8acb666e7bfe40dfc98515c2d21b43fc58f8","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e4"]}

--- thread ID: 0x1df0, 2021.08.01 13:58:16.252
epoch = 431 (next epoch in 20508 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:58:17.251, 998 ms
{"id":0,"jsonrpc":"2.0","result":["0xe97aa0546200f0ad365de31817fee82f3347b56cc3634a4a901738f80d02f2eb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e4"]}

--- thread ID: 0x18b4, 2021.08.01 13:58:17.251
epoch = 431 (next epoch in 20508 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:58:19.536, 2285 ms
{"id":0,"jsonrpc":"2.0","result":["0xc011c71d9dc4649a099ade50a26101a1b6744da07cab5176adcaaec775c6920b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e4"]}

--- thread ID: 0x2630, 2021.08.01 13:58:19.536
epoch = 431 (next epoch in 20508 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:58:19.618, 82 ms
{"id":0,"jsonrpc":"2.0","result":["0x4acb012f70abd0c51cd0a1fc8a7aafc3449654209e46433aab61a5440f1dedcb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e5"]}

--- thread ID: 0x24b4, 2021.08.01 13:58:19.618
epoch = 431 (next epoch in 20507 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:58:19.873, 255 ms
{"id":0,"jsonrpc":"2.0","result":["0xbcfc1e0e2aab0a528d79fd87560e560c6d0b5b101db2721f0dde138ce82acf90","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e5"]}

--- thread ID: 0x2610, 2021.08.01 13:58:19.874
epoch = 431 (next epoch in 20507 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:58:21.710, 1836 ms
{"id":0,"jsonrpc":"2.0","result":["0x38a7d9cb0ca770043f9d8e63d1e6147299cc67bda0842458f0dfd56a54479d8b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e5"]}

--- thread ID: 0x2768, 2021.08.01 13:58:21.710
epoch = 431 (next epoch in 20507 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:58:22.702, 992 ms
{"id":0,"jsonrpc":"2.0","result":["0x8139dd790f020539958c7c9baa64a3aa6a042d85ab99586017d6f8a89f3b151b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e5"]}

--- thread ID: 0x2648, 2021.08.01 13:58:22.702
epoch = 431 (next epoch in 20507 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:58:23.437, 734 ms
{"id":0,"jsonrpc":"2.0","result":["0xfea471b095741661f8edb062156eafb93fff15d52968e4baec815e9658a64fa0","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0xedc, 2021.08.01 13:58:23.437
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:58:23.506, 69 ms
{"id":0,"jsonrpc":"2.0","result":["0xd0cbe8ad8354fdaa88cf8da55353f5396c09a5b04e52b23946bd1ee963dc0601","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x2628, 2021.08.01 13:58:23.507
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:58:25.667, 2160 ms
{"id":0,"jsonrpc":"2.0","result":["0xe817588eeef4f3125f4fd729ed0e58ac4b567082ab886652f342005701536ab1","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x1df0, 2021.08.01 13:58:25.667
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:58:27.337, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:10:45.853)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:01:39.271, 28 ms], [fan = 99%, 2932 rpm, 53°C], 28.646307 MH/s ( 99.95 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:05:08.742, 52 ms], [fan = 99%, 2607 rpm, 65°C], 29.203843 MH/s (100.21 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:02:52.611, 20 ms], [fan = 99%, 2650 rpm, 66°C], 29.198229 MH/s (100.53 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:01:44.302,  0 ms], [fan = 99%, 2655 rpm, 65°C], 29.216609 MH/s (101.75 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 5, S = 0, R = 0, I = 0], [00:00:43.909, 34 ms], [fan = 99%, 3288 rpm, 68°C], 28.609236 MH/s ( 99.00 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:03:41.437,  3 ms], [fan = 99%, 3237 rpm, 63°C], 28.662302 MH/s (100.93 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:07:55.667, 15 ms], [fan = 99%, 2543 rpm, 68°C], 29.126203 MH/s (103.37 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:01:54.879, 55 ms], [fan = 99%, 2648 rpm, 60°C], 29.206582 MH/s (102.70 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:01:41.091, 20 ms], [fan = 99%, 2644 rpm, 64°C], 29.202097 MH/s (102.88 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:01:48.071, 16 ms], [fan = 99%, 2636 rpm, 62°C], 29.172623 MH/s (102.79 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 7, S = 0, R = 0, I = 0], [00:00:12.433, 41 ms], [fan = 99%, 2638 rpm, 67°C], 28.668550 MH/s (102.58 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:09:12.426, 14 ms], [fan = 99%, 2701 rpm, 67°C], 27.342727 MH/s (100.82 W) = 346.255308 MH/s (1217.52 W)

<<< thread ID: 0x18b4, 2021.08.01 13:58:27.342, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014a36fcc","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:58:27.357, 1690 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:58:27.526, 168 ms
{"id":0,"jsonrpc":"2.0","result":["0x963b2b13b1287d81a8517c357eac2dc2179cd7b71786e7d1810895f20033be60","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x24b4, 2021.08.01 13:58:27.526
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:58:29.509, 1983 ms
{"id":0,"jsonrpc":"2.0","result":["0x111dca58bec5609b64b97e3840e1d5d2dfc57a9d7253c04e29533e15c595ed56","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x2610, 2021.08.01 13:58:29.509
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:58:34.517, 5008 ms
{"id":0,"jsonrpc":"2.0","result":["0x26e4843c79b895a8d9a78bb74c74aa2a9d04231c7679841a795633510fd0c078","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x2768, 2021.08.01 13:58:34.517
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:58:42.352, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:11:00.867)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:01:54.286, 16 ms], [fan = 99%, 2926 rpm, 54°C], 28.678057 MH/s (100.05 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:05:23.756, 10 ms], [fan = 99%, 2592 rpm, 64°C], 29.167036 MH/s ( 99.20 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:03:07.625,  0 ms], [fan = 99%, 2665 rpm, 66°C], 29.196517 MH/s (100.64 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:01:59.316, 26 ms], [fan = 99%, 2638 rpm, 65°C], 28.652942 MH/s (101.01 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 5, S = 0, R = 0, I = 0], [00:00:58.923, 12 ms], [fan = 99%, 3322 rpm, 68°C], 28.668225 MH/s ( 99.17 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:03:56.452, 31 ms], [fan = 99%, 3325 rpm, 63°C], 28.781732 MH/s (102.03 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:08:10.681, 69 ms], [fan = 99%, 2558 rpm, 68°C], 28.671369 MH/s (102.42 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:02:09.893, 31 ms], [fan = 99%, 2668 rpm, 60°C], 29.191093 MH/s (102.98 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:01:56.106,  0 ms], [fan = 99%, 2620 rpm, 64°C], 29.198853 MH/s (102.84 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:02:03.085, 12 ms], [fan = 99%, 2652 rpm, 63°C], 29.011104 MH/s (103.06 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 7, S = 0, R = 0, I = 0], [00:00:27.447, 27 ms], [fan = 99%, 2622 rpm, 67°C], 28.661344 MH/s (102.82 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:09:27.441, 21 ms], [fan = 99%, 2701 rpm, 67°C], 27.311017 MH/s (100.95 W) = 345.189289 MH/s (1217.16 W)

<<< thread ID: 0x2648, 2021.08.01 13:58:42.356, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014932ba9","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0xedc, 2021.08.01 13:58:42.374, 7856 ms (17 ms)
{"id":13,"jsonrpc":"2.0","result":true}

--- thread ID: 0x4e8, 2021.08.01 13:58:42.633, PCIe: 00000000:0d:00.0, GPU.05 share found (search channel 1).
 nonce: 0x13d0a850d8306c20
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x00000000db551de79d9d3ce216d3beb44b8902f46ed70bf19e0fb8bc1206c159
   mix: 0x78256bd0acae4cb22b621f8307bf8ae4cc81b3f4e32139d9f21dea1eaad01343

<<< thread ID: 0x2628, 2021.08.01 13:58:42.633, 0 ms
{"jsonrpc":"2.0","id":1046,"method":"eth_submitWork","params":["0x13d0a850d8306c20","0x26e4843c79b895a8d9a78bb74c74aa2a9d04231c7679841a795633510fd0c078","0x78256bd0acae4cb22b621f8307bf8ae4cc81b3f4e32139d9f21dea1eaad01343"],"worker":"alphagruis"}

--- thread ID: 0x1df0, 2021.08.01 13:58:42.648, PCIe: 00000000:0d:00.0, GPU.05 share accepted.

>>> thread ID: 0x1df0, 2021.08.01 13:58:42.648, 274 ms (15 ms)
{"id":1046,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:58:45.526, 2878 ms
{"id":0,"jsonrpc":"2.0","result":["0xc8d959f118d580bf407af038a4a65cd87cd13df3347754618b54c35259c1a551","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x18b4, 2021.08.01 13:58:45.527
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:58:47.530, 2003 ms
{"id":0,"jsonrpc":"2.0","result":["0x140ac2fb15cd6cde0aff54d388ca332cf983e7bceae9c0d0a808370d4646f41f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x2630, 2021.08.01 13:58:47.530
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:58:49.574, 2043 ms
{"id":0,"jsonrpc":"2.0","result":["0x1ea72a3f75c3b3b46bbb6bfeefe7615fa00c852d91dabca43208722571237135","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e6"]}

--- thread ID: 0x24b4, 2021.08.01 13:58:49.574
epoch = 431 (next epoch in 20506 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:58:50.333, 759 ms
{"id":0,"jsonrpc":"2.0","result":["0x533e62d3e5370c036a465751d6808a45d759f963a3158d025362b193138ad9d4","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e7"]}

--- thread ID: 0x2610, 2021.08.01 13:58:50.333
epoch = 431 (next epoch in 20505 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:58:50.720, 387 ms
{"id":0,"jsonrpc":"2.0","result":["0x9d229bdd118a5c5a566d1369e2f71001945889858738788479b13884dc409955","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e7"]}

--- thread ID: 0x2768, 2021.08.01 13:58:50.720
epoch = 431 (next epoch in 20505 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:58:50.751, 30 ms
{"id":0,"jsonrpc":"2.0","result":["0x712aea4e6544c69eb0dad3df6df9d9e1616bc3037d4b13a2ff183b4bdb795b4d","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e7"]}

--- thread ID: 0x2648, 2021.08.01 13:58:50.751
epoch = 431 (next epoch in 20505 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:58:53.481, 2729 ms
{"id":0,"jsonrpc":"2.0","result":["0xa51d486c11dc0ffe283b1185e89c760cfe8bbbe24574234c4c300effb3be8d4c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e7"]}

--- thread ID: 0xedc, 2021.08.01 13:58:53.481
epoch = 431 (next epoch in 20505 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:58:57.368, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:11:15.883)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:02:09.302,  4 ms], [fan = 99%, 2922 rpm, 53°C], 29.214741 MH/s (100.98 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:05:38.773,  1 ms], [fan = 99%, 2611 rpm, 64°C], 28.641132 MH/s ( 98.89 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:03:22.641, 18 ms], [fan = 99%, 2657 rpm, 66°C], 29.216424 MH/s (100.79 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:02:14.332, 61 ms], [fan = 99%, 2667 rpm, 65°C], 28.753082 MH/s (101.31 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 6, S = 0, R = 0, I = 0], [00:00:14.735, 41 ms], [fan = 99%, 3317 rpm, 68°C], 28.785213 MH/s (100.14 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:04:11.468, 13 ms], [fan = 99%, 3228 rpm, 63°C], 29.167601 MH/s (101.82 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:08:25.697, 41 ms], [fan = 99%, 2550 rpm, 68°C], 28.616522 MH/s (102.52 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:02:24.909, 10 ms], [fan = 99%, 2668 rpm, 60°C], 29.210074 MH/s (102.88 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:02:11.122, 17 ms], [fan = 99%, 2648 rpm, 64°C], 29.214721 MH/s (102.96 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 4, S = 0, R = 0, I = 0], [00:02:18.101, 45 ms], [fan = 99%, 2628 rpm, 62°C], 28.719880 MH/s (102.13 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 7, S = 0, R = 0, I = 0], [00:00:42.464, 39 ms], [fan = 99%, 2610 rpm, 67°C], 28.711379 MH/s (103.52 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:09:42.457, 62 ms], [fan = 99%, 2705 rpm, 67°C], 27.411136 MH/s (101.91 W) = 345.661905 MH/s (1219.85 W)

<<< thread ID: 0x2628, 2021.08.01 13:58:57.372, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x00000000000000000000000000000000000000000000000000000000149a61d1","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x1df0, 2021.08.01 13:58:57.390, 3909 ms (18 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:58:57.755, 364 ms
{"id":0,"jsonrpc":"2.0","result":["0xbb5b0c74ea746ec59a2b611b2cd4135edfd233971854b3eb57c91fafde72763f","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e7"]}

--- thread ID: 0x18b4, 2021.08.01 13:58:57.755
epoch = 431 (next epoch in 20505 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:59:05.547, 7791 ms
{"id":0,"jsonrpc":"2.0","result":["0xb41e475b5984ecffd271c6280fb954639af0af738399607f11bf260bdd3f2d8d","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e7"]}

--- thread ID: 0x2630, 2021.08.01 13:59:05.547
epoch = 431 (next epoch in 20505 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x23a0, 2021.08.01 13:59:06.539, PCIe: 00000000:01:00.0, GPU.10 share found (search channel 1).
 nonce: 0x13d0a852c522a796
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000000346d5a93e72a0f226f5718696a61acf8debe5695b69618692915400
   mix: 0x125dad6ae22432d4ffb956ca400d79eba5690320ba1d41f2d596667eeb716dc2

<<< thread ID: 0x24b4, 2021.08.01 13:59:06.539, 0 ms
{"jsonrpc":"2.0","id":1047,"method":"eth_submitWork","params":["0x13d0a852c522a796","0xb41e475b5984ecffd271c6280fb954639af0af738399607f11bf260bdd3f2d8d","0x125dad6ae22432d4ffb956ca400d79eba5690320ba1d41f2d596667eeb716dc2"],"worker":"alphagruis"}

--- thread ID: 0x2610, 2021.08.01 13:59:06.555, PCIe: 00000000:01:00.0, GPU.10 share accepted.

>>> thread ID: 0x2610, 2021.08.01 13:59:06.555, 1007 ms (16 ms)
{"id":1047,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2768, 2021.08.01 13:59:09.821, 3265 ms
{"id":0,"jsonrpc":"2.0","result":["0xd79721b9f1b9a22594cbc090d5e9372c97f1c042cb087808a414513b0ab3e844","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e8"]}

--- thread ID: 0x2768, 2021.08.01 13:59:09.821
epoch = 431 (next epoch in 20504 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 13:59:09.949, 128 ms
{"id":0,"jsonrpc":"2.0","result":["0xcef6f0ea1adf0f2b89e7392f261622e0475dc6b8cca89950f284f3c8c8f48a77","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e8"]}

--- thread ID: 0x2648, 2021.08.01 13:59:09.949
epoch = 431 (next epoch in 20504 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:59:12.384, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:11:30.900)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:02:24.318, 50 ms], [fan = 99%, 2931 rpm, 53°C], 29.211234 MH/s (101.00 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:05:53.789, 17 ms], [fan = 99%, 2595 rpm, 64°C], 28.746788 MH/s ( 99.88 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:03:37.658, 25 ms], [fan = 99%, 2657 rpm, 66°C], 29.206263 MH/s (100.84 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:02:29.349,  0 ms], [fan = 99%, 2671 rpm, 65°C], 29.211603 MH/s (101.96 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 6, S = 0, R = 0, I = 0], [00:00:29.752, 14 ms], [fan = 99%, 3324 rpm, 68°C], 29.193769 MH/s (100.10 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 3, S = 0, R = 0, I = 0], [00:04:26.484,  0 ms], [fan = 99%, 3249 rpm, 63°C], 29.210713 MH/s (101.83 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:08:40.714,  2 ms], [fan = 99%, 2539 rpm, 68°C], 28.609280 MH/s (102.59 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:02:39.926, 59 ms], [fan = 99%, 2664 rpm, 60°C], 29.200289 MH/s (102.75 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:02:26.138, 20 ms], [fan = 99%, 2636 rpm, 65°C], 29.195383 MH/s (102.82 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 5, S = 0, R = 0, I = 0], [00:00:05.846, 17 ms], [fan = 99%, 2644 rpm, 62°C], 29.058257 MH/s (102.45 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 7, S = 0, R = 0, I = 0], [00:00:57.480, 49 ms], [fan = 99%, 2633 rpm, 67°C], 28.813561 MH/s (102.45 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:09:57.473, 16 ms], [fan = 99%, 2697 rpm, 67°C], 27.236378 MH/s (101.18 W) = 346.893518 MH/s (1219.84 W)

<<< thread ID: 0xedc, 2021.08.01 13:59:12.389, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014ad2cce","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2628, 2021.08.01 13:59:12.404, 2455 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 13:59:14.085, 1680 ms
{"id":0,"jsonrpc":"2.0","result":["0x44db24d6bfaeb122a7c7bbcc2022062f836bfb7c34241c94ef3ba406ab5c4986","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e8"]}

--- thread ID: 0x1df0, 2021.08.01 13:59:14.085
epoch = 431 (next epoch in 20504 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:59:15.946, 1861 ms
{"id":0,"jsonrpc":"2.0","result":["0x34f48ddae9ea837aa7e61e126a1be87025a3c29e3284b430925b24264e3c243e","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e8"]}

--- thread ID: 0x18b4, 2021.08.01 13:59:15.946
epoch = 431 (next epoch in 20504 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:59:16.892, 945 ms
{"id":0,"jsonrpc":"2.0","result":["0x711dce00945097c3397580f22d35f5058507d7a1e048a06d0c773496d7655a57","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e8"]}

--- thread ID: 0x2630, 2021.08.01 13:59:16.892
epoch = 431 (next epoch in 20504 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:59:19.963, 3071 ms
{"id":0,"jsonrpc":"2.0","result":["0xef502040c74dcd3745c6486d806123e6483b45b4fc9ca93c16449269250d3c73","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e8"]}

--- thread ID: 0x24b4, 2021.08.01 13:59:19.963
epoch = 431 (next epoch in 20504 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x10c4, 2021.08.01 13:59:20.010, PCIe: 00000000:02:00.0, GPU.06 share found (search channel 1, stale: 46 ms of delay).
 nonce: 0x13d0a853dbe2f257
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000004c65b97eb974585345875c2d3a772aa38aef48baccf53532f8851b24
   mix: 0x0be158963643ce43496d7e88a41d8955b6ae6317d845acade0dda68331b070bf

<<< thread ID: 0x2610, 2021.08.01 13:59:20.010, 0 ms
{"jsonrpc":"2.0","id":1048,"method":"eth_submitWork","params":["0x13d0a853dbe2f257","0x711dce00945097c3397580f22d35f5058507d7a1e048a06d0c773496d7655a57","0x0be158963643ce43496d7e88a41d8955b6ae6317d845acade0dda68331b070bf"],"worker":"alphagruis"}

--- thread ID: 0x2768, 2021.08.01 13:59:20.027, PCIe: 00000000:02:00.0, GPU.06 share accepted.

>>> thread ID: 0x2768, 2021.08.01 13:59:20.027, 63 ms (16 ms)
{"id":1048,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2648, 2021.08.01 13:59:21.495, 1468 ms
{"id":0,"jsonrpc":"2.0","result":["0x640623b317f5ba23200ec63db02686322721f3da56a2b8ff2a9a0f27e4774a66","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e9"]}

--- thread ID: 0x2648, 2021.08.01 13:59:21.496
epoch = 431 (next epoch in 20503 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0xedc, 2021.08.01 13:59:21.835, 339 ms
{"id":0,"jsonrpc":"2.0","result":["0x6b380cb41dbf6c8a06ee3a56c28e7d24efc24abd859ea0f0391f146bda10d8ac","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e9"]}

--- thread ID: 0xedc, 2021.08.01 13:59:21.835
epoch = 431 (next epoch in 20503 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x18c8, 2021.08.01 13:59:22.480, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 0).
 nonce: 0x13d0a8540f21efec
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x0000000087775ce7f543d2462e74bdecc0262f42c3f474d54ed4d09ec9f6ec7a
   mix: 0x7fb1a8409ad314a1ad4dfa8c98603c60efec6acc8163502bd0f41c60039afc12

<<< thread ID: 0x2628, 2021.08.01 13:59:22.480, 0 ms
{"jsonrpc":"2.0","id":1049,"method":"eth_submitWork","params":["0x13d0a8540f21efec","0x6b380cb41dbf6c8a06ee3a56c28e7d24efc24abd859ea0f0391f146bda10d8ac","0x7fb1a8409ad314a1ad4dfa8c98603c60efec6acc8163502bd0f41c60039afc12"],"worker":"alphagruis"}

--- thread ID: 0x1df0, 2021.08.01 13:59:22.496, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0x1df0, 2021.08.01 13:59:22.496, 660 ms (15 ms)
{"id":1049,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x18b4, 2021.08.01 13:59:23.671, 1175 ms
{"id":0,"jsonrpc":"2.0","result":["0xeff7a6d5ae3b7eede8ff784e1809adec780f911571c64a92fd379506d30ea7c2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e9"]}

--- thread ID: 0x18b4, 2021.08.01 13:59:23.671
epoch = 431 (next epoch in 20503 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:59:24.588, 917 ms
{"id":0,"jsonrpc":"2.0","result":["0x67e87d9c6a554fe626d82fe7a8c6cb1b2ad668e8641152c71541bda8ee104f8b","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e9"]}

--- thread ID: 0x2630, 2021.08.01 13:59:24.588
epoch = 431 (next epoch in 20503 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:59:27.400, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:11:45.915)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:02:39.333, 20 ms], [fan = 99%, 2920 rpm, 54°C], 29.219342 MH/s (101.08 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:06:08.804,  2 ms], [fan = 99%, 2603 rpm, 65°C], 29.212734 MH/s ( 99.92 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:03:52.673, 49 ms], [fan = 99%, 2657 rpm, 66°C], 29.217772 MH/s (100.72 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:02:44.364, 34 ms], [fan = 99%, 2630 rpm, 65°C], 29.219432 MH/s (101.99 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 6, S = 0, R = 0, I = 0], [00:00:44.767,  1 ms], [fan = 99%, 3336 rpm, 68°C], 29.211682 MH/s (100.17 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 4, S = 1, R = 0, I = 0], [00:00:07.390, 34 ms], [fan = 99%, 3225 rpm, 63°C], 29.219818 MH/s (101.85 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 2, S = 0, R = 0, I = 0], [00:08:55.729, 43 ms], [fan = 99%, 2566 rpm, 68°C], 28.813947 MH/s (103.52 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:02:54.941, 31 ms], [fan = 99%, 2675 rpm, 60°C], 29.216759 MH/s (102.96 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:02:41.154, 49 ms], [fan = 99%, 2652 rpm, 65°C], 29.217470 MH/s (103.10 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 5, S = 0, R = 0, I = 0], [00:00:20.861,  1 ms], [fan = 99%, 2640 rpm, 62°C], 29.212848 MH/s (102.91 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 8, S = 0, R = 0, I = 0], [00:00:04.919,  0 ms], [fan = 99%, 2622 rpm, 67°C], 28.787572 MH/s (103.49 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:10:12.489, 13 ms], [fan = 99%, 2689 rpm, 67°C], 27.294799 MH/s (101.39 W) = 347.844175 MH/s (1223.10 W)

<<< thread ID: 0x24b4, 2021.08.01 13:59:27.404, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014bbae4f","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2610, 2021.08.01 13:59:27.420, 2831 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2768, 2021.08.01 13:59:27.595, 174 ms
{"id":0,"jsonrpc":"2.0","result":["0x085741b3b716ad9254c93dfc9e6775aca7601406c967f2723007bae94a996a05","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e9"]}

--- thread ID: 0x2768, 2021.08.01 13:59:27.595
epoch = 431 (next epoch in 20503 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x1638, 2021.08.01 13:59:28.075, PCIe: 00000000:0f:00.0, GPU.07 share found (search channel 0).
 nonce: 0x13d0a854832fb051
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000001c34693a20409378c37081da6e45443828b38fb10ee473579a4d7501
   mix: 0x8ec4a4d78f1e2383d1ed6c19a72c4181880d4f5ca65c196d379fc223388c24c9

<<< thread ID: 0x2648, 2021.08.01 13:59:28.075, 0 ms
{"jsonrpc":"2.0","id":1050,"method":"eth_submitWork","params":["0x13d0a854832fb051","0x085741b3b716ad9254c93dfc9e6775aca7601406c967f2723007bae94a996a05","0x8ec4a4d78f1e2383d1ed6c19a72c4181880d4f5ca65c196d379fc223388c24c9"],"worker":"alphagruis"}

--- thread ID: 0xedc, 2021.08.01 13:59:28.090, PCIe: 00000000:0f:00.0, GPU.07 share accepted.

>>> thread ID: 0xedc, 2021.08.01 13:59:28.090, 495 ms (15 ms)
{"id":1050,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:59:36.655, 8564 ms
{"id":0,"jsonrpc":"2.0","result":["0x1239aa71a14ef07e3faee87884141e278c2c6789909b74643d06ff4f16754839","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570e9"]}

--- thread ID: 0x2628, 2021.08.01 13:59:36.655
epoch = 431 (next epoch in 20503 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:59:36.778, 123 ms
{"id":0,"jsonrpc":"2.0","result":["0x923f39d4b3f1486d71e01ac8f9eb928cff8b8f778cc6dbb60e9562b66be654ed","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ea"]}

--- thread ID: 0x1df0, 2021.08.01 13:59:36.778
epoch = 431 (next epoch in 20502 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:59:36.878, 99 ms
{"id":0,"jsonrpc":"2.0","result":["0xa09afbc58adf98a7e04fb626fab239befd80fe633151c692d986f6496b0ce170","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ea"]}

--- thread ID: 0x18b4, 2021.08.01 13:59:36.878
epoch = 431 (next epoch in 20502 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:59:38.468, 1590 ms
{"id":0,"jsonrpc":"2.0","result":["0xa31ab469a0f8dcf5102c3413d78e6a35ad85d60ab7417e212e5f748d31ae6abd","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570eb"]}

--- thread ID: 0x2630, 2021.08.01 13:59:38.468
epoch = 431 (next epoch in 20501 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:59:38.684, 216 ms
{"id":0,"jsonrpc":"2.0","result":["0x177d9d70fecaf6cdf1f0d8bc6f5334e537f7fe9cedb9e7ee67cdcd636bc3b0b2","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570eb"]}

--- thread ID: 0x24b4, 2021.08.01 13:59:38.685
epoch = 431 (next epoch in 20501 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:59:40.496, 1811 ms
{"id":0,"jsonrpc":"2.0","result":["0x405e4e937762d61c28b19e8fd7d80eb86bed2fe6dcbbc9581764f0337553c0da","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ec"]}

--- thread ID: 0x2610, 2021.08.01 13:59:40.496
epoch = 431 (next epoch in 20500 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 13:59:40.663, 166 ms
{"id":0,"jsonrpc":"2.0","result":["0xd379eb303264a507a6883b33b3402cf5aba0fb1edb39353499149f0b05fe2f7c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ec"]}

--- thread ID: 0x2768, 2021.08.01 13:59:40.663
epoch = 431 (next epoch in 20500 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:59:42.415, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:12:00.931)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:02:54.349, 37 ms], [fan = 99%, 2964 rpm, 53°C], 29.213531 MH/s (100.75 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:06:23.820, 27 ms], [fan = 99%, 2592 rpm, 65°C], 29.216257 MH/s (100.02 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:04:07.689, 32 ms], [fan = 99%, 2661 rpm, 66°C], 29.093335 MH/s (100.71 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:02:59.380,  9 ms], [fan = 99%, 2642 rpm, 65°C], 29.209066 MH/s (101.89 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 6, S = 0, R = 0, I = 0], [00:00:59.783, 23 ms], [fan = 99%, 3324 rpm, 68°C], 29.216512 MH/s (100.04 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 4, S = 1, R = 0, I = 0], [00:00:22.405,  8 ms], [fan = 99%, 3268 rpm, 63°C], 29.213365 MH/s (101.85 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 3, S = 0, R = 0, I = 0], [00:00:14.340, 16 ms], [fan = 99%, 2585 rpm, 68°C], 28.604387 MH/s (102.17 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:03:09.957,  0 ms], [fan = 99%, 2660 rpm, 60°C], 29.220160 MH/s (102.93 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:02:56.169, 54 ms], [fan = 99%, 2628 rpm, 65°C], 29.031830 MH/s (102.75 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 5, S = 0, R = 0, I = 0], [00:00:35.877, 37 ms], [fan = 99%, 2648 rpm, 62°C], 29.216874 MH/s (102.94 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 8, S = 0, R = 0, I = 0], [00:00:19.935,  0 ms], [fan = 99%, 2618 rpm, 67°C], 29.028227 MH/s (103.48 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:10:27.505, 35 ms], [fan = 99%, 2681 rpm, 67°C], 27.135823 MH/s (100.84 W) = 347.399367 MH/s (1220.36 W)

<<< thread ID: 0x2648, 2021.08.01 13:59:42.420, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b4e4c7","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0xedc, 2021.08.01 13:59:42.436, 1772 ms (15 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x2628, 2021.08.01 13:59:42.685, 249 ms
{"id":0,"jsonrpc":"2.0","result":["0xffdfdced3eaec94e7c5e521d5485b4c8182ab98ebe0070d5b9e8d9002a136364","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ed"]}

--- thread ID: 0x2628, 2021.08.01 13:59:42.685
epoch = 431 (next epoch in 20499 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:59:42.815, 129 ms
{"id":0,"jsonrpc":"2.0","result":["0x94794d725f8b8ba74881b7df7063a37774a2c2b1399a0c909f65ab7cc4172194","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ed"]}

--- thread ID: 0x1df0, 2021.08.01 13:59:42.815
epoch = 431 (next epoch in 20499 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 13:59:44.895, 2080 ms
{"id":0,"jsonrpc":"2.0","result":["0x0842bfc8c58b5a87d3462a69ce148c35a3313b18475b7eae4e3fe82c9742a1e0","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ed"]}

--- thread ID: 0x18b4, 2021.08.01 13:59:44.895
epoch = 431 (next epoch in 20499 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2630, 2021.08.01 13:59:45.938, 1042 ms
{"id":0,"jsonrpc":"2.0","result":["0x95484501e64feca20f399c4510db913cd2890e5d595302e2252df1f63969b544","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ed"]}

--- thread ID: 0x2630, 2021.08.01 13:59:45.938
epoch = 431 (next epoch in 20499 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x24b4, 2021.08.01 13:59:48.833, 2894 ms
{"id":0,"jsonrpc":"2.0","result":["0x2ed53d3c5d9be9c328efa8c603690fcd6e735b85371e35186e7434d6373bb177","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ed"]}

--- thread ID: 0x24b4, 2021.08.01 13:59:48.833
epoch = 431 (next epoch in 20499 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 13:59:52.959, 4126 ms
{"id":0,"jsonrpc":"2.0","result":["0x61c0330e17725c24d179f99bd65434a0d3bd5a773467fc98ce7621f07aaa38f9","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ed"]}

--- thread ID: 0x2610, 2021.08.01 13:59:52.959
epoch = 431 (next epoch in 20499 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x18c8, 2021.08.01 13:59:53.075, PCIe: 00000000:03:00.0, GPU.11 share found (search channel 1).
 nonce: 0x13d0a85688dcd15f
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000001985a4b039637ccacf15bbfeb81a753c5994f93604de75211bf29bf0
   mix: 0xde084b3a820e054bf314a1a8d85dc2bdfd6ba98fcf91dc4eacda03a0b2a28aef

<<< thread ID: 0x2768, 2021.08.01 13:59:53.076, 0 ms
{"jsonrpc":"2.0","id":1051,"method":"eth_submitWork","params":["0x13d0a85688dcd15f","0x61c0330e17725c24d179f99bd65434a0d3bd5a773467fc98ce7621f07aaa38f9","0xde084b3a820e054bf314a1a8d85dc2bdfd6ba98fcf91dc4eacda03a0b2a28aef"],"worker":"alphagruis"}

--- thread ID: 0x2648, 2021.08.01 13:59:53.092, PCIe: 00000000:03:00.0, GPU.11 share accepted.

>>> thread ID: 0x2648, 2021.08.01 13:59:53.092, 132 ms (16 ms)
{"id":1051,"jsonrpc":"2.0","result":true}

>>> thread ID: 0xedc, 2021.08.01 13:59:54.537, 1445 ms
{"id":0,"jsonrpc":"2.0","result":["0x2444dc06d278ecfffb67146d687b72e6083be6f695e1552faa380d08923c1805","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0xedc, 2021.08.01 13:59:54.537
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2628, 2021.08.01 13:59:54.642, 105 ms
{"id":0,"jsonrpc":"2.0","result":["0x9590bf6529784ccafd4cb3879330a15f44e18e40e4d59d6ab198b17cb2e6224c","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x2628, 2021.08.01 13:59:54.642
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x1df0, 2021.08.01 13:59:56.636, 1994 ms
{"id":0,"jsonrpc":"2.0","result":["0xea136778a013fb5000260fcc1d6b83ab8e1acc2cb9cf95783957fb0f3fd1d9bb","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x1df0, 2021.08.01 13:59:56.636
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x2170, 2021.08.01 13:59:57.431, eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:12:15.947)
PCIe: 00000000:09:00.0, GPU.01: [A = 2, S = 1, R = 0, I = 0], [00:03:09.365, 20 ms], [fan = 99%, 2953 rpm, 53°C], 29.213647 MH/s (101.14 W) +
PCIe: 00000000:0a:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:06:38.836,  3 ms], [fan = 99%, 2599 rpm, 65°C], 29.203725 MH/s (100.13 W) +
PCIe: 00000000:04:00.0, GPU.03: [A = 4, S = 0, R = 0, I = 0], [00:04:22.705,  3 ms], [fan = 99%, 2669 rpm, 66°C], 29.215208 MH/s (100.57 W) +
PCIe: 00000000:0e:00.0, GPU.04: [A = 6, S = 0, R = 0, I = 0], [00:03:14.396, 22 ms], [fan = 99%, 2663 rpm, 65°C], 29.218753 MH/s (102.01 W) +
PCIe: 00000000:0d:00.0, GPU.05: [A = 6, S = 0, R = 0, I = 0], [00:01:14.799, 36 ms], [fan = 99%, 3348 rpm, 68°C], 29.208369 MH/s (100.30 W) +
PCIe: 00000000:02:00.0, GPU.06: [A = 4, S = 1, R = 0, I = 0], [00:00:37.421, 14 ms], [fan = 99%, 3300 rpm, 63°C], 29.202310 MH/s (101.89 W) +
PCIe: 00000000:0f:00.0, GPU.07: [A = 3, S = 0, R = 0, I = 0], [00:00:29.356, 30 ms], [fan = 99%, 2569 rpm, 68°C], 29.054673 MH/s (103.45 W) +
PCIe: 00000000:0c:00.0, GPU.08: [A = 7, S = 0, R = 0, I = 0], [00:03:24.973, 22 ms], [fan = 99%, 2668 rpm, 60°C], 29.223653 MH/s (102.96 W) +
PCIe: 00000000:06:00.0, GPU.09: [A = 2, S = 0, R = 0, I = 0], [00:03:11.185, 30 ms], [fan = 99%, 2636 rpm, 64°C], 28.694428 MH/s (101.83 W) +
PCIe: 00000000:01:00.0, GPU.10: [A = 5, S = 0, R = 0, I = 0], [00:00:50.893, 22 ms], [fan = 99%, 2636 rpm, 62°C], 29.185909 MH/s (102.95 W) +
PCIe: 00000000:03:00.0, GPU.11: [A = 9, S = 0, R = 0, I = 0], [00:00:04.356, 18 ms], [fan = 99%, 2618 rpm, 67°C], 28.839019 MH/s (103.42 W) +
PCIe: 00000000:05:00.0, GPU.12: [A = 1, S = 0, R = 0, I = 0], [00:10:42.520, 10 ms], [fan = 99%, 2697 rpm, 67°C], 27.193429 MH/s (100.61 W) = 347.453123 MH/s (1221.26 W)

<<< thread ID: 0x18b4, 2021.08.01 13:59:57.436, 0 ms
{"jsonrpc":"2.0","id":13,"method":"eth_submitHashrate","params":["0x0000000000000000000000000000000000000000000000000000000014b5b6c3","0x162ebe6b87cc164a0c22e8ddb06086e3155b772e361a9d6e869ff64559fecb5f"],"worker":"alphagruis"}

>>> thread ID: 0x2630, 2021.08.01 13:59:57.452, 815 ms (16 ms)
{"id":13,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x24b4, 2021.08.01 13:59:57.662, 210 ms
{"id":0,"jsonrpc":"2.0","result":["0x88eea495edf6bec00642d839c2c8e136562a4bdf9ad9956e998484f0205a24bc","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x24b4, 2021.08.01 13:59:57.662
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2610, 2021.08.01 14:00:01.774, 4112 ms
{"id":0,"jsonrpc":"2.0","result":["0x053ea8f05db79696ae130ce108a287b7a9e30c52b2446e82635265236a6b4988","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x2610, 2021.08.01 14:00:01.774
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2768, 2021.08.01 14:00:03.626, 1852 ms
{"id":0,"jsonrpc":"2.0","result":["0x5edf1159d2b47c18575d14e941ec00c37ef15d3b955ac3fa70dd3512b09ce750","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x2768, 2021.08.01 14:00:03.626
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x2648, 2021.08.01 14:00:07.792, 4166 ms
{"id":0,"jsonrpc":"2.0","result":["0x606b75871371cde7d2a717c7c917a697a739ecdd806fd87ec755483baffaf591","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x2648, 2021.08.01 14:00:07.792
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

--- thread ID: 0x10c4, 2021.08.01 14:00:09.715, PCIe: 00000000:02:00.0, GPU.06 share found (search channel 1).
 nonce: 0x13d0a857e1fbb44e
target: 0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000
result: 0x000000007934bf3d23115acc5a8c7428de35461c0080c7f666b6da8d73319ed1
   mix: 0x05b568671790ad88eba268ee9526d8d27e3fce7c442be464316aad88d06121e7

<<< thread ID: 0xedc, 2021.08.01 14:00:09.716, 0 ms
{"jsonrpc":"2.0","id":1052,"method":"eth_submitWork","params":["0x13d0a857e1fbb44e","0x606b75871371cde7d2a717c7c917a697a739ecdd806fd87ec755483baffaf591","0x05b568671790ad88eba268ee9526d8d27e3fce7c442be464316aad88d06121e7"],"worker":"alphagruis"}

--- thread ID: 0x2628, 2021.08.01 14:00:09.731, PCIe: 00000000:02:00.0, GPU.06 share accepted.

>>> thread ID: 0x2628, 2021.08.01 14:00:09.731, 1938 ms (15 ms)
{"id":1052,"jsonrpc":"2.0","result":true}

>>> thread ID: 0x1df0, 2021.08.01 14:00:09.790, 59 ms
{"id":0,"jsonrpc":"2.0","result":["0x3ce8dabc4e963af4d6ebd07cc27fb9010cded49bbee1941b4f38f6ab9a9894a5","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x1df0, 2021.08.01 14:00:09.790
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

>>> thread ID: 0x18b4, 2021.08.01 14:00:11.623, 1832 ms
{"id":0,"jsonrpc":"2.0","result":["0xa9bb12c1b5a7d9507b2b03f778d1e498c0d7daf2b044ae7b325878918ad96cfd","0x787fc048d668f524ffd65484f99d9e60a25cfa3e5e8254f111e6b7968f195e9c","0x00000000ffff00000000ffff00000000ffff00000000ffff00000000ffff0000","0xc570ee"]}

--- thread ID: 0x18b4, 2021.08.01 14:00:11.623
epoch = 431 (next epoch in 20498 blocks), share difficulty = 4.295032833 GH.

quitting...

--- thread ID: 0xf5c, 2021.08.01 14:00:11.997
disconnected from eu1.ethermine.org:5555 (172.65.207.106:5555 TLSv1.2, 00:12:30.512)

--- thread ID: 0x2fc, 2021.08.01 14:00:12.451
PCIe: 00000000:0e:00.0, GPU.04: exit thread.

--- thread ID: 0xf4c, 2021.08.01 14:00:12.533
PCIe: 00000000:0c:00.0, GPU.08: exit thread.

--- thread ID: 0x5e8, 2021.08.01 14:00:12.554
PCIe: 00000000:05:00.0, GPU.12: exit thread.

--- thread ID: 0x18c8, 2021.08.01 14:00:12.564
PCIe: 00000000:03:00.0, GPU.11: exit thread.

--- thread ID: 0x2420, 2021.08.01 14:00:12.564
PCIe: 00000000:06:00.0, GPU.09: exit thread.

--- thread ID: 0x25d8, 2021.08.01 14:00:12.569
PCIe: 00000000:0a:00.0, GPU.02: exit thread.

--- thread ID: 0x10c4, 2021.08.01 14:00:12.595
PCIe: 00000000:02:00.0, GPU.06: exit thread.

--- thread ID: 0x1638, 2021.08.01 14:00:12.595
PCIe: 00000000:0f:00.0, GPU.07: exit thread.

--- thread ID: 0x1970, 2021.08.01 14:00:12.604
PCIe: 00000000:09:00.0, GPU.01: exit thread.

--- thread ID: 0x2ec, 2021.08.01 14:00:12.607
PCIe: 00000000:04:00.0, GPU.03: exit thread.

--- thread ID: 0x23a0, 2021.08.01 14:00:12.612
PCIe: 00000000:01:00.0, GPU.10: exit thread.

--- thread ID: 0x4e8, 2021.08.01 14:00:12.620
PCIe: 00000000:0d:00.0, GPU.05: exit thread.

```

</p>
</details>
