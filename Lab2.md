# Lab: PowerShell Scripting
## About
- Author: Logan Cessac
- Course: IS 3513-01T
- Professor: Eric Wooldridge
- Date Created: July 5, 2026


## Method and Experience
I had an interesting experience with PowerShell in this lab. Previous courses that I’ve taken have covered basic tasks in PowerShell, such as using “dir” to list the files in a directory. I’ve also had the privilege of learning about scripting in Linux based VM’s, such as in Ubuntu and Kali. However, I’ve never tried scripting with PowerShell. This makes more sense to me, because I use Windows-based computers far more often than I do Linux-based machines. This lab was a great opportunity for me to explore a different approach to scripting. I also liked the fact that the script applied directly to cyber security, because it involved scanning through the security log in Event Viewer. I can see how important this would be if I ever needed to process records in my event logs. I imagine that this applies for different areas of cyber, such as computer forensics, where I’d look for certain suspicious records, or traffic inspection, where I’d need to calculate statistics for the kinds of traffic traveling through a host or events happening on a host. 

I wondered where to start with this lab. I wondered whether to create a .csv file to append the data from the script to or to write the script to create a new file from the data it extracts. I decided to go with the second option, because it streamlined the process. I opened PowerShell and, under the “File” tab in the taskbar, I clicked “New” to create a new script. I had tried to create my own text file and convert it to a script after, but it proved easier to just use the PowerShell application to create a new script. I named my new script “Cessac_seq370_IS_3513_PS_Script.ps1.” (See Figure 4) The instructions said to name the script with the *.ps convention. However, I was unable to get the script to run with this convention. It kept telling me it couldn’t find and execute this file. When I used the *.ps1 convention, though, the script was able to run smoothly. Once I got past this problem, I continued to start working through the structure of the code. This process of events was easy to formulate. First, I needed to import all the log entries from the “Security” log in Event Viewer. I did this using the “Get-WinEvent” command, which proved to be an efficient tool in my script. I then counted them with “.Count” on the end of my variable which held the imported entries. Using “Select-Object,” I pieced the data together into a table of entries that could be exported in a readable fashion to the .csv file.

The next step was to export the results to the .csv file and begin analysis of the data. I piped the results from entries to the “Export-Csv” command to be able to read the data more easily. I chose to display the same fields for each entry as the example .csv file. I then needed to find 4 main things: the number of audit failures in the log, the number of audit successes in the log, the most common Event ID among the failed audits, and the most common Event ID among the successful audits. Once I found the right commands to use for the first 2, they were relatively easy to construct. All I needed to do was filter the results based on whether the keyword display name was “audit failure” or “audit success.” Then I would just count the entries similarly to how I counted the total number of entries in the log. The other two were slightly more difficult, because I had to make sure that I was not only extracting the correct field of data, but that I was displaying it correctly, so that it would fit the standard output. I ended up piping the audit result counts previously mentioned to group them using the “Group-Object” command and then sort them using the “Sort-Item” command. Then I selected the first item from the sorted results and retrieved name of the item. This gave me the most found Event ID from each of the filtered groups. I then had all of my calculations. All I had left to do with the data was to format and display it in standard output.

To format the data, I used the “Write-Host” command, which made this an easy step. For this, I decided to limit the number of entries that would be processed to 100 entries, which allowed me to run the script many times and debug any issues without having to wait long amounts of time. I ran it several times and wrote the code to return the following format where “X” represents a variable: “Number of Audit Failures: X failures of X entries Most common Event ID: X Number of Audit Successes: X successes of X entries Most common Event ID: X.” (See Figure 1) With the format tailored how I needed it, I decided to run it a few times to confirm that it was able to run with 100 entries. After that I removed the limit for the number of entries to allow the script to process the entire log. I also looked at the log, which gave me a good idea of what to edit in my script. (See Figure 2)

