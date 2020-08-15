# Principles of Crittr

Crittr's goal is to make developers lives easier when _developing and debugging_ their games. To ensure we continue to meet this goal, we've developed
**three principles** to help guide us:

1. [High quality reports by default](#high-quality-reports)
2. [Reduce report friction](#reduce-friction)
3. [Focus on privacy](#focus-on-privacy)

## High quality reports

Reports should always be sent with relevant system and metadata to an issue. Low quality reports like "my game broke" or "game frozen" without any
additional context are unfortunately the current norm. These types of reports are unhelpful when debugging an issue.

High quality reports have:
* User submitted title and description of the issue
* Contextual information (i.e. device info, gpu, os)
* Developer attached metadata (i.e. screenshots, save file, etc.)

You can always expect reports sent by Crittr to include relevant information by default. If the default metadata is not enough, our APIs are extensible enough to fit your own custom needs.

## Reduce friction

Not only should reports be high quality they also need to be easy to send! You can have a high quality report with a multitude of inputs for the player to enter, but if they're tedious to fill out, players won't send them. At Crittr, we want to balance high quality reports with reports actually being sent.

Here are some examples of how we maintain that balance:
* Automated reports on exceptions.
* In-game reporting by default
* QR codes for keyboard-less environments (i.e. consoles, VR, AR)

## Focus on privacy

At Crittr, we are concerned with how our data being used without consent. We want to change that and make sure players and testers feel safe submitting reports. As such, we're asking game developers to be conscious with the data that they collect and send per report.

To help developers deal with privacy we will always include a **pre-send event hook** that you can use to filter out any PII (personally identifiable information) from your reports. If you want to include this data, we recommend following the [GDPR](https://gdpr.eu/), [CCPA](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=201720180AB375), or any other privacy act's guideline on getting a reporter's consent.
