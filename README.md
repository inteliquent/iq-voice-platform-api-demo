# Inteliquent Voice Platform Developer Resource
## Overview
This repository is intended to provide developers, who are looking to develop their applicaitons on the Inteliquent Voice Platform, with useful code from basic building blocks to entire apps. Our goals as the Inteliquent team is to get your development team to a useful code as fast as possible. 


## Table of Content

>Note: Each code snippet should be associated with an Inteliquent Number/Domain to function as described below.

Code Snippets
- [Hello World](#helloworld)
- [Forward call to SIP URI](#sipuri)
- [Forward call to another number](#number)

- DTMF
- Call Forwarding

Demos:
- [Doorman app](README_doorman_demo.md)



#### Hello World <a href='#helloworld' id='helloworld' class='anchor' aria-hidden='true'></a>

1. Call is answered
2. "Hello World" text is played after text-to-speech conversion.
3. Call is hung-up

#### Forward call to SIP URI <a href='#sipuri' id='sipuri' class='anchor' aria-hidden='true'></a>

1. Call is Accepted
2. Ringing tone is played to calling leg
3. New call leg is initiated to SIP URI
4. `INBOUND_CALLER_NUMBER` variable is used as Caller Id
5. When SIP URI answers the two call legs are joined
6. When either party hangs up both call legs are hung up


#### Forward call to another number <a href='#number' id='number' class='anchor' aria-hidden='true'></a>

1. Call is Accepted
2. Ringing tone is played to calling leg
3. New call leg is initiated to a dialalbe number
4. `INBOUND_CALLER_NUMBER` variable is used as Caller Id
5. When called party answers the two call legs are joined
6. When either party hangs up both call legs are hung up