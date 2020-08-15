# Concepts of Crittr

## Studio

A **studio** is the governing organization of all your [projects](#projects), [members](#members), and [reports](#reports). When signing up, you will be prompted to create or
join an organization before you can submit reports to Crittr's dashboard. If you create a studio, you will be the **owner** of that
studio.

## Members

A **member** is a user who is a part of a studio. Members are grouped into distinct roles. The following
sections are a list of the member roles and their respective privileges.

##### Owner
The creator of the studio with **admin** privileges. There can only be _one owner_ per [studio](#studio).

##### Manager
The highest role after an owner. Usually is responsible for a [project](#projects), or several projects.

##### QA
A member of an organization who can modify and view reports. Commonly assigned to testers or internal QA. 

##### Member
Has read only permissions with reports and projects. Useful if you work with publishers or players who you send development builds to.

?> A single account can be a member of multiple studios. You can always check your membership role in the _Members_ tab of a studio.

## Projects

A **project** is a game or application that your [studio](#studio) develops. [Reports](#reports) are submitted to a project using the `connection uri` set in the SDK. You can find the
connection uri in the project settings SDK section on [Crittr's dashboard](https://dashboard.crittr.co/studio/projects)

## Reports

A **report** contains system information, user generated data, and additional metadata to help you and your team with debugging. Reports
can be **automated** or **manually triggered** by a tester or player. A report is the main entity of the Crittr ecosystem. 

Examples of what are contained in a report:
* Title and description of the bug
* Category (bug, feedback, automated error, etc.)
* Status (open, resolved, archived)
* Screenshot
* Device info (mobile, desktop, console, memory, etc.)
* GPU (family, name, memory size, etc)
* OS (windows, linux, iOS, etc.)
* Logs
* Environment (debug, release, beta, etc.)
* Contact information

You can also attach metadata like:
* Tags (e.g. priority, type of bug, etc.)
* Attachments (e.g. save file, log files, etc.)
* Additional screenshots
* Extras (player position, current level, etc.)
