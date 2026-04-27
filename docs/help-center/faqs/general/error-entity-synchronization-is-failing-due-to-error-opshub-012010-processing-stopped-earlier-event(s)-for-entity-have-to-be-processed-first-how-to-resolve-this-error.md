# Error: Entity synchronization is failing due to error: OpsHub-012010: Processing Stopped – earlier e

## Description

Received the error: Entity synchronization is failing due to error: OpsHub-012010: Processing Stopped – earlier event(s) for entity have to be processed first. How to resolve this error?

## Solution

A failed event on a given entity is blocking further synchronization. For example, if <code class="expression">space.vars.SITENAME</code> notices that for entity E1, there is already a failed event in the queue, then all further updates will fail with the above error.\
To fix this error, first find the entity on which the error is coming and fix the error. To get the Entity Id of the entity on which error is coming, follow the steps given below:

* Go to <code class="expression">space.vars.SITENAME</code> Dashboard and click on the Integration Name:
* The exclamation marks represent errors. Pink exclamation mark is Global Failure and Red exclamation mark is Processing Failure. You can click the error directly or click the relevant tab (Global Failure/Processing Failure) to know what the error is. We click the Processing Failure tab.
* Click the  in the error (right corner) to expand the error.
* You can see the Entity Id column listed in the error.
* Fix the error on the entity and retry all failed events for the entity. The error OpsHub-012010 should be processed during retries.
