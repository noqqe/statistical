# statistical

statistical is a tiny easy-to-use bash script collection for visualizing simple data in your terminal. 

## Usage 

statistical is following a simple key:value scheme like in json or similar. Just
add key:value pairs as parameters and watch the generic statistical graph.

    $ h-barplot john:433 alice:49 linus:12 bob:231
    $ v-barplot john:433 alice:49 linus:12 bob:231

## h-barplot Examples 

    $ h-barplot john:433 alice:49 linus:12 bob:231 
    john    |########################################### (433)
    alice   |#### (49)
    linus   |# (12)
    bob     |####################### (231

Maybe a some more complex example. There is a bit bash magic :) statistical can read from stdin as well. So you can just pipe some formated informations into it like:

    $ cd ~/Projects/bash-it
    $ for a in $(git shortlog -sn --all | cut -f2 | cut -f1 -d' '); do echo -n \
    "$a:" ; git log $LOGOPTS --all --numstat --format="%n" --author=$a | cut -f3 \
    | sort -iu | wc -l; done  | h-barplot 
    Mark          |##################
    Robert        |#########################################################################
    Florian       |##############
    Jesus         |######
    John          |##############
    Rich          |########
    Piotr         |###
    Travis        |####
    Fedyashev     |##
    zerobearing2  |####
    Andy          |###
    Daniel        |####
    Jeff          |##
    Karl          |##
    Robert        |#########################################################################
    Sirupsen      |##

## v-barplot Examples

The new v-barplot script does the same as h-barplot. It includes scaling for your terminal!

    $ ./v-barplot foo:24 bar:90 alice:76 bob:32
    90 |    ###         
    87 |    ###         
    84 |    ###         
    81 |    ###         
    78 |    ###         
    75 |    ### ###     
    72 |    ### ###     
    69 |    ### ###     
    66 |    ### ###     
    63 |    ### ###     
    60 |    ### ###     
    57 |    ### ###     
    54 |    ### ###     
    51 |    ### ###     
    48 |    ### ###     
    45 |    ### ###     
    42 |    ### ###     
    39 |    ### ###     
    36 |    ### ###     
    33 |    ### ###     
    30 |    ### ### ### 
    27 |    ### ### ### 
    24 |### ### ### ### 
    21 |### ### ### ### 
    18 |### ### ### ### 
    15 |### ### ### ### 
    12 |### ### ### ### 
     9 |### ### ### ### 
     6 |### ### ### ### 
     3 |### ### ### ### 
       |================
        foo bar ali bob 
