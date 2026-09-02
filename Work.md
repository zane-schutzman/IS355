Week 1 - Tutorial 1

Task 1: Start Your GitHub Portfolio

For this task, I set up my GitHub account and created my GitHub profile.

I also created an images directory in my repository, which will be used to store screenshots and other images that provide evidence of my tutorial activities.

Evidence

Task 2: View Your Computer Information

For this task, I used Windows PowerShell to find information about my computer's hardware and memory.

Commands Used

I used the following command to view my computer's memory information:

Get-ComputerInfo -Property "*memory*"

I used the following command to view my processor information:

Get-ComputerInfo -Property "*processor*"

My Results

CsTotalPhysicalMemory        : 16834949024
CsPhysicallyInstalledMemory  : 16777216
OsTotalVisibleMemorySize     : 16440376
OsFreePhysicalMemory         : 2532160
OsTotalVirtualMemorySize     : 25877560
OsFreeVirtualMemory          : 6275280
OsInUseVirtualMemory         : 19602280
OsMaxProcessMemorySize       : 137438953344

Memory Information and Answers

Total Physical Memory: 16,834,949,024 Bytes

Total Physical Memory: Approximately 16.83 GB

Physically Installed Memory: 16,777,216 KB

Physically Installed Memory: 16 GB

Total Visible Memory: 16,440,376 KB

Free Physical Memory: 2,532,160 KB

Total Virtual Memory: 25,877,560 KB

Free Virtual Memory: 6,275,280 KB

In-Use Virtual Memory: 19,602,280 KB

Maximum Process Memory Size: 137,438,953,344 Bytes

My computer has 16 GB of physically installed RAM. PowerShell reports the total physical memory as 16,834,949,024 Bytes.

Processor Results

The processor command produced the following results:

CsNumberOfLogicalProcessors : 20

CsNumberOfProcessors        : 1

CsProcessors                : {13th Gen Intel(R) Core(TM) i7-13700H}

Processor Information and Answers

Logical Processors: 20

Physical Processors: 1

Processor: 13th Gen Intel(R) Core(TM) i7-13700H

My computer has 1 physical processor and 20 logical processors. The processor is a 13th Gen Intel(R) Core(TM) i7-13700H.

Evidence

The screenshot below shows the PowerShell commands I used and the results produced by the commands.

![PowerShell Computer Information](images/week1-task2-screenshot.png)


Operating System and Disk Information

The tutorial also asks for information about the computer's operating system and disk sizes.

The commands that can be used to find this information are:

Get-ComputerInfo -Property "*os*"

Get-Volume

These commands were not included in my current screenshot, so I have not recorded specific OS or disk values without verifying them.


What I Learned

This tutorial taught me how to begin using GitHub as a portfolio and journal for the IS355 course.

I learned that GitHub repositories can be used to organize my course work and that Markdown can be used to create formatted journal entries. I also learned how to create an images folder and upload screenshots into the repository.

I learned how to use PowerShell to find information about my computer. The Get-ComputerInfo command can display detailed information about different parts of the computer depending on the property specified.

From the commands I ran, I learned that my computer has:

16 GB of physically installed RAM.

16,834,949,024 Bytes of total physical memory.

20 logical processors.

1 physical processor.

A 13th Gen Intel(R) Core(TM) i7-13700H processor.

I also learned that computer memory can be displayed using different units. For example, the physically installed memory was displayed as 16,777,216 KB, which is equivalent to 16 GB.


Challenges

One challenge I experienced was learning how to organize my GitHub repository for the journal.

I needed to create an images directory so that my screenshots could be stored separately from my Markdown file. I learned that GitHub creates a folder when a file is created inside a folder path.

Another challenge was understanding the different memory values returned by PowerShell. The command displayed several different memory measurements, including total physical memory, free physical memory, total virtual memory, and free virtual memory.

At first, these values could be confusing because they are all different numbers. I learned that each value represents a different type or measurement of memory, so I need to pay attention to the property name when recording the results.

I also learned that some values need to be converted into a more understandable format. For example, the physically installed memory is reported as 16,777,216 KB, which is equivalent to 16 GB.


Project Contribution

My main contribution during this tutorial was setting up my individual GitHub portfolio and journal for the IS355 course.

I created the repository and organized it so that I can document my work throughout the unit. I also created an images directory and uploaded screenshots showing evidence of my completed tutorial activities.

This setup will allow me to continue adding my weekly tutorial work, screenshots, commands, results, answers, and project contributions throughout the course.


Reflection

This tutorial helped me become familiar with GitHub and PowerShell.

I learned how to create a GitHub repository and use Markdown to document my course work. I also learned how to organize screenshots in an images folder and include those screenshots in my Markdown journal.

Using PowerShell gave me a better understanding of the hardware in my computer. I was able to find my computer's RAM and processor information using commands instead of manually searching through different Windows settings.

The most useful part of the tutorial was learning how to document the results of the commands I used. Recording the commands, results, screenshots, and explanations will make it easier to show my progress and refer back to what I learned later in the unit.

Overall, I successfully completed the GitHub setup and used PowerShell to find my computer's memory and processor information. I now have a foundation for maintaining my weekly GitHub journal throughout the course.
