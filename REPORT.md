# Lab 4 WebSocket -- Project Report

## Description of Changes
In this lab, the `onChat` test was completed to verify the interaction between a WebSocket client and the Eliza server, 
simulating a real conversation.

## Technical Decisions
To begin with, the `onMessage` function was completed by adding logic to send a message with the content "you" whenever 
the message "---" is received. This indicates that the server has finished sending its message and is expecting a reply
from the client.

Next, the `onChat` test was completed by adding the following checks:
```
val size = list.size
assert(size = 4 || size == 5)
assertEquals("We were discussing you, not me.", list[3])
```
In this test, storing the list size in the variable size is necessary to avoid race conditions, since the list can be
updated asynchronously and its size could change during the test execution.

Additionally, `assert` is used instead of `assertEquals` in the first verification because we need to check for a range 
of valid values, not an exact one. The result depends on multiple factors such as timing, system performance...

The test checks specifically for the values 4 or 5 because, given the instruction CountDownLatch(4), we know that at 
least four messages will be exchanged. However, due to the server’s behavior, it is possible for five messages to be 
received:
- Three initial welcome messages,
- One reply from the server (or two if the message "---" is also included in the exchange).

For the second verification, a predefined message is used that corresponds to the server’s expected reply after 
receiving the client’s "you" message. It is compared to the fourth message in the list because that position contains 
the server’s response in the interaction sequence.

## Learning Outcomes
Before this lab, I had never needed to write tests for asynchronous communication using WebSockets. Through this 
exercise, I learned how to handle concurrency issues in tests, how to use CountDownLatch to synchronize client–server 
interactions, and how to design assertions that are reliable even when message timing is non-deterministic.

## AI Disclosure
### AI Tools Used
- ChatGPT

### AI-Assisted Work
- ChatGPT was used for translation purposes.

### Original Work
- The implementation of the `onChat` test done originally by me.