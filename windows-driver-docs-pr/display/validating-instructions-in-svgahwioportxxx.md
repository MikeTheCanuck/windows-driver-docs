---
title: Validating Instructions in SvgaHwIoPortXxx
description: Validating Instructions in SvgaHwIoPortXxx
ms.assetid: 70fe2acb-10ff-4182-96a5-78bff0d8f8a0
keywords: ["video miniport drivers WDK Windows 2000 , VGA, SvgaHwIoPortXxx functions", "VGA WDK video miniport , SvgaHwIoPortXxx functions", "SvgaHwIoPortXxx functions"]
---

# Validating Instructions in SvgaHwIoPortXxx


## <span id="ddk_validating_instructions_in_svgahwioportxxx_gg"></span><span id="DDK_VALIDATING_INSTRUCTIONS_IN_SVGAHWIOPORTXXX_GG"></span>


As already mentioned in [VGA-Compatible Miniport Driver's HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md), the IOPM set for directly accessible I/O ports usually includes all SVGA registers except the sequencer registers and the miscellaneous output register, which the VGA-compatible miniport driver continues to monitor with its *SvgaHwIoPortXxx* functions. The sequencer registers control internal chip timing on VGA-compatible video adapters. If a full-screen MS-DOS application touches other adapter registers during a synchronous reset, the machine can hang. Likewise, if the miscellaneous output register is set to select a nonexistent clock, the machine can hang.

VGA-compatible miniport drivers must ensure that full-screen MS-DOS applications do not issue instructions that cause the machine to hang. Each such miniport driver must supply *SvgaHwIoPortXxx* functions that monitor application-issued instructions to the I/O ports for the adapter sequencer registers and miscellaneous output register. Each new VGA-compatible miniport driver for an adapter with special features also must monitor and continue to validate any I/O ports to which an application might send any instruction sequence that could hang the machine.

Whenever an application attempts to access the sequencer clock register, the *SvgaHwIoPortXxx* function must change the IOPM in order to trap all instructions coming in during a synchronous reset. As soon as an application sends an instruction that affects the sequencer or attempts to write to the miscellaneous output register, the *SvgaHwIoPortXxx* function should adjust the IOPM by calling [**VideoPortSetTrappedEmulatorPorts**](https://msdn.microsoft.com/library/windows/hardware/ff570366) to disable direct access to all adapter registers.

The miniport driver-supplied *SvgaHwIoPortXxx* functions should buffer subsequent **IN** (or **INSB/INSW/INSD**) and/or **OUT** (or **OUTSB/OUTSW/OUTSD**) instructions in the **EmulatorAccessEntriesContext** area it set up in the VIDEO\_PORT\_CONFIG\_INFO (see [VGA-Compatible Miniport Driver's HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)) until the synchronous reset is done, or until the application either restores the miscellaneous output register or resets it to a "safe" clock.

Then, the miniport driver is responsible for checking that the buffered instructions cannot hang the machine. If not, the miniport driver should process the buffered instructions, usually by calling [**VideoPortSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff570372) with a driver-supplied [*HwVidSynchronizeExecutionCallback*](https://msdn.microsoft.com/library/windows/hardware/ff567369) function. Otherwise, the miniport driver should discard the buffered instructions.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20Validating%20Instructions%20in%20SvgaHwIoPortXxx%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



