## Assumptions:
- Have access to VM system with bccal program installed
- Executing bccal commands in the correct directory
- Have access to leex7842@umn.edu.ics file

# Vulnerability 1
This is replicating first vulnerability explained in the Summary of Findings. If the input message is too large it will give a segmentation fault (core dumped) and will not show the full message that was originally stored.

To exploit this vulnerability do the following first type this:
> bccal-add 20201010T100000 hellotherehellotherehellotherehellotherehellotherehellotherehellotherehellotherehellotherehellotherehellothere

second type this:
> bccal-list

third type this:
> sudo cat /var/bccald.state

### Explanation of vulnerability 1
The example here used a message string of length size 110. You can see that there is a Segmentation fault (core dumped) after step 2. After step 3, you can see that the state file did not store the full 110 characters in the message. Only 87 characters were stored.


# Vulnerability 2
Insert a large ics file which will delete previous messages (DOS/Tampering)

To exploit this vulnerability do the following first type this:
>bccal-add 20201010T100000 message1

Second type this:
>bccal-add 20201010T100000 message2

Third type tihs:
> bccal-invite leex7842@umn.edu.ics

Fourth type this:
>bccal-list


### Explanation of vulnerability 2
After step 4, you can see that the alerts from step 1 and step 2 are now gone. All messages will be deleted and no alarm events will be displayed in the list.
