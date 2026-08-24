# 2FA (Two-factor authentication)

If _2FA (Two-factor authentication)_ is activated, an extra code is needed in the APP, when changing Employee.

As standard the code is send by e-mail. First priority is the _Company E-Mail_ otherwise the _E-mail_ from the Employee.

For _Two-factor_ to take effect, the _first factor_ [PIN-code](./registration-pin-code.md) must of course also be activated.

The behavor can be overridden with code by using [OnTable\_JobManEmployee\_TwoFactorCode???](../advanced-setup/code-customization.md). That could be setting up and SMS/Text service.

The sender is the mail specified under _Company Information_. **It is important that the account under _SMTP Mail Setup_ is granted to send on behalf of this sender.**

## See also

[Mobile Registration Client App](../mobile-registration-client-app/README.md)