This part took a lot of time. While the number kept changing, my Security log had about 36,070 entries at the time that the script ran. I was able to view this by opening Event Viewer and navigating to the Security log. The script took, on average, around 25-30 minutes to process these many records and record them to the .csv file, which I named Log_Entry.csv for testing purposes. After I ran the script, though, I changed the name of the log file to “Cessac_seq370_IS_3513_Log_Entry.csv,” (See Figure 4) according to the instructions. The .csv file occupied almost 18 MB, and it became difficult to edit the file with Excel. I had to shut down the software many times, because it would stop responding. However, I was able to view it and get an idea of what it contained. I received odd results. The script processed 35,994 entries, when the log held around 36,080 entries, meaning that there were almost 100 entries that weren’t accounted for. Among these was the only failed audit on the list, which would’ve proved useful to be able to show in the output. According to the statistics, my audits have a 100% success rate, but I know that there is a single failed audit that wasn’t processed by the script. I guess that this is because it ran for so long and processed so much data that there was data loss. I ran the script again. (See Figure 3) This time, the audit failure was processed, and it read that there was 1 failed audit out of 35,857 entries and 35,856 successful audits out of 35,857 entries. The most common failed Event ID was 4625, and the most common successful Event ID was 5379. The difference in total number of records between the first and second runs was confusing, but, again, my first guess is data loss with the processing of the vast number of records I have. 

This was a very interesting experience, and I learned a lot about how PowerShell works by playing with it. I got to see both advantages and disadvantages with it. I look forward to using this tool in scripting as another tool in the arsenal. This showed me how I can take raw data and automate the process of breaking down the data into readable deductions. After my script ran with the proper formatting, I was able to immediately see summary statistics computed with thousands of log entries. This can save me a lot of time in the future. Even though it took my computer about 25 minutes to process all the log entries, it would take me days or longer to manually compute the same statistics.


## Associated Research
PowerShell is a wonderful tool for me to learn about, because of how central it is. It is able to manipulate Windows-based systems and many of the installed applications on the OS. It is a command line interface that has graphical capabilities, making it an easy-to-learn environment. It can execute not only simple commands, but heavier scripts, and it’s “built on the .NET Framework.” (Rose et. al, 2024) It has lately been seen as an “indispensable tool for system administrators, primarily due to its ability to create and execute ScriptBlocks, which are composable, reusable, and modifiable blocks of code.” (Rose et. al, 2024) These ScriptBlocks, as the author later mentions, are a “fundamental building block in the PowerShell scripting language and act as a versatile and reusable container for script code.” (Rose, Graham, and Kabban, 2024) This lab had me working with similar pieces of code, which PowerShell was able to manipulate and process with ease. ScriptBlocks are a tool that enables compartmentalizing code, much like a custom function. One can create a ScriptBlock and then use it several times in similar areas of code. This makes PowerShell a critical tool to know for automation and penetration testing. 

However, with the powerful capabilities of PowerShell comes powerful risks. ScriptBlocks can be snuck past detection systems through a process called ScriptBlock Smuggling, which exploits the flexibility of ScriptBlocks. This process requires the tools that PowerShell provides. One of the main concerns, though, is that many attacks can utilize PowerShell to aid in the spread and masking of harmful code. For example, in a file-less attack, an attacker can insert “malicious code into the victim's command line prompt, which remains undetected by the victim's anti-virus or firewall with the help of legitimate tools like PowerShell.” (Sankha and Nisha, 2022) Because of this risk, many businesses and individuals block unnecessary PowerShell capabilities to reduce their attack front. Another concern is the amount of access that PowerShell has. Not only is it a powerful tool, but it has access to virtually every aspect of a Windows-based host. In the case of advanced persistent threats, attackers will use PowerShell to control hosts, and to “inject Shellcode into the victim’s computer.” (Yong and Zhou, 2021)

