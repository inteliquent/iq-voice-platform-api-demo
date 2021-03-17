# Inteliquent Voice Platform Developer Resource
## Overview
This repository is intended to provide developers, who are looking to develop their applications on the Inteliquent Voice Platform, with useful code from basic building blocks to entire apps. Our goal at Inteliquent is to get your development team to a useful code as fast as possible. 


## Table of Content

>Note: Each code snippet should be associated with an Inteliquent Number/Domain to function as described below.

Code Snippets
- [Hello World](#helloworld)
- [Hello World w/ callback](#callback)
- [Forward call to SIP URI](#sipuri)
- [Forward call to another number](#number)
- [Forward call to registered SIP client](#regclientin)
- [Dial from registered client](#regclientout)
- [Snippet](#snippet)
- [Record something](#record)
- [Record something in your GCP bucket](#gcp)
- [Voicemail](#voicemail)
- [Outbound A2P call](#a2p)
- [IVR](#ivr)
- [Audio Forking](#forking)
- [Live transcription](#livetranscription)
- [Keywordspotter](#keyword)


Demos:
- [Doorman app](README_doorman_demo.md)



#### Hello World <a href='#helloworld' id='helloworld' class='anchor' aria-hidden='true'></a> [see xml](/sample/helloworld.xml)

1. Call is answered
2. "Hello World" text is played after text-to-speech conversion.
3. Call is hung-up

#### Hello World with callback <a href='#callback' id='callback' class='anchor' aria-hidden='true'></a> [see xml](/sample/callback.xml)

1. Call is answered
2. "Hello World" text is played after text-to-speech conversion.
3. Call is hung-up
4. Call related information is sent to specified webhook



#### Forward call to SIP URI <a href='#sipuri' id='sipuri' class='anchor' aria-hidden='true'></a> [see xml](/sample/sipuri.xml)

1. Call is Accepted
2. Ringing tone is played to calling leg
3. New call leg is initiated to SIP URI
4. `INBOUND_CALLER_NUMBER` variable is used as Caller Id
5. When SIP URI answers the two call legs are joined
6. When either party hangs up both call legs are hung up


#### Forward call to another number <a href='#number' id='number' class='anchor' aria-hidden='true'></a> [see xml](/sample/number.xml)

1. Call is Accepted
2. Ringing tone is played to calling leg
3. New call leg is initiated to a dialable number
4. `INBOUND_CALLER_NUMBER` variable is used as Caller Id
5. When called party answers the two call legs are joined
6. When either party hangs up both call legs are hung up


#### Forward call to registered SIP client <a href='#regclientin' id='regclientin' class='anchor' aria-hidden='true'></a> [see xml](/sample/regclientin.xml)

1. Call is Accepted
2. Ringing tone is played to calling leg
3. New call leg is initiated to a registered client on Inteliquent's network
4. `INBOUND_CALLER_NUMBER` variable is used as Caller Id
5. When called party answers the two call legs are joined
6. When either party hangs up both call legs are hung up

>Note 1: Inteliquent's syntax allows for the full control of all call legs. This requires that each leg is named. The name is also used to hang up the specific leg should the other one be disconnected first.


>Note 2: Client specific domains include the `vp.sip.global` suffix. Customer specific registration domain will be established during customer onboarding.

#### Dial from registered SIP client <a href='#regclientout' id='regclientout' class='anchor' aria-hidden='true'></a> [see xml](/sample/regclientout.xml)

1. Call from client is Accepted
2. Ringing tone is played to calling leg
3. New call leg is initiated to PSTN
4. `INBOUND_CALLER_NUMBER` variable is used as Caller Id and `INBOUND_CALLEE_NUMBER` variable is used for the dialed number.
5. When called party answers the two call legs are joined
6. When either party hangs up both call legs are hung up

#### Snippet <a href='#snippet' id='snippet' class='anchor' aria-hidden='true'></a> [see xml](/sample/snippet.xml)

1. Call is answered
2. `helloworld` snippet is referenced
3. the snippet will convert "Hello World" text to speech and play it to customer. 
3. Call is hung-up

>Note 1: Snippets are re-usable code objects. As such they need to be defined at the beginning of the script before any call event (e.g. <answer>) Snippets are very useful in IVRs


#### Record something <a href='#record' id='record' class='anchor' aria-hidden='true'></a> [see xml](/sample/record.xml)

1. Call is answered
2. `record_and_playback` snippet is called
3. Text is converted to speech and played
4. External Audio file with the "Beep" sound is played
5. Recording with maximum duration of 5 seconds is started.
6. After the 5 second elapsed time the recorded audio is played to customer.
7. Call is hung up

>Note : In this example Inteliquent's internal storage product is used. The next example demonstrates the use of Bring Your Own storage functionality as an alternative(Google Cloud Platform is supported). We expect to add AWS to BYOS offering soon. 

#### Record something in your GCP bucket<a href='#gcp' id='gcp' class='anchor' aria-hidden='true'></a> [see xml](/sample/gcp.xml)


1. Call is answered
2. GCP authentication and account information is declared
3. `record_and_playback` snippet is called
4. Text is converted to speech and played
5. External Audio file with the "Beep" sound is played
6. Recording with maximum duration of 10 seconds is started.
7. Format of the file is `mp3` (wav is the used if omitted)
8. After the 10 second elapsed time the recorded audio is played to customer.
9. Call is hung up

>Note : For more detail refer to our [API documentation](https://inteliscript.docs.apiary.io/#reference/media-actions/record)


#### Voicemail <a href='#voicemail' id='voicemail' class='anchor' aria-hidden='true'></a> [see xml](/sample/voicemail.xml)


1. Snippet `voicemail` is declared
2. Call is accepted 
3. Leg to registered client is dialed.
4. Timer of 20 seconds for the registered client to answer is started
5. Upon expiration of the timer the client leg is hung up
6. `voicemail` snippet is called
7. Voicemail prompt is played to the caller
8. Audio file with "beep" sound is played
9. Recording with 1 minute max duration is started
10. When recording is complete link to the recording and call parameters is POSTed to a webhook.
11. At the end of the 1 minute timer or whenever the caller hangs up all legs are hungh up.
12. Bonus: `voicemail` snippet is called for variety of cause codes generated by the platform.

>Note : For more detail refer to our [Disconnect Codes](https://pbxbook.com/other/isdncode.html)


#### Outbound A2P call <a href='#a2p' id='a2p' class='anchor' aria-hidden='true'></a> [see xml](/sample/a2p.xml)


1. Call from +17200000001 to +17200000002 is dialed
2. When +17200000002 answers text converted to speech is played.conversion.
3. Call is hung-up

>Note : A2P calls are cURL calls to https://external-api.inteliquent.net/callback/submit?apiKey= , API Key is required before this API endpoint can be used. Above is an example of XML script included in the cURL.