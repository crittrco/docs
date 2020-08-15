# Unity SDK

In this guide, you'll find the steps to get you started with using Unity with Crittr. The SDK
is open source and comes bundled with scripts and prefabs to make the set up simple and quick. For
reference, you can find it at this [Github repo](https://github.com/crittrco/unity-sdk).

At the end of this guide, you should have:
* Installed the Unity SDK into a new or existing project
* Sent your first automated report
* Added manual reporting screens
* Extended the SDK to populate metadata

?> If you like video tutorials instead, we have [a Youtube tutorial]() going through the installation process

Let's get started!

## Installing the SDK

The easiest way to install the SDK is using the _install from git_ option in the package manager. In this section
we'll cover how to install it using the Unity package manager.

!> Note, the SDK has been tested to work with versions 2019.4.x. Using other versions might cause issues with your installation. If you encounter any problems, you can always [contact us](/support#contact)

To set up using Github:
1. Open up Unity to an existing project, or create a new project.
2. Follow the instructions from the [official Unity documentation](https://docs.unity3d.com/Manual/upm-ui-giturl.html) using Crittr Unity SDK's [Github repo](https://github.com/crittrco/unity-sdk).

?> We recommend using a specific release instead of using the master branch. You should use the tag of the newest release found [here](https://github.com/crittrco/unity-sdk/releases). Append the tag to the end of the clone url (e.g. with `v0.1.0`: `https://github.com/crittrco/unity-sdk.git#v0.1.0`)

Once you have installed the SDK, you now have access the the Crittr API. Included in the SDK are the `CrittrReporter` and `CrittrCanvas` prefabs which exist in the `Assets/Prefabs` directory. For reference, `CrittrReporter` sends the reports whereas `CrittrCanvas` displays the manual reports UI.

![Crittr prefabs](/media/prefabs.PNG)

## Sending your first automatic report

1. Add the `CrittrReporter` prefab to your Scene.

2. Add the Connection URI to the `CrittrReporter` game object instance:
    * Scroll to the `CrittrSDK` script component.
    * Input the Connection URI for your project (you can find this in the project settings SDK section on [Crittr's dashboard](https://dashboard.crittr.co/studio/projects))

![Add connection uri](/media/connection_uri_reporter.PNG)

3. Check the _Send Automatic Reports_ option in the `CrittrSDK` component.

![Send automatic reports](/media/send_automatic_reports.PNG)

4. Run your game and throw an exception.
    * If you get a log message with a location to your report on the dashboard then your report has been sent successfully. Go to the [Crittr dashboard](https://dashboard.crittr.co) to see the report.
    * If you got a log error, check that you have entered a valid connection uri.

## Sending a manual report

1. Add the `CrittrReporter` and `CrittrCanvas` prefabs to your Scene.

2. Add the Connection URI to the `CrittrReporter` game object (if you haven't already):
    * Scroll to the `CrittrSDK` script component.
    * Input the Connection URI for your project (you can find this in the project settings SDK section on [Crittr's dashboard](https://dashboard.crittr.co/studio/projects))

![Add connection uri](/media/connection_uri_reporter.PNG)

3. In the `CrittrReporter` game objects's `CrittrSDK` script component, add the `CrittrCanvas` game object from your Scene to the following report lifecycle events:
    * On Show Form, select the `CrittrUIManager -> HandleShowForm` function.
    * On Report Success, select the `CrittrUIManager -> HandleShowSuccess` function.
    * On Report Failure, select the `CrittrUIManager -> HandleShowFailure` function.

![CrittrReporter events](/media/crittr_report_events.PNG)

4. In the `CrittrCanvas` game object, scroll to the **Crittr UI Manager** script component. Add the `CrittrReporter` game object to the **Crittr Reporter** selection. 

![CrittrCanvas reporter property](/media/crittr_canvas_reporter.PNG)

5. Run your game and then press the default keyboard binding: `F8`. A screenshot of your game will be taken and a form to send your report should pop up. Send a report with any title or description and you should see a success screen pop up.
    * If a screen does not pop up, check the logs to see if you have inputted the connection uri correctly.
    * If the failure screen shows, check that you have a valid connection uri.

6. Navigate to the report using the QR code or link, then edit it with a new title and description.

7. That's it! You should be able to see a screenshot and the report in your [list of reports](https://dashboard.crittr.co/reports) for the project.

## Custom metadata

You can use Crittr with the default settings, but you can also add additional context to your reports. To customize your reports, you'll need to extend the API. A few reasons why you'll want to extend the API are:

1. Adding **tagging** (like: `priority: high`)
2. Adding **additional attachments** (like save files, or log files).
3. **Removing PII** (personally identifiable information)

To extend the API, we'll start by creating a new script component in the `CrittrReporter` game object. 
We'll name the new script `CrittrReporterManager` and we'll inherit from the `CrittrSDK` class. Once you've
created the script, copy the below code to override one of the CrittrSDK methods: `ModifyReportBeforeSend()`.

```C#
// filename: CrittrReporterManager.cs

class CrittrReporterManager : CrittrSDK {

    // TODO: Copy this method.
    public override void ModifyReportBeforeSend(Report report) {
        // Modify your report here.
    }
}
```

The `ModifyReportBeforeSend()` method does exactly what the name implies. The generated report is passed into
the method where you can modify the report before it is sent. You can modify any of the reports properties
which are defined in the [`CrittrReport.cs`](https://github.com/crittrco/unity-sdk/blob/master/Runtime/CrittrReport.cs) file.

In this example, we'll add a custom tag to our report. Tags are key-value maps of `string -> string`. To add the tag we'll call the `report.AddTag()` method on the report instance and set the key `foo` to the value `bar`.


```C#
class CrittrReporterManager : CrittrSDK {

    public override void ModifyReportBeforeSend(Report report) {
        report.AddTag("foo", "bar")
    }

}
```

Save the file and then run your game. Press the default keyboard binding (`F8`) to create and send your report. On the success screen, navigate to the report and check the tags to see if your tag was added!

#### Next steps 

There are more ways you can customize the CrittrSDK script to suit your needs. All public methods are overrideable, and if you don't want to extend the API, the options in the `CrittrSDK` component should be customizable enough. In the next section, you'll find references to the API and more details on each property of the `CrittrSDK` component.

## API Reference

### CrittrSDK

![CrittrSDK API](/media/crittr_sdk_api.png)

#### Connection URI

The Connection URI for your project (you can find this in the project settings SDK section on [Crittr's dashboard](https://dashboard.crittr.co/studio/projects))

#### Send Automatic Reports

Toggle sending automatic reports on exceptions.

#### Max Logs

Sets the max amount of log lines sent with the report. Defaults to **100**.

#### Is Verbose

Toggles the debug mode and displays logs. 

!> We recommend turning this option off when releasing your game.

#### Keyboard Input Trigger

A keyboard `KeyCode` input that triggers the sending the report. 

#### Controller Input Triggers

An array of `KeyCode` inputs that are required to press down to send the report.


#### Events

##### On Show Form

Event that is fired when the manual report input has been triggered. If there is no event, a form is not shown
and a manual report will be sent to the dashboard with no title or description. Works well with `CrittrUIManager.HandleShowForm()` method on the `CrittrCanvas` game object.

!> We recommend only using this event if you're deploying a game that is easy to input text (like Desktop or Mobile). If you are deploying a console game, we recommend keeping this event list empty and allowing console players to update the report using the QR code. For more details, read about our [Reduce Friction](/principles#reduce-friction) principle for reports.

##### On Report Sent

Event that is fired when the report has been sent to the web dashboard. Recommended use is to show some loading indicator.

##### On Report Success

Event that is fired when the report create has returned a successful response from the server. Works well with `CrittrUIManager.HandleShowSuccess()` method on the `CrittrCanvas` game object.

##### On Report Failure

Event that is fired when the report create has returned a failed response from the server. Works well with `CrittrUIManager.HandleShowFailure()` method on the `CrittrCanvas` game object.