The goal is to enforce least privilege for every user in a network. This is because unnecessary privilege can provide a vulnerability, increasing risk to a system or network. One way to prevent attacks from using PowerShell on a target host is to limit its capabilities. In fact, it “can be used in constrained language mode to limit PowerShell to basic functionality.” (Sankha and Nisha, 2022) Windows provides native tools to carry this out. However, this can’t prevent all attacks. There are many approaches to mitigating this area of risk, such as “detection models based on real-time operation and machine learning.” (Yong and Zhou, 2021) There are problems with this like script obfuscation, which require de-obfuscating detection models. This is just one example of many approaches to mitigating this risk. Some employ very advanced methods to overcome many hurdles placed by the powerful nature of PowerShell. This requires many individuals to keep exploring options to be able to protect systems as the frontier of cyber threats continues to reform.   

## Script Code
This is the code that was used to process the records. It is designed to read the events in the "Security" log in Windows Event Viewer and export them in csv format. Then it displays some basic information about the records.
```powershell
$Events = Get-WinEvent -LogName 'Security'
$EventsNum = $Events.Count
$Table = $Events | Select-Object TimeCreated, LogName, ProviderName, Id,
    LevelDisplayName, UserId, TaskDisplayName, Keywords.Name, Message, MachineName

$Table | Export-Csv -Path "C:\Users\logan\OneDrive\Desktop\Summer 2026\IS-3513 Information Assurance and Security\Lab2\Log_Entry.csv" -NoTypeInformation

$Failures = $Events | Where-Object {$_.KeywordsDisplayNames -contains "Audit Failure"}
$FailureNum = $Failures.Count
$FailId = ($Failures | Group-Object Id | Sort-Object Count -Descending | Select-Object -First 1).Name

$Successes = $Events | Where-Object {$_.KeywordsDisplayNames -contains "Audit Success"}
$SuccessNum = $Successes.Count
$SuccessId = ($Successes | Group-Object Id | Sort-Object Count -Descending | Select-Object -First 1).Name

Write-Host "Number of Audit Failures: $FailureNum failures of $EventsNum entries Most common Event ID: $FailId"
Write-Host "Number of Audit Successes: $SuccessNum successes of $EventsNum entries Most common Event ID: $SuccessId"
```


## Appendices
Figure 1. Open Script and Results in Standard Output (first run)
<img width="973" height="521" alt="image" src="https://github.com/user-attachments/assets/0253a416-7c31-4512-9a79-075340648e49" />
Figure 2. Security Log .csv File Output (the actual .csv file is attached) 
<img width="976" height="520" alt="image" src="https://github.com/user-attachments/assets/d31bbc35-8b91-4b30-beb9-b7cdad77c432" />
Figure 3: Open Script and Results in Standard Output (second run)
<img width="979" height="496" alt="image" src="https://github.com/user-attachments/assets/445d4630-af92-441b-aab6-fd2c433520b1" />
Figure 4: “Lab2” folder that contains all files used in this lab
<img width="979" height="201" alt="image" src="https://github.com/user-attachments/assets/2fc23d3d-eaaf-4e3c-a1e9-46fac2c6b16b" />


## Bibliography
- Rose, A. J., Graham, S. R., Schubert Kabban, C.,M., Krasnov, J. J., & Henry, W. C. (2024). ScriptBlock smuggling: Uncovering stealthy evasion techniques in PowerShell and .NET environments. Journal of Cybersecurity and Privacy, 4(2), 153. doi:https://doi.org/10.3390/jcp4020008
- Fang, Y., Zhou, X., & Huang, C. (2021). Effective method for detecting malicious PowerShell scripts based on hybrid features. Neurocomputing, 448, 30–39. doi:10.1016/j.neucom.2021.03.117
- Chakraborty, S., & Nisha, T. N. (2022). Next generation proactive cyber threat hunting: A complete framework. AIP Conference Proceedings, 2519(1), 030093. doi:10.1063/5.0109674






