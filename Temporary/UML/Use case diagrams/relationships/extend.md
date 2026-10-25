extremely similar to [[include]] but instead of being a **REQUIREMENT** the extended functional is **OPTIONAL** 

meaning the user could choose the user it after the main functionality or he could decide not to use it

# How to create it

we create it in the same way we [[include#How to create it|the same way we create include]] except that it is in the opposite direction (from the extension use case to the extended use case) and it contains the word **`<<extend>>`** above it

![[image-25.png]]


# Example

In a system that handles user sessions, the core action is **Log In**. The option to require a security code is an optional step that only occurs if the user's account is flagged for two-factor authentication.

- **Base Use Case (Standard):** Log In
- **Extending Use Case (Optional):** Require Security Code

The relationship is read as: **"Require Security Code may optionally extend the Log In process."**

![[image-26.png]]

this is different than [[include]] because not **ALL** users are required to enter a security code it is only required for those who chose the option to enable it

# Extension points

extension points are **ONLY** used with [[extend]] ,they act as a summary and an explanation to why we have extended that use case and when extended use case will be used

## How to create it

extension is created inside the extended use case by separting its title with a horizontal rule and writing the following under that line:

- **`Extension points`**
- the summary/explanation of why we have an extension

the extension summaries **MUST** be ordered in the same order of the extensions

## Example

lets say you are trying to login to you account and you want to explain that when the users fails to login when will be shown an error message otherwise if he successfully logins we will be prompted with the main page

![[image-29.png]]
