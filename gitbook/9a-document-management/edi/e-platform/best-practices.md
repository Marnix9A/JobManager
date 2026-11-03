# Best Practices

## Limit Logic

Despite the fact that e-platform **can** do transformations, it should be noted that logic should be limited to an absolute minimum.

Reason: Every logical operations has exceptions and will eventually run into unexpected problems. When this happens, there must be a way to view failed messages and to edit those messages / release the flow. Due to limited options for customers to view messages, let alone modify those messages, flows can get stuck. And this may only be noticed several days or even weeks later.&#x20;

Resolution: put the logic there where there is a user interface available to display errors to the user.

Note: it is better to see e-platform as a dumb pipe, with some extra features.

It seems to be popular belief that because something is possible, it is also a good idea.\
(Or worse: it even _must_ be used! No.)

## Accept Incorrect Input

When a messages arrives from E-Platform that has invalid data, do not just decline it. But if possible register the message, and display the problem to the end user.

Note that E-Platform itself does not create the message. It merely forwards it from another service. As a result it is not responsible for the content of the message, and has often no idea how to recover from a failure.

The only recovery strategy available for E-Platform is to retry the delivery. But it will not result in a different message content. So if the data is wrong, the delivery will fail again, and again. \
Also note that E-Platform will not send a message to the original sender to notify it that something was wrong.

## Provide Proper Input

Often the "sending" application just pushes data in whatever format was easiest to get it from it's source. And just expects the e-platform to translate it to a proper format. However input should always already be in a "proper" format.&#x20;

The idea is that a sender can provide one "general" message, and that depending on the destination it can be transformed to the format that the receiver expects. But both input and output should be "proper" formats.

Garbage in will likely result in errors in production when unexpected input conditions generate bad outputs. And once more these cannot easily be detected or corrected.

## Dates & Numbers

Always serialize dates and numbers using _invariant culture_. This is because receivers of serialized messages (including e-platform) don't know what culture the user that created the data happend to be using. Expecting receivers to guess the culture is a bad idea.

Some examples:

Number `1 000,23` should be send as `1000.23`\
Number `1000,23` should be send as `1000.23`\
Date [`3/9/2021`](#user-content-fn-1)[^1] should be send as [`2021-03-09`](#user-content-fn-2)[^2]





[^1]: Is this 03-09-2021, or 09-03-2021? just by looking at this endpoint it is impossible to guess, which will result in errors at some point.

[^2]: Format should be yyyy-MM-dd\
    Also known as the "universal format".
