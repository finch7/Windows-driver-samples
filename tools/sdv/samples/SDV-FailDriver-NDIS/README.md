---
page_type: sample
description: "Demonstrates how Static Driver Verifier (SDV) can find errors in a NDIS driver."
languages:
- cpp
products:
- windows
- windows-wdk
---


<!---
    name: SDV-FailDriver-NDIS
    platform: WDM
    language: cpp
    category: StaticDriverVerifier Network
    description: Demonstrates how Static Driver Verifier (SDV) can find errors in a NDIS driver.
    samplefwlink: http://go.microsoft.com/fwlink/p/?LinkId=617995
--->

# SDV-FailDriver-NDIS

The SDV-FailDriver-NDIS sample driver contains intentional code errors that are designed to show the capabilities and features of [Static Driver Verifier](http://msdn.microsoft.com/en-us/library/windows/hardware/ff552808) (SDV). SDV is a static verification tool that systematically analyzes the source code of Windows kernel-mode drivers. SDV is included in the Windows Driver Kit (WDK) and can be run from Microsoft Visual Studio. The sample demonstrates how SDV can find errors in an NDIS driver.

**Caution** These sample drivers contain intentional code errors that are designed to show the capabilities and features of SDV. These sample drivers are not functional and are not intended as examples for real driver development projects.

## Run the sample

1. In the **Solutions Explorer** window, select the driver project (sdvmp.vcxProj).

    From the **Driver** menu, click **Launch Static Driver Verifier...**.

    This opens the Static Driver Verifier application, where you can control, configure, and schedule when Static Driver Verifier performs an analysis.

1. Click the **Rules** tab to select which driver DDI usage rules to verify when you start the analysis.

    Static Driver Verifier detects the type of driver you are analyzing (WDF, WDM, NDIS, or Storport) and selects the default set of rules for your driver type. If this is the first time you are running SDV on your driver, you should run the default rule set. To shorten the amount of time it takes to analyze the sample driver, you can select the **Custom rule selection**.

    Use the default rule set, or select **Custom rule selection**, click **Clear All**, and then select the following rules for the NDIS sdvmp sample:

    - [NdisAllocateMemoryWithTagPriority](http://msdn.microsoft.com/en-us/library/windows/hardware/ff549326)
    - [Init\_RegisterSG](http://msdn.microsoft.com/en-us/library/windows/hardware/ff547153)
    - [NdisStallExecution\_Delay](http://msdn.microsoft.com/en-us/library/windows/hardware/ff549332)
    - [Flags\_Irql](http://msdn.microsoft.com/en-us/library/windows/hardware/ff546123)
    - [Irql\_Synch\_Function](http://msdn.microsoft.com/en-us/library/windows/hardware/ff548015)

    For information about the rules, see [DDI Compliance Rules](http://msdn.microsoft.com/en-us/library/windows/hardware/ff552840).

1. Start the static analysis. Click the **Main** tab, and click **Start**. When you click **Start**, a message is displayed to let you know that static analysis is scheduled and that the analysis can take a long time to run. Click **OK** to continue.

## View and analyze the results

As the static analysis proceeds, SDV reports the status of the analysis. When the analysis is complete, SDV reports the results and statistics. If the driver fails to satisfy a DDI usage rule, the result is reported as a defect. SDV finds 5 defects in this sample.

On the **Main** tab, under **Results**, click the **Rules** tab. This tab displays the name of each rule that was verified in the last run and the results of the analysis. To view the reported defects, click the **Defect** link in the **Results** column. This opens the [Static Driver Verifier Report Page](http://msdn.microsoft.com/en-us/library/windows/hardware/ff552834) and the [Trace Viewer](http://msdn.microsoft.com/en-us/library/windows/hardware/ff544659), which displays a trace of the code path to the rule violation. For more information, see [Interpreting Static Driver Verifier Results](http://msdn.microsoft.com/en-us/library/windows/hardware/ff547228).