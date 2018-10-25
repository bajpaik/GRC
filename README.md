# GOVERANCE RISK AND COMPLAINCE

https://community.servicenow.com/community?id=community_article&sys_id=4649966fdb95db400e3dfb651f96199a


Knowing the Kingston GRC - 1(Policy and Compliance) 




Being in the technical team, of course I would be more focusing on the technical stuff of ServiceNow. Suddenly one fine day my manager was at my desk asking me to analyze the GRC. I was confused “What kind of analysis is that?” Is it some sort of technical review on what is feasible in GRC (Of course as it is built on ServiceNow we can twist it as required). No, it’s not that. We would like to know more about the hierarchy, process flows, and workflows. As a whole and sole “Complete ServiceNow Kingston GRC architecture” (in detail).

I went through lot of sites and met people to understand how exactly the GRC works and how that has been framed in ServiceNow. It’s been a bit hard as the ServiceNow docs are bit scattered and you can’t find the complete info in one place. This article will give a basic understanding to the people who are new to GRC terminology and ServiceNow Kingston GRC.

 

What exactly GRC in ServiceNow is?

Let me start the answer with a question, “What is an incident in ServiceNow”? When something breaks, a ticket will be raised and will be redirected to appropriate team. Respective team will look into the issue and resolves it and updates the incident ticket in ServiceNow. In the whole scenario ServiceNow is being just used as a tracking tool to know the status of the issue.

Same applies for GRC as well, all the organizations has their own rules, regulations and their set of policies to follow. They have policies right from hiring to firing. How can they ensure that every one is compliant to all their rules and regulations? Here comes the need of a tool where they can put their policies and can monitor them all across the organization. If any of the policy is not being followed any of the team or person, it will be popped up in the report based on the criteria they set for being compliant. In short I can see all the people, teams who are non-compliant.

Let us see how that has been configured in ServiceNow Kingston Release -

Activating the plugins:

Here is the list of important plugins related to GRC:

GRC: Policy and Compliance Management

GRC: Audit Management

GRC: Risk Management

Developers has to activate any of these plugins from the plugins module of the instance. (This comes with a different subscription from ServiceNow)

ServiceNow GRC has been primarily divided into 3 modules –
1.Policy and Compliance Management
2.Audit Management
3.Risk Management

Not to look for the word “Governance” in the plugins. There is no dedicated plugin as such...

Let’s stick to “Policy and Compliance Management” plugin in this article.

 From now we will come across the following terminology frequently:
1.Authority Documents
2.Citations
3.Policy Statements
4.Policies
5.Controls
6.Indicators
7.Indicator tasks
8.Issues
9.Policy Exceptions
10.Remediation Tasks

 

Authority Documents: As we spoke a lot about compliance, we first should know what we complying to. An Authority document is the overview of the rules, regulations, policies and standards of that Framework. Say ISO is a frame work, to comply with ISO we need to follow some set of Processes and standards. So an overview of this can be in the Authority Document (You can imply this to ITIL as well).

 Citations: Citation is a subset of the Authority document. This says one specific element of the Authority document. As I said Authority document gives an overview of a framework/entity, Citations will describe the Authority document elaborately by segregating it into different elements.

Policies: Here comes action part. Policies can be stand alone or they can be mapped to any of the authority document or citation, this should be usually recommended by your compliance team. Say we have “Facility Management Policy” which says what rules should be followed to make sure you manage your office facility effectively, this policy might or might not have an associated Citation or Authority document.

Policies should be reviewed and approved before publishing. We don’t have this kind of reviews or approvals in AD or citation. So the policies will be made which are more specific to the organization.

Policy Statements:

A policy can have multiple policy statements. Say we have “Facility Management policy” as a policy then there can be lot of policy statements associate with it like –
1.Prepare the alternate facility for an emergency offsite relocation
2.Test the continuity plan at the alternate facility
3.Install a generator sized support the facility

What this means, let’s go one by one - Organization has a Facility management policy, to make the organization complaint different teams would be working on it. As part of it, few teams will take care of alternate facility in case of emergency. That facility will facilitate the business continuity plan for the organization. If you look at the Policy Statements above there might be a team who has to “prepare the alternate facility for an emergency offsite relocation”, their might be another team to “test the continuity plan at the alternate facility”. So, all these teams need to be compliant to make the complete Facility management policy to be compliant.

*Policy and Policy Statements are many to many relationships.

* For the people using Legacy GRC, Legacy Controls becomes Policy Statements

Profile Types:

As we discussed different teams/persons would be working to ensure that the policy should be compliant, what are those teams or who are those people? On what basis we choose them? This should be done using Profile types.

In profile types we have “profile filters” where we can choose the table and criteria to pick the records. Say, one particular region all the departments (may be assignment groups) has some role to play to make sure the policy is compliant then the filter is going to be table name is “sys_user_group” and region = Asia.

This generates all the profiles with the individual name belongs to those departments/Assignment groups.

These profile types and profiles will be used all across GRC application.

Controls:

Controls will be generated when a profile is added to the policy statement or Policies. Control is the gateway to generate the tasks or to automatically fetch the non-compliant records based on the frequency.

Controls has to be mapped with a profile. Once you add profile to control, “Owned by” user of the profile will become “Owner” in the control.

Technical stuff like assigning the field work will start from the controls. 

Control starts with the Draft, Control Attestation is the state where the attestation respondents (it’s the field in the control) will attest that the control has been implemented. Then it passes from the attestation state to Review and Monitor. Monitor is the state where all the task assignment takes place.

Indicators:

In the hierarchy Indicators will be tagged under Controls. Indicator has the capability to automatically check if there are any non-compliant records in the ServiceNow or it can generate the task to appropriate team based on the schedule to check the non-complaint across the organization.

To explain with an example – for Change management policy:
•There is a policy statement which says there should be no change request proceeding without a back out plan.
•A profile type “Change managers” has been attached to Policy statement.
•It has created controls to all the respective location change managers as control owners.

Control says this has to be reviewed every quarter by the control owner.

Now comes the Indicator, Indicator will be create either tasks for the respective change managers to evaluate any change has been processed without back out plan .Or if the data is available in ServiceNow it automatically evaluates the data based on the filter condition we set and it generates the indicator results.

While creating the indicator, pick the control in the item field. Choose the frequency when that indicator has to be triggered. Select either Basic (automatic) or Manual (Generate tasks and people has to work).

If the supporting data is available in ServiceNow, then you can set the filter criteria. If you would like to go to Basic model then you have to mention what is the condition which says whether a control or Policy Statement is compliant or not. Using the same back out plan example, you have set the criteria as:Table = “Change_request” and Blackout plan is empty.

If this filter finds any record, then you can say the indicator result is failed (non-complaint).

Otherwise if you opt for Manual, it just generate the indicator task for the respective people and people who handles the ticket should tell whether it is complaint (Passed) or not (Failed).

Issue:

When any of the indicator Results fail, it creates an issue in the Control. Which says you are non-compliant for that particular policy statement. So either you should have exception saying why you are not compliant or a remediation task on how are you going to remediate it. Either way (Exception or Remediation task) your issue should be closed.

Policy Exception: 

As I said in the issue section when there is an exception for being non-compliant, for example you cannot back out one particular change so there is no back out plan in the change request, then you can raise an exception. This exception has to be approved by appropriate manager, once it get approved this policy exception will be considered for that issue and issue will be closed.

Remediation Tasks: 

If you would like to remediate an issue, you can create a remediation task and work on it close it then you can close the Issue. 

