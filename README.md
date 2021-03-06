RPC-Assignment
==============

To compile:

1. $ rpcgen smoking.x
2. $ make server
3. $ make client

To clean directory:

$ make clean

The agent delves out supplies to smoker processes that request them.  It makes a smoker wait up to 
3 seconds if it was the last process to request supplies.  Unless, of course, there is only one smoker left.

An agent does the following:

    1. The agent takes in a struct defined in smoking.x and uses a character to determine which supply to give.
    2. If there are sufficient supplies it gives them to the smoker process IF there are more than one smoker process active
        and it is not the same smoker process as the last request
    3. If there are not sufficient supplies, it lets the smoker know and the smoker kills itself
    4. If there is only one smoker left and insufficient supplies to give to the smoker it sends a message to the smoker 
        to let it know to terminate the agent

The smoker does the following:

    1. It will kill itself if the agent does not have sufficient supplies to handle its request.
    2. If there are sufficient supplies, it will update its supply and attempt to smoke again
    3. If it is told to wait, it will wait
    4. If it is told it is the last smoker and there are no more supplies, it will kill itself and the server

To execute:

$ ./agent will run the server
$ ./smokeri HOSTNAME   //  where i = {1,2,3} will run the corresponding client process

Use something like what Tekin specified to run on 4 different machines.
$ ssh -f grz5@eecslinab2.case.edu "./RPC-Assignment/agent"; ssh -f grz5@eecslinab3.case.edu "./RPC-Assignment/smoker1 eecslinab2.case.edu"; ssh -f grz5@eecslinab4.case.edu "./RPC-Assignment/smoker2 eecslinab2.case.edu"; ssh -f grz5@eecslinab7.case.edu "./RPC-Assignment/smoker3 eecslinab2.case.edu";

output.txt: 
An example of the scripts being run.
If you would like to alter the supplies of any of the scripts the variables just below the header statements.
