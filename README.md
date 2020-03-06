## Assumptions:
- Have access to VM system with bccal program installed
- Executing bccal commands in the correct directory
- Have access to leex7842@umn.edu.ics file

## Vulnerability 1
This is replicating first vulnerability explained in the Summary of Findings. If the input message is too large it will give a segmentation fault (core dumped) and will not show the full message that was originally stored.

To exploit this vulnerability do the following:
First type this:
> bccal-add 20201010T100000 hellotherehellotherehellotherehellotherehellotherehellotherehellotherehellotherehellotherehellotherehellothere

second:
> bccal-list

third:
> sudo cat /var/bccald.state

The example here used a message string of length size 110. You can see that there is a Segmentation fault (core dumped) after step 2. After step 3, you can see that the state file did not store the full 110 characters in the message. Only 87 characters were stored.




Insert a large ics file which will delete previous messages (DOS/Tampering)
To exploit this vulnerability do the following:
bccal-add 20201010T100000 message1
bccal-add 20201010T100000 message2
bccal-invite leex7842@umn.edu.ics
bccal-list

After step 4, you can see that the alerts from step 1 and step 2 are now gone. If you go from step 3 to step 4 fast enough you can see the screen print a large amount of alarm events (from the ics file) and a Segmentation fault (core dumped) at the bottom. Although if you wait any longer than a second after step 3, then execute step 4, all messages will be deleted including the alarm events from step 1 and step 2. No alarm events will be displayed in the list.
