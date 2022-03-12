# Computer Forensics Acquisition

## Introduction

Crime and Investigation scenes in the movies are overrated period.

It has led many of us to wish and believe to fascinate about the prospect of hacking into systems with hoodies, secret codes, signals, flashing binary digits, the FBI, and whatnot.

&#x20;                                              ![](https://miro.medium.com/max/960/1\*WiISJgYF5u6HYh-KUO-DMQ.jpeg)

Well, when coming into the prospect of working with computers in an investigation, where digital evidence needs to be plucked out, there are a few best practices to follow, to keep the situation ethical. You can’t just go poking around everywhere for fun, without following some guidelines.

This activity, known as Computer Forensics can be applied to cases dealing with Child porn, bank fraud, etc.

## Steps of a Computer Forensics Investigation

Let’s discuss the steps involved in a Computer Forensics Investigation:-

&#x20;                                             ![](https://miro.medium.com/max/1308/1\*2dGEiRmqwKJMO5TIs7u0kw.jpeg)

### Preparation

&#x20;                                              ![](https://miro.medium.com/max/1400/0\*HNd9Xyzr4FYmxM-9.jpg)

The golden tip, in any investigation, is to take a copy of the disk, to ensure that the original is maintained for judicial and evidence submission purposes.

The investigative team must know their legal boundaries. What is permitted to do and what not. Having a legal team, on the side, is an advantage.

Ensure that the devices to be investigated, are properly secured, under physical security mechanisms, and are available for investigation, at all times. This is why the Chain of Custody mechanism is important.

Targets on a device-Log files, metadata, encryption keys etc. Prioritize devices, as per their importance towards the case.

### Triage

&#x20;                                                    ![](https://miro.medium.com/max/1400/0\*WjiwafStz0ilMMn5.jpg)

Triage is carried out to preview the data present on the device, to prevent inspecting files or data that may prove useless to the case.

A tool that can be used for device triage is Cyber Triage, developed by Basis Technologies.

Once the relevant data is uncovered, these can be transferred to another storage device, for hassle-free investigation. Documentation for this process is relevant. Note the data that has been left out. It may prove useful, at a later stage.

### Working with the evidence

&#x20;                                            ![](https://miro.medium.com/max/1252/0\*Y8DYnyNrN8qrwIEA.jpg)

The guiding principle for computer forensic acquisitions is to minimize, to the fullest extent possible, changes to the source data. This is usually accomplished by the use of a hardware device, software configuration, or application intended to allow reading data from a storage device without allowing changes (writes) to be made to it. This is done to prevent the data’s integrity loss.\
\
Encrypted Data-Will requires a key or passphrase to be decrypted.

The faster the key is gained, the better for the investigation

Keys may be obtained through technical means, i.e. storage of keys onto cloud platforms or security vaults

Non-technical means involve procuring it from the culprit, dumpster diving among papers, etc.

Log files-Timestamps and date stamps are of vital importance and should not be discarded

Every application will have a log file associated with it.

It has to be kept in mind that tools such as netcat and PsTools can be used to wipe records from logs

TYPES OF EVIDENCE ACQUISITION

## Types of Evidence Acquisition

### Physical Acquisition

It means to copy data verbatim (ditto) from the storage media of the device. It is done with making modifications.

Here, we perform data dumping after which the decoding phase. Once we get the physically extracted copy, we can chase and find records of deleted media. This is demonstrated in the Autopsy software too.

### Logical Acquisition

Anything ranging from a full device backup, containing files and folders can be considered as a logical acquisition.

### Targeted

In this method, we target specific files ranging from documents, images, log files, etc., that pique our interest. Rightful targets can help a long way in solving the case.

### Forensics Cloning

A forensic clone is the process of creating a bitstream duplicate of data, from one storage media to another.

DOCUMENTATION OF EVIDENCE

## Documentation of Evidence

&#x20;                                                 ![](https://miro.medium.com/max/676/0\*ckHG\_zkOcrWm0QGz)

These may involve any of the following:-

1. Electronic Tags
2. Acquisition Record/Report for each device acquired
3. Hash Values

## Reflection

&#x20;                                                   ![](https://miro.medium.com/max/1400/0\*VnaB55kyiESczPoA.png)

Upon the successful closure of the case, these are a few things that investigators can ponder on:-

a. What evidence was overlooked?\
b. How did it change the overall view of the case?\
c. Did it prove important towards the end?\
d. What were the mistakes made during the investigation?\
e. Correction mechanisms to overcome it in the next investigation?\
f. Were all members of the investigation team involved?\
g. Was anyone’s suggestions overlooked?

## Conclusion

This article gave a clear insight into what goes into a computer forensics investigation. Criminals are getting smarter by the day and security mechanisms that are released by the day are being used by them, for their immoral deeds.

Bitlocker encryption, security vaults…Phew!!

It surely seems challenging and doesn’t appear to be what we see at the movies, but surely it is a cool thing to do besides putting those miscreants behind bars.

## References

1\)SWGDE\_Best\_Practices\_for\_Computer\_Forensic\_Acquisitions

2\)[https://resources.infosecinstitute.com/topic/android-forensic-logical-acquisition/#:\~:text=The%20logical%20acquisition%20is%20a,and%20parsed%20by%20forensic%20tools.](https://resources.infosecinstitute.com/topic/android-forensic-logical-acquisition/#:\~:text=The%20logical%20acquisition%20is%20a,and%20parsed%20by%20forensic%20tools.)

3\)[https://blog.eccouncil.org/how-to-handle-data-acquisition-in-digital-forensics/](https://blog.eccouncil.org/how-to-handle-data-acquisition-in-digital-forensics/)
